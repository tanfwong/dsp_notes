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
  {eq}`e:butterworthTF` are $s_k = \omega_c e^{j\frac{2k+1+N}{2N}}$ for
  $k=0,1,\ldots, 2N_1$. That is, they are $2N$ evenly spaced points on
  the circle of radius $\omega_c$ centered at the origin on the $s$-plane. 
  Selecting all the roots on the left-half plane, we obtain a stable filter with
  transfer function:
  \begin{equation*}
  H(s) = 
  \frac{1}{\prod_{k=0}^{N-1} (s-s_k)}
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
  ellipse centered at the origin on the $s$-plane with major ans minor
  axis radii $\displaystyle r_1 = \frac{\omega_p (\beta^2
  +1)}{2\beta}$ and $\displaystyle r_2 = \frac{\omega_p (\beta^2
  -1)}{2\beta}$, where $\displaystyle \beta = \left(
  \frac{\sqrt{1+\varepsilon^2} +1}{\varepsilon} \right)^{\frac{1}{N}}$.  

* The type-I Chebyshev filter is equiripple in the passband and flat in the stopband.
