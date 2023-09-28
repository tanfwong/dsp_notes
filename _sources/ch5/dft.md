# Discrete Fourier Transform

The frequency-domain sampling result given in {eq}`e:fsamp` motivates
  the following definition of $M$-point **Discrete Fourier Transform
  (DFT)** pair between a signal of length at most $M$ and the $M$
  frequency domain samples $X_k = X(e^{j\frac{2\pi k}{M}})$ for
  $k=0,1,2,\ldots,M-1$:

  **Forward DFT**:
  \begin{align*}
  X_k &= \sum_{n=0}^{M-1} x[n] e^{-j\frac{2\pi kn}{M}} & k=0,1,2,
  \ldots, M-1
  \end{align*}
  
  **Inverse DFT**:
  \begin{align*}
  x[n] &= \frac{1}{M} \sum_{k=0}^{M-1} X_k e^{j\frac{2\pi kn}{M}} &
  n=0,1,2, \dots, M-1
  \end{align*}

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
  - $X_k \circledast_M Y_k$ 
    
* - Parseval Theorem
  - $\displaystyle \sum_{n=0}^{M-1} x[n] y^*[n]$
  - $\displaystyle \frac{1}{M} \sum_{k=0}^{M-1} X_k Y^*_k$
```
