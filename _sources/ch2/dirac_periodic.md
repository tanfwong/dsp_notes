# Periodic Dirac delta

* Common ideal signals, such as sinusoids and the unit step, do not
  have finite energy. The forward DTFT series on the RHS of
  {eq}`e:dtft` do not converge for these signals, and hence they do not
  have DTFTs strictly speaking.
* These signals are mathematical idealizations that are much nicer to
  deal with than their practical counterparts. We may use the
  $z$-transform toolset described before to analyze these
  infinite-energy signals. However, doing so we lose the
  frequency-domain interpretation/intuition provided by DTFT because
  the ROCs of the $z$-transforms of these signals do not contain the
  unit circle.
* A standard way to "extend" the DTFT toolset to cover these common
  infinite-energy signals is by way of the *periodic Dirac delta*
  function.

## "Limit" of window signal
* Recall the window signal in {ref}`the previous
section<sec:wlambda>`:
  \begin{equation*}
  w_{\lambda} [n] = \lambda^{|n|} 
  ~~\stackrel{\text{DTFT}}{\longleftrightarrow} ~~
  W_{\lambda}(e^{j\hat\omega})
  = \frac{1 - \lambda^2}{1 - 2\lambda \cos \hat{\omega} + \lambda^2}
  \end{equation*}
  where $\lambda \in (0,1)$.

* Recall $w_{\lambda} [n] \in \ell^1$. For each $n \in \mathbb{Z}$,
  $\lim_{\lambda \rightarrow 1} w_{\lambda} [n] = 1$. 
  Intuitively, $w_{\lambda} [n]$ becomes closer
  and closer to the constant signal $1$ (not in $\ell^1$) as 
  $\lambda$ approaches $1$.

* Similarly, the DTFT $W_{\lambda}(e^{j\hat\omega})$ satisfies
  1. $W_{\lambda}(e^{j\hat\omega}) > 0$ and is an even function.
  2. $\displaystyle \lim_{\lambda \rightarrow 1} $
  3. $\displaystyle \frac{1}{2\pi} \int_{-\pi}^{\pi} W_{\lambda}(e^{j\hat\omega})
  d\hat\omega} =  w_{\lambda} [0] = 1$. 
