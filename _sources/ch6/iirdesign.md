# IIR Filter Design

* Typically, we convert standard continuous-time (analog) filters to
  obtain discrete-time IIR filters by applying appropriate
  transformations. 

(sec:afilter)=
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
  $\omega_c = \varepsilon^{-\frac{1}{N}} \omega_p$ is the $3$dB cutoff
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
  $k=0,1,\ldots, 2N-1$. That is, they are $2N$ evenly spaced points on
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

(sec:atrans)=
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

## Impulse Invariance Method
* Sample the impulse response $h(t)$ of an analog lowpass
   filter prototype at sampling rate $f_s$ to obtain the impulse
   response $\displaystyle h[n] = \frac{1}{f_s} h\left(\frac{n}{f_s}
   \right)$ of the target discrete-time lowpass IIR filter.

* If $h(t)$ is bandlimited and we oversample $h(t)$ to get $h[n]$,
  then from that the Poisson sum formula {eq}`e:folded_spectrum`,
  the frequency response of $h[n]$ is
  \begin{align*}
  H(e^{j\hat\omega}) 
  &= H(\hat\omega f_s)
  & \text{  for  }  -\pi \leq \hat\omega < \pi
  \end{align*}
  where $H(\omega)$ is the frequency response of $h(t)$.
  Thus, the design specification $(\hat\omega_p, \hat\omega_s,
  \delta_1, \delta_2)$ of the discrete-time lowpass IIR filter will be
  met if we set $\omega_p = \hat\omega_p f_s$, $\omega_s =
  \hat\omega_s f_s$, and design the continuous-time lowpass filter
  prototype to satisfy the specification $(\omega_p, \omega_s,
  \delta_1, \delta_2)$.

* Often, we use the Butterworth, Chebyshev, and elliptic filters
  described above as prototypes for the analog filter design.
  ```{tip}
  Since the magnitude responses of the Butterworth, Chebyshev, and
  elliptic (see  {eq}`e:butterworth`, {eq}`e:chebyshevI`, {eq}`e:chebyshevII`,
  and {eq}`e:elliptic`) are functions of the ratio
  $\frac{\omega}{\omega_p}$ or $\frac{\omega_s}{\omega}$, we may
  simply set $f_s = 1$ in the design process without any loss of generality. 
  ```
  ```{caution}
  As none of the Butterworth, Chebyshev, and
  elliptic filters are strictly bandlimited, the impulse invariance
  design obtained by sampling the impulse response of the analog
  filter prototype may suffer from aliasing, typically causing larger
  stopband ripples. To overcome this problem, we may need to use a
  tigter values for $\delta_1$ and $\delta_2$ so that the achieved
  ripples in the passband and stopband are within the original specification. 
  ```
* Note that the analog filter prototypes described in
  {numref}`sec:afilter` above all have single-order poles. Hence their
  continuous-time transfer functions have the following partial
  fraction expansion:
  \begin{equation*}
  H(s) = A_0 + \sum_{k=0}^{N-1} \frac{A_k}{s - p_k}
  \end{equation*}
  where $p_0, p_1, \ldots, p_{N-1}$ are the poles. Taking inverse
  Laplace transform to get the causal impulse response
  \begin{equation*}
  h(t) = A_0 \delta(t)+ \sum_{k=0}^{N-1} A_k e^{p_k t} u(t).
  \end{equation*}
  Sampling $h(t)$ at $f_s=1$ gives
  \begin{equation*}
  h[n] = A_0 \delta[n]+ \sum_{k=0}^{N-1} A_k e^{p_k n} u[n].
  \end{equation*}
  Taking $z$-transform on $h[n]$, we get
  \begin{equation*}
  H(z) = A_0 + \sum_{k=0}^{N-1} \frac{A_k}{1 - e^{p_k} z^{-1}}
  \end{equation*}
  Since $H(s)$ is table by construction, $\text{Re}(p_k) < 0$ for
  $k=0,1,\ldots, N-1$. Thus the poles $e^{p_k}$ of the transfer
  function $H(z)$ of the resulting discrete-time IIR filter are all
  strictly inside the unit circle, i.e., $H(z)$ is also stable.
 
* **MATLAB Example 7**:

  Consider again the same design specification as in Examples 1 and 4
  in {numref}`sec:firdesign`, except in this example we want to design
  a lowpass IIR filter with the specification $(0.3\pi, 0.35\pi, 0.01,
  0.001)$ based on a analog type-I Chebyshev filter prototype. Using the
  impulse invariance method with $f_s=1$, the required specifications
  of the analog type-I Chebyshev filter prototype are $\omega_p=0.3\pi$,
  $\omega_s=0.35\pi$, $\delta_1=0.01$, and $\delta_2=0.001$.

  Next, we employ {eq}`e:chebyshevI` to determine the value
  of $\varepsilon$ and the filter order $N$ required to meet the
  specifications. We can be done using the MATLAB function `cheb1ord`:
  ```matlab
  >> Rp = -20*log10(1-0.01);
  >> Rs = -20*log10(0.001);
  >> [N, wp] = cheb1ord(0.3*pi, 0.35*pi, Rp, Rs, 's')

  N =

      17


  wp =

      0.9425
  ```
  to get that the filter required order is $N=17$. Note that the value
  of $\varepsilon$ depends only on $\delta_1$ and $\omega_p$. 
  Then we can use the MATLAB function `cheby1` to obtain the analog 
  type-I Chebyshev filter prototype:
  ```matlab
  >> [bc, ac]= cheby1(N, Rp, wp, 's');
  >> freqs(bc, ac, [0:0.0001:pi]);
  ```
  We can see that the analog filter prototype meets its specifications.
  Finally, we may use the MATLAB function `impinvar` to apply the
  impulse invariance method to obtain the target discrete-time IIR filter:
  ```matlab
  >> [b, a] = impinvar(bc, ac);
  >> fvtool(b, a);
  ```
  We can check that the original specification $(0.3\pi, 0.35\pi, 0.01,
  0.001)$  is met.
  ```{tip}
  Note that the order of the IIR filter obtained from the impulse
  invariance method is much smaller than those of
  the FIR filters obtained in Examples 1 and 4 with the same
  specification. However, the group
  delay of the IIR filter is not a constant over the passband. 
  ```

* **MATLAB Example 8**:

  Repeat Example 7 using an analog elliptic filter prototype instead:
  ```matlab
  >> Rp = -20*log10(1-0.01);
  >> Rs = -20*log10(0.001);
  >> [N, wp] = ellipord(0.3*pi, 0.35*pi, Rp, Rs, 's')
  
  N =

      9


  wp =

      0.9425

  >> [bc, ac] = ellip(N, Rp, Rs, wp, 's');
  >> freqs(bc, ac, [0:0.0001:pi]);
  ```
  We can see that this analog filter prototype also meets its specifications.
  However, applying the impulse invariance method:
    ```matlab
  >> [b, a] = impinvar(bc, ac);
  >> fvtool(b, a);
  ```
  We see that the resulting IIR filter violates its specifications
  in both the passband and stopband. Redoing the design with more
  stringent values for $\delta_1$ and $\delta_2$:
  ```matlab
  >> Rp = -20*log10(1-0.01);
  >> Rs = -20*log10(0.001);
  >> [N, wp] = ellipord(0.3*pi, 0.35*pi, Rp*0.75, Rs+15, 's')
  
  N =

      10


  wp =

      0.9425

  
  >> [bc, ac] = ellip(N, Rp*0.75, Rs+15, wp, 's');
  >> [b, a] = impinvar(bc, ac);
  >> fvtool(b, a);
  ```
  gives an IIR filter that satisfies the specification of $(0.3\pi, 0.35\pi, 0.01,
  0.001)$. Note that the order of this IIR filter is $N=10$, smaller
  than that of the IIR filter obtained from the type-I Chebyshev prototype.


## Bilinear Transform Method
* Obtain the transfer function $H(z)$ of the discrete-time IIR filter
  directly from the transfer function $H(s)$ of an anlog prototype
  filter by the bilinear transformation:
  ```{math}
  :label: e:bilinear
  \begin{equation}
  s = 2f_s \left( \frac{ 1- z^{-1}}{1+z^{-1}} \right)
  \end{equation}
  ```
  where $f_s$ is the sampling rate.

* Let $s=\sigma + j \omega$. Inverting the bilinear transform gives
  \begin{align*}
  z
  &=
  \frac{1 + \frac{s}{2f_s}}{1 - \frac{s}{2f_s}}
  \\
  &=
  \frac{1 + \frac{\sigma}{2f_s} + j\frac{\omega}{2f_s}}{1 -
  \frac{\sigma}{2f_s} - j\frac{\omega}{2f_s}}.
  \end{align*}
  Thus:
  1. If $\sigma<0$, then $|z| < 1$. That is, the left half $s$-plane is
     mapped onto the inside of the unit circle in the $z$-plane by the
     bilinear transform.
  2. If $\sigma>0$, then $|z| > 1$. That is, the right half $s$-plane is
     mapped onto the outside of the unit circle in the $z$-plane by the
     bilinear transform.
  3. If $\sigma=0$, then $|z| = 1$. That is, the $j\omega$ axis of
     $s$-plane is mapped onto the unit circle of the $z$-plane by the
     bilinear transform.

* From observation 1, the bilinear transform {eq}`e:bilinear` maps
  causal stable analog filter to a causal stable discrete-time IIR filter.

* Based on observation 3, substituting $s=j\omega$ and
  $z=e^{j\hat\omega}$ into {eq}`e:bilinear` gives 
  ```{math} 
  :label: e:bilinfreq 
  \begin{align} 
  \omega 
  &= \frac{2 f_s}{j} \left( \frac{1 -
  e^{-j\hat\omega}}{1 + e^{-j\hat\omega}} \right) 
  \\ 
  &= 2 f_s \tan \frac{\hat\omega}{2} 
  \end{align} 
  ``` 
  for $-\pi \leq \hat\omega < \pi$, which shows that 
  the mapping between the $j\omega$ axis
  of $s$-plane and the unit circle of the $z$-plane, i.e., between the
  angular frequency $\omega$ of the analog filter and the normalized
  radian frequency $\hat\omega$ of the discrete-time filter, induced
  by the bilinear transform {eq}`e:bilinear` is one-to-one. As a
  result, **the bilinear transform  {eq}`e:bilinear` can be employed to
  turn lowpass, highpass, bandpass, and bandstop analog filter
  prototypes to their respective discrete-time counterparts**. 

* The design steps of the bilinear tranform method are then simply:
  1. Starting from the specification of the discrete-time IIR filter,
     use {eq}`e:bilinfreq` to convert the specification to one for the
     analog filter prototype. For example, the specification
     $(\hat\omega_p, \hat\omega_s, \delta_1, \delta_2)$ for the case
     of a lowpass discrete-time filter is converted to the
     specification $(\omega_p, \omega_s, \delta_1, \delta_2)$ of a
     lowpass analog filter prototype, where $\omega_p$ and $\omega_s$
     are obtained from $\hat\omega_p$ and $\hat\omega_s$ using
     {eq}`e:bilinfreq`, respectively.
  2. Design an analog filter prototype that satisfies the
     specification obtained in step 1.
  3. Use the bilinear transform  {eq}`e:bilinear` to obtain the
     transfer function $H(z)$ of the target discrete-time IIR filter
     from the transfer function $H(s)$ of the analog filter prototype
     in step 2.
  ```{tip}
  As in the impulse invariance method, 
  since the magnitude responses of the Butterworth, Chebyshev, and
  elliptic (see  {eq}`e:butterworth`, {eq}`e:chebyshevI`, {eq}`e:chebyshevII`,
  and {eq}`e:elliptic`) are functions of the ratio
  $\frac{\omega}{\omega_p}$ or $\frac{\omega_s}{\omega}$, we may
  set $f_s = 1$ in the design process above without any loss of generality. 
  ```
* **MATLAB Example 9**:

  Repeat Example 7 above, except using the bilinear transform method
  with $f_s=1$ to obtain the discrete-time IIR filter from an analog
  type-I Chebyshev filter prototype. First, use {eq}`e:bilinfreq` to
  obtain $\omega_p$ and $\omega_s$ from the IIR filter's specification
  in order to design the analog prototype:
  ```matlab
  >> Rp = -20*log10(1-0.01);
  >> Rs = -20*log10(0.001);
  >> wp = 2*tan(0.3*pi/2);
  >> ws = 2*tan(0.35*pi/2);
  >> [N, wp] = cheb1ord(wp, ws, Rp, Rs, 's')
  N =

      16

  wp =

      1.0191

  >> [bc, ac] = cheby1(N, Rp, Rs, wp, 's');
  >> freqs(bc, ac, [0:0.0001:pi]);
  ```
  Then, we can use the MATLAB function `bilinear` to apply the
  bilinear transformation in {eq}`e:bilinear` to get the discrete-time
  IIR filter:
  ```matlab
  >> [b, a] = bilinear(bc, ac, 1);
  >> fvtool(b, a);
  ```

  ```{tip}
  One may more conveniently use the MATLAB function `cheby1` to
  directly perform the steps above:
  ~~~matlab
  >> [N, wp] = cheb1ord(0.3, 0.35, Rp, Rs)
  
  N =

      16

  wp =
  
      0.3000

  >> [b, a] = cheby1(N, Rp, wp);
  >> fvtool(b, a);
  ~~~
  ```

* **MATLAB Example 10**:
  
  Design a discrete-time highpass IIR filter with passband $[0.7\pi,
  \pi]$ and ripple tolerance $\delta_1 = 0.01$, and stopband
  $[0,0.65\pi]$ and ripple tolerance $\delta_2=0.001$ as in Example 5
  in {numref}`sec:firdesign`. Following Example 9, we use the type-I
  Chebyshev filter as our prototype analog filter to perform the design.

  The following MATLAB commands:
  ```matlab
  >> Rp = -20*log10(1-0.01);
  >> Rs = -20*log10(0.001);
  >> [N, wp] = cheb1ord(0.7, 0.65, Rp, Rs)

  N =

      16

  wp =

      0.7000
  
  >> [b, a] = cheby1(N, Rp, wp, 'high');
  >> fvtool(b, a);
  ```
   design an analog lowpass type-I Chebyshev filter with $\omega_p =
   1$ radian per second satisfying the $\delta_1$ and $\delta_2$
   specifications, transform the lowpass prototype to a highpass
   prototype using the table in {numref}`sec:atrans`, and finally
   apply the bilinear transformation to obtain the desired
   discrete-time highpass IIR filter.

## Frequency Transformation of IIR filters
* In {numref}`sec:freqtrans`, we discuss how to transform a lowpass
  FIR filter to a highpass one by frequency shifting. The same
  frequency-shifting transformation clearly applies to IIR filters
  also. As a matter of fact, a more general class of transformations
  that map the unit circle (on the $z$-plane) onto itself can be
  applied to convert a lowpass IIR filter to another IIR filter fo
  other types. 

* Write the mapping discussed above as $z^{-1} \mapsto
  G(z^{-1})$. Since the unti circle is mapped onto itself,
  $|G(z^{-1})| = 1$. That means, we can think of $G(z^{-1})$ as the
  transfer function of an allpass filter of the general form
  {eq}`e:allpass_gen` with $b_0=\pm 1$, i.e., 
  \begin{equation*}
  G(z^{-1}) = \pm \prod_{k=1}^N \frac{-a_k^* + z^{-1}}{1 - a_k z^{-1}}.
  \end{equation*}
  For example, the frequency shifting by $\pi$ considered in
  {numref}`sec:freqtrans` corresponds to the mapping $z^{-1} \mapsto
  G(z^{-1}) = - z^{-1}$.

* Other useful mappings of this form are summarized in the table
  below. The listed mappings can be employed to convert a lowpass IIR
  filter with passband edge frequency $\hat\omega_p$ to another lowpass 
  filter, a highpass filter, a bandpass filter, and a bandstop filter, respectively.
  ```{list-table}
  :header-rows: 1

  * - New filter type
    - New band edge(s)
    - Transformation
    - Parameter(s)

  * - Lowpass
    - $\hat\omega'_p$
    - $\displaystyle z^{-1} \mapsto \frac{-a + z^{-1}}{1-az^{-1}}$
    - $\displaystyle a 
      = \frac{\sin\frac{\hat\omega_p - \hat\omega'_p}{2}}{
      \sin\frac{\hat\omega_p + \hat\omega'_p}{2}}$

  * - Highpass
    - $\hat\omega'_p$
    - $\displaystyle z^{-1} \mapsto -\frac{-a + z^{-1}}{1-az^{-1}}$
    - $\displaystyle a 
      = \frac{\cos\frac{\hat\omega_p + \hat\omega'_p}{2}}{
      \cos\frac{\hat\omega_p - \hat\omega'_p}{2}}$

  * - Bandpass
    - $\hat\omega_l, \hat\omega_u$
    - $\displaystyle z^{-1} \mapsto
      -\frac{a_2-a_1z^{-1}+z^{-2}}{1-a_1z^{-1}+a_2z^{-2}}$
    - $\begin{align*} 
      a_1 &= \frac{2\alpha K}{K+1}
      \\
      a_2 &= \frac{K-1}{K+1}
      \\
      \alpha &= \frac{\cos\frac{\hat\omega_u + \hat\omega_l}{2}}{
      \cos\frac{\hat\omega_u - \hat\omega_l}{2}}
      \\
      K &= \cot\frac{\hat\omega_u - \hat\omega_l}{2} \tan
      \frac{\hat\omega_p}{2}
      \end{align*}$
  
  * - Bandstop
    - $\hat\omega_l, \hat\omega_u$
    - $\displaystyle z^{-1} \mapsto
      \frac{a_2-a_1z^{-1}+z^{-2}}{1-a_1z^{-1}+a_2z^{-2}}$
    - $\begin{align*} 
      a_1 &= \frac{2\alpha K}{K+1}
      \\
      a_2 &= \frac{1-K}{1+K}
      \\
      \alpha &= \frac{\cos\frac{\hat\omega_u + \hat\omega_l}{2}}{
      \cos\frac{\hat\omega_u - \hat\omega_l}{2}}
      \\
      K &= \tan\frac{\hat\omega_u - \hat\omega_l}{2} \tan
      \frac{\hat\omega_p}{2}
      \end{align*}$
  ```

