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
   with ROC $= \{|z|>|a|\}$.
   ```{admonition} Notation
   Instead of writing $\{ z \in \mathbb{C}:  |z|>|a|\}$ all the time,
   we will henceforth use the shorthand notation $\{|z|>|a|\}$.
   ```

2. Consider the anti-causal signal $x_2[n] = -a^n u[-n-1]$, where $a$ is a complex number.
   From {eq}`e:z`, we have
   \begin{align*}
   X_2(z) 
   &= \sum_{n=-\infty}^{\infty} x_2[n] z^{-n} \\
   &= -\sum_{n=-\infty}^{\infty} a^n u[-n-1] z^{-n} \\
   &= -\sum_{m=1}^{\infty} \left( a^{-1} z \right)^m \\
   &= 1 - \sum_{m=0}^{\infty} \left( a^{-1} z \right)^m \\
   &= \begin{cases}
     1-\frac{1}{1-a^{-1}z}, & |z|<|a| \\
     \text{diverges}, & |z| \geq |a|.
     \end{cases}
   \end{align*}
   Thus, the $z$-transform of $x_2[n]$ is $X_2(z) = \frac{1}{1-az^{-1}}$
   with ROC $= \{|z|<|a|\}$.
   ```{caution}
   - Note that $X_1(z)$ and $X_2(z)$ have the same expression but
     different ROCs.
   - In general, the expression **AND** the ROC of $X(z)$ together uniquely
   determine $x[n]$.
   ```
3. Consider the signals $u[n]$, $x_3[n] = \frac{1}{n} u[n-1] $ and
   $x_4[n] = \frac{1}{n^2}u[n-1] $.
   - From Example 1. above, the $z$-transform of $u[n]$ is $U(z) =
     \frac{1}{1-z^{-n}}$ with ROC $= \{ |z|>1\}$.
   - Clearly, $X_3(z) = \sum_{n=1}^{\infty} \frac{z^{-1}}{n}$
     converges for $|z|>1$ and diverges for $|z|<1$. It turns out that
     $X_3(z)$ also converges for every $z$ on the unit circle (i.e.,
     $|z|=1$) except at $z=1$ where the power series diverges. Hence,
     the ROC of $X_3(z)$ is $\{ |z| \geq 1\} \setminus \{z=1\}$.
   - It can also be shown that $X_4(z) = \sum_{n=1}^{\infty}
     \frac{z^{-n}}{n^2}$ converges for $|z| \geq 1$ and diverges for
     $|z| < 1$. Hence, the ROC of $X_4(z)$ is $\{ |z| \geq 1\}$.
