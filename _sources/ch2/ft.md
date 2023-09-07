# Continuous-Time Fourieer Transform (FT)

For a continuous-time signal $x(t)$:
* **<u>Forward FT</u>**:
  ```{math}
  :label: e:ft
  \begin{equation}
  X(\omega) = \int_{-\infty}^{\infty} x(t) e^{-j\omega t} \, dt
  \end{equation}
  ```
* **<u>Inverse FT</u>**: 
  ```{math}
  :label: e:ift
  \begin{equation}
  x(t) = \frac{1}{2\pi} \int_{-\infty}^{\infty} X(\omega)
  e^{j\omega t} \, d\omega
  \end{equation}
  ```
```{admonition} Notation
1. We use the notation $x(t) \stackrel{\text{FT}}{\longleftrightarrow}
   X(\omega)$ to denote the mapping between the
   signal $x(t)$ and its FT $X(\omega)$ according to the
   forward and inverse FT formulas above.
2. A signal $x(t)$ is *absolutely integrable*, denoted by $x(t) \in
   L^1$, if $\int_{-\infty}^{\infty} |x(t)| dt < \infty$.
3. A FT function $X(\omega)$ is *absolutely integrable*,
   denoted also by $X(\omega) \in L^1$, if 
   $\frac{1}{2\pi} \int_{-\infty}^{\infty} |X(\omega)| d\omega < \infty$.
4. A signal $x(t)$ has *finite energy*, denoted by $x(t) \in
   L^2$, if $\int_{-\infty}^{\infty} |x(t)|^2 dt< \infty$.
5. A FT function $X(\omega)$ is *square-integrable*,
   denoted also by $X(\omega) \in L^2$, if 
   $\frac{1}{2\pi} \int_{-\infty}^{\infty} |X(\omega)|^2 d\omega < \infty$.
~~~{tip}
* Like before, when considering a signal $x(t) \in L^p$ ($p=1,2$), 
  we do not make any distinction between $x(t)$
  and another signal $\tilde{x}(t)$ such that $\int_{-\infty}^{\infty} 
  \left|\tilde{x}(t) - x(t) \right|^p dt = 0$. 
  We group all such signals in an equivalence
  class and consider the equivalence class as a unique member of 
  $L^p$.
* The same equivalence class consideration applies to FTs in $L^p$
  ($p=1,2$) as well.
~~~
```

* Similar to the case of DTFT, we have to consider the conditions for
  existence of the integrals on the RHS of both the forward and
  inverse FT formulas, {eq}`e:ft` and {eq}`e:ift`.  Similar to the
  case of DTFT, a simple sufficient condition can be obtained as follows:
  - If $x(t) \in L^1$, then the integral on the RHS of {eq}`e:ft`
     exists. Let $X(\omega)$ be the FT given by {eq}`e:ft`.
  - If this $X(\omega) \in L^1$, then the integral $\frac{1}{2\pi} \int_{-\pi}^{\pi} X(\omega)
    e^{j\omega t} d\omega$ on the RHS of {eq}`e:ift` exists and is
    continuous for all $t \in \mathbb{R}$.
  - In addition, the inverse FT formula {eq}`e:ift` holds almost
    everywhere on $\mathbb{R}$.
  
  These results indeed provide a meaning to the mapping 
  $x(t) \stackrel{\text{FT}}{\longleftrightarrow} X(\omega)$.
