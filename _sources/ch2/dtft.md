# Discrete-Time Fourier Transform (DTFT)

* **<u>Forward DTFT</u>**:
  ```{math}
  :label: e:dtft
  \begin{equation}
  X(e^{j\hat\omega}) = \sum_{n=-\infty}^{\infty} x[n] e^{-j\hat\omega n}
  \end{equation}
  ```
* **<u>Inverse DTFT</u>**: 
  ```{math}
  :label: e:idtft
  \begin{equation}
  x[n] = \frac{1}{2\pi} \int_{-\pi}^{\pi} X(e^{j\hat\omega})
  e^{j\hat\omega n} d\hat\omega
  \end{equation}
  ```
```{admonition} Notation
1. We use the notation $x[n] \stackrel{\text{DTFT}}{\longleftrightarrow}
   X(e^{j\hat\omega})$ to denote the mapping between the
   signal $x[n]$ and its DTFT $X(e^{j\hat\omega})$ according to the
   forward and inverse DTFT formulas above.
2. A signal $x[n]$ is *absolutely summable*, denoted by $x[n] \in
   \ell^1$, if $\sum_{n=-\infty}^{\infty} |x[n]| < \infty$.
3. A DTFT function $X(e^{j\hat\omega})$ is *absolutely integrable* over $[-\pi,\pi]$,
   denoted by $X(e^{j\hat\omega}) \in L^1[-\pi,\pi]$, if 
   $\frac{1}{2\pi} \int_{-\pi}^{\pi} |X(e^{j\hat\omega})| d\hat\omega < \infty$.
```

## About convergence ...
* The RHS of the forward DTFT formula {eq}`e:dtft` is an infinite
  series, and thus we need to be a bit more careful about the condition for 
  it to converge as well as the type of the convergence. In addition,
  we also want a more careful specification for what the DTFT mapping 
  $x[n] \stackrel{\text{DTFT}}{\longleftrightarrow}
  X(e^{j\hat\omega})$ actually means.

* A simple sufficient condition that guarantees uniform convergence and 
  continuity of the infinite series on the RHS of {eq}`e:dtft` on $[-\pi,\pi]$ is 
  $x[n] \in \ell^1$. Under this condition, the DTFT as defined by {eq}`e:dtft`
  $X(e^{j\hat\omega}) = \sum_{n=-\infty}^{\infty} x[n] e^{-j\hat\omega n}
  \in L^1[-\pi,\pi]$. Thus, the integral on RHS of the inverse formula 
  {eq}`e:idtft` exists for each $n \in \mathbb{Z}$ and the inverse formula holds
  (recall the orthonormality of $\{e^{j\hat\omega n}\}_{n \in \mathbb{Z}}$ on 
  $[-\pi,\pi]$).

* On the other hand, given any DTFT $X(e^{j\hat\omega}) \in L^1[-\pi,\pi]$,
  the integral on The RHS of the inverse DTFT formula {eq}`e:idtft` exists for each 
  $n \in \mathbb{Z}$. Let $x[n]$ be the signal given
  by the inverse DTFT formula {eq}`e:idtft`. If $x[n] \in \ell^1$, then we
  have $X(e^{j\hat\omega})$ equals $\sum_{n=-\infty}^{\infty} x[n] e^{-j\hat\omega
  n}$ *almost everywhere* on $[-\pi,\pi]$ (w.r.t. the Lebesgue
  measure) {cite}`rudin1987real`. 
  
* Indeed, by grouping all aboslutely integrable DTFTs that
  differ only in a subset of length $0$ into the same equivalence
  class, the conclusion in the two bullet points above gives a concrete notion 
  to the *mapping* $x[n] \stackrel{\text{DTFT}}{\longleftrightarrow}
  X(e^{j\hat\omega})$ defined by the forward and inverse DTFT
  formulas for the pair $x[n] \in \ell^1$ and $X(e^{j\hat\omega}) \in
  L^1[-\pi,\pi]$.
  ```{caution}
  This doesn't mean that the DTFT mapping is a *bijection*
  between the set of absolutely summable signals and the set of
  absolutely integrable DTFTs because there exist signals $x[n] \notin
  \ell^1$ that are given
  by the inverse DTFT formula {eq}`e:idtft` with $X(e^{j\hat\omega}) \in
  L^1[-\pi,\pi]$. Can you give one such counterexample?
  ```

* For any $x[n] \in \ell_1$ (or equivalently the ROC of its $z$-transform
  $X(z)$ contains the unit circle), $\left. X(z)
  \right|_{z = e^{j\hat\omega}} = \sum_{n=-\infty}^{\infty} x[n]
  e^{-j\hat\omega n}$ converges (uniformly) on $[-\pi,\pi]$. 
  This means that $x[n] \stackrel{\text{DTFT}}{\longleftrightarrow} \left. X(z)
  \right|_{z = e^{j\hat\omega}}$, i.e., *evaluating the $z$-transform
  $X(z)$ of $x[n]$ on the unit circle gives the DTFT
  $X(e^{j\hat\omega})$ of $x[n]$*.

## More about convergence ...
