# Dirac delta and FTs of infinite-energy signals

* Similar to DTFT, we can use windowing to extend the FT toolset to
  some common infinite-energy continuous-time signals by considering
  the following counterpart of the window signal in continuous time:
  \begin{equation*}
  w_{\mu} (t) = e^{\mu |t|} ~~\stackrel{\text{FT}}{\longleftrightarrow} 
  ~~ W_{\mu}(\omega) = \frac{2\mu}{\mu^2 + \omega^2}
  \end{equation*}
  for any $\mu >0$.
