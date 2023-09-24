# Short-time DTFT

* Many practical signals, such as musical signals, have time-varying
  spectrums. That is, their frequency contents (i.e., FT or DTFT)
  change over time. 

* For example, consider a discrete-time signal $x[n]$ that is obtained
  by oversampling a piece of music. The DTFT $X(e^{j\hat\omega})$ of
  the whole $x[n]$ contains all the frequency contents (i.e., all the
  notes played) over the whole piece of music.  In particular, we
  can't tell from $X(e^{j\hat\omega})$ which note is played at which
  time. This means that the time resolution of $X(e^{j\hat\omega})$ is
  poor. The uncertainty principle thus implies that we may be able to
  obtain a fine frequency resolution.

* We may employ the windowing approach to improve time
  resolution: 
  - Consider a discrete-time window signal $\tilde{w}[n]$ whose energy
    is concentrated around $n=0$ and have a small $\sigma_t$ (in the
    interpretation for discrete-time signals given in
    {numref}`sec:uncertainty`).
  - Apply windowing to the time of interest, say $n=m$, by multiplying
    $x[n]$ with $\tilde{w}[n-m]$.
  - Take DTFT of the windowed signal $x[n] \tilde{w}[n-m]$.
  
  Intuitively, windowing $x[n]$ by $\tilde{w}[n-m]$ focuses our
  attention to the parts of $x[n]$ around the time $m$.

* Note that different DTFTs may be obtained at different times of
  interest. The collection of all such DTFTs over the range of $m$ is
  called the **short-time DTFT** $X(e^{j\hat\omega}; m)$ of $x[n]$:
  \begin{equation*}
  X(e^{j\hat\omega}; m) = \sum_{n=-\infty}^{\infty} x[n]
  \tilde{w}[n-m] e^{-j\hat\omega n}.
  \end{equation*}

* From the uncertainty principle, we know that for each fixed $m$, we
  will suffer from a poorer frequency resolution by using
  $X(e^{j\hat\omega}; m)$ instead of $X(e^{j\hat\omega})$ because the
  time resolution of the windowed signal $x[n] \tilde{w}[n-m]$ is
  finer than that of the whole signal $x[n]$.
