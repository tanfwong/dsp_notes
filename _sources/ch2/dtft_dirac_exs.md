# DTFTs of infinite-energy signals

* For any infinite-energy signal $x[n]$ whose signal magnitude
  increases at most polynomially with $|n|$ (i.e., $|x[n]| =
  \mathcal{O}(|n|^{\alpha})$ for some $\alpha>0$), its windowed
  version $w_{\lambda} [n] x[n] \in \ell^1$ and hence the DTFT mapping 
  $w_{\lambda}[n] x[n] \stackrel{\text{DTFT}}{\longleftrightarrow} 
  X_{w_{\lambda}}(e^{j\hat{\omega}})$ exists for all $\lambda \in (0,1)$.
  As discussed in {numref}`sec:wlimit`, we may define
  $\lim_{\lambda \rightarrow 1} X_{w_{\lambda}}(e^{j\hat{\omega}})$
  (if the limit exists) as the DTFT $X(e^{j\hat{\omega}})$ )$ of $x[n]$. 
* Note that the limit of $X_{w_{\lambda}}(e^{j\hat{\omega}})$ may not
  exist for any general $x[n]$. Even if it exists, calculating it may
  be difficult. Luckily, for some of the most common infinite-energy
  signals, we can express $\lim_{\lambda \rightarrow 1}
  X_{w_{\lambda}}(e^{j\hat{\omega}})$ in terms of
  $\delta(e^{j\hat{\omega}})$ as shown below.

## Sinusoid $x[n] = e^{j\hat{\omega}_0 n}$
First, note that 
\begin{align*} 
X_{w_{\lambda}}(e^{j\hat{\omega}}) 
&=
\sum_{n=-\infty}^{\infty} w_{\lambda}[n] x[n] e^{-j\hat{\omega} n} \\
&= 
\sum_{n=-\infty}^{\infty} \lambda^{|n|} e^{j\hat{\omega}_0 n}
e^{-j\hat{\omega} n} \\ & = \frac{1 - \lambda^2}{1-2\lambda
\cos(\hat{\omega}-\hat{\omega}_0) + \lambda^2} \\ 
&=
W_{\lambda}(e^{j(\hat{\omega}-\hat{\omega}_0)}).  
\end{align*} 
Hence, $\displaystyle X(e^{j\hat{\omega}}) = \lim_{\lambda \rightarrow
1} X_{w_{\lambda}}(e^{j\hat{\omega}}) = \lim_{\lambda \rightarrow 1}
W_{\lambda}(e^{j(\hat{\omega}-\hat{\omega}_0)}) = 2\pi \delta
(e^{j(\hat{\omega}-\hat{\omega}_0)})$. In other words, we have
established the DTFT pair 
\begin{equation*}
e^{j\hat{\omega}_0 n} ~~
\stackrel{\text{DTFT}}{\longleftrightarrow} 
~~ 2\pi \delta (e^{j(\hat{\omega}-\hat{\omega}_0)}).
\end{equation*}

