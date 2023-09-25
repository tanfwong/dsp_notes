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

* To further see this tradeoff,  let $\tilde{w}[n]
  \stackrel{\text{DTFT}}{\longleftrightarrow}
  \tilde{W}(e^{j\hat\omega})$. Since $X(e^{j\hat\omega}; m)$
  is the DTFT of  $x[n] \tilde{w}[n-m]$, the time-shifting and
  multiplication properties of DTFT gives
  \begin{equation*}
  X(e^{j\hat\omega}; m)
  =
  \frac{1}{2\pi} \int_{-\pi}^{\pi} X(e^{j\theta})
  \tilde{W}(e^{j(\hat\omega -\theta)}) e^{j(\hat\omega -\theta)m}
  \,d\theta.
  \end{equation*}
  That is, $X(e^{j\hat\omega}; m)$ is the circular convolution between
  $X(e^{j\hat\omega})$ and $\tilde{W}(e^{j\hat\omega}) e^{-j\hat\omega
  m}$ in the frequency domain. Pictorially, it means that the plot of
  $X(e^{j\hat\omega})$ is "blurred" or "smoothed out" by
  $\tilde{W}(e^{j\hat\omega}) e^{-j\hat\omega m}$.

* In practice, we don't usually calculate $X(e^{j\hat\omega}; m)$ for
  every $m$. Instead, we only need to at most step through the range
  of $m$ of interest with a step size comparable to the lower bound on
  $\sigma_t$ of $\tilde{w}[n]$ because the lower bound gives the
  finest possible time resolution using the window $\tilde{w}[n]$.

* The table below gives some commonly used window signals. Note that
  the expression of each window signal $w[n]$ given doesn't centered
  at $n=0$ (this is the form usually given in textbooks). For the
  purpose of windowing in short-time DTFT, we use only odd-length
  windows. That is, we may obtain the $0$-centered window
  $\tilde{w}[n]$ from the window $w[n]$ provided by letting
  $\tilde{w}[n] = w\left[ n + \frac{L-1}{2} \right]$, where $L$ is the
  odd window length of $w[n]$.
  
  ```{list-table}
  :header-rows: 1
  
  * - **Window name**
    - $\boldsymbol{w[n]}~~$ **for** $\boldsymbol{0 \leq n \leq L-1}$ 

  * - Bartlett (triangular)
    - $\displaystyle 1 - \frac{2\left| n - \frac{L-1}{2}
      \right|}{L-1}$

  * - Blackman
    - $\displaystyle 0.42 - 0.5\cos \left(\frac{2\pi n}{L-1}\right) +
      0.08 \cos \left(\frac{4\pi n}{L-1}\right)$

  * - Hamming
    - $\displaystyle 0.54 - 0.46 \cos \left(\frac{2\pi n}{L-1}\right)$

  * - Hanning
    - $\displaystyle \frac{1}{2} \left[ 1 - \cos \left(\frac{2\pi
      n}{L-1}\right) \right]$
  ```
