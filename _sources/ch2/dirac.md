# Dirac delta and FTs of infinite-energy signals

* Similar to DTFT, we can use windowing to extend the FT toolset to
  some common infinite-energy continuous-time signals by considering
  the following counterpart of the window signal in continuous time:
  \begin{equation*}
  w_{\mu} (t) = e^{\mu |t|} ~~\stackrel{\text{FT}}{\longleftrightarrow} 
  ~~ W_{\mu}(\omega) = \frac{2\mu}{\mu^2 + \omega^2}
  \end{equation*}
  for any $\mu >0$.

* Similar to before, we can define the following (aperiodic) *Dirac delta*
  "function":
  1. $\displaystyle \delta(\omega) = \lim_{\mu \rightarrow 0}
     \frac{W_{\mu}(\omega)}{2\pi} = \begin{cases}
      \infty, & \omega = 0  \\
      0, & \omega \neq 0 ,
      \end{cases}$
  2. $\displaystyle \int_{-\infty}^{\infty} \delta(\omega) \, d\omega
     = 1$, and
  3. If $X(\omega)$ is bounded and continuous at $\omega = \omega_0$, then
     $\displaystyle \int_{-\infty}^{\infty} \delta(\theta)
     X(\omega_0 - \theta) \, d\theta = X(\omega_0)$,

  as a mnemonic to shorthand the limiting processing of considering
  $w_{\mu} (t) \stackrel{\text{FT}}{\longleftrightarrow}
  W_{\mu}(\omega)$ as $\mu \rightarrow 0$.

* For an infinite-energy signal $x(t)$ that grows only polynomially in
  $|t|$, the windowed signal $w_{\mu} (t) x(t) \in L^1 \cap L^2$ and hence
  has FT $X_{w_{\mu}}(\omega)$. Since $\lim_{\mu \rightarrow 0}
  w_{\mu} (t) x(t) = x(t)$ for each fixed $t \in \mathbb{R}$, we may
  define the limit of $X_{w_{\mu}}(\omega)$ as $\mu \rightarrow 0$
  (note again that such a limit may not exist) to be the FT of $x(t)$.

* **Examples**: Calculation of the FTs of the following signals in
  terms of $\delta(\omega)$ is similar to the DTFT examples given in
  {numref}`sec:dtft_dirac_exs`. 
  1. $\displaystyle ~~e^{j\omega_0 t} \stackrel{\text{FT}}{\longleftrightarrow} 2\pi
     \delta(\omega - \omega_0)$
  2. $\displaystyle ~~\cos(\omega_0 t) \stackrel{\text{FT}}{\longleftrightarrow} 
     \pi \delta(\omega - \omega_0) + \pi \delta(\omega + \omega_0)$
  3. $\displaystyle ~~\sin(\omega_0 t) \stackrel{\text{FT}}{\longleftrightarrow} 
     \frac{\pi}{j} \delta(\omega - \omega_0) - \frac{\pi}{j} \delta(\omega + \omega_0)$
