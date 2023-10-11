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

(sec:rational)=
## FIR and IIR Filters
* We will focus on the design of causal LTI systems whose transfer
  functions are in the rational form:
  \begin{equation*}
  H(z) = \frac{B(z)}{A(z)} = \frac{\sum_{k=0}^M b_k z^{-k}}{\sum_{k=0}^N a_k z^{-k}}
  \end{equation*}
  where $a_0 = 1$. These include both FIR and IIR filters. The $b_k$'s
  and $a_k$'s are often called the *feedforward* and *feedback* taps,
  respectively.

* Let $z_1, z_2, \ldots, z_M$ and $p_1, p_2, \ldots, p_N$ be the roots
  of $B(z)$ and $A(z)$, respectively. We can rewrite
  \begin{equation*}
  H(z) = b_0 \frac{\prod_{k=1}^M (1- z_k z^{-1})}{\prod_{k=1}^N (1-p_k
  z^{-1})}.
  \end{equation*}
  If $\{z_k\}_{k=1}^M$ and $\{p_k\}_{k=1}^N$ do not intersect, then
  $\{z_k\}_{k=1}^M$ are *zeros* and $\{p_k\}_{k=1}^N$ are *poles*
  of $H(z)$.
  ```{caution}
  There may be additional zeros ($M<N$) or poles ($M>N$) at $z=0$.
  ```
* If all the poles are strictly inside the unit circle, then the
  system is *stable*, and its frequency response is given by
  ```{math}
  :label: e:freq_resp
  \begin{equation}
  H(e^{j\hat\omega}) 
  =
  b_0 \frac{\prod_{k=1}^M (1- z_k e^{-j\hat\omega})}{\prod_{k=1}^N (1-p_k
  e^{-j\hat\omega})}.
  \end{equation}
  ```

* Let $|\cdot|_{\text{dB}} = 20 \log_{10} |\cdot|$. Then
  {eq}`e:freq_resp` gives the following formulas for the *magnitude*
  and *phase* responses:
  ```{math}
  :label: e:freq_resp_comp
  \begin{align*}
  |H(e^{j\hat\omega})|_{\text{dB}} 
  &= |b_0|_{\text{dB}}  + 
  \sum_{k=1}^M |1- z_k e^{-j\hat\omega})|_{\text{dB}} 
  - \sum_{k=1}^N |1- p_k e^{-j\hat\omega})|_{\text{dB}} 
  \\
  \angle H(e^{j\hat\omega})
  &= \angle b_0 + 
  \sum_{k=1}^M \angle (1- z_k e^{-j\hat\omega})
  - \sum_{k=1}^N \angle (1- p_k e^{-j\hat\omega}).
  \end{align*}
  ```
  Hence, both the magnitude and phase responses are governed by those
  of first-order systems with transfer functions in the form of
  $1-cz^{-1}$. 

