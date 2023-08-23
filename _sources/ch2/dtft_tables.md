# DTFT properties and tables

## Table of DTFT pairs
```{list-table}
:header-rows: 1

* - $\boldsymbol{x[n]}$ 
  - $\boldsymbol{X(e^{j{\hat{\omega}}})}$ 
  - Condition 

* - $\displaystyle a^n u[n]$ 
  - $\displaystyle \frac{1}{1 - a e^{-j \hat{\omega}}}$
  - $|a| < 1$ 
  
* - $\displaystyle (n+1) a^n u[n]$ 
  - $\displaystyle \frac{1}{(1-a e^{-j \hat{\omega}})^2}$
  - $|a| < 1$

* - $\displaystyle \frac{(n+r-1)!}{n! (r-1)!} a^n u[n]$ 
  - $\displaystyle \frac{1}{(1-a e^{-j \hat{\omega}})^r}$
  - $|a| < 1$

* - $\displaystyle \delta[n]$ 
  - $\displaystyle 1$
  -

* - $\displaystyle \delta[n - n_0]$ 
  - $\displaystyle e^{-j \hat{\omega} n_0}$
  -

* - $\displaystyle u[n]-u[n-N]$
  - $\displaystyle \frac{\sin(N\hat{\omega}/2)}{\sin(\hat{\omega} /
  2)} e^{-j(\frac{N-1}{2})\hat\omega}$
  -

* - $\displaystyle \frac{\sin(\hat\omega_0 n)}{\pi n}$
  - $ X(e^{j{\hat{\omega}}}) = 
      \begin{cases}
      1, & 0 \leq |\hat{\omega}| \leq \hat\omega_0 \\
      0. & \hat\omega_0 < |\hat{\omega}| \leq  \pi
      \end{cases}$
  -
  
* - $\displaystyle 1$ 
  - $\displaystyle 2 \pi \delta(e^{j\hat{\omega}})$
  - 

* - $\displaystyle u[n]$ 
  - $\displaystyle \frac{1}{1-e^{-j \hat{\omega}}} + \pi \delta(e^{j\hat{\omega}})$
  -

* - $\displaystyle e^{j \hat{\omega}_0 n}$ 
  - $\displaystyle 2 \pi \delta(e^{\hat{\omega}  - \hat{\omega}_0})$
  -

* - $\displaystyle \cos(\hat{\omega}_0 n)$ 
  - $\displaystyle \pi \left[ \delta(e^{j(\hat{\omega}-\hat{\omega}_0)}) + 
    \delta(e^{j(\hat{\omega}+\hat{\omega}_0)}) \right]$
  -

* - $\displaystyle \sin(\hat{\omega}_0 n)$
  - $\displaystyle \frac{\pi}{j} \left[ \delta(e^{j(\hat{\omega}-\hat{\omega}_0)}) + 
    \delta(e^{j(\hat{\omega}+\hat{\omega}_0)}) \right]$
  -
  
* - $\displaystyle \sum_{k=-\infty}^{\infty} \delta[n - kN]$
  - $\displaystyle \frac{2 \pi}{N} \sum_{k=0}^{N-1}
    \delta\left(e^{j\left(\hat{\omega} - \frac{2 \pi k}{N} \right)}
    \right)$
  - 
```

## Table of DTFT properties
For each property listed below, assume 
$x[n] \stackrel{\text{DTFT}}{\longleftrightarrow}
X(e^{j\hat\omega})$ and $y[n] \stackrel{\text{DTFT}}{\longleftrightarrow}
Y(e^{j\hat\omega})$:
```{list-table}
:header-rows: 1

* - Property
  - Time domain
  - Frequency domain

* - Linearity
  - $\alpha x[n] + \beta y[n]$
  - $\alpha X(e^{j{\hat{\omega}}}) + \beta Y(e^{j{\hat{\omega}}})$

* - Time Shifting
  - $x[n-n_0]$
  - $X(e^{j{\hat{\omega}}}) e^{-j \widehat{\omega} n_0}$

* - Frequency Shifting
  - $x[n] e^{j \hat{\omega}_0 n}$
  - $X(e^{j(\hat{\omega}-\hat{\omega}_0)})$

* - Conjugation 
  - $x^*[n]$
  - $X^*(e^{-j\hat{\omega}})$

* - Time Reversal
  - $x[-n]$ 
  - $X(e^{-j\hat{\omega}})$

* - Convolution
  - $x[n]*y[n]$
  - $X(e^{j\hat{\omega}}) Y(e^{j\hat{\omega}})$

* - Multiplication
  - $x[n] y[n]$
  - $\displaystyle \frac{1}{2\pi} \int_{-\pi}^{\pi}
    X(e^{j\theta}) Y(e^{j(\hat{\omega}-\theta)}) d\theta$
    
* - Time Differencing
  - $x[n]-x[n-1]$
  - $(1-e^{-j\hat{\omega}})X(e^{j\hat{\omega}})$

* - Accumulation
  - $\sum_{k=-\infty}^{n} x[k]$
  - $\frac{X(e^{j\hat{\omega}})}{1 - e^{-j\hat{\omega}}} + 
    \pi X(e^{j0}) \delta(e^{j\hat{\omega}})$

* - Frequency Differentiation
  - $n x[n]$
  - $\displaystyle j\frac{d X(e^{j\hat{\omega}})}{d\hat{\omega}}$

* - Parseval Theorem
  - $\sum_{n=-\infty}^{N} x[n] y^*[n]$
  - $ \frac{1}{2\pi} \int_{-\pi}^{\pi}
    X(e^{j\hat\omega}) Y^*(e^{j\hat\omega}) d\hat\omega$
```
