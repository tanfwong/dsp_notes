# Discrete-time signals
* **Discrete-time signal** $x : \mathbb{Z} \longrightarrow \mathbb{R}$
  or $\mathbb{C}$.
  ```{admonition} Notation
  Use $x[n]$ to denote a discrete-time signal, where the square
  brackets indicate "discrete time", and letters $n$, $m$,
  $k$, and $l$ take on integer "time" values.
  ```

* **Continuous-time signal** $x : \mathbb{R} \longrightarrow \mathbb{R}$
  or $\mathbb{C}$.
  ```{admonition} Notation
  Use $x(t)$ to denote a continuous-time signal, where the 
  parantheses indicate "continuous time", and letters $t$, and $s$
  take on real "time" values.
  ```

* Simple, but important, discrete-time signals:
  - **Unit impulse signal** $\delta[n] = \begin{cases} 1 & n=0 \\ 0 & n
    \neq 0 \end{cases}$
  - **Unit step signal** $u[n] = \begin{cases} 1 & n \geq 0 \\ 0 & n
    < 0 \end{cases}$
  - **(Complex-valued) sinusoid** $Ae^{j\phi} e^{j\hat\omega n}$
    ```{note}
    Euler's identity implies $A\cos(\hat\omega n + \phi) =
    \frac{A}{2}e^{j\phi} e^{j\hat\omega n} + \frac{A}{2}e^{-j\phi} e^{-j\hat\omega n}$.
    ```
  - **Stepped sinusoid** $Ae^{j\phi} e^{j\hat\omega n} u[n]$

* Some important signal properties:
  - **Periodicity**:
     - $x[n]$ is <em>periodic</em> with period $N$ $(N\geq 0)$ if $x[n] = x[n+N]$
       for all $n \in \mathbb{Z}$.
     - The smallest such $N$ is called the <em>fundamental period</em>.
       ```{note}
       Often, we simply call the fundamental period of $x[n]$ the
       **<em>period</em>** of the signal when there is no ambiguity.
       ```
     - If no such $N$ exists, $x[n]$ is <em>aperiodic</em>.
   - **Signal energy**: $E_x = \sum_{n=-\infty}^{\infty}  |x[n]|^2$.
   - **Signal power**: $P_x = \lim_{M \rightarrow \infty} \frac{1}{2M+1} \sum_{n=-M}^{M}  |x[n]|^2$.
       ```{note}
       If $x[n]$ is periodic with period $N$, $P_x = \frac{1}{N} \sum_{n=0}^N |x[n]|^2$.
       ```
   
   
