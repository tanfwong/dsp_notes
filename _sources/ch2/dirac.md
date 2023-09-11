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
  4. $\displaystyle ~~u(t) = \begin{cases}
      1, & t \geq 0  \\
      0, & t < 0 
      \end{cases} \stackrel{\text{FT}}{\longleftrightarrow} 
      \pi \delta(\omega) + \frac{1}{j\omega}$.
  5. Let $x(t)$ be a finite-power periodic signal with period
      $T$. Hence, $x(t)$ has the FS expansion
      $x(t) = \sum_{k=-\infty}^{\infty} a_k e^{j\frac{2\pi k t}{T}}$, 
      where $a_k$ is the $k$th FS coefficient of $x(t)$. By the
      linearity property of FS and Example 1. above, we may 
      extend the FT mapping to $x(t)$ as:
      \begin{equation*}
      x(t) \stackrel{\text{FT}}{\longleftrightarrow}  2\pi
      \sum_{k=-\infty}^{\infty} a_k \delta\left(\omega - \frac{2\pi k
      t}{T} \right)
      \end{equation*}
      ```{caution}
      We have assumed the linearity property of FT extends to the infinite series of the
      FS synthesis formula above. This assumption can be justified in
      this case by first considering the partial sum $\sum_{k=-N}^{N}
      a_k e^{j\frac{2\pi k t}{T}}$ and then the
      $L^2[-T/2,T/2]$-convergence of the partial sum to $x(t)$ as $N
      \rightarrow \infty$.
      ```

* Similarly, we may extend the FT toolset to handle some
  infinite-energy FTs by considering the following frequency-domain window:
   \begin{equation*}
  \tilde{w}_{\mu} (t) = \frac{\mu}{\pi (\mu^2 + t^2)}~~\stackrel{\text{FT}}{\longleftrightarrow} 
  ~~ \tilde{W}_{\mu}(\omega) = e^{\mu |\omega|} 
  \end{equation*}
  for any $\mu >0$. The same Dirac delta mnemonics 1.-3. can be used 
  
* For an infinite-energy FT $X(\omega)$ that grows only polynomially in
  $|\omega|$, the windowed FT $\tilde{W}_{\mu} (\omega) X(\omega) \in L^1 \cap
  L^2$ and hence has an inverse FT $x_{\tilde{w}_{\mu}} (t)$.  Since
  $\lim_{\mu \rightarrow 0} \tilde{W}_{\mu} (\omega) X(\omega) =
  X(\omega)$ for every $\omega \in \mathbb{R}$, we may define the
  limit of $x_{\tilde{w}_{\mu}} (t)$ as $\mu \rightarrow 0$ as the
  inverse FT of $X(\omega)$. 

* **Example**:

  6. $\displaystyle ~~\delta(t-t_0) \stackrel{\text{FT}}{\longleftrightarrow}
     e^{-j\omega t_0}$
