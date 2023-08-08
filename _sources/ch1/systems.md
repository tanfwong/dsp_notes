# Discrete-time systems
* A discrete-time system maps an input signal $x[n]$ to an output
  signal $y[n]$.
  ```{admonition} Notation
  Denote the system $\mathcal{T}$ as an operator that acts on $x[n]$:
  \begin{equation*}
  y[n] = \mathcal{T}(x[n])
  \end{equation*}
  or with a <em>block diagram</em>:
  \begin{equation*}
  x[n] \xrightarrow{\hspace{30pt}}
  \boxed{ 
  \begin{array}{ccc} 
  & & \\[-10pt] 
  & \mathcal{\Large T} & \\[-10pt] 
  & &
  \end{array}}
  \xrightarrow{\hspace{30pt}}  y[n]
  \end{equation*}
  ```
* In most cases, we care only about this I/O mapping, which may be
  specified by the:
  - **difference equation**
  - **impulse response** $h[n]$
  - **frequency response** $H(e^{j\hat\omega})$ 
  - **transfer function** $H(z)$
  - block diagram 
     
     $\hspace{30pt} \vdots$

## LTI and stability
* **<u>Linearity</u>**:
  
  A system $\mathcal{T}$ is *linear* if
  $\mathcal{T} ( \alpha x_1[n] + \beta x_2[n]) =
  \alpha \mathcal{T} (x_1[n]) + \beta \mathcal{T}(x_2[n])$
  for all $\alpha$, $\beta$, $x_1[n]$, and $x_2[n]$.

* **<u>Time invariance</u>**:

  A system $\mathcal{T}$ is *time-invariant* if $\mathcal{T} (
  x[n]) = y[n]$ implies $\mathcal{T} ( x[n-n_0]) = y[n-n_0]$ for all
  $n_0$ and $x[n]$.

* **<u>Causality</u>**:

  A system $\mathcal{T}$ is *causal* if $\mathcal{T} (
  x[n]) $ depends only on the current and past input, i.e., $x[n]$,
  $x[n-1]$, $\ldots$.

* **<u>Bounded Input Bounded Output (BIBO) stability</u>**:

  A system $\mathcal{T}$ is *(BIBO) stable* if 
  $|\mathcal{T} (x[n])| \leq M_y < \infty$ for every $x[n]$ that
  satisfies $|x[n]| \leq M_x < \infty$.

## Impulse response and convolution
* The *impulse response* $h[n]$ of a system $\mathcal{T}$ is
  the system's output when the input is the unit impulse signal, i.e.,
  $h[n] = \mathcal{T}(\delta[n])$.
* **<u>Convolution</u>**: 

  For any LTI system $\mathcal{T}$ with impulse response $h[n]$
  and any input $x[n]$, the output is given by
  \begin{equation*}
  \mathcal{T}(x[n]) = \sum_{k=-\infty}^{\infty} x[k] h[n-k].
  \end{equation*}
  - *"Proof":* Write $x[n] = \sum_{k=-\infty}^{\infty} x[k]
    \delta[n-k]$. Then
    \begin{align*}
    \mathcal{T}(x[n]) &= \mathcal{T}\left( \sum_{k=-\infty}^{\infty}
    x[k] \delta[n-k] \right) \\
    &= \sum_{k=-\infty}^{\infty} x[k] \mathcal{T}(\delta[n-k] ) &
    (\mathcal{T} \text{ is linear})\\
    &= \sum_{k=-\infty}^{\infty} x[k] h[n-k] & (\mathcal{T}  \text{ is time-invariant})
    \end{align*}
    ```{note}
    In above and also hereafter, implictly convergence (in some sense)
    is assumed when we write an infinite series like
    $\sum_{k=-\infty}^{\infty} x[k] h[n-k]$.
    We may sometimes discuss more about the assumed convergence.
    ```
    ```{admonition} Notation
    Write the convolution sum using the following notation:
    \begin{equation*}
    \sum_{k=-\infty}^{\infty} x[k] h[n-k] = x[n]*h[n] = (x*h)[n].
    \end{equation*}
    
    ```
