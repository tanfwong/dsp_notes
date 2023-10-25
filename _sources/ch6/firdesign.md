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

* For the Kaiser window, extensive numerical studies have been
  performed to obtain empirical formulas for good choices of $M$ and
  $\beta$ in order to satisfy the design specification $(\hat\omega_p,
  \hat\omega_p + \Delta\hat\omega, \delta, \delta)$
  (see {cite}`oppenheim2010` Chapter 7 for details):
  ```{math}
  :label: e:kaiserord
  \begin{align}
  \beta 
  &= 
  \begin{cases}
  0.1102 (D - 8.7) & \text{if } D>50
  \\
  0.5842(D-21)^{0.4} + 0.07886 (D-21) & \text{if } 21 \leq D \leq 50
  \\
  0 & \text{if } D < 21
  \end{cases}
  \\
  M 
  &= 
  \frac{D-7.95}{2.285 \Delta\hat\omega}
  \end{align}
  ```
  where $D = -20\log_{10} \delta$. As a result, one may use
  {eq}`e:kaiserord` as a choice for step 1 in the design
  procedure above to avoid going through the iterative design process. 
  
* **MATLAB Example 1**:

  The objective is to design a lowpass generalized linear-phase FIR
  filter with the specification $(0.3\pi, 0.35\pi, 0.001, 0.001)$. We
  use the Kaiser window and {eq}`e:kaiserord` to select $M$ and
  $\beta$. One may use the MATLAB function `kaiserord` to calculate
  the choices of $M$ and $\beta$ given by {eq}`e:kaiserord`:
  ```matlab
  >> [M, wc, beta, ftype] = kaiserord([0.3, 0.35], [1, 0], [0.001, 0.001])
  
  M =
 
     146


  wc =
 
      0.3250


  beta =

      5.6533


  ftype =

      'low'
  ```
  Set the desired frequency response to be that of an ideal
  lowpass filter, i.e., $H_d(e^{j\hat\omega}) = \begin{cases}
  1 & \text{if } |\hat\omega| \leq 0.325\pi \\
  0 & \text{if } 0.325\pi < |\hat\omega| \leq \pi.
  \end{cases}$ Taking inverse DTFT gives $\displaystyle h_d[n] =
  \frac{\sin(0.325\pi n)}{\pi n}$.  For $M=146$, we need to delay
  $h_d[n]$ by $\frac{M}{2}=73$ time instants to get a symmetric
  desired impulse response $h_d[n-\frac{M}{2}]$ before applying the Kaiser
  window to obtain the target type-1 filter $h[n]$:
  ```matlab
  >> n = [0:M];
  >> hd = sin(0.325*pi*(n-M/2)) ./ (n-M/2) / pi;
  >> hd(M/2+1) = 0.325;
  >> h1 = kaiser(M+1, beta).' .* hd;
  >> fvtool(h1, 1);
  ```
  It turns out that the specification of $\delta = 0.001$ (-$60$ dB)
  is slightly violated in the stopband. The achieved value is $\delta
  = 0.001053$ ($-59.55$ dB). This is often acceptable in
  practice. 
  ```{caution}
  Increasing the order $M$ while keeping the value of $\beta$
  unchanged does not monotonically reduce the ripples in the passband
  and stopband. For example, setting $M=150$ meets the specification
  of $\delta=0.001$ in the stopband, but fails to meet the same 
  requirement in the passband by a slight margin!
  ```

  One may also use the MATLAB function `fir1` to generate
  the desired impulse response by a least square optimization (instead of using
  the ideal lowpass filter formula) and then apply the Kaiser window:
  ```matlab
  >> h1f = fir1(M, wc, ftype, kaiser(M+1, beta));
  >> fvtool(h1f, 1)
  ```
  The filter given by `fir1` is very similar to the one obtained above
  using the ideal lowpass filter formula to generate the desired impulse
  response $h_d[n]$, but the specification of $\delta = 0.001$ is now 
  slightly violated in both the passband and stopband.
  
* **MATLAB Example 2**:
 
  One may employ the frequency transformations described in
  {numref}`sec:freqtrans` to obtain other types of filters from the
  lowpass filter obtained in Example 1 above. For instance, setting
  $\hat h[n] = (-1)^n h[n]$ will give us a highpass, generalized
  linear-phase FIR filter with stopband $[0, 0.65\pi]$ and passband
  $[0.7\pi, \pi]$.

  However, it is more convenient to use the MATLAB function `fir1`
  again to design a highpass generalized linear-phase FIR filter:
  ```matlab
  >> [M, wc, beta, ftype] = kaiserord([0.65, 0.7], [0, 1], [0.001, 0.001])
  >> h2 = fir1(M, wc, ftype, kaiser(M+1, beta));
  >> fvtool(h2, 1);
  ```

* **MATLAB Example 3**:
  
  To design a bandpass generalized linear-phase FIR filter with
  passband $[0.3\pi, 0.65\pi]$ and stopband $[0,0.25\pi] \cup [0.7\pi,
  \pi]$, we can similarly use `fir1`:
  ```matlab
  >> [M, wc, beta, ftype] = kaiserord([0.25, 0.3, 0.65, 0.7], [0, 1, 0], [0.001, 0.001, 0.001])
  >> h3 = fir1(M, wc, ftype, kaiser(M+1, beta));
  >> fvtool(h3, 1);
  ```

## Equiripple Design - Parks-McClellan Algorithm
* The Parks-McClellan algorithm is a systematic procedure to generate
  a generalized linear-phase FIR filter of order $M$ that satisfies
  the specification $(\hat\omega_p, \hat\omega_s, \delta_1,
  \delta_2)$.

* To explain the algorithm, first note that the real-valued component
  $A(e^{j\hat\omega})$ in the frequency response of any of the four
  types of generalized linear-phase FIR filters described in
  {numref}`sec:glinphaseFIR` can be expressed in the following form:
  \begin{equation*}
  A(e^{j\hat\omega}) = Q(e^{j\hat\omega}) P(e^{j\hat\omega})
  \end{equation*}
  where
  \begin{equation*}
  Q(e^{j\hat\omega}) 
  =
  \begin{cases}
  1 & \text{ Type 1: } \text{even } M, \text{symmetric } h[n]\\
  \cos \frac{\hat\omega}{2} & \text{ Type 2: } \text{odd } M,
  \text{symmetric } h[n] \\
  \sin \hat\omega & \text{ Type 3: } \text{even } M, \text{antisymmetric }
  h[n] \\
  \sin \frac{\hat\omega}{2} & \text{ Type 4: } \text{odd } M,
  \text{antisymmetric } h[n]
  \end{cases}
  \end{equation*}
  and
  \begin{equation*}
  P(e^{j\hat\omega}) = \sum_{k=0}^{N} \alpha_k \cos(\hat\omega k)
  \end{equation*}
  with
  \begin{equation*}
  N =
  \begin{cases}
  \frac{M}{2} & \text{ Type 1} \\
  \frac{M-1}{2} & \text{ Types 2 \& 4} \\
  \frac{M}{2} - 1 & \text{ Type 3}
  \end{cases}
  \end{equation*}
  and the coefficients $\{\alpha_k\}_{k=0}^{N}$ are functions of
  $h[n]$ depending on the type of the generalized linear-phase FIR
  filter (see {cite}`proakis2022` $\S$10.2.4 for details). 
