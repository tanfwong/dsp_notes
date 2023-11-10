# Rate Conversion
* Consider interpolating $x[n]$ by a factor $U$ and then downsampling
  by a factor $D$:
  ```{image} ../figs/rateconv1.jpg 
  :alt: interpolate by $U$ and downsample by $D$ 
  :width: 800px 
  :align: center 
  ``` 
  The rate of the output signal $\tilde{x}^U_D[n]$ if $\frac{U}{D}$
  times that of the input $x[n]$.

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
      |\hat\omega| \leq \pi$ from {eq}`e:upspectrum`.
