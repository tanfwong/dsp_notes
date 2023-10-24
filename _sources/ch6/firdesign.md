# FIR Filter Design

* We discuss two common approaches to design FIR filters that
  approximate the frequency responses of the ideal filters. We focus
  on the design of lowpass filter. The design approaches extend almost
  trivially to other types of filters. One may also use the frequency
  transformation methods in {numref}`sec:freqtrans` to convert the
  lowpass filter to other types of filters.


## Filter Specifications
* The first step in the filter design process is to specify in what
way we are to approximate the frequency response of an ideal lowpass
filter. 

* In the following discussion, we consider the specification of the
  magnitude response shown in the figure below:
  ```{image} ../figs/fspec.png
  :alt: Lowpass filter specification
  :width: 800px
  :align: center
  ```
  This specification is quantified by the quadruple 
  $(\hat\omega_p, \hat\omega_s, \delta_1, \delta_2)$.

* For the phase response, we impose the restriction that the group
  delay of the filter must be a constant. That is, the filter must be
  a generalized linear-phase FIR filter.


## Design by Windowing

* **Design Procedure**:
  1. Pick a window $w[n]$ of length $L=M+1$ from the {ref}`table
     <tab:windows>` in {numref}`sec:stft`.
  2. Let $H_d(e^{j\hat\omega})$ be the desired frequency
     response. e.g., that of an ideal lowpass filter. Take the inverse
     DTFT of $H_d(e^{j\hat\omega})$ to obtain the desired impulse
     response $h_d[n]$. Time-shift $h_d[n]$, if necessary, to make
     $h_d[n]$ symmetric (antisymmetric), i.e., $h_d[M-n] = h_d[n]$
     ($h_d[M-n] = -h_d[n]$) for $n=0,1,\ldots,M$.
  3. Apply the window to $h_d[n]$ to generate the FIR impulse response
     $h[n] = w[n] h_d[n]$ of order $M$.
  4. Calculate the magnitude response $|H(e^{j\hat\omega})|$ of $h[n]$
     to check whether the specification $(\hat\omega_p, \hat\omega_s,
     \delta_1, \delta_2)$ is met. 
     - If yes, terminate and output $h[n]$.
     - If no, increment $M$ and/or change other window parameters and
       go back to step 2. 

* Note that every window $w[n]$ listed in the {ref}`table
  <tab:windows>` in {numref}`sec:stft` is symmetric. As a result, if
  $h_d[n]$ is symmetric (antisymmetric), then $h[n]$ will be symmetric
  (antisymmetric). That is, the filter $h[n]$ obtained will be a
  generalized linear-phase FIR filter. For lowpass filter design, we
  want $h[n]$ to be symmetric (types 1 & 2).

* By the multiplication property of DTFT,
  \begin{equation*}
  H(e^{j\hat\omega}) = \frac{1}{2\pi} \int_{-\pi}^{\pi} H_d(e^{j\theta})
  W(e^{j(\hat\omega - \theta)}) \, d\theta.
  \end{equation*}
  Pictorially, the DTFT $W(e^{j\hat\omega})$ of the window $w[n]$
  smooths out any abrupt transitions in $H_d(e^{j\hat\omega})$ and
  causes **ripples** in the passband and stopband.  These effects
  become less prominent as the window length $L$ (order $M$)
  increases. The choice between different windows often amounts to a
  tradeoff between a wider transition band and smaller $\delta_1$ and
  $\delta_2$. 
