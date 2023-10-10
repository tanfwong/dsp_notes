# Frequency Response of LTI System

* The **frequency response** $H(e^{j\hat\omega})$ of an LTI system is
  the DTFT (if exists) of the system's impulse response $h[n]$, i.e.,
  $h[n] \stackrel{\text{DTFT}}{\longleftrightarrow}
 c$.

## Properties of Frequency Response
* Let $h[n] \stackrel{z}{\longleftrightarrow} H(z)$. If the ROC of the
  transfer function $H(z)$ contains the unit circle, then $H(e^{j\hat\omega})
  = H(z) \big|_{z=e^{j\hat\omega}}$. 

* The convolution properties of DTFT gives:

  If $x[n] \stackrel{\text{DTFT}}{\longleftrightarrow}
  X(e^{j\hat\omega})$ and $y[n] \stackrel{\text{DTFT}}{\longleftrightarrow}
  Y(e^{j\hat\omega})$ are the input and output signals of the LTI
  system, then $Y(e^{j\hat\omega}) =  H(e^{j\hat\omega})
  X(e^{j\hat\omega})$.

* For the special case $x[n] = Ae^{j\phi} e^{j\hat\omega_0 n}$, the
  DTFT of the output signal of the LTI system is $Y(e^{j\hat\omega}) =
  H(e^{j\hat\omega}) 2\pi Ae^{j\phi} \delta((e^{j(\hat\omega -
  \hat\omega_0)}) = H(e^{j\hat\omega_0}) 2\pi Ae^{j\phi}
  \delta(e^{j(\hat\omega - \hat\omega_0)}) $, and hence the output
  signal is $y[n] = H(e^{j\hat\omega_0}) Ae^{j\phi} e^{j\hat\omega_0
  n}$.

* The **phase delay** of the LTI system is defined as $\displaystyle
  \tau_p(e^{j\hat\omega}) = -\frac{ \angle
  H(e^{j\hat\omega})}{\hat\omega}$, and the **group delay** of the LTI
  system is defined as $\displaystyle \tau_g(e^{j\hat\omega}) =
  -\frac{ d\angle H(e^{j\hat\omega})}{d\hat\omega}$. The phase and
  group delays are of interest in many practical applications as we
  will see later. The following two examples help to illustrate the
  physical interpretation of the phase and group delays:

  - **Example 1**:  Let $\displaystyle H(e^{j\hat\omega}) =
    e^{-j\hat\omega  \tau_p(e^{j\hat\omega})}$, i.e.,
    $|H(e^{j\hat\omega})| = 1$ and $\angle H(e^{j\hat\omega}) =
    -\hat\omega \tau_p(e^{j\hat\omega})$. Consider the sinusoidal input
    $x[n] = e^{j\hat\omega_0 n}$. Then the output is 
    \begin{equation*}
    y[n] = e^{-j\hat\omega_0 \tau_p(e^{j\hat\omega_0})} e^{j\hat\omega_0 n} =
    e^{j\hat\omega_0( n - \tau_p(e^{j\hat\omega_0}))}. 
    \end{equation*}
    As a result, we may interpret the phase delay
    causing a *phase shift* of  $-\hat\omega_0
    \tau_p(e^{j\hat\omega_0})$, or equivalently a *time shift* of
    $\tau_p(e^{j\hat\omega_0})$, to the input sinusoid at frequency
    $\hat\omega_0$. 
    ```{tip}
    If $\tau_p(e^{j\hat\omega_0})$ is anot an integer, we may
    interpret that $x[n]$ is obtained from oversampling (with sampling
    rate $f_s$) a
    continuous-time sinusoid $x(t)$ with frequency $\hat\omega_0 f_s$
    and $y[n]$ is the sampled (at $f_s$) signal obtained from the
    delayed version $x(t - \frac{\tau_p(e^{j\hat\omega_0})}{f_s})$.
    ```

  - **Example 2**: Consider the same frequency response in **Example
    1**, but instead with input signal $x[n] =
    2\cos(\frac{\Delta\hat\omega}{2} n) e^{j\hat\omega_0 n} =
    e^{j(\hat\omega_0 + \frac{\Delta\hat\omega}{2}) n} +
    e^{j(\hat\omega_0 - \frac{\Delta\hat\omega}{2}) n}$ where
    $|\Delta\hat\omega| \ll |\hat\omega_0|$. Using the following 
    Taylor series approximations
    \begin{align*}
    \angle H(e^{j(\hat\omega_0 + \frac{\Delta\hat\omega}{2})}) 
    &\approx 
    \angle H(e^{j\hat\omega_0}) - \frac{\Delta\hat\omega}{2} \tau_g(e^{j\hat\omega_0})
    = -  \hat\omega_0 \tau_p(e^{j\hat\omega_0}) -
    \frac{\Delta\hat\omega}{2} \tau_g(e^{j\hat\omega_0})
    \\
    \angle H(e^{j(\hat\omega_0 - \frac{\Delta\hat\omega}{2})}) 
    &\approx 
    \angle H(e^{j\hat\omega_0}) + \frac{\Delta\hat\omega}{2} \tau_g(e^{j\hat\omega_0})
    = -  \hat\omega_0 \tau_p(e^{j\hat\omega_0}) +
    \frac{\Delta\hat\omega}{2} \tau_g(e^{j\hat\omega_0}),
    \end{align*}
    we get the output signal
    \begin{align*}
    y[n]
    &=
    e^{j\angle H(e^{j(\hat\omega_0 + \frac{\Delta\hat\omega}{2})})}
    e^{j(\hat\omega_0 + \frac{\Delta\hat\omega}{2}) n}
    + 
    e^{j\angle H(e^{j(\hat\omega_0 - \frac{\Delta\hat\omega}{2})})}
    e^{j(\hat\omega_0 - \frac{\Delta\hat\omega}{2}) n}
    \\
    & \approx
    2 \cos\left(\frac{\Delta\hat\omega}{2} (n -
    \tau_g(e^{j\hat\omega_0})) \right) e^{j\hat\omega_0(n -
    \tau_p(e^{j\hat\omega_0}) )}.
    \end{align*}
    Since $|\Delta\hat\omega| \ll |\hat\omega_0|$, the term
    $2\cos(\frac{\Delta\hat\omega}{2} n)$ in $x[n]$ slowly varies the
    amplitude of the underlying sinusoid $e^{j\hat\omega_0 n}$. As a
    result, $2\cos(\frac{\Delta\hat\omega}{2} n)$ is often called the
    **envelope** of $x[n]$. The group delay of the system thus then
    specifies the delay in the envelope of $x[n]$.
