# Pole-Zero Placement

* From {numref}`sec:rational`, we see that the magnitude and phase
  responses of any causal, stable FIR (IIR) filter can be decomposed into
  those of first-order systems, specified by the poles and zeros of
  the FIR (IIR) filter. Thus, it is necessary to study the magnitude
  and phase responses of first-order systems in detail.

* There are two types of causal, stable first-order systems:
  1. **first-order FIR filter**: $\displaystyle H(z) = 1 - cz^{-1}$
  2. **first-order IIR filter**: $\displaystyle H(z) = \frac{1}{1 -
     cz^{-1}}$ where $|c| < 1$.

  Here, we focus on investigating the magnitude and phase responses as
  a function of the parameter $c$, i.e., the zero (pole) of the
  first-order FIR (IIR) filter.
 
* Note also that the magnitude (phase) response of the first-order IIR
  filter is simply the reciprocal (negation) of that of the
  first-order FIR filter (if $|c| <1$). Hence, it suffices to consider
  only the first-order FIR filter.

* Write $c=re^{j\phi}$ where $r=|c|$ and $\phi = \angle c$. Then
  $H(e^{j\hat\omega}) = 1 - re^{-j(\hat\omega - \phi)}$, and 
  \begin{align*}
  |H(e^{j\hat\omega}) | 
  &=
  1 + r^2 - 2r\cos(\hat\omega - \phi)
  \\
  \angle H(e^{j\hat\omega})
  &=
  \text{arctan2} \left( r\sin(\hat\omega - \phi), 1-
  r\cos(\hat\omega - \phi) \right).
  \end{align*}
  For $0<r<1$, the plots of the magnitude response $|H(e^{j\hat\omega})|$ and
  phase responses $\angle H(e^{j\hat\omega})$ look like the following figures:
  ```{image} ../figs/magphase.jpg
  :alt: Magnitude and phase responses of a first-order FIR filter
  :width: 800px
  :align: center
  ```
  In particular, $|H(e^{j\hat\omega})|$ reaches its maximum and
  minimum at $\hat\omega = \phi-\pi$ and $\hat\omega=\phi$,
  respectively. 
