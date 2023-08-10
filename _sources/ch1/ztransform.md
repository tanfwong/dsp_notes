# $z$-Transform
* The $z$-transform $X(z)$ of a signal $x[n]$ is the *power series* (or infinite-degree
  polynomial) with the values of $x[n]$ as coefficients:
  \begin{equation*}
  X(z) = \sum_{n=-\infty}^{\infty} x[n] z^{-n}.
  \end{equation*}
* The *region of convergence (ROC)* of $X(z)$ is the set of complex
  numbers at which the power series converges.
  ```{tip}
  From the theory of power series, there must be non-negative
  $r_+$ and $r_-$ (both could be $\infty$), specifying the regions
  $\mathcal{R}_+ =\{z \in \mathbb{C}: |z| > r_+ \}$ and 
  $\mathcal{R}_- =\{z \in \mathbb{C}: |z| < r_- \}$ such that 
  $\sum_{n=-\infty}^{\infty} x[n] z^{-n}$ converges for 
  $z \in \mathcal{R}_+ \cap \mathcal{R}_-$ and diverges for $z \notin
  \mathcal{\bar R}_+ \cap \mathcal{\bar R}_-$, 
  where the bar denotes the closure of a subset in $\mathbb{C}$.
  ```
