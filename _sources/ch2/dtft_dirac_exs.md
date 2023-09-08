# DTFTs of infinite-energy signals

* For any infinite-energy signal $x[n]$ whose signal magnitude
  increases at most polynomially with $|n|$ (i.e., $|x[n]| =
  \mathcal{O}(|n|^{\alpha})$ for some $\alpha>0$), its windowed
  version $w_{\lambda} [n] x[n] \in \ell^1$ and hence the DTFT mapping 
  $w_{\lambda}[n] x[n] \stackrel{\text{DTFT}}{\longleftrightarrow} 
  X_{w_{\lambda}}(e^{j\hat{\omega}})$ exists for all $\lambda \in (0,1)$.
  As discussed in {numref}`sec:wlimit`, we may define
  $\lim_{\lambda \rightarrow 1} X_{w_{\lambda}}(e^{j\hat{\omega}})$
  as the DTFT $X(e^{j\hat{\omega}})$ of $x[n]$. 
* Note that the limit of $X_{w_{\lambda}}(e^{j\hat{\omega}})$ may not
  exist for any general $x[n]$. Even if it exists, calculating it may
  be difficult. Luckily, for some of the most common infinite-energy
  signals, we can express $\lim_{\lambda \rightarrow 1}
  X_{w_{\lambda}}(e^{j\hat{\omega}})$ in terms of
  $\delta(e^{j\hat{\omega}})$ as shown below.

(sec:dtft_ex1)=
## Sinusoid $x[n] = e^{j\hat{\omega}_0 n}$
Because
\begin{align*} 
X_{w_{\lambda}}(e^{j\hat{\omega}}) 
&=
\sum_{n=-\infty}^{\infty} w_{\lambda}[n] x[n] e^{-j\hat{\omega} n} 
\\
&= 
\sum_{n=-\infty}^{\infty} \lambda^{|n|} e^{j\hat{\omega}_0 n}
e^{-j\hat{\omega} n} 
\\ 
& = \frac{1 - \lambda^2}{1-2\lambda
\cos(\hat{\omega}-\hat{\omega}_0) + \lambda^2} 
\\ 
&=
W_{\lambda}(e^{j(\hat{\omega}-\hat{\omega}_0)}),
\end{align*} 
$\displaystyle X(e^{j\hat{\omega}}) = \lim_{\lambda \rightarrow
1} X_{w_{\lambda}}(e^{j\hat{\omega}}) = \lim_{\lambda \rightarrow 1}
W_{\lambda}(e^{j(\hat{\omega}-\hat{\omega}_0)}) = 2\pi \delta
(e^{j(\hat{\omega}-\hat{\omega}_0)})$. In other words, we have
established the DTFT pair 
\begin{equation*}
e^{j\hat{\omega}_0 n} ~~
\stackrel{\text{DTFT}}{\longleftrightarrow} 
~~ 2\pi \delta (e^{j(\hat{\omega}-\hat{\omega}_0)})
\end{equation*}
For the case of $\hat{\omega}_0 = 0$, we have
\begin{equation*}
1 ~~
\stackrel{\text{DTFT}}{\longleftrightarrow} 
~~ 2\pi \delta (e^{j\hat{\omega}})
\end{equation*}
By the Euler identity and linearity of DTFT, we get
\begin{align*}
\cos(\hat{\omega}_0 n) ~~
&\stackrel{\text{DTFT}}{\longleftrightarrow} 
~~ \pi \delta (e^{j(\hat{\omega}-\hat{\omega}_0)}) + \pi \delta
(e^{j(\hat{\omega}+\hat{\omega}_0)})
\\
\sin(\hat{\omega}_0 n) ~~
&\stackrel{\text{DTFT}}{\longleftrightarrow} 
~~ \frac{\pi}{j} \delta (e^{j(\hat{\omega}-\hat{\omega}_0)}) -
\frac{\pi}{j} \delta
(e^{j(\hat{\omega}+\hat{\omega}_0)})
\end{align*}


## Unit step $u[n]$
The DTFT $U_{w_{\lambda}}(e^{j\hat{\omega}})$ of $w_{\lambda}[n] u[n]$ is given by
\begin{equation*}
U_{w_{\lambda}}(e^{j\hat{\omega}}) 
=
\sum_{n=-\infty}^{\infty} w_{\lambda}[n] u[n] e^{-j\hat{\omega} n} 
= 
\sum_{n=0}^{\infty} \lambda^{n} e^{-j\hat{\omega} n} 
= \frac{1}{1-\lambda e^{-j \hat{\omega}}}. 
\end{equation*}
```{caution}
* Note that we can't directly take limit of
  $U_{w_{\lambda}}(e^{j\hat{\omega}})$ as $\lambda \rightarrow 1$ to
  obtain the DTFT $U(e^{j\hat{\omega}})$ of the unit step $u[n]$
  because the limit doesn't exist (see Example 3. in {numref}`sec:z_exs`)!
* To overcome this difficulty, we will express
  $U_{w_{\lambda}}(e^{j\hat{\omega}})$ in terms of
  $W_{\lambda}(e^{j\hat{\omega}})$ before taking
  limit to let the Dirac delta function
  $\delta(e^{j\hat{\omega}})$ absorb all problems
  associated with the limiting process.
```
By the time reversal property, $\displaystyle w_{\lambda}[-n] u[-n]
  \stackrel{\text{DTFT}}{\longleftrightarrow} U_{w_{\lambda}}(e^{-j\hat{\omega}}) =
  \frac{1}{1-\lambda e^{j \hat{\omega}}} =U_{w_{\lambda}}^*(e^{j\hat{\omega}}) $. 

Since $w_{\lambda}[n] u[n] + w_{\lambda}[-n] u[-n] = w_{\lambda}[n] +
  \delta[n]$, taking DTFT on both sides of this equation gives
```{math}
:label: e:UaddU*
\begin{equation}
U_{w_{\lambda}}(e^{j\hat{\omega}}) + U_{w_{\lambda}}^*(e^{j\hat{\omega}})
= 
W_{\lambda}(e^{j\hat{\omega}}) + 1.
\end{equation}
```
On the other hand, 
```{math}
:label: e:UminusU*
\begin{equation}
U_{w_{\lambda}}(e^{j\hat{\omega}}) - U_{w_{\lambda}}^*(e^{j\hat{\omega}})
= 
\frac{1}{1-\lambda e^{-j\hat{\omega}}} - \frac{1}{1-\lambda
  e^{j\hat{\omega}}}
=
\frac{-2j\lambda \sin\hat{\omega}}{1-2\lambda \cos\hat{\omega} +
  \lambda^2}.
\end{equation}
```
Adding {eq}`e:UaddU*` and  {eq}`e:UminusU*`gives
```{math}
:label: e:UasW
\begin{equation}
U_{w_{\lambda}}(e^{j\hat{\omega}}) 
= 
\frac{1}{2} W_{\lambda}(e^{j\hat{\omega}}) + \frac{1}{2}  \left(
  1 - \frac{2j\lambda \sin\hat{\omega}}{1-2\lambda \cos\hat{\omega} +
  \lambda^2} \right).
\end{equation}
```
Since $\displaystyle \lim_{\lambda \rightarrow 1} \frac{1}{2}  \left(
  1 - \frac{2j\lambda \sin\hat{\omega}}{1-2\lambda \cos\hat{\omega} +
  \lambda^2} \right) = \begin{cases}
  \frac{1}{2}, & \hat{\omega} = 0 \bmod 2\pi \\
  \frac{1}{1-e^{-j\hat{\omega}}}, &  \hat{\omega} \neq 0 \bmod 2\pi,
  \end{cases}$ taking limit as $\lambda\rightarrow 1$ on both sides
  of {eq}`e:UasW` gives
\begin{equation*}
U (e^{j\hat{\omega}}) = \pi \delta(e^{j\hat{\omega}}) + 
  \frac{1}{1-e^{-j\hat{\omega}}}.
\end{equation*}
```{tip}
Note the second term on the RHS above should be 
$\begin{cases}
  \frac{1}{2}, & \hat{\omega} = 0 \bmod 2\pi \\
  \frac{1}{1-e^{-j\hat{\omega}}}, &  \hat{\omega} \neq 0 \bmod 2\pi.
  \end{cases}$ 
However, the exact value of the term at $\hat{\omega} = 0 \bmod 2\pi$
  is immaterial (as long as it is finite) because any such value can
  be abosrbed into the infinite value of $\delta(e^{j\hat{\omega}})$
  at the same $\hat{\omega}$. Hence, for convenience, we may simply write
  $\frac{1}{1-e^{-j\hat{\omega}}}$ as in above with the implicit
  understanding that the term's value at $\hat{\omega} = 0 \bmod 2\pi$ is,
  say, $0$.
```
In summary, we have
\begin{equation*}
u[n] ~~
\stackrel{\text{DTFT}}{\longleftrightarrow} 
~~ \pi \delta(e^{j\hat{\omega}}) + \frac{1}{1-e^{-j\hat{\omega}}}
\end{equation*}

## Impulse train $\delta_N[n] = \sum_{k=-\infty}^{\infty} \delta[n-kN]$
Note that $\delta_N[n]$ is periodic with period $N$. Let $\Delta_{N,
w_{\lambda}}(e^{j\hat{\omega}})$ be the DTFT of $w_{\lambda}[n] \delta_N[n]$. 
Then
\begin{align*}
\Delta_{N, w_{\lambda}}(e^{j\hat{\omega}})
&= 
\sum_{n=-\infty}^{\infty} w_{\lambda}[n] \delta_N[n] e^{-j\hat{\omega} n} 
\\
&=
\sum_{k=-\infty}^{\infty} \lambda^{|Nk|} e^{-j\hat{\omega} Nk} 
\\
&=
\frac{1 - \lambda^{2N}}{1-2\lambda^N \cos(N\hat{\omega}) + \lambda^{2N}}
\\
& = W_{\lambda^{N}}(e^{jN\hat{\omega}}).
\end{align*}
It is easy to see that $W_{\lambda^{N}}(e^{jN\hat{\omega}})$ behaves
similar to $W_{\lambda}(e^{\hat{\omega}})$:
* $W_{\lambda^{N}}(e^{jN\hat{\omega}})$ is periodic in $\hat\omega$ with
  period $\frac{2\pi}{N}$,
* $\displaystyle \lim_{\lambda \rightarrow 1} 
  W_{\lambda^{N}}(e^{jN\hat{\omega}}) = \begin{cases}
  \infty, & \hat\omega = 0 \bmod \frac{2\pi}{N} \\
  0 & \hat\omega \neq 0 \bmod \frac{2\pi}{N},
  \end{cases}$ and
* $\displaystyle \lim_{\lambda \rightarrow 1} \frac{1}{2\pi}
  \int_{-\pi}^{\pi} W_{\lambda^{N}}(e^{jN\hat{\omega}}) \,
  d\hat{\omega} = 1$.

As a matter of fact, we may express $\lim_{\lambda \rightarrow 1}
W_{\lambda^{N}}(e^{jN\hat{\omega}})$ in terms of the Dirac delta
function $\delta(e^{j\hat{\omega}})$: 
\begin{equation*} 
\lim_{\lambda \rightarrow 1} W_{\lambda^{N}}(e^{jN\hat{\omega}}) 
= 
\frac{2\pi}{N} \sum_{k = 0}^{N-1} \delta\left(e^{j(\hat{\omega} - \frac{2\pi k}{N})}
\right).  
\end{equation*} 
```{caution} 
This however only holds at the limit. That is, 
$W_{\lambda^{N}}(e^{jN\hat{\omega}}) 
\neq \frac{2\pi}{N} \sum_{k = 0}^{N-1} 
W_{\lambda}\left(e^{j(\hat{\omega} - \frac{2\pi k}{N})} \right)$
for any $\lambda \in (0,1)$.
``` 
As a result, the DTFT $\displaystyle \Delta_N (e^{j\hat{\omega}}) =
\lim_{\lambda \rightarrow 1} W_{\lambda^{N}}(e^{jN\hat{\omega}}) =
\frac{2\pi}{N} \sum_{k = 0}^{N-1} \delta\left(e^{j(\hat{\omega} -
\frac{2\pi k}{N})} \right)$. In other words, we have the DTFT mapping
\begin{equation*}
\delta_N[n] ~~
\stackrel{\text{DTFT}}{\longleftrightarrow}
~~ \frac{2\pi}{N} \sum_{k = 0}^{N-1} \delta\left(e^{j(\hat{\omega} - \frac{2\pi k}{N})}
\right)
\end{equation*}

## General periodic $x[n]$ with period $N$
Note that we can write $\displaystyle x[n] = \sum_{k=0}^{N-1} x[k] \delta_N[n-k]$.
Hence, by the linearity and time shifting properties, the DTFT $X(e^{j\hat{\omega}})$
of $x[n]$ is given by
\begin{align*}
X(e^{j\hat{\omega}})
&=
\sum_{k=0}^{N-1} x[k] e^{-j \hat{\omega} k} \cdot
\sum_{l = 0}^{N-1} \delta\left(e^{j(\hat{\omega} - \frac{2\pi l}{N})}\right)
\\
&=
2\pi \sum_{l = 0}^{N-1} \bigg( \underbrace{\frac{1}{N} \sum_{k=0}^{N-1} x[k]
e^{-j\frac{2\pi l k}{N}} }_{\displaystyle a_l} \bigg)
\delta\left(e^{j(\hat{\omega} - \frac{2\pi l}{N})}\right).
\end{align*}
In summary, we have just established the following DTFT mapping for
any periodic $x[n]$ of period $N$:
\begin{equation*}
x[n] ~~
\stackrel{\text{DTFT}}{\longleftrightarrow}
~~ 2\pi \sum_{l = 0}^{N-1} a_l \delta\left(e^{j(\hat{\omega} - \frac{2\pi l}{N})}
\right)
\end{equation*}
```{tip}
* The coefficients $a_0, a_1, \ldots, a_{N-1}$ are referred to as the
  *discrete Fourier series (DFS)* coefficients of the periodic $x[n]$.
* The inverse DTFT formula {eq}`e:idtft` gives
  \begin{align*}
  x[n]
  &=
  \frac{1}{2\pi} \int_{-\pi}^{\pi} X(e^{j\hat{\omega}})
  e^{j\hat{\omega}n} \, d\hat{\omega}
  \\
  &=
  \sum_{l=0}^{N-1} a_l \int_{-\pi}^{\pi} e^{j\hat{\omega}n}
  \delta\left(e^{j(\hat{\omega} - \frac{2\pi l}{N})}\right)
  \, d\hat{\omega}
  \\
  &=
  \sum_{l=0}^{N-1} a_l e^{j \frac{2\pi ln}{N}}
  & (\text{sifting property of periodic Dirac delta}).
  \end{align*}
* The formulas
  \begin{align*}
  a_l 
  &=
  \frac{1}{N} \sum_{k=0}^{N-1} x[k] e^{-j\frac{2\pi l k}{N}}, 
  & l=0,1,\ldots, N-1
  \\
  x[n]
  &= 
  \sum_{l=0}^{N-1} a_l e^{j \frac{2\pi ln}{N}},
  & n=0,1,\ldots, N-1
  \end{align*}
  are the DFS *analysis* and *synthesis* formulas, respectively. They
  provide a shortcut to go directly between the periodic signal $x[n]$
  and its DTFT $X(e^{j\hat{\omega}})$
```
