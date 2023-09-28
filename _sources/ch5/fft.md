# Fast Fourier Transform

* We use **Fast Fourier Transform (FFT)** to describe a general class
  of computationally efficient algorithms to calculate DFT and IDFT of
  any size.

* The main idea behind any FFT algorithm is to look for repetitive
  patterns in the calculation of DFT/IDFT and store results of
  calculations that can be repeatedly reused later to reduce the total
  amount of calculations needed. In this sense, FFT trades
  computational (or time) complexity against storage complexity.

* Typically, we look for the repetitive patterns by a
  divide-and-conquer approach:

  Suppose we want to calculate the $M$-point DFT of a signal
  $x[n]$. Write $M=p_1 p_2 \cdots p_{\nu}$, where $p_i$ is a factor of
  $M$. Note that the factors in this deposition need not be
  distinct. Repetitive patterns can then be established by rearranging
  the (1-D) signal $x[n]$ into a $\nu$-D array with sizes $p_1, p_2,
  \ldots, p_\nu$. For simplicity, we will consider only the case of
  *radix-2* ($M=2^\nu$) here.

* Write $\displaystyle w^k_M = e^{-j\frac{2\pi k}{M}}$. It is not hard
  to verify that the reduction rule for any product of terms in the
  form of $w^k_M$ is the same as that for a sum of the fractions
  $\frac{k}{M}$ modulo $1$ (i.e., the reduction rule for the sum
  fraction removing any whole number part). For example, $w^k_M \cdot
  w^{k'}_{M'} = w^l_N$ where $\frac{l}{N} = \left(\frac{k}{M} +
  \frac{k'}{M'} \right) \bmod 1$.

* Rewrite the forward DFT formula {eq}`e:dft` in terms of $w^k_M$:
  ```{math}
  :label: e:dftw
  \begin{equation}
  X_k = \sum_{k=0}^{M-1} x[n] w^{kn}_{M}.
  \end{equation}
  ```
