# Rate Conversion
* Consider interpolating $x[n]$ by a factor $U$ and then downsampling
  by a factor $D$:
  ```{image} ../figs/rateconv1.jpg 
  :alt: Interpolate by $U$ and downsample by $D$ 
  :width: 800px 
  :align: center 
  ``` 
  The rate of the output signal $\tilde{x}^U_D[n]$ if $\frac{U}{D}$
  times that of the input $x[n]$.

* From {eq}`e:Uiterp`, we get
  \begin{align*}
  \tilde{x}^U_D[n] &= \tilde{x}^U[Dn]
  \\
  &= 
  \sum_{k=-\infty}^{\infty} x[k] \, \frac{\sin
  \left(\frac{\pi}{U/D} (n-k\frac{U}{D}) \right)}{\frac{\pi}{U/D}
  (n-k\frac{U}{D})}.
  \end{align*}
  
* Working backward from $\tilde{x}^U_D[n]$, we can recover
  $\tilde{x}^U[n]$ (and hence $x[n]$) if the downsampling process
  doesn's suffer from aliasing, i.e., its DTFT
  $\tilde{X}^U(e^{j\hat\omega}) = 0$ for$\frac{\pi}{D} \leq
  |\hat\omega| \leq \pi$:
  1. If $U \geq D$, this oversampling requirement is automatically
     satisfied since $H_U(e^{j\hat\omega}) = 0$ for $\frac{\pi}{D} \leq
     |\hat\omega| \leq \pi$.
  2. If $U < D$, the oversampling requirement is satisfied only
      if $\tilde{X}^U(e^{j\hat\omega}) = 0$ for $\frac{\pi}{D} \leq
      |\hat\omega| \leq \pi$, which in turn implies the requirement of
      $X(e^{j\hat\omega}) = 0$ for $\frac{\pi U}{D} \leq
      |\hat\omega| \leq \pi$ because of  {eq}`e:upspectrum`.

* For case 2, we may replace the ideal lowpass filter between the
  upsampler and downsampler with an antialiasing ideal lowpass filter
  with cutoff frequency $\frac{\pi}{\max(U,D)}$:
  ```{image} ../figs/rateconv2.jpg 
  :alt: Rate conversion with antialiasing filter 
  :width: 800px 
  :align: center 
  ``` 
