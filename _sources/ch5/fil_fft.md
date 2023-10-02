# Linear Filtering with FFT

* Consider passing a signal $x[n]$ of length $N$ to an FIR Filter with
  impulse response $h[n]$ of length $L$. In practice, we often have $N
  \gg L$. We will adopt this assumption in the discussion below.

* Direct implementation of the the convolution $h[n]*x[n]$ requires
  $\mathcal{O}(NL)$ complex multiplications (and additions). While
  performing the convolution in the frequency domain using  FFT algorithms
  to calculate DFT and IDFT as suggested in {numref}`sec:freq_fil`
  requires $\mathcal{O}(M\log_2 M)$ complex multiplications, where $M
  \geq N+L-1$. Since $N \gg L$, the computational complexity of this
  frequency-domain filtering approach is thus $\mathcal{O}(N\log_2 N)$.
