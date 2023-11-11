# Multi-rate Filtering
 * A **multi-rate filter** is one whose input and output rates
  differ.  That is, the filter outputs more/fewer than one sample per
  each input sample.

* In practice, a fixed-rate ADC (and/or DAC)  is often used. We may
  want to process the sampled signal at a rate different from the
  sampling rate of the ADC. In such cases, performing *rate
  conversion* in discrete time using a multi-rate filter would be
  convenient.

* A general $\frac{U}{D}$-rate filter can be obtained by replacing the
  ideal lowpass filter in the rate conversion system in
  {numref}`sec:rateconv` with a general lowpass filter $h[n]$
  operating at the interpolated rate $U$:
  ```{image} ../figs/mfilter.jpg 
  :alt: $\frac{U}{D}$-rate filter
  :width: 800px 
  :align: center 
  ``` 
* Clearly, if $X(e^{j\hat\omega}) \neq 0$ for $\frac{U\pi}{D} \leq
     |\hat\omega| \leq \pi$, we must have $H(e^{j\hat\omega}) = 0$ for
     $\frac{\pi}{\max(U,D)} \leq |\hat\omega| \leq \pi$ for
     interpolation and anti-aliasing.

* Direct implementation of the multi-rate filter above may not be
  desirable in practice because the filter $h[n]$ needs to be
  implemented at $U$ times the input rate.

* For the case that $h[n]$ is an FIR filter of length $L$, a direct
  time-domain implementation (convolution) of the $\frac{U}{D}$-rate
  filter requires $\displaystyle \left\lfloor \frac{NU+L-1}{D}
  \right\rfloor L$ multiplications when the length of the input signal
  is $N$. Assuming $NU \gg L \gg UD$, the number of multiplications
  needed to implement the $\frac{U}{D}$-rate is thus
  $\mathcal{O}(\frac{UL}{D})$ per input sample.

* One may reduce the computational complexity of implementing the
  $\frac{U}{D}$-rate filter by performing frequency-domain filter
  using FFT based on the overlap-save or overlap-add algorithm
  discussed in {numref}`sec:filfft`.
