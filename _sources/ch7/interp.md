(sec:interp)=
# Interpolation
 
* Given $x[n] \stackrel{z}{\longleftrightarrow} X(z)$. Consider the
  *upsampled* signal $x^U[n] = \begin{cases}
  x[ \frac{n}{U}] & \text{if } n \text{ is divisible by } U
  \\
  0 & \text{otherwise} 
  \end{cases}$
  where $U$ is a positive integer. That is, $x^U[n]$ is obtained from
  $x[n]$ by inserting $U-1$ zero-valued samples between each pair of
  adjacent samples in $x[n]$. The rate of $x^U[n]$ is $U$ times that
  of $x[n]$, i.e., every sample of $x[n]$ produces $U$ samples of
  $x^U[n]$.

* The $z$-transform of $x^U[n]$ is
  \begin{align*}
  X^U(z) 
  &=
  \sum_{n=-\infty}^{\infty} x^U[n] z^{-n}
  \\
  &=
  \sum_{m=-\infty}^{\infty} x[m] z^{-mU}
  \\
  &=
  X(z^U).
  \end{align*}
  ```{tip}
  If $x[n]$ is causal and the ROC of $X(z)$ is $\{|z| > r\}$, then the
  ROC of $X_D(z)$ is $X(z)$ is $\{|z| > r^{\frac{1}{U}}\}$.
  ```

* Suppose the ROC of $X(z)$ contains the unit circle. Then the ROC of
  $X^U(z)$ also does, and hence the DTFT of the upsampled signal
  $x^U[n]$ is given by
  ```{math}
  :label: e:upspectrum
  \begin{equation}
  X^U(e^{j\hat\omega}) = X(e^{j\hat\omega U})
  \end{equation}
  ```
* Passing the upsampled signal $x^U[n]$ through an ideal lowpass
  filter with frequency response $\displaystyle  H_U(e^{j\hat\omega}) = \begin{cases}
     U & \text{for } |\hat\omega| < \frac{\pi}{U} \\
     0  & \text{for } \frac{\pi}{U} \leq |\hat\omega| \leq \pi
     \end{cases}$ and impulse response $h_U[n] = \frac{\sin
  (\frac{\pi}{U} n)}{\frac{\pi}{U} n}$ 
  ```{image} ../figs/Uinterp.jpg 
  :alt: Interpolation
  :width: 800px 
  :align: center 
  ``` 
  gives the **interpolated signal** 
  $\tilde{x}^U[n]$ whose DTFT $\tilde{X}(e^{j\hat\omega}) = X^U(e^{j\hat\omega})
  H_U(e^{j\hat\omega})$:
  ```{image} ../figs/Uspectrum.jpg 
  :alt: Frequency-domain interpretation of interpolation 
  :width: 800px 
  :align: center 
  ``` 
  In the time domain,
  ```{math}
  :label: e:Uiterp
  \begin{align*}
  \tilde{x}^U[n]
  &=
  x^U[n] * h_U[n]
  \\
  &=
  \sum_{k=-\infty}^{\infty} x[k] \frac{\sin
  \left(\frac{\pi}{U} (n-kU) \right)}{\frac{\pi}{U} (n-kU)}
  \end{align*}
  ```
  ```{tip}
  It is not hard to check from {eq}`e:Uiterp` that $\tilde{x}^U[nU] =
  x[n]$. Thus, {eq}`e:Uiterp` indeed represents an interpolation
  operation in discrete time using the kernel $h_U[n]$. 
  ```
