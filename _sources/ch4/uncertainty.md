# Uncertainty Principle

* Consider a finite-energy continuous-time signal $x(t)
  \stackrel{\text{FT}}{\longleftrightarrow} X(\omega)$ with energy
  $\displaystyle E_x = \int_{-\infty}^{\infty} |x(t)|^2 \, dt - \frac{1}{2\pi}
  \int_{-\infty}^{\infty} |X(\omega)|^2 \,d\omega$.

* Without loss of generality, assume $x(t)$ satisfies:
  - $\displaystyle\int_{-\infty}^{\infty} t |x(t)|^2 \,
    dt = 0$, and
  - $\displaystyle \frac{1}{2\pi} \int_{-\infty}^{\infty}  \omega
    |X(\omega)|^2 \,d\omega = 0$.

  Note that these two assumptions mean that the signal energy is
  centered about $t=0$ in the time domain and about $\omega = 0$ in
  the frequency domain.  If either assumption is not satisfied, we may
  simply shift the time or frequency axis to force the assumption to
  hold.

* Define the quantities
  \begin{align*}
  \sigma_t 
  &=
  \sqrt{\frac{1}{E_x}
  \int_{-\infty}^{\infty} t^2 |x(t)|^2 \, dt 
  }
  \\
  \sigma_{\omega}
  &=
  \sqrt{\frac{1}{2\pi E_x}
  \int_{-\infty}^{\infty}  \omega^2
    |X(\omega)|^2 \,d\omega
   }
  \end{align*}
  to measure the spreads of signal energy about the centers in the time and
  frequency domains, respectively. 

  **Example**: 
  For $\displaystyle \tilde{w}_{\mu} = \frac{\mu}{\pi (\mu^2+t^2)}
  \stackrel{\text{FT}}{\longleftrightarrow} \tilde{W}_{\mu}(\omega) =
  e^{-\mu |\omega|}$, $\sigma_t = \sqrt{\pi} \mu$ and $\sigma_{\omega} =
  \frac{1}{\sqrt{2} \mu}$.

* Now, suppose $\sigma_t < \infty$ (i.e., $tx(t) \in L^2$). Then, we have
  - $tx(t) \rightarrow 0$ and hence $t|x(t)|^2  \rightarrow 0$ as $t \rightarrow \pm \infty$
  - $tx(t) \stackrel{\text{FT}}{\longleftrightarrow}  j
    \frac{dX(\omega)}{d\omega}$
  
  Further, suppose $\frac{dx(t)}{dt}$ exists on $\mathbb{R}$. Then
  - $\displaystyle \frac{d|x(t)|^2}{dt} = \frac{dx(t)}{dt} \cdot
    x^*(t) + x(t) \cdot \left(  \frac{dx(t)}{dt} \right)^*$
  - $\displaystyle \frac{dx(t)}{dt}
    \stackrel{\text{FT}}{\longleftrightarrow}  j\omega X(\omega)$
  - $\displaystyle \int_{-\infty}^{\infty} \left| \frac{dx(t)}{dt}
    \right|^2 \,dt  = \frac{1}{2\pi} \int_{-\infty}^{\infty} \omega^2
     | X(\omega)|^2 \,d\omega$.
  
  As a result, integration by parts gives
  ```{math}
  :label: e:uncert
  \begin{align*}
  E_x 
  &=
  \int_{-\infty}^{\infty} |x(t)|^2 \, dt 
  \\
  &= 
  t|x(t)|^2 \Big|_{-\infty}^{\infty}  - \int_{-\infty}^{\infty} t
  \frac{d|x(t)|^2}{dt} \, dt
  \\
  &=
  -  \int_{-\infty}^{\infty} t \frac{d|x(t)|^2}{dt} \, dt
  \\
  &=
  - \int_{-\infty}^{\infty} \frac{dx(t)}{dt} \cdot (tx(t))^* \, dt 
  - \int_{-\infty}^{\infty} (tx(t)) \cdot \left(  \frac{dx(t)}{dt}
  \right)^* \,dt
  \\
  &\leq
  2 \int_{-\infty}^{\infty}  \left| \frac{dx(t)}{dt} \right| \cdot 
  |tx(t)| \,dt
  \\
  &\leq 
  2 \sqrt{\int_{-\infty}^{\infty}  \left| \frac{dx(t)}{dt} \right|^2
  \,dt} \cdot
  \sqrt{\int_{-\infty}^{\infty} t^2 |x(t)|^2 \,dt}
  & \text{(Cauchy-Schwartz inequality)}
  \\
  &=
  2 
  \sqrt{ \frac{1}{2\pi} \int_{-\infty}^{\infty} \omega^2
    | X(\omega)|^2 \,d\omega}
  \cdot
  \sqrt{\int_{-\infty}^{\infty} t^2 |x(t)|^2 \,dt}.
  \end{align*}
  ```
  Expressing {eq}`e:uncert` in terms of $\sigma_t$ and
  $\sigma_{\omega}$, we get:
  ```{admonition} Uncertainty Principle
  :class: tip
  For any finite-energy, differentiable signal $x(t)$, its
  ***time-bandwidth product*** $\displaystyle
  \sigma_t \sigma_{\omega} \geq \frac{1}{2}$.
  ```