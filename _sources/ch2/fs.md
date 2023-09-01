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
  to an equivalence class) 
  periodic $s(t) \in L^2\left[-\frac{T}{2}, \frac{T}{2}\right]$, there is a
  unique FS coefficient sequence $\{a_n\}_{n \in \mathbb{Z}} \in
  \ell^2$ such that both FS synthesis and analysis formulas,
  {eq}`e:fs_syn` and {eq}`e:fs_ana`, hold with the convergence in the
  infinite series on the RHS of the synthesis formula interpreted as 
  \begin{equation*}
  \lim_{N \rightarrow \infty} \frac{1}{T} \int_{-T/2}^{T/2} \left|
  s(t) - \sum_{n=-N}^{N} a_n e^{j\frac{2\pi n t}{T}} \right|^2 dt = 0.
  \end{equation*}

