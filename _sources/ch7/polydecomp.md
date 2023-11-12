# Polyphase Decomposition & Related Identities

* We want to develop an efficient approach of implementing multi-rate
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
  
  
