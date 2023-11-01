# IIR Filter Design

* Typically, we convert standard continuous-time (analog) filters to
  obtain discrete-time IIR filters by applying appropriate
  transformations. 

## Prototype Analog Filters
* Let's start by introducing a few common **lowpass** analog filter prototypes.

### Butterworth Filter
* A **Butterworth filter** of order $N$ is an all-pole filter
  characterized by the following square-magnitude response: 
  ```{math}
  :label: e:butterworth 
  \begin{equation} 
  |H(\omega)|^2 
  = 
  \frac{1}{1 + \varepsilon^2 \left( \frac{\omega}{\omega_p} \right)^{2N}} 
  =
  \frac{1}{1 + \left( \frac{\omega}{\omega_c} \right)^{2N}}
  \end{equation} 
  ``` 
  where $\omega_p$ is the passband edge and
  $\omega_c = \varepsilon^{-\frac{1}{M}} \omega_p$ is the $3$dB cutoff
  frequency.

* The transfer function $H(s)$ (the Laplace transform of the impulse
  response $h(t)$ of the Butterworth filter satisfies:
  ```{math}
  :label: e:butterworthTF
  \begin{equation}
  H(s) H(-s) = 
  \frac{1}{1 + \left( \frac{s}{j\omega_c} \right)^{2N}}.
  \end{equation}
  ```
  ```{tip}
  Note that $|H(\omega)|^2 = H(s)H(-s) \big|_{s=j\omega}$. 
  ```
  The roots of the denominator polynomial on the RHS of
  {eq}`e:butterworthTF` are $\tilde s_k = \omega_c e^{j\frac{2k+1+N}{2N}}$ for
  $k=0,1,\ldots, 2N_1$. That is, they are $2N$ evenly spaced points on
  the circle of radius $\omega_c$ centered at the origin on the $s$-plane. 
  Selecting all the roots on the left-half plane, we obtain a stable filter with
  transfer function:
  \begin{equation*}
  H(s) = 
  \frac{K}{\prod_{k=0}^{N-1} (s- \tilde s_k)}
  \end{equation*}
  which gives our lowpass Butterworth filter prototype.

* Note that $|H(\omega)|^2$ in {eq}`e:butterworth` is monotone
  decreasing in (positive) $\omega$. Thus there are no ripples in
  either the passband or stopband for the Butterworth filter. We often
  say that the Butterworth filter has *flat* passband and stopband.

### Type-I Chebyshev Filter
* A **type-I Chebyshev filter** of order $N$ is an all-pole filter
  characterized by:
  ```{math}
  :label: e:chebyshevI 
  \begin{equation} 
  |H(\omega)|^2 
  = 
  \frac{1}{1 + \varepsilon^2 T^2_N\left( \frac{\omega}{\omega_p} \right)} 
  \end{equation} 
  ```
  where
  \begin{equation*}
  T_N(x) = \begin{cases}
  \cos \left( N \cos^{-1}(x) \right) & \text{if } |x| \leq 1
  \\
  \cosh \left( N \cosh^{-1}(x) \right) & \text{if } |x| > 1
  \end{cases}
  \end{equation*} 
  is the Chebyshev polynomial of degree $N$.
  ```{tip}
  One may also get the Chebyshev polynomials using the following recursion:
  \begin{align*}
  T_0(x) &= 1 \\
  T_1(x) &= x \\
  T_{n+1}(x) &= 2xT_n(x) - T_{n-1}(x)
  & \text{for } n \geq 1.
  \end{align*}
  ```

* The poles of $H(s)H(-s)$ of the type-I Chebyshev filter lie on an
  ellipse centered at the origin on the $s$-plane with major and minor
  axis radii $\displaystyle r_1 = \frac{\omega_p (\beta^2
  +1)}{2\beta}$ and $\displaystyle r_2 = \frac{\omega_p (\beta^2
  -1)}{2\beta}$, where $\displaystyle \beta = \left(
  \frac{\sqrt{1+\varepsilon^2} +1}{\varepsilon}
  \right)^{\frac{1}{N}}$.  Choosing all poles on the left half plane
  gives a stable
  \begin{equation*}
  H(s) = 
  \frac{K}{\prod_{k=0}^{N-1} (s-s_k)}
  \end{equation*}
  where $s_k = r_2 \cos \phi_k  + j r_1 \sin \phi_k$ and $\phi_k =
  \frac{2k+1+N}{2N}$ for $k=0,1,\ldots, N-1$.

* The type-I Chebyshev filter is equiripple in the passband and flat in the stopband.

### Type-II Chebyshev Filter
* A **type-II Chebyshev filter** of order $N$ is a filter with $N$
  zeros and $N$ poles characterized by:
  ```{math}
  :label: e:chebyshevII 
  \begin{equation} 
  |H(\omega)|^2 
  = 
  \frac{1}{1 + \varepsilon^2 \frac{T^2_N\left(\frac{\omega_s}{\omega_p}\right)}{
  T^2_N\left( \frac{\omega_s}{\omega} \right)} }
  \end{equation} 
  ```
  where $\omega_p$ and $\omega_s$ are the passband and stopband edge
  frequency, respectively.

* For a stable filter, the transfer function of the type-II Chebyshev
  filter is given by
  \begin{equation*}
  H(s) = 
  \frac{K \prod_{k=0}^{N-1} (s-z_k)}{\prod_{k=0}^{N-1} (s-p_k)}
  \end{equation*}
  where $z_k = \frac{j\omega_s}{\sin \phi_k}$ and $p_k =
  \frac{\omega_s s_k}{\sqrt{r_2^2 \cos^2 \phi_k  + r_1^2 \sin^2
  \phi_k}}$ for $k=0,1,\ldots, N-1$.

* The type-II Chebyshev filter is equiripple in the stopband and flat
  in the passband.

### Elliptic Filter
* An **elliptic filter** of order $N$ is a filter with $N$
  zeros and $N$ poles characterized by:
  ```{math}
  :label: e:elliptic 
  \begin{equation} 
  |H(\omega)|^2 
  = 
  \frac{1}{1 + \varepsilon^2 U^2_N\left(\frac{\omega}{\omega_p}\right)}
  \end{equation} 
  ```
  where $U_N(\cdot)$ is the Jacobian elliptic function of order $N$
  (see {cite}`orfanidis2006` for details).

* The zeros of the transfer function $H(s)$ of the elliptic filter are
  on the $j\omega$-axis. 

* The elliptic filter is equiripple in both the passband and stopband.

* The elliptic filter has a lower order than the Butterworth and
  Chebyshev filters for the same specification.

### Analog Filter Design
* To design an analog lowpass filter with specification $(\omega_p,
  \omega_s, \delta_1, \delta_2)$:
  1. Pick a filter type from above (Butterworth, type-I Chebyshev,
     type-II Chebyshev, or elliptic).
  2. Use {eq}`e:butterworth`, {eq}`e:chebyshevI`, {eq}`e:chebyshevII`,
     or {eq}`e:elliptic` to determine the value $\varepsilon$ from
     $\delta_1$. 
  3. Find the minimum filter order $N$ such that the specifications of
     $\delta_1$ and $\delta_2$ are satisfied at $\omega_p$ and
     $\omega_s$, respectively.

* After obtaining the transfer function $H(s)$ of a lowpass prototype
  design with passband edge frequency $\omega_p$, one may use the
  transformations given in the table below to get the transfer
  function $H'(s)$ of another type of filter:
  ```{list-table}
  :header-rows: 1

  * - New filter type
    - New band edge(s)
    - Transformation

  * - Lowpass
    - $\omega'_p$
    - $H'(s) = H \left(\frac{\omega_p}{\omega'_p} s\right)$

  * - Highpass
    - $\omega'_p$
    - $\displaystyle H'(s) = H \left(\frac{\omega_p\omega'_p}{s} \right)$

  * - Bandpass
    - $\omega_l, \omega_u$
    - $\displaystyle H'(s) = H \left(\omega_p \frac{s^2+\omega_u
      \omega_l}{s(\omega_u-\omega_l)} \right)$
  
  * - Bandstop
    - $\omega_l, \omega_u$
    - $\displaystyle H'(s) = H \left(\omega_p \frac{s(\omega_u-
      \omega_l)}{s^2+\omega_u \omega_l} \right)$
  ```