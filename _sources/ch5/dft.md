# Discrete Fourier Transform

* The frequency-domain sampling result given in {eq}`e:fsamp` motivates
  the  following definition of $M$-point **Discrete Fourier Transform
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
