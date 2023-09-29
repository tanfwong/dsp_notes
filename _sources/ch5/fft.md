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

## Radix-2 Decimation-in-Time Algorithm

* Let $x[n]$ be of length at most $M=2^{\nu}$. We will use binary
  sequences of length at most $\nu -1$ bits to index "sub-signals"
  generated from $x[n]$. Let $b$ be a binary sequence ($b$ can be a
  null sequence). Then $0b$ and  $1b$ denote
  concatenating a most significant bit to $b$.

* Define $x^{(\nu)}[n] = x[n]$. For $i=\nu-1, \nu-2, \ldots, 1$,
  define iteratively:
  \begin{align*}
  x^{(i)}_{0b}[n] &= x^{(i+1)}_b [2n] \\
  x^{(i)}_{1b}[n] &= x^{(i+1)}_b [2n+1] 
  \end{align*}
  for each $n=0,1,\ldots,2^i-1$ and each binary sequence $b$ of length $\nu-1-i$.

* Note that the length of $x^{(i)}_{b}[n]$  is $2^i$. 
  Write the $2^i$-point DFT of $x^{(i)}_{b}[n]$ as:
  \begin{align*}
  X^{(i)}_{b,k} &= \sum_{n=0}^{2^i-1} x^{(i)}_{b}[n] w^{kn}_{2^i} &
  k=0,1,\ldots, 2^i-1.
  \end{align*}

* Now, consider the forward DFT formula {eq}`e:dftw`:
  ```{math}
  :label: e:fft_dit1
  \begin{align}
  X_k 
  &= 
  \sum_{n=0}^{2^\nu-1} x^{(\nu)}[n] w^{kn}_{2^\nu}
  \\
  &=
  \sum_{n=0}^{2^{\nu-1}-1} x^{(\nu)}[2n]  w^{k(2n)}_{2^\nu} +
  \sum_{n=0}^{2^{\nu-1}-1} x^{(\nu)}[2n+1]  w^{k(2n+1)}_{2^\nu} 
  \\
  &=
  \sum_{n=0}^{2^{\nu-1}-1} x^{(\nu-1)}_0[n] w^{kn}_{2^{\nu-1}} +
  w^{k}_{2^\nu}  \left(
  \sum_{n=0}^{2^{\nu-1}-1} x^{(\nu-1)}_1[n] w^{kn}_{2^{\nu-1}} 
  \right)
  & k=0,1,\ldots,2^\nu -1
  \end{align}
  ```
  Notice that the two sums in the last expression of {eq}`e:fft_dit1` above are simply 
  $2^{\nu-1}$-point DFTs. We may rewrite {eq}`e:fft_dit1` in the
  following form:
  ```{math}
  :label: e:fft_dit2
  \begin{align}
  X_k 
  & =
  X^{(\nu-1)}_{0,k} +  w^{k}_{2^\nu} X^{(\nu-1)}_{1,k}
  \\
  X_{k+2^{\nu-1}} 
  &= 
  X^{(\nu-1)}_{0,k} +w^{k+2^{\nu-1}}_{2^\nu} X^{(\nu-1)}_{1,k}
  & k=0,1,\ldots,2^{\nu-1} -1
  \end{align}
  ```
* Repeat the decomposition above recursively, we get, for $i=\nu-1, \nu-2, \ldots, 1$,
  ```{math}
  :label: e:fft_dit3
  \begin{align}
  X^{(i)}_{b,k} 
  & =
  X^{(i-1)}_{0b,k} +  w^{k}_{2^i} X^{(i-1)}_{1b,k}
  \\
  X^{(i)}_{b,k+2^{i-1}} 
  &= 
  X^{(i-1)}_{0b,k} +w^{k+2^{i-1}}_{2^i} X^{(i-1)}_{1b,k}
  \end{align}
  ```
    for each $k=0,1,\ldots,2^{i-1} -1$ and each binary sequence $b$ of
    length $\nu-i$ until reaching the trivial terminating case:
    ```{math}
  :label: e:fft_dit4
  \begin{align}
  X^{(1)}_{b,0} 
  &=
  X^{(0)}_{0b,0} + w^{0}_{2} X^{(0)}_{1b,0}
  =
  x^{(0)}_{0b}[0] + x^{(0)}_{1b}[0]
  \\
  X^{(1)}_{b,1} 
  &= 
  X^{(0)}_{0b,0} + w^{1}_{2} X^{(0)}_{1b,0}
  =
  x^{(0)}_{0b}[0] - x^{(0)}_{1b}[0]
  \end{align}
  ```
  for each binary sequence $b$ of length $\nu-1$. 
  Note that in {eq}`e:fft_dit4`, for each binary sequence $b$ of
  length $\nu$, $x^{(0)}_{b}[0] = x[b]$ where $b$ in $x[b]$ should be
  interpreted as the standard binary representation of the time index
  $n$ in $x[n]$. For example, if $\nu = 4$, $x^{(0)}_{1000}[0] = 
  x[1000] = x[8]$.

* The decomposition from {eq}`e:fft_dit2` to  {eq}`e:fft_dit4` shows
  that the original $2^{\nu}$-point DFT of $x[n]$ can be obtained as a
  simple combination of two $2^{\nu-1}$-point DFTs (see
  {eq}`e:fft_dit2`), each of which can be calculated from two
  $2^{\nu-2}$-point DFTs and so on (see {eq}`e:fft_dit2`) until the
  terminating case of $2$-point DFTs that can be calculated trivially
  from the time-domain signal $x[n]$ (see  {eq}`e:fft_dit4`). This
  recursive process is best expressed by the well known
  ***butterfly*** diagram. For example, see the following butterfly
  diagram for the case of $M=2^3 = 8$:
  ```{image} ../figs/fft_dit_bfly.jpg
  :alt: 8-point decimation-in-time FFT butterfly 
  :width: 800px
  :align: center
  ```
  
