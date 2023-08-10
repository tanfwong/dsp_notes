# $z$-Transform
* The $z$-transform $X(z)$ of a signal $x[n]$ is the *power series* (or infinite-degree
  polynomial) with the values of $x[n]$ as coefficients:
  ```{math}
  :label: e:z
  \begin{equation}
  X(z) = \sum_{n=-\infty}^{\infty} x[n] z^{-n}.
  \end{equation}
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
  - If $r_- < r_+$, then the power series does not converge at any $z
  \in \mathbb{C}$ and $x[n]$ does not have a $z$-transform.
  - If $x[n]$ is causal (i.e., $x[n]=0$ for all $n<0$), then $r_- =
  \infty$ and hence the ROC includes $\mathcal{R}_+$. 
  - If  $x[n]$ is *anti-causal* (i.e., $x[n]=0$ for all $n \geq 0$), 
  then $r_+ = 0$ (and the power series also trivially converges at $z=0$)
  and hence the ROC includes $\mathcal{R}_-$.
  - Convergence on the boundaries of $\mathcal{R}_+$ and
  $\mathcal{R}_-$ needs to be worked out for each specific $x[n]$.
  
  ```

## Examples
1. Consider the causal signal $x_1[n] = a^n u[n]$, where $a$ is a complex number.
   From {eq}`e:z`, we have
   \begin{align*}
   X_1(z) 
   &= \sum_{n=-\infty}^{\infty} x_1[n] z^{-n} \\
   &= \sum_{n=-\infty}^{\infty} a^n u[n] z^{-n} \\
   &= \sum_{n=0}^{\infty} \left( a z^{-1} \right)^n \\
   &= \begin{cases}
     \frac{1}{1-az^{-1}}, & |z|>|a| \\
     \text{diverges}, & |z| \leq |a|.
     \end{cases}
   \end{align*}
   Thus, the $z$-transform of $x_1[n]$ is $X_1(z) = \frac{1}{1-az^{-1}}$
   with ROC $= \{ z \in \mathbb{C}:  |z|>|a|\}$.
