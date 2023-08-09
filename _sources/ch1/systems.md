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
  
  A system $\mathcal{T}$ is *linear (L)* if
  $\mathcal{T} ( \alpha x_1[n] + \beta x_2[n]) =
  \alpha \mathcal{T} (x_1[n]) + \beta \mathcal{T}(x_2[n])$
  for all $\alpha$, $\beta$, $x_1[n]$, and $x_2[n]$.

* **<u>Time invariance</u>**:

  A system $\mathcal{T}$ is *time-invariant (TI)* if $\mathcal{T} (
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
    ```{admonition} Assumption
    :class: important
    In above and also hereafter, implict convergence (in some sense)
    is assumed when we write an infinite series like
    $\sum_{k=-\infty}^{\infty} x[k] h[n-k]$.
    We may sometimes discuss more about the assumed convergence.
    ```
    ```{admonition} Notation
    Write the convolution sum using the following notation:
    \begin{equation*}
    \sum_{k=-\infty}^{\infty} x[k] h[n-k] = x[n]*h[n] = (x*h)[n]
    \end{equation*}
    
    ```
    ```{tip}
    $y[n] = x[n]*h[n]$ can also be viewed as a matrix multiplication:
    \begin{equation*}
    \left[
    \begin{array}{c}
    \vdots \\
    y[-1] \\
    y[0] \\
    y[1] \\
    \vdots
    \end{array}
    \right] 
    = 
    \left[
    \begin{array}{ccccc}
    & \vdots & \vdots & \vdots \\
    \cdots & h[0] & h[-1] & h[-2] & \cdots \\
    \cdots & h[1] & h[0] & h[-1] & \cdots \\
    \cdots & h[2] & h[1] & h[0] & \cdots \\
    & \vdots & \vdots & \vdots \\
    \end{array}
    \right] 
    \left[
    \begin{array}{c}
    \vdots \\
    x[-1] \\
    x[0] \\
    x[1] \\
    \vdots
    \end{array}
    \right] 
    \end{equation*}

    ```
* **<u>Algebraic properties of convolution</u>**
  - **Commutativity**: $x_1[n]*x_2[n] = x_2[n]*x_1[n]$
  - **Associativity**:  $x_1[n]*(x_2[n]*x_3[n]) =
    (x_1[n]*x_2[n])*x_3[n]$
  - **Distributivity**: $(\alpha x_1[n]+ \beta x_2[n])*h[n] = \alpha
    x_1[n]*h[n] + \beta x_2[n]*h[n]$
  - **Identity**: $x[n] * \delta[n-n_0] = x[n-n_0]$

## LTI system, FIR and IIR filters 
* An LTI system with impulse response $h[n]$ is causal if and only if
  $h[n] = 0$ for all $n<0$.
  ```{admonition} Notation
  It is common to slightly abuse the terminology to call a signal
  $x[n]$, which may not be associated with the impulse response of 
  any LTI system, *causal* if $x[n]=0$ for all $n<0$.
  ```
* An LTI system  with impulse response $h[n]$ is (BIBO) stable if and only if
  $\sum_{n=-\infty}^{\infty} |h[n]| < \infty$.
* The cascade of two LTI systems with impulse responses $h_1[n]$ and
  $h_2[n]$ is LTI with impulse response $h_1[n]*h_2[n]$.
* **FIR filter**:
  A causal *finite-impulse-response (FIR) filter* is an LTI system
  that is specified by the difference equation
  \begin{equation*}
  y[n] = \sum_{k=0}^M b_k x[n-k]
  \end{equation*}
  where $b_0, b_1, \ldots, b_M$ are the *filter taps*,  $M$ is the
  *filter order*, and $L=M+1$ is the *filter length*. Clearly, the filter's
  impulse response is $h[n] = \sum_{k=0}^M b_k \delta[n-k]$.
* **IIR filter**:
  A causal *infinite-impulse-response (IIR) filter* is an LTI system
  that is specified by the difference equation
  \begin{equation*}
  \sum_{k=0}^N a_k y[n-k] = \sum_{k=0}^M b_k x[n-k]
  \end{equation*}
  where $a_0=1$, $a_1,a_2, \ldots, a_N$ are the *feedback* taps, and
  $b_0, b_1, \ldots, b_M$ are the *feedforward* taps.
  ```{caution}
  $N$ (not $M$) is usually referred to as the order of the IIR filter.
  ```
