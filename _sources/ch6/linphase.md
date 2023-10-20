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
* A linear-phase filter with a constant magnitude response over the
  passband is considered as an **ideal filter**. For example, the
  frequency response of an **ideal lowpass filter** is 
  ```{math}
  :label: e:idealLPF
  \begin{equation}
  H_{\text{LP}}(e^{j\hat\omega}) = \begin{cases}
  e^{-j\hat\omega\alpha} & \text{if } |\hat\omega| <
  \hat\omega_{\text{LP}} \\
  0 & \text{if } \hat\omega_{\text{LP}} \leq |\hat\omega| \leq \pi
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

