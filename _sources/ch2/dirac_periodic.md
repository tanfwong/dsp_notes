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

(sec:wlimit)=
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

* For any $x[n] \in \ell^1$, the DTFT $X(e^{j\hat{\omega}})$ of
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
  w_{\lambda}[n] x[n] = x[n]$ for each $n \in \mathbb{Z}$ because
  $\lim_{\lambda \rightarrow 1}  w_{\lambda}[n] = 1$ as discussed above.
  On the RHS, we have $\displaystyle \lim_{\lambda \rightarrow 1} 
  \frac{1}{2\pi} \int_{-\pi}^{\pi} W_{\lambda}(e^{j\theta}) X(e^{j(\hat{\omega}-\theta)})
  \, d\theta = X(e^{j\hat{\omega}})$ for each $\hat{\omega}$ from 3.
  above. Thus in this sense, we can say that the DTFT mapping in
  {eq}`e:wx-intWX` is *preserved* through the limiting process as
  $\lambda \rightarrow 1$.
  
* Consider now $x[n]$ is an infinite-energy sinusoid (or the unit
  step). For every $\lambda \in (0,1)$, the "windowed" signal 
  $w_{\lambda}[n] x[n] \in \ell^1$, and hence its DTFT
  $X_{w_{\lambda}}(e^{j\hat{\omega}})$ exists. 
  ```{caution}
  However, {eq}`e:wx-intWX` fails to hold, i.e.,
  $X_{w_{\lambda}}(e^{j\hat{\omega}})$ is not given by the RHS of
  {eq}`e:wx-intWX`, because the DTFT $X(e^{j\hat{\omega}})$ of $x[n]$
  simply does not exist!
  ```
  Nonetheless, we still have $\lim_{\lambda \rightarrow 1} w_{\lambda}[n] x[n] =
  x[n]$ for each $n \in \mathbb{Z}$. Thus, it makes intuitive sense to
  mimic the above limiting process in the case of absolutely summable signals to
  define a "DTFT" for the infinite-energy sinusoid $x[n]$. That is, we want to
  call $\lim_{\lambda \rightarrow 1}
  X_{w_{\lambda}}(e^{j\hat{\omega}})$ (if the limit exists) the DTFT of $x[n]$,
  even if such a "limit" may not be exactly a mathematically
  meaningful function in $\hat{\omega}$.
  ```{tip}
  In order to avoid using more math machinery, we will interpret this
  limiting process as our way to extend the DTFT toolset to
  infinite-energy signals. Note that as long as the
  windowed signal $w_{\lambda}[n] x[n] \in \ell^1$, $w_{\lambda}[n]
  x[n] \stackrel{\text{DTFT}}{\longleftrightarrow}
  X_{w_{\lambda}}(e^{j\hat{\omega}})$ and all the DTFT
  properties in {numref}`sec:dtft_table` apply to this proper DTFT
  mapping. As a result, all the DTFT properties also apply to the extended
  DTFT of $x[n]$ defined through the limiting process.
  ```

## Periodic Dirac delta "function"
* It is annoying however to keep referring to the above limiting
process and writing down $\lim_{\lambda \rightarrow 1}$ every time we
apply DTFT tools to an infinite-energy signal. For convenience, we
define the *periodic Dirac delta "function"*
$\delta(e^{j\hat{\omega}})$ as a mnemonic for the limiting
process. Specifically, properties 1.-3. above are re-expressed in
terms of $\delta(e^{j\hat{\omega}})$:
  1. $\displaystyle \delta(e^{j\hat{\omega}}) = 
      \begin{cases}
      \infty, & \hat\omega = 0 \bmod 2\pi \\
      0, & \hat\omega \neq 0 \bmod 2\pi
      \end{cases}
       ~~\left[ = \lim_{\lambda \rightarrow 1}
      \frac{W_{\lambda}(e^{j\hat\omega})}{2\pi} \right]$.
  2. $\displaystyle \int_{-\pi}^{\pi} \delta(e^{j\hat{\omega}}) \,
      d\hat{\omega} = 1$.
  3. For any bounded $X(e^{j\hat{\omega}})$ that is continuous at
     $\hat{\omega} = \hat{\omega}_0$,
     \begin{equation*}
     \int_{-\pi}^{\pi}
     \delta(e^{j\theta}) X(e^{j(\hat{\omega}_0-\theta)}) \, d\theta =
     X(e^{j\hat{\omega}_0}).
     \end{equation*}
      This is often referred to as the *sifting property* of the Dirac delta.
  ```{caution}
  * Note that $\delta(e^{j\hat{\omega}})$ is not a well-defined function
    in $\hat{\omega}$ by property 1. because its value is infinite when
    $\hat\omega = 0 \bmod 2\pi$. This infinite value implies
    that $a\delta(e^{j\hat{\omega}}) = \delta(e^{j\hat{\omega}})$ for
    any $a > 0$, which in turn implies $\delta(e^{j\hat{\omega}})
    \equiv 0$ contradicting 1. above. 
  * In fact, it is more appropiate to associate the scaled Dirac delta
    $a\delta(e^{j\hat{\omega}})$ with property 2. such that 
    $\displaystyle \int_{-\pi}^{\pi} a \delta(e^{j\hat{\omega}}) \,
    d\hat{\omega} = a$, i.e., the area underneath the Dirac delta
    over a period, rather than the "function" value, is scaled by the
    factor $a$. Property 2., not 1., provides the basis to perform
    linear algebraic operations with $\delta(e^{j\hat{\omega}})$.
  * The somewhat hand-waving limiting process associated with 
    $\delta(e^{j\hat{\omega}})$ can be made more rigorous by considering
    a sequuence of math objects called *distributions* in place of
    $\frac{W_{\lambda}(e^{j\hat\omega})}{2\pi}$. It turns out that
    there is a valid distribution, playing the role of
    $\delta(e^{j\hat{\omega}})$, that is the limit (in some sense)
    of the sequence of distributions corresponding to 
    $\frac{W_{\lambda}(e^{j\hat\omega})}{2\pi}$ as $\lambda
    \rightarrow 1$.
  ```
