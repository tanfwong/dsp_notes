(sec:polydecomp)=
# Polyphase Decomposition & Related Identities

* We want to develop an efficient way to implement multi-rate
  filters. To that end, we start by introducing a number of simple
  algebraic results that help such a development.

## Polyphase Decomposition
* Let $h[n] \stackrel{z}{\longleftrightarrow} H(z)$ be the impulse
  response and transfer function of an LTI filter.
  Fix a positive integer $M$. Define
  ```{math}
  :label: e:ek
  \begin{equation}
  e_k [n] = h[nM+k]
  \end{equation}
  ```
  for $k=0,1,\ldots,M-1$. We may interpret that $e_k[n]$ is obtained
  from downsampling $h[n+k]$, which is referred to as a **phase** of
  $h[n]$, by factor $M$.

* Let $e_k[n] \stackrel{z}{\longleftrightarrow} E_k(z)$. Then
  ```{math}
  :label: e:polydecomp
  \begin{align}
  H(z) 
  &=
  \sum_{n=-\infty}^{\infty} h[n] z^{-n} 
  \\
  &=
  \sum_{k=0}^{M-1} \sum_{m=-\infty}^{\infty} h[mM+k] z^{-(mM+k)}
  \\
  &=
  \sum_{k=0}^{M-1} \left( \sum_{m=-\infty}^{\infty} e_k[m] z^{-mM}
  \right) z^{-k}
  \\
  &=
  \sum_{k=0}^{M-1}  z^{-k} E_k(z^M)
  \end{align}
  ```
  which is called the **polyphase decomposition** of the filter $H(z)$.
  It implies the following structures for implementing $H(z)$:
  - **Direct polyphase form**:
    ```{image} ../figs/polyd.jpg 
    :alt: Direct polyphase form
    :width: 800px 
    :align: center 
    ``` 
  - **Transposed polyphase form**:
    ```{image} ../figs/polyt.jpg 
    :alt: Transposed polyphase form
    :width: 800px 
    :align: center 
    ``` 
  
## Downsampling Identity
* The following two systems are equivalent:
  ```{image} ../figs/downid.jpg 
  :alt: Downsampling identity
  :width: 800px 
  :align: center 
  ``` 
* We call the equivalence above the **downsampling identity**. It can
  be shown by first recalling from {eq}`e:downz` that 
  \begin{equation*}
  X_D(z) = \frac{1}{D} \sum_{k=0}^{D-1} X\left(  e^{-j\frac{2\pi k}{D}}
  z^{\frac{1}{D}} \right).
  \end{equation*}
  Moreover, $\tilde{Y}(z) = H(z^D) X(z)$ from the second system in the
  figure above. From the first system, we have 
  \begin{align*}
  Y(z) 
  &=
  H(z) X_D(z)
  \\
  &=
  \frac{1}{D} \sum_{k=0}^{D-1} H(z) X\left(  e^{-j\frac{2\pi k}{D}}
  z^{\frac{1}{D}} \right)
  \\
  &=
  \frac{1}{D} \sum_{k=0}^{D-1} H\left( \left(e^{-j\frac{2\pi k}{D}}
  z^{\frac{1}{D}} \right)^D \right) X\left(  e^{-j\frac{2\pi k}{D}}
  z^{\frac{1}{D}} \right)
  \\
  &=
  \frac{1}{D} \sum_{k=0}^{D-1} \tilde{Y}\left(  e^{-j\frac{2\pi k}{D}}
  z^{\frac{1}{D}} \right).
  \end{align*}
  That is to say $y[n]$ is the downsampled version of $\tilde{y}[n]$
  by factor $D$; thus establishing the equivalence of the two systems.

## Upsampling Identity
* The following two systems are equivalent:
  ```{image} ../figs/upid.jpg 
  :alt: Upsampling identity
  :width: 800px 
  :align: center 
  ``` 
* We call the equivalence above the **upsampling identity**. To show
  this identity, recall from {eq}`e:upz` that $X^U(z) = X(z^U)$ in the
  second system. Similarly, considering the first system, we have
  \begin{align*}
  Y(z) 
  &= \tilde{Y}(z^U)
  \\
  &= H(z^U) X(z^U)
  \\
  & = H(z^U) X^U(z)
  \end{align*}
  which is exactly the output of the second system; thus establishing
  the identity.
  