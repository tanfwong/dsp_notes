# Review of discrete-time signals and systems

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
  - **Unitstep signal** $u[n] = \begin{cases} 1 & n \geq 0 \\ 0 & n
    < 0 \end{cases}$
  - **(Complex-valued) sinusoid** $Ae^{j\phi} e^{j\hat\omega n}$
    ```{note}
    Euler's identity implies $A\cos(\hat\omega n + \phi) =
    \frac{A}{2}e^{j\phi} e^{j\hat\omega n} + \frac{A}{2}e^{-j\phi} e^{-j\hat\omega n}$.
    ```
  - **Step sinusoid** $Ae^{j\phi} e^{j\hat\omega n} u[n]$
