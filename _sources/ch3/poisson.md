# Poisson Sum Formula

## Time-domain Poisson sum formula
Let us re-develop a slightly more general version of the Poisson sum
formula:
* Consider $x(t) \in L^1 \cap L^2$. Fix $T>0$. Then
  - $\sum_{n=-\infty}^{\infty} |x(t+nT)| < \infty$ for almost
    everywhere on $\mathbb{R}$,
  - $x(t)$ has its FT $X(\omega) \in L^2$, and
  
  Thus, $x_T (t) = T \sum_{n=-\infty}^{\infty} x(t+nT)$ is
  well-defined and finite. Clearly, $x_T(t)$ is a periodic signal with
  period $T$ and it is of finite power, i.e., $x_T(t) \in
  L^2 \left[-\frac{T}{2}, \frac{T}{2}\right]$. As a consequence, $x_T
  (t)$ has a FS expansion.

* Now, according to the forward FT formula {eq}`e:ft` 
  \begin{align*}
  X(\omega)
  &=
  \int_{-\infty}^{\infty} x(t) e^{-j\omega t} \, dt
  \notag \\
  &= 
  \sum_{n=-\infty}^{\infty} \int_{nT-\frac{T}{2}}^{nT+\frac{T}{2}}
  x(t) e^{-j\omega t} \, dt
  \notag \\
  &=
  \sum_{n=-\infty}^{\infty} \int_{-\frac{T}{2}}^{\frac{T}{2}}
  x(t) e^{-j\omega (t+nT)} \, dt
  \notag \\
  &=
  \int_{-\frac{T}{2}}^{\frac{T}{2}} \left( \sum_{n=-\infty}^{\infty} 
  x(t) e^{-j\omega (t+nT)} \right) \, dt
  & \text{(dominated convergence)}
  \end{align*}
  In particular, at $\omega = \frac{2\pi k}{T}$, for $k \in \mathbb{Z}$,
  we get
  \begin{equation*}
  X\left(\frac{2\pi k}{T}\right)
  = \frac{1}{T} \int_{-\frac{T}{2}}^{\frac{T}{2}} x_T(t) 
  e^{-j\frac{2\pi k t}{T}} \, dt.
  \end{equation*}
  That is, $X\left(\frac{2\pi k}{T}\right)$ is simply the $k$th FS coefficient
  of $x_T(t)$.  Hence, 
  $\left\{X\left(\frac{2\pi k}{T}\right) \right\}_{k \in \mathbb{Z}} \in l^2$. 
  The FS synthesis formula {eq}`e:fs_syn` then gives the following version
  of the *Poisson sum formula*:
  ```{admonition} Poisson Sum Formula (time-domain)
  :class: tip
  For any $x(t) \in L^1 \cap L^2$,
  ~~~{math}
  :label: e:poisson_x
  \begin{equation}
  \sum_{n=-\infty}^{\infty} x(t+nT)
  = 
  \frac{1}{T} \sum_{k=-\infty}^{\infty} X\left(\frac{2\pi k}{T}\right) 
  e^{j\frac{2\pi k t}{T}} 
  \end{equation}
  ~~~
  where $x(t) \stackrel{\text{FT}}{\longleftrightarrow}  X(\omega)$.
  ```

## Periodic vs aperiodic Dirac delta
* Consider the time-domain versions of the periodic and aperiodic
  Dirac delta function:
  - **Periodic**: 
    $\frac{2\pi}{T} \delta (e^{j\frac{2\pi t}{T}})
    = \lim_{\lambda \rightarrow 1} \frac{W_{\lambda} 
    (e^{j\frac{2\pi t}{T}})}{T}$
  - **Aperiodic**:
    $\delta(t) = \lim_{\mu \rightarrow 0} \tilde{w}_{\mu}(t)$
  
  These two Dirac deltas are related to one another and the
  relationship can be established using the Poisson sum formula in
  {eq}`e:poisson_x`.

* Let $x[n] = \tilde{w}_{\mu}(t)
  \stackrel{\text{FT}}{\longleftrightarrow} X(\omega) =
  \tilde{W}_{\mu}(\omega)$ in {eq}`e:poisson_x`. We get
  ```{math} 
  :label: e:dirac_rel
  \begin{align}
  \sum_{n=-\infty}^{\infty}  \tilde{w}_{\mu}(t+nT)
  &=
  \frac{1}{T} \sum_{k=-\infty}^{\infty} \tilde{W}_{\mu} \left(
  \frac{2\pi k}{T}\right)  e^{j\frac{2\pi k t}{T}}
  \notag \\
  &=
  \frac{1}{T} \sum_{k=-\infty}^{\infty} e^{-\mu\frac{2\pi |k|}{T}} 
  \cdot  e^{j\frac{2\pi k t}{T}}
  \notag \\
  &=
  \frac{1}{T} \cdot \frac{1 - e^{-\frac{4\pi\mu}{T}}}{1 - 
  2e^{-\frac{2\pi\mu}{T}} \cos\left(\frac{2\pi t}{T}\right) 
  +e^{-\frac{4\pi \mu}{T}}} 
  \notag \\
  &=
  \frac{1}{T} \cdot W_{e^{-\frac{2\pi\mu}{T}}} \left(e^{j\frac{2\pi
  t}{T}} \right). 
  \end{align}
  ```
* Taking "limit" as $\mu \rightarrow 0$ on both sides of {eq}`e:dirac_rel`, 
  we obtain
  ```{math}
  :label: e:delta_pva
  \begin{equation}
  \sum_{n=-\infty}^{\infty} \delta(t+nT) = \frac{2\pi}{T} \delta
  \left(e^{j\frac{2\pi t}{T}} \right)
  \end{equation}
  ```
  which confirms the pictorial intuition that the periodic Dirac delta
  $\frac{2\pi}{T} \delta (e^{j\frac{2\pi t}{T}})$ is simply a train of
  aperiodic Dirac deltas separated by $T$.

* Using {eq}`e:delta_pva`, the earlier version of the Poisson sum
  formula given in {eq}`e:poisson` can now be re-written as
  ```{math}
  :label: e:poisson1
  \begin{equation}
  \sum_{n=-\infty}^{\infty} \delta(t+nT) 
  =
  \frac{1}{T} \sum_{n=-\infty}^{\infty} e^{j\frac{2\pi n t}{T}}
  \end{equation}
  ```
  which can be thought of as the extension of {eq}`e:poisson_x` to the
  Dirac delta signal $\delta(t)$ because $\delta(t) \stackrel{\text{FT}}{\longleftrightarrow} 1$
  from Example 6. in {numref}`sec:dirac`. Of course, one should
  interpret {eq}`e:poisson1` as a mnemonic for the limiting process of
  {eq}`e:poisson_x` with $x(t) = \tilde{w}_{\mu}(t)$ and $X(\omega) =
  \tilde{W}_{\mu}(\omega)$ as $\mu \rightarrow 0$.

## FT of a Dirac delta train
* **Example**:

    7. Taking FT on both sides of the Poisson sum formula {eq}`e:poisson1`
       and using the linearity property of FT and Example 1. in
       {numref}`sec:dirac`, we get
       \begin{equation*}
       \sum_{n=-\infty}^{\infty} \delta(t+nT) 
       =
       \frac{1}{T} \sum_{n=-\infty}^{\infty} e^{j\frac{2\pi n t}{T}}
       ~~ 
       \stackrel{\text{FT}}{\longleftrightarrow} 
       ~~
       \frac{2\pi}{T} \sum_{n=-\infty}^{\infty} \delta \left(\omega +
       \frac{2\pi n}{T} \right)
       \end{equation*}

## Frequency-domain Poisson sum formula
Let us re-develop the Poisson sum fromula from a frequency-domain perspective:

* 
