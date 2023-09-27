# Frequency-domain Sampling

* The sampling theorem (see {numref}`sec:sampthm`) tells us that we
  can reconstruct a bandlimited continuous-time signal $x(t)$ with
  bandwidht $B$ Hz from its samples $x[n]=x\left(\frac{n}{f_s}\right)$
  as long as we oversample, i.e., choose the sampling frequency $f_s >
  2B$.

* One may ask whether a similar result applies to sampling the FT
  $X(\omega)$ in the frequency domain. That is, can we get back
  $X(\omega)$ (and hence $x(t)$) from its samples? If so, what is the
  condition under which we can do that. 

* We will answer the above questions in the context of a discrete-time
  signal $x[n]$ and its DTFT $X(e^{j\hat\omega})$, leaving the
  continuous-time counterpart as an exercise. More specifically,
  consider $x[n] \stackrel{\text{DTFT}}{\longleftrightarrow}
  X(e^{j\hat\omega})$. Suppose we take $M$ samples in one period of
  $X(e^{j\hat\omega})$ at the normalized radian frequencies
  $\hat\omega = \frac{2\pi k}{M}$ for $k=0,1,\ldots,M-1$.
  ```{tip}
  Recall that $X(e^{j\hat\omega})$ is periodic in $\hat\omega$ with
  period $2\pi$. In particular, $\displaystyle
  X(e^{j\hat\omega})\Big|_{\hat\omega = \frac{2\pi k}{M}} =
  X(e^{j\hat\omega})\Big|_{\hat\omega = \frac{2\pi
  (M-k)}{M}}$. Thus there is no difference between taking samples over
  the periods $[0,2\pi)$ and $[-\pi,\pi)$. The former is usually
  considered in the context of frequency-domain sampling.
  ```
  We want to determine whether, and if so the condition under which,
  the DTFT $X(e^{j\hat\omega})$ can be recovered from the $M$
  frequency-domain samples $\left\{X(e^{j\frac{2\pi k}{M}})
  \right\}_{k=0}^{M-1}$. This frequency-domain sampling question can
  again be answered by way of the Poisson sum formula(s).

* Let $x[n]$ be obtained from sampling a continuous-time signal $x(t)$
  at the sampling rate $f_s = \frac{1}{T_s}$ samples per second, i.e.,
  $x[n] = x(nT_s)$ and set $T=MT_s$. Then the time-domain Poisson sum
  formula {eq}`e:poisson_x` gives
  \begin{equation*}
  \sum_{m=-\infty}^{\infty} x(t+mMT_s)
  = 
  \frac{1}{MT_s} \sum_{l=-\infty}^{\infty} X\left(\frac{2\pi l}{MT_s}
  \right) e^{j\frac{2\pi l t}{MT_s}} 
  \end{equation*}
  where
  $x(t) \stackrel{\text{FT}}{\longleftrightarrow} X(\omega)$. At
  $t=nT_s$, we get
  \begin{align*}
   \sum_{m=-\infty}^{\infty} x[n+mM] 
   &=
   \frac{1}{MT_s}  \sum_{l=-\infty}^{\infty} X\left(\frac{2\pi
  l}{MT_s} \right) e^{j\frac{2\pi l n}{M}} 
  \\
  &= 
  \frac{1}{M} \sum_{k=0}^{M-1} f_s \sum_{m=-\infty}^{\infty} X\left(
  \frac{2\pi (k+mM)}{MT_s} \right) e^{j\frac{2\pi (k+mM) n}{M}}. 
  \end{align*}
