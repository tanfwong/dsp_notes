# Frequency-domain Sampling

* The sampling theorem (see {numref}`sec:sampthm`) tells us that we
  can reconstruct a bandlimited continuous-time signal $x(t)$ with
  bandwidht $B$ Hz from its samples $x[n]=x\left(\frac{n}{f_s}\right)$
  as long as we oversample, i.e., choose the sampling frequency $f_s >
  2B$.

* One may ask whether a similar result applies to sampling the FT
  $X(\omega)$ in the frequency domain. That is, can we get back
  $X(\omega)$ (and hence $x(t)$) from its samples? If so, what is the
  condition under which we can do that. 

* We will answer the above questions in the context of a discrete-time
  signal $x[n]$ and its DTFT $X(e^{j\hat\omega})$, leaving the
  continuous-time counterpart as an exercise. More specifically,
  consider $x[n] \stackrel{\text{DTFT}}{\longleftrightarrow}
  X(e^{j\hat\omega})$. Suppose we take $M$ samples in one period of
  $X(e^{j\hat\omega})$ at the normalized radian frequencies
  $\hat\omega = \frac{2\pi k}{M}$ for $k=0,1,\ldots,M-1$.

