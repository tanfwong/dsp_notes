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
  the circle of radius $\omega_c$ centered at the origin.  
