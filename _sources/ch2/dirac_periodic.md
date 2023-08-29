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
* Recall the window signal in {numref}`sec:wlambda`:
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

* Clearly, the DTFT $W_{\lambda}(e^{j\hat\omega})$ is a positive,
even, and periodic (with period $2\pi$) function in $\hat\omega$. It
also satisfies the following properties:
    1. $\displaystyle \lim_{\lambda \rightarrow 1} W_{\lambda}(e^{j\hat\omega}) = 
    \begin{cases}
    \infty, & \hat\omega = 0 \bmod 2\pi \\
    0, & \hat\omega \neq 0 \bmod 2\pi.
    \end{cases}$
    2. Since $\displaystyle \frac{1}{2\pi} \int_{-\pi}^{\pi} W_{\lambda}(e^{j\hat\omega})
    \, d\hat\omega =  w_{\lambda} [0] = 1$ for all $\lambda \in
    (0,1)$, we may set
    $\displaystyle \lim_{\lambda \rightarrow 1} \int_{-\pi}^{\pi} 
    \frac{W_{\lambda}(e^{j\hat\omega})}{2\pi} \, d\hat\omega =1.$
    3. For any bounded $X(e^{j\hat{\omega}})$, the *circular
    convolution* integral $\displaystyle \frac{1}{2\pi} \int_{-\pi}^{\pi}
    W_{\lambda}(e^{j\theta}) X(e^{j(\hat{\omega}-\theta)}) \,d\theta$
    exists. In addition, if the bounded $X(e^{j\hat{\omega}})$ is
    continuous at $\hat{\omega} = \hat{\omega}_0$, then it can be shown that
    \begin{equation*}
     \lim_{\lambda \rightarrow 1} \int_{-\pi}^{\pi} 
    \frac{W_{\lambda}(e^{j\theta})}{2\pi} X(e^{j(\hat{\omega}_0-\theta)}) \, d\theta =
    X(e^{j\hat{\omega}_0}).
    \end{equation*} 

*   For any $x[n] \in \ell^1$, the DTFT $X(e^{j\hat{\omega}})$ of
    $x[n]$ is bounded and continuous on $[-\pi,\pi]$ as discussed in
    {numref}`sec:dtft_convergence`. In addition, the multiplication
    property of DTFT gives
    ```{math}
    :label: e:wx-intWX
    \begin{equation}
    w_{\lambda}[n] x[n] ~~\stackrel{\text{DTFT}}{\longleftrightarrow} ~~
    \frac{1}{2\pi} \int_{-\pi}^{\pi}
    W_{\lambda}(e^{j\theta}) X(e^{j(\hat{\omega}-\theta)}) \, d\theta.
    \end{equation}
    ```
    Taking limit on the LHS of {eq}`e:wx-intWX`, $\lim_{\lambda \rightarrow 1}
    w_{\lambda}[n] x[n] = x[n]$ for each $n \in \mathbb{Z}$ from 2.
    above. On the RHS, we have $\displaystyle \lim_{\lambda \rightarrow 1} 
    \frac{1}{2\pi} \int_{-\pi}^{\pi} W_{\lambda}(e^{j\theta}) X(e^{j(\hat{\omega}-\theta)})
    \, d\theta = X(e^{j\hat{\omega}})$ for each $\hat{\omega}$ from 3. above. Thus,
    in this sense, we can say that the DTFT mapping in
    {eq}`e:wx-intWX` is *preserved* through the limiting process of
    $\lambda \rightarrow 1$.
  
