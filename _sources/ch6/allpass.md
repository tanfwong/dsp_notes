# Allpass Filter
* Consider the cascade of the (causal) first-order FIR filter with transfer
  function $-a^*+z^{-1}$ and the (causal) first-order IIR filter with transfer
  function $\frac{1}{1-az^{-1}}$, where $a=re^{j\phi}$ and $0<r<1$. 
  The transfer function of the cascade is
  ```{math}
  :label: e:allpass
  \begin{equation}
  H(z) = \frac{-a^* + z^{-1}}{1-az^{-1}}.
  \end{equation}
  ```
  Clearly, this cascaded filter has a pole at $z=a$ and a zero at $z=
  \frac{1}{a^*}$. it is causal and stable.

* The frequency response of the filter with transfer function in
  {eq}`e:allpass` is thus
  \begin{equation*}
  H(e^{j\hat\omega})
  =
  \frac{-a^* + e^{-j\hat\omega}}{1 - a e^{-j\hat\omega}}.
  \end{equation*}
  Hence, its magnitude is
  ```{math}
  :label: e:allpass_mag
  \begin{equation*}
  |H(e^{j\hat\omega})|
  = | e^{-j\hat\omega}| \cdot
  \frac{|1-a^* e^{j\hat\omega}|}{|1 - a e^{-j\hat\omega}|}
  = 1,
  \end{equation*}
  ```
  its phase response is 
  \begin{equation*}
  \angle H(e^{j\hat\omega})
  =
  -\hat\omega - 2 \text{arctan2} \left(r\sin(\hat\omega - \phi), 1 -
  r\cos(\hat\omega - \phi) \right),
  \end{equation*}
  and its group delay is
  \begin{equation*}
  \tau_g (e^{j\hat\omega})
  = -\frac{d \angle H(e^{j\hat\omega})}{d\hat\omega} =
  \frac{1-r^2}{|1-re^{-j(\hat\omega - \phi)}|^2} \geq 0
  \end{equation*}
  since $0< r < 1$.

* From the magnitude response in {eq}`e:allpass_mag`, we know that
  this filter is an **allpass** filter. In fact, it is the simplest,
  non-trivial, allpass rational filter.

* Using the allpass filter in {eq}`e:allpass` as a prototype, it is
  easy to see that every stable, allpass, rational filter must have its
  transfer function in the following form:
  ```{math}
  :label: e:allpass_gen
  \begin{equation*}
  H(z) 
  = b_0 \cdot
  \prod_{k=1}^N \frac{-a_k^* + e^{-j\hat\omega}}{1 - a_k e^{-j\hat\omega}}
  \end{equation*}
  ```
  where $|a_k| < 1$ for $k=1,2,\ldots,N$.

* For the general allpass filter in {eq}`e:allpass_gen`, the number
  of poles is the same as the number of zeros. All poles and zeros are
  in pairs of the form $(a_k, \frac{1}{a^*_k})$. Stability requires
  the pole $a_k$ (the zero $\frac{1}{a_k^*}$) to be strictly inside
  (outside) of the unit circle.
