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
