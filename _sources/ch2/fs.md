# Fourier Series

For a continuous-time periodic signal $s(t)$ of period $T$, i.e.,
$s(t+T) = s(t)$ for all $t \in \mathbb{R}$:

* **<u>Synthesis</u>**:
  ```{math}
  :label: e:fs_syn
  \begin{equation}
  s(t) = \sum_{n=-\infty}^{\infty} a_n e^{j\frac{2\pi n t}{T}}
  \end{equation}
  ```
* **<u>Analysis</u>**: 
  ```{math}
  :label: e:fs_ana
  \begin{equation}
  a_n = \frac{1}{T} \int_{-T/2}^{T/2} s(t) e^{-j\frac{2\pi n t}{T}}
  dt, ~~~n \in \mathbb{Z}
  \end{equation}
  ```
The complex numbers $\{a_n\}_{n \in \mathbb{Z}}$ are called the
*Fourier series (FS) coefficients* of $s(t)$.

* Considering the "change of variable" $t = -\frac{\hat\omega
  T}{2\pi}$, $s( -\frac{\hat\omega T}{2\pi})$ is periodic in
  $\hat\omega$ with period $2\pi$. Treating $s( -\frac{\hat\omega
  T}{2\pi})$ as $X(e^{j\hat\omega})$ and $a_n$ as $x[n]$, the FS
  synthesis and analysis formulas, {eq}`e:fs_syn` and {eq}`e:fs_ana`,
  become the forward and inverse DTFT formulas, {eq}`e:dtft` and
  {eq}`e:idtft`, respectively. As a result, all the convergence
  results for DTFT apply to FS under this translation.

* In particular, the Riesz-Fisher theorem tells us that for each (up
  to an equivalence class) periodic $s(t) \in L^2\left[-\frac{T}{2},
  \frac{T}{2}\right]$ (i.e., $s(t)$ has finite *power*), there is a
  unique FS coefficient sequence $\{a_n\}_{n \in \mathbb{Z}} \in
  \ell^2$ such that both FS synthesis and analysis formulas,
  {eq}`e:fs_syn` and {eq}`e:fs_ana`, hold with the convergence in the
  infinite series on the RHS of the synthesis formula interpreted as
  \begin{equation*} 
  \lim_{N \rightarrow \infty} \frac{1}{T}
  \int_{-T/2}^{T/2} \left| s(t) - \sum_{n=-N}^{N} a_n e^{j\frac{2\pi n
  t}{T}} \right|^2 dt = 0.  
  \end{equation*} 
  The power of $s(t)$ is given by $\displaystyle \frac{1}{T} 
  \int_{-T/2}^{T/2} |s(t)|^2 dt = \sum_{n=-\infty}^{\infty} |a_n|^2$.

* The extension of DTFT for infinite-energy signals also translates to
  a similar extension of FS for FS coefficient sequences $\{a_n\}_{n
  \in \mathbb{Z}} \notin \ell^2$ by the change of variable $\hat\omega
  = -\frac{2\pi t}{T}$ and the substitutions $a_n \leftarrow x[n]$
  and $x\left( -\frac{2\pi t}{T} \right) \leftarrow X(e^{j\hat\omega})$.

  **Example**: 
  From the example in {numref}`sec:dtft_ex1` and
  linearity, we have $\frac{1}{T} \stackrel{\text{DTFT}}{\longleftrightarrow} 
  \frac{2\pi}{T} \delta (e^{j\hat{\omega}})$. By the above change of
  variable, the FS coefficients of the periodic (period $=T$) signal $\frac{2\pi}{T} 
  \delta \left(e^{-j \frac{2\pi t}{T}}\right) = \frac{2\pi}{T} \delta \left(e^{j
  \frac{2\pi t}{T}} \right)$ (recall $\delta (e^{j\hat{\omega}})$ is an even
  function) are $a_n = \frac{1}{T}$ for all $n \in \mathbb{Z}$. Hence,
  the FS synthesis formula  {eq}`e:fs_syn` becomes
  ```{math}
  :label: e:poisson
  \begin{equation}
  \frac{2\pi}{T} \delta \left(e^{j \frac{2\pi t}{T}} \right)
  = \frac{1}{T} \sum_{n=-\infty}^{\infty} e^{j\frac{2\pi n t}{T}}
  \end{equation}
  ```
  which is often referred to as the **<em>Poisson sum formula</em>**.
  ```{tip}
  Note that the Poisson sum formula {eq}`e:poisson` above
  is simply a mnemonic for the limiting process of the mapping between
  the window signal $w_{\lambda}[n]$ and its DTFT 
  $W_{\lambda}(e^{j\hat\omega})$, i.e., $\displaystyle
  W_{\lambda}\left(e^{-j \frac{2\pi t}{T}} \right) = 
  \sum_{n=-\infty}^{\infty} \lambda^{|n|} e^{j\frac{2\pi n
  t}{T}}$, as $\lambda \rightarrow 1$.
  ```
