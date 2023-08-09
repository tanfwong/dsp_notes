# $z$-Transform
* The $z$-transform $X(z)$ of a signal $x[n]$ is the *power series* (or infinite-degree
  polynomial) with the values of $x[n]$ as coefficients:
  \begin{equation*}
  X(z) = \sum_{n=-\infty}^{\infty} x[n] z^{-n}.
  \end{equation*}
* The *region of convergence (ROC)* of $X(z)$ is the set of complex
  numbers at which the power series converges.
  ```{tip}
  From the thoery of power series, there must be non-negative
  $r_1$ and $r_2$ (both could be $\infty$), specifying an open "ring"
  region $\mathcal{R}=\{z \in \mathbb{C}: r_1 < |z| < r_2 \}$ such that 
  $\sum_{n=-\infty}^{\infty} x[n] z^{-n}$ converges for 
  $z \in \mathcal{R}$ and diverges for $z \notin \mathcal{\bar R}$
  (the closure of $\mathcal{R}$).
  ```
