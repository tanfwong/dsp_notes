# Discrete Fourier Transform

The frequency-domain sampling result given in {eq}`e:fsamp` motivates
  the following definition of $M$-point **Discrete Fourier Transform
  (DFT)** pair between a signal of length at most $M$ and the $M$
  frequency domain samples $X_k = X(e^{j\frac{2\pi k}{M}})$ for
  $k=0,1,2,\ldots,M-1$:

  **Forward DFT**:
  ```{math}
  :label: e:dft
  \begin{align}
  X_k &= \sum_{n=0}^{M-1} x[n] e^{-j\frac{2\pi kn}{M}} & k=0,1,2,
  \ldots, M-1
  \end{align}
  ```
  
  **Inverse DFT**:
  ```{math}
  :label: e:idft
  \begin{align}
  x[n] &= \frac{1}{M} \sum_{k=0}^{M-1} X_k e^{j\frac{2\pi kn}{M}} &
  n=0,1,2, \dots, M-1
  \end{align}
  ```

```{admonition} Notation
We use the notation $x[n] \stackrel{M\text{-DFT}}{\longleftrightarrow}
X_k$ to denote the mapping between a discrete-time signal of at most
length $M$ and its set of $M$-point DFT coefficients $\{X_k\}_{k=0}^{M-1}$.
```

## DFT properties
* Since the DFT coefficients $X_k$'s are the frequency-domain samples
  of the DTFT $X(e^{j\hat\omega})$, the properties of DTFT (see
  {numref}`sec:dtft_table`) carry over to DFT with the caveat that we
  have to consider the periodic extension $x_M[n]$ instead of $x[n]$
  when the operation involved makes the resulting signal violate the
  condition that its value must be zero except for $n=0,1,2,\ldots,M-1$.
  We consider two examples below.

* **Circular Time Shifting**:
  
  Let $x[n] \stackrel{\text{DTFT}}{\longleftrightarrow}
  X(e^{j\hat\omega})$. Then from the time shifting property of DTFT,
  we have $x[n-n_0] \stackrel{\text{DTFT}}{\longleftrightarrow}
 e^{-j\hat\omega n_0} X(e^{j\hat\omega})$. From {eq}`e:fsamp`, the
  frequency-domain samples $\{ e^{-j\frac{2\pi k n_0}{M}}
  X(e^{j\frac{2\pi k }{M}}) \}_{k=0}^{M-1}$ give the periodic
  extended signal $x_M[n-n_0]$. As the length of $x[n]$ is at most
  $M$, the period of $x_M[n-n_0]$ over $n=0,1,2,\dots, M-1$ is simply
  a circularly shifted version of $x[n]$ by $n_0$.
  ```{admonition} Notation
  We denote the circular shifting of the time index $n$ by $n_0$ with
  the notation $(n-n_0)\bmod M$ or $(n-n_0)_M$. For example, the
  circularly shifted version of $x[n]$ will be $x[(n-n_0)_M]$.
  ```
  Since the frequency-domain samples $\{ e^{-j\frac{2\pi k n_0}{M}}
  X(e^{j\frac{2\pi k }{M}}) \}_{k=0}^{M-1}$ are by definition the DFT
  coefficients of the circularly shifted $x[(n-n_0)_M]$, we have just
  established the DFT mapping:
  \begin{equation*}
  x[(n-n_0)_M] ~~\stackrel{M\text{-DFT}}{\longleftrightarrow} 
  ~~e^{-j\frac{2\pi k n_0}{M}} X_k
  \end{equation*}

* **Circular convolution**:

  Let $x[n] \stackrel{\text{DTFT}}{\longleftrightarrow}
  X(e^{j\hat\omega})$ and $y[n]
  \stackrel{\text{DTFT}}{\longleftrightarrow} Y(e^{j\hat\omega})$. The
  convolution property of DTFT gives $x[n]*y[n]
  \stackrel{\text{DTFT}}{\longleftrightarrow} X(e^{j\hat\omega})
  Y(e^{j\hat\omega})$. Then from {eq}`e:fsamp`, the frequency-domain
  samples $\{ X(e^{j\frac{2\pi k}{M}}) Y(e^{j\frac{2\pi
  k}{M}})\}_{k=0}^{M-1}$ give the periodic extended signal
  $(x*y)_M[n]$. 

  Let us examine  the signal $(x*y)_M[n]$ in detail for the case that
  the lengths of both $x[n]$ and $y[n]$ are at most $M$:
  ```{math}
  :label: e:circonv
  \begin{align}
  (x*y)_M[n]
  &=
  \sum_{m=-\infty}^{\infty} (x*y)[n+mM]
  \\
  &=
  \sum_{m=-\infty}^{\infty}  \sum_{k=-\infty}^{\infty} x[k]y[n+mM-k] 
  \\
  &=
  \sum_{k=-\infty}^{\infty} x[k] y_M[n-k]
  \\
  &=
  \sum_{k=0}^{M-1} x[k] y[(n-k)_M]
  \end{align}
  ```
   The last expression in {eq}`e:circonv` is similar to a convolution
  sum between $x[n]$ and $y[n]$, except that we use the circularly
  shifted version $y[(n-k)_M]$ instead. This observation motivates the
  following definition of circular convolution:
  ```{admonition} Notation
  $\displaystyle x[n] \circledast_M y[n] =  \sum_{k=0}^{M-1} x[k]
  y[(n-k)_M]$ denotes the **circular convolution** between two signals
  $x[n]$ and $y[n]$ of length at most $M$.
  ```
  With this definition, we get the following DFT mapping:
  \begin{equation*}
   x[n] \circledast_M y[n] ~~\stackrel{M\text{-DFT}}{\longleftrightarrow} 
   ~~ X_k Y_k
  \end{equation*}

  It is easy to check circular convolution has the following
  properties similar to standard convolution:
  - **Commutativity**:  $x[n] \circledast_M y[n] = y[n] \circledast_M
    x[n]$
  - **Associativity**: $(x[n] \circledast_M y[n]) \circledast_M z[n] =
    x[n] \circledast_M (y[n] \circledast_M z[n])$
  - **Distributivity**:  $x[n] \circledast_M (\alpha y[n] + \beta z[n]
    = \alpha x[n] \circledast_M y[n] + \beta  x[n] \circledast_M z[n]$
  - **Identity**: $x[n] \circledast_M \delta[n-k] = x[(n-k)_M]$ for
    $k=0,1,\ldots, M-1$
  - **Reduction to convolution**: Let $N$ and $L$ be the lengths of $x[n]$ and $y[n]$,
    respectively. If $M \geq N+L-1$, then $x[n] \circledast_M y[n] =
    x[n]*y[n]$.


## DFT property table
For each property listed below, assume both $x[n]$ and $y[n]$ are
signals of at most length $M$, as well as
$x[n] \stackrel{M\text{-DFT}}{\longleftrightarrow}
X_k$ and $y[n] \stackrel{M\text{-DFT}}{\longleftrightarrow}
Y(e^{j\hat\omega})$:
```{list-table}
:header-rows: 1

* - Property
  - Time domain
  - Frequency domain

* - Linearity
  - $\alpha x[n] + \beta y[n]$
  - $\alpha X_k + \beta Y_k$

* - Circular Time Shifting
  - $x[(n-n_0)_M]$
  - $e^{-j \frac{2\pi k n_0}{M}} X_k$

* - Circular Frequency Shifting
  - $x[n] e^{j \frac{2\pi ln}{M}}$
  - $X_{(k-l)_M}$

* - Conjugation 
  - $x^*[n]$
  - $X^*_{M-k}$

* - Time Reversal
  - $x[M-n]$ 
  - $X_{M-k}$

* - Circular Convolution
  - $x[n] \circledast_M y[n]$
  - $X_k Y_k$

* - Multiplication
  - $x[n] y[n]$
  - $\frac{1}{M} X_k \circledast_M Y_k$ 
    
* - Parseval Theorem
  - $\displaystyle \sum_{n=0}^{M-1} x[n] y^*[n]$
  - $\displaystyle \frac{1}{M} \sum_{k=0}^{M-1} X_k Y^*_k$
```


(sec:freq_fil)=
## Frequency-domain filtering using DFT

* The last property of circular convolution given above allows us to
  perform convolution $x[n]*y[n]$ in the frequency domain using DFT
  between signals of finite lengths:
  1. Let $N$ and $L$ be the lengths of $x[n]$ and $y[n]$. Choose $M
     \geq N+L-1$ (length of $x[n]*y[n]$).
  2. Calculate the $M$-point DFT of $x[n]$ to get $\{X_k\}_{k=0}^{M-1}$.
  3. Calculate the $M$-point DFT of $y[n]$ to get $\{Y_k\}_{k=0}^{M-1}$.
  4. Calculate the $M$-point IDFT of $\{X_k Y_k\}_{k=0}^{M-1}$ to
     obtain $x[n] \circledast_M y[n] = x[n]*y[n]$.

* Note that direct implementation of the step above, using the DFT and
  IDFT formulas {eq}`e:dft` and {eq}`e:idft`, is actually higher than
  doing convolution directly. Luckily, the FFT algorithms can
  significantly speed up the calculations of DFT and IDFT; thus making
  the frequency-domain analysis above much more computationally
  efficient.
