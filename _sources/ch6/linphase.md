# Linear-phase Filter
* A **linear-phase filter** is an LTI system that has frequency response 
  of the form:
  \begin{equation*}
  H(e^{j\hat\omega}) = |H(e^{j\hat\omega})| e^{-j\hat\omega \alpha}.
  \end{equation*}
  That is, its phase response  $\angle  H(e^{j\hat\omega}) = -
  \hat\omega \alpha$ is linear in $\hat\omega$ with slope $-\alpha$.

* It is easy to check that both the phase delay and group delay of a
  linear-phase filter are equal to the constant $\alpha$, i.e.,
  $\tau_p(e^{j\hat\omega}) = \tau_g(e^{j\hat\omega}) = \alpha$. This
  means that all frequency components as well as the envelope of the
  input signal are delayed by the same amount ($\alpha$). This is a
  desirable property in some applications, e.g., digital
  communications, where the envelope is employed to convey
  information.

## Ideal Filter
* A linear-phase filter whose magnitude response equals $1$ over the
  passband and $0$ over the stopband is considered as an **ideal filter**. 
  For example, the frequency response of an **ideal lowpass filter** is 
  ```{math}
  :label: e:idealLPF
  \begin{equation}
  H_{\text{LP}}(e^{j\hat\omega}) = \begin{cases}
  e^{-j\hat\omega\alpha} & \text{if } |\hat\omega|\leq 
  \hat\omega_{\text{LP}} \\
  0 & \text{if } \hat\omega_{\text{LP}} < |\hat\omega| \leq \pi
  \end{cases}
  \end{equation}
  ```
  where $\hat\omega_{\text{LP}}$ is the cutoff frequency of the
  ideal lowpass filter. For $\hat\omega_{\text{LP}} = \pi$, the filter
  is called an **ideal allpass filter**.

* It is easy to check that the impulse response of the ideal lowpass
  filter in {eq}`e:idealLPF` is
  \begin{equation*}
  h_{\text{LP}}[n] = \frac{\sin \left(\hat\omega_{\text{LP}} (n -
  \alpha) \right)}{\pi (n - \alpha)}.
  \end{equation*}

* For any input signal $x[n]$ to the ideal lowpass filter in
  {eq}`e:idealLPF`, the output is
  \begin{equation*}
  y[n] = x[n]*h_{\text{LP}}[n] 
  = \sum_{k=-\infty}^{\infty} x[k] \, \frac{\sin
  \left(\hat\omega_{\text{LP}} (n - k -
  \alpha) \right)}{\pi (n - k - \alpha)}.
  \end{equation*}
  For the special case of the ideal allpass filter
  ($\hat\omega_{\text{LP}} = \pi$), if one interprets $x[n]$ as an
  oversampled version of a continuous-time signal $x(t)$ at the
  sampling rate $f_s$, then $y[n]$ is the sampled version of
  $x\left(t-\frac{\alpha}{f_s}\right)$ obtained at the same sampling
  rate.

* The frequency responses of ideal highpass, bandpass, and bandstop
  filters are respectively given as below:
  \begin{align*}
  H_{\text{HP}}(e^{j\hat\omega})
  &= 
  \begin{cases}
  e^{-j\hat\omega\alpha} & \text{if } \hat\omega_{\text{LP}} 
  < |\hat\omega| \leq \pi
  \\
  0 & \text{if } |\hat\omega| \leq \hat\omega_{\text{HP}} 
  \end{cases}
  \\
  H_{\text{BP}}(e^{j\hat\omega}) 
  &= 
  \begin{cases}
  e^{-j\hat\omega\alpha} & \text{if } 
  \hat\omega_{l} \leq |\hat\omega| \leq \hat\omega_{u} 
  \\
  0 & \text{if } 0 \leq |\hat\omega| < \hat\omega_{l} \text{ or } 
  \hat\omega_{u} < |\hat\omega| \leq \pi
  \end{cases}
  \\
  H_{\text{BS}}(e^{j\hat\omega}) 
  &= 
  \begin{cases}
  e^{-j\hat\omega\alpha} & \text{if } 
  0 \leq |\hat\omega| < \hat\omega_{l} \text{ or } 
  \hat\omega_{u} < |\hat\omega| \leq \pi
  \\
  0 & \text{if } 
  \hat\omega_{l} \leq |\hat\omega| \leq \hat\omega_{u} 
  \end{cases}
  \end{align*}

    ```{caution}
    The transfer function of a general ideal filter is not rational. Hence, we
    can't use an FIR/IIR filter to implement an ideal filter, except for
    the special case of the ideal allpass filter
    ($\hat\omega_{\text{LP}} = \pi$) with an integer $\alpha$ where
    impulse response reduces to $ h_{\text{LP}}[n] = \delta[n - \alpha]$.
    ```

## Generalized Linear-phase Filter
* A **generalized linear-phase filter** has frequency response of the
  following form: 
  \begin{equation*} 
  H(e^{j\hat\omega}) =
  A(e^{j\hat\omega}) e^{-j(\hat\omega \alpha + \beta)} 
  \end{equation*}
  where $A(e^{j\hat\omega})$ is a real-valued (periodic) function of
  $\hat\omega$.

* The magnitude response of the generalized linear-phase filter is $|H(e^{j\hat\omega})| =
  |A(e^{j\hat\omega})|$ and the phase response is $\displaystyle
  \angle H(e^{j\hat\omega}) = \begin{cases}
  -\hat\omega \alpha- \beta & \text{if } A(e^{j\hat\omega}) \geq 0 \\
   -\hat\omega \alpha- \beta + \pi  & \text{if } A(e^{j\hat\omega}) < 0.
   \end{cases}$ Therefore, the group delay $\tau_g(e^{j\hat\omega})$ is
  essentially (except at frequencies where $A(e^{j\hat\omega})$
  changes sign) constant at the value $\alpha$. Hence, **the constant
  group delay advantage of a linear-phase filter still holds for the
  generalized linear-phase filter**.

(sec:glinphaseFIR)=
## Causal Generalized Linear-phase FIR Filter
```{admonition} Notation
Let $h[n]$ be the impulse response of a causal FIR filter of order $M$
with real-valued filter taps. We say that $h[n]$ is **symmetric** 
(**antisymmetric**) if $h[n] = h[M-n]$ ($h[n] = -h[M-n]$) 
for $n=0,1,\ldots, M$.
```

* The following four conditions give causal generalized linear-phase FIR filters:
  1. **Symmetric $h[n]$ with an even order $M$**: 
     \begin{equation*}
     H(e^{j\hat\omega}) = \underbrace{\sum_{k=0}^{\frac{M}{2}}
      \tilde{b}_k \cos (\hat\omega k) }_{A(e^{j\hat\omega})}
      \cdot e^{-j\hat\omega \frac{M}{2}}
     \end{equation*}
     where $\tilde{b}_0 = h\left[\frac{M}{2}\right]$ and $\tilde{b}_k = 2
     h\left[\frac{M}{2} -k\right]$ for $k=1,2,\ldots, \frac{M}{2}$.

  2. **Symmetric $h[n]$ with an odd order $M$**: 
     \begin{equation*}
     H(e^{j\hat\omega}) = \underbrace{\sum_{k=0}^{\frac{M+1}{2}}
      \tilde{b}_k \cos \left(\hat\omega (k - \frac{1}{2}) \right)}_{A(e^{j\hat\omega})}
      \cdot e^{-j\hat\omega \frac{M}{2}}
     \end{equation*}
     where $\tilde{b}_k = 2 h\left[\frac{M+1}{2} -k\right]$ for $k=1,2,\ldots,
     \frac{M+1}{2}$.

  3. **Antisymmetric $h[n]$ with an even order $M$**: 
     \begin{equation*}
     H(e^{j\hat\omega}) = \underbrace{\sum_{k=0}^{\frac{M}{2}}
      \tilde{b}_k \sin (\hat\omega k)}_{A(e^{j\hat\omega})}
      \cdot e^{-j\left(\hat\omega \frac{M}{2} - \frac{\pi}{2} \right)}
     \end{equation*}
     where $\tilde{b}_k = 2 h\left[\frac{M}{2} -k\right]$ for $k=1,2,\ldots,
     \frac{M}{2}$.

  4. **Antisymmetric $h[n]$ with an odd order $M$**: 
     \begin{equation*}
     H(e^{j\hat\omega}) = \underbrace{\sum_{k=0}^{\frac{M+1}{2}}
      \tilde{b}_k \sin \left(\hat\omega (k - \frac{1}{2}) \right)}_{A(e^{j\hat\omega})}
      \cdot e^{-j\left(\hat\omega \frac{M}{2} - \frac{\pi}{2} \right)}
     \end{equation*}
     where $\tilde{b}_k = 2 h\left[\frac{M+1}{2} -k\right]$ for $k=1,2,\ldots,
     \frac{M+1}{2}$.

* The zeros of the 4 types of causal generalized linear-phase FIR
  filters above satisfy the following properties:
  - **Types 1 & 2**: 
    
    Since $h[n]$ is symmetric, we have $H(z) = z^{-M}
    H(z^{-1})$. Hence, if $z_0$ is a zero of $H(z)$, then
    $\frac{1}{z_0}$ is also  a zero. That is, $H(z)$ always have
    zero-pairs $(z_0, \frac{1}{z_0})$. In particular, for type 2 ($M$
    is odd), $H(-1) = -H(-1)$ which implies $H(-1)=0$; so there must
    be a zero at $z=-1$, i.e., the filter can't be a highpass one.
    
  - **Types 3 & 4**:

    Since $h[n]$ is antisymmetric, we have $H(z) =
    -z^{-M} H(z^{-1})$. Again, $H(z)$ always have zero-pairs $(z_0,
    \frac{1}{z_0})$. In addition, $H(1)=-H(1)$ which implies $H(1)=0$;
    so there must be a zero at $z=1$, i.e., the filter can't be a
    lowpass one. For type 4 ($M$ is odd), $H(-1) = -H(-1)$ which
    implies $H(-1)=0$; so there must be a zero at $z=-1$, i.e., the
    filter can't be a highpass one either.
 
 * It is not hard to show that any causal, generalized linear-phase,
   $M$-order FIR filter of any of the 4 types above has the following
   factorization:
   \begin{equation*}
   H(z) = H_{\min}(z) \cdot H_{\text{uc}}(z) \cdot H_{\max}(z)
   \end{equation*}
   where $H_{\text{uc}}(z)$ is the transfer function whose zeros lie
   solely on the unit circle, and $H_{\min}(z)$ and $H_{\max}(z)$ are
   a pair of minimum-phase and maximum-phase FIR filters of order
   $\tilde{M}$ satisfying $H_{\max}(z) = z^{-\tilde{M}}
   H_{\min}(z^{-1})$. 

(sec:freqtrans)=
## Frequency Transformation
* Suppose that we have a prototype design of a lowpass generalized
  linear-phase filter with real-valued impulse response $h[n]$ and
  frequency response $H(e^{j\hat\omega}) = A(e^{j\hat\omega})
  e^{-j(\hat\omega\alpha+\beta)}$. By the conjugation property of
  DTFT, $H(e^{j\hat\omega})$ must be conjugate symmetric, i.e.,
  $H(e^{-j\hat\omega}) = H^*(e^{j\hat\omega})$, which implies
  $A(e^{-j\hat\omega}) = A(e^{j\hat\omega}) e^{2j\beta}$. It is then
  easy to check that only the following two cases are possible:
  - $A(e^{-j\hat\omega}) = A(e^{j\hat\omega})$ and $\beta=0$, or
  - $A(e^{-j\hat\omega}) = -A(e^{j\hat\omega})$ and $\beta=\pm
    \frac{\pi}{2}$.
  
  Note that the type-1 and -2 generalized linear-phase FIR filters
  follow the former case while  the type-3 and -4 filters follow the
  latter case.

* Since $|H(e^{-j\hat\omega})| = |H(e^{j\hat\omega})|$, it suffices to
  describe the specification of the lowpass generalized linear-phase
  filter over the positive frequency axis. Let its **passband** be
  $[0, \hat\omega_p]$ and **stopband** be $[\hat\omega_s, \pi]$, where
  $\hat\omega_p \leq \hat\omega_s$. The frequency range
  $[\hat\omega_p, \hat\omega_s]$ is called the **transition band**.

* We may obtain a highpass, bandpass, or bandstop filter from the
  lowpass prototype while maintaining the design specifications in the
  passband and stopband by doing some simple (circular) frequency
  shifting operations.

* To get a highpass filter with frequency response $\hat
  H(e^{j\hat\omega})$, frequency shift $H(e^{j\hat\omega})$ by $\pi$, i.e.,
  ```{math}
  :label: e:lp2hp
  \begin{equation} 
  \hat H(e^{j\hat\omega}) = H(e^{j(\hat\omega-\pi)})
  = A(e^{j(\hat\omega-\pi)}) e^{-j(\hat\omega\alpha+\beta -
  \alpha\pi)}.
  \end{equation}
  ```
  It is clear from {eq}`e:lp2hp` that $\hat H(e^{j\hat\omega})$ is a
  generalized linear-phase filter. It is also easy to check that the
  passband of $\hat H(e^{j\hat\omega})$ is $[\pi - \hat\omega_p,
  \pi]$, the stopband of $\hat H(e^{j\hat\omega})$ is $[0, \pi -
  \hat\omega_s]$, and the specifications the passband and stopband of
  $H(e^{j\hat\omega})$ carry over to those of $\hat
  H(e^{j\hat\omega})$. Note that the transfer function of the
  transformed highpass filter $\hat H(z) = H(-z)$, where $H(z)$ is the
  transfer function of the prototype lowpass filter. This implies the
  highpass filter's impulse response $\hat h[n] = (-1)^n h[n]$.

* To get a bandpass filter frequency response $\tilde
  H(e^{j\hat\omega})$, frequency modulate $h[n]$ by $\hat\omega_0$
  where $\hat\omega_s < \hat\omega_0 \leq \pi-\hat\omega_s$. That is,
  obtain the impulse response of the bandpass filter as $\tilde{h}[n]
  = 2h[n]\cos(\hat\omega_0 n)$. By the frequency shifting property of
  DTFT, we have
  ```{math}
  :label: e:lp2bp
  \begin{align}
  \tilde H(e^{j\hat\omega})
  &= 
  H(e^{j(\hat\omega-\hat\omega_0)}) +
  H(e^{j(\hat\omega+\hat\omega_0)})
  \\
  &= 
  A(e^{j(\hat\omega-\hat\omega_0)})
  e^{-j(\hat\omega\alpha-\hat\omega_0\alpha +\beta)}
  + 
  A(e^{j(\hat\omega+\hat\omega_0)}) 
  e^{-j(\hat\omega\alpha+\hat\omega_0\alpha +\beta)}
  \\
  &\approx
  \begin{cases}
  A(e^{j(\hat\omega-\hat\omega_0)})
  e^{-j(\hat\omega\alpha-\hat\omega_0\alpha +\beta)}
  & \text{if } \hat\omega_0 - \hat\omega_p \leq \hat\omega 
  \leq \hat\omega_0 + \hat\omega_p 
  \\
  A(e^{j(\hat\omega+\hat\omega_0)}) 
  e^{-j(\hat\omega\alpha+\hat\omega_0\alpha +\beta)}
  & \text{if } -\hat\omega_0 - \hat\omega_p \leq \hat\omega 
  \leq -\hat\omega_0 + \hat\omega_p 
  \\
  0 & \text{if } |\hat\omega| \leq \hat\omega_0 - \hat\omega_s
  \text{ or } \hat\omega_0 + \hat\omega_s \leq |\hat\omega| \leq \pi
  \end{cases}
  \end{align}
  ```
  
  where the last approximation is obtained from the assumption that
  $|A(e^{j\hat\omega})| \approx 0$ in the stopband of the prototype
  lowpass filter, i.e., for $\hat\omega_s \leq |\hat\omega| \leq
  \pi$. From {eq}`e:lp2bp`, we see that the passband of $\tilde
  H(e^{j\hat\omega})$ is $[\hat\omega_0 - \hat\omega_p, \hat\omega_0 +
  \hat\omega_p]$ and the stopband of $\tilde H(e^{j\hat\omega})$ is
  $[0, \hat\omega_0 - \hat\omega_s] \cup [\hat\omega_0+\hat\omega_s,
  \pi]$. The specifications the passband and stopband of
  $H(e^{j\hat\omega})$ also approximately carry over to those of
  $\tilde H(e^{j\hat\omega})$. Although $\tilde H(e^{j\hat\omega})$ is
  not a generalized linear-phase filter, we may nevertheless conclude
  from {eq}`e:lp2bp` that the group delay of $\tilde
  H(e^{j\hat\omega})$ is approximately constant at the value $\alpha$
  within its passband.
  
* Finally, we may obtain a bandstop filter by frequency shifting
  $\tilde H(e^{j\hat\omega})$ by $\pi$. 

  
