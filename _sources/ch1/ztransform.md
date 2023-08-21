# $z$-Transform
* The $z$-transform $X(z)$ of a signal $x[n]$ is the *power series* (or infinite-degree
  polynomial) with the values of $x[n]$ as coefficients:
  ```{math}
  :label: e:z
  \begin{equation}
  X(z) = \sum_{n=-\infty}^{\infty} x[n] z^{-n}.
  \end{equation}
  ```
  ```{admonition} Notation
  We use the notation $x[n] \stackrel{z}{\longleftrightarrow} X(z)$ or
  $X(z)=\mathcal{Z}(x[n])$ to say that $X(z)$ is the $z$-transform of $x[n]$.
  ```
* The *region of convergence (ROC)* of $X(z)$ is the set of complex
  numbers at which the power series converges.
  ```{tip}
  From the standard power series results {cite}`rudin_baby`, there must be non-negative
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

## Properties and tables
Typically, it is more convenient to find the $z$-transform of a signal
by consulting a pair of tables listing common $z$-transform
properties and $z$-transform pairs. For example, see the [tables from
  Wikipedia](https://en.wikipedia.org/wiki/Z-transform).

**Use of table example**:

4. Consider 
    \begin{equation*}
     x_5[n] = n \cos(\hat\omega_0 n) u[n] 
     = \frac{1}{2} e^{j \hat\omega_0 n} u[n] 
     + \frac{1}{2} e^{-j \hat\omega_0 n} u[n].
    \end{equation*}
    Hence, the $z$-transform of $x_5[n]$ is
    \begin{align*}
     X_5(z) 
     &= \frac{1}{2}  \mathcal{Z}\left( ne^{j \hat\omega_0 n} u[n] \right) 
     + \frac{1}{2}  \mathcal{Z}\left( ne^{-j \hat\omega_0 n} u[n] \right) 
     & \text{(linearity)} \\
     & = \frac{e^{j \hat\omega_0} z^{-1}}{2(1 - e^{j \hat\omega_0} z^{-1})^2}
     + \frac{e^{-j \hat\omega_0} z^{-1}}{2(1 - e^{-j \hat\omega_0} z^{-1})^2}
     & \text{(directly from $z$-transfrom pair table)} \\
     & = \frac{(\cos\hat\omega_0) z^{-1} -2 z^{-2} + (\cos\hat\omega_0)
     z^{-3}}{\left( 1 - (2 \cos\hat\omega_0) z^{-1} + z^{-2} \right)^2}
    \end{align*}
    with ROC $=\{ |z|>1\}$.

## Inverse $z$-transform
Let $x[n] \stackrel{z}{\longleftrightarrow} X(z)$. The inverse
$z$-transform formula is 
\begin{equation*} 
x[n] = \frac{1}{2\pi j} \oint_C X(z) z^{n-1} dz 
\end{equation*} 
where $C$ is any closed counterclockwise contour in the ROC of $X(z)$
enclosing the origin.
```{tip}
- Since $X(z)$ is analytic (a power series), the contour integral may be
  calculated with the help of the Cauchy integral formula and/or the
  residue theorem {cite}`brown2009complex`.
- If $X(z)$ is rational, inverse $z$-transform of $X(z)$ may be
  performed by long division, or more commonly by the method of partial
  fraction expansion:
  1. Obtain the partial fraction expansion of $X(z)$.
  2. Perform table lookup to obtain the inverse $z$-transform of
     each partial fraction.
  3. Use linearity to combine the inverse $z$-transforms of all
     component partial fractions.
- Watch this
[video](https://ocw.mit.edu/courses/res-6-008-digital-signal-processing-spring-2011/resources/lecture-6-the-inverse-z-transform/)
by Prof. Oppenhiem from MIT Open Courseware for more discussions and
examples.
```

## Transfer function
- The *transfer function* $H(z)$ of an LTI system is the $z$-transform
of its impulse response $h[n]$, i.e., $h[n]
\stackrel{z}{\longleftrightarrow} H(z)$.

- From the fact that an LTI system is stable if and only if
$\sum_{n=-\infty}^{\infty} |h[n]| < \infty$, the LTI system is stable
if and only if the ROC of its transfer function $H(z)$ contains the
unit circle.

- For a causal FIR filter, $H(z) = \sum_{k=0}^M b_k z^{-k}$.
   
   For a causal IIR filter, $H(z) = \frac{\sum_{k=0}^M b_k z^{-k}}{\sum_{k=0}^N a_k z^{-k}}$
   
   In both cases, $H(z) = \frac{B(z)}{A(z)}$ is *rational*, where
   $B(z)$ and $A(z)$ are a numerator polynomial and a denominator
   polynomial in $z^{-1}$. 

## Poles and zeros
- **<u>Pole</u>**: 
  $z_p \in \mathbb{C}$ is a *pole* of $H(z)$ if $\lim_{z \rightarrow
  z_p} |H(z)| = \infty$.
- **<u>Zero</u>**:
  $z_0 \in \mathbb{C}$ is a *zero* of $H(z)$ if $H(z_0)=0$.
```{tip}
For a rational $H(z) = \frac{B(z)}{A(z)}$: 
- The roots of $B(z)$ gives the zeros of $H(z)$.
- The roots of $A(z)$ gives the poles of $H(z)$. 
- If $z_0$ is a root for both $B(z)$ and $A(z)$, then it does not
give a pole or zero because of cancellation of the same factor in
$B(z)$ and $A(z)$. 
```
- For a causal LTI system with a rational transfer function $H(z)$,
   the system is stable if and only if **all** its poles are strictly
   inside the unit circle.

