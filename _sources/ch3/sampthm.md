# Sampling Theorem
* Suppose that a continuous-time signal $x(t)$ is sampled at the
  sampling rate of $f_s$ samples per second to obtain the
  discrete-time signal $x[n] = x(\frac{n}{f_s})$. The frequency-domain
  version of the Poisson sum formula {eq}`e:poisson_f` relates the
  DTFT $X(e^{j\hat\omega})$ of the sampled signal $x[n]$ to the FT 
  $X(\omega)$ of the original continuous-time signal $x(t)$:
  ```{math}
  :label: e:folded_spectrum
  \begin{equation}
  X(e^{j\hat\omega}) = f_s \sum_{k=-\infty}^{\infty}
  X((\hat\omega+2\pi k)f_s)
  \end{equation}
  ```
  where the quantity on the RHS is often referred tp as the ***folded
  spectrum*** of $x(t)$. In other words, the DTFT of the sampled
  signal $x[n]$ is the folded spectrum of $x(t)$.
  ```{tip}
  One may extend the Poisson sum formula to include all finite-energy
  and some common infinite-energy signals and FTs based on the
  limiting process with windowing as we did before.
  ```

* From {eq}`e:folded_spectrum`, it is clear that the folded spectrum
  depends on both the FT of the continuous-time signal and the sampling
  rate. The effects of both factors are best explained in
  picture. First, let us introduce the concept of *bandlimtedness*:
  ```{admonition} Notation
  A continuous-time signal $x(t)$ is ***bandlimited*** to $\Omega =
  2\pi B$ radian per second (or $B$ Hz) if its FT $X(\omega) = 0$ for
  $|\omega| > \Omega$. The quantity $\Omega$ (or $B$) is called the
  ***bandwidth*** of $x(t)$.
  ```
* For a simple illustration, consider a bandlimited continuous-time
  signal $x(t)$ whose FT $X(\omega)$ is of real-valued and as shown below:
  ```{image} ../figs/blspectrum.jpg
  :alt: A bandlimited spectrum
  :width: 400px
  :align: center
  ```
  The bandwidth of $x(t)$ is $\Omega$ radians per second, or $B$ Hz.
  To draw the folded spectrum of $x(t)$, we need to consider two
  different cases:

    1. If $f_s > 2B$, then the folded spectrum is as below:
    ```{image} ../figs/oversample.jpg
    :alt: Folded spectrum (oversampling)
    :width: 800px
    :align: center
    ```
    ```{admonition} Notation
    The condition $f_s > 2B$ is referred to as ***oversampling***.
    ```
    2. If $f_s \leq 2B$, then the folded spectrum is as below:
    ```{image} ../figs/undersample.jpg
    :alt: Folded spectrum (undersampling)
    :width: 600px
    :align: center
    ```
    ```{admonition} Notation
    The condition $f_s \leq 2B$ is referred to as ***undersampling***.
    ```

*
