# Sampling Theorem
* Suppose that a continuous-time signal $x(t)$ is sampled at the
  sampling rate of $f_s$ samples per second to obtain the
  discrete-time signal $x[n] = x(\frac{n}{f_s})$. The frequency-domain
  version of the Poisson sum formula {eq}`e:poisson_f` relates the
  DTFT $X(e^{j\hat\omega})$ of the sampled signal $x[n]$ to the FT 
  $X(\omega)$ of the original continuous-time signal $x(t)$:
  ```{math}
  :label: e:folded_spectrum
  \begin{equation}
  X(e^{j\hat\omega}) = f_s \sum_{k=-\infty}^{\infty}
  X((\hat\omega+2\pi k)f_s)
  \end{equation}
  ```
  where the quantity on the RHS is often referred tp as the ***folded
  spectrum*** of $x(t)$. In other words, the DTFT of the sampled
  signal $x[n]$ is the folded spectrum of $x(t)$.

* The folded spectrum is best interpreted in picture.
  ```{admonition} Notation
  A continuous-time signal $x(t)$ is ***bandlimited*** to $\Omega =
  2\pi B$ radian per second (or $B$ Hz) if its FT $X(\omega) = 0$ for
  $|\omega| > \Omega$.
  ```
