# Multi-rate Filtering
 * A **multi-rate filter** is one whose output and output rates
  differ.  That is, the filter outputs more/fewer than one sample per
  each input sample.

* In practice, a fixed-rate ADC (and/or DAC)  is often used. We may
  want to process the sampled signal at a rate different from the
  sampling rate of the ADC. In such cases, performing *rate
  conversion* in discrete time using a multi-rate filter would be
  convenient.

* We start by discussing the simple cases of integer rate reduction
  (i.e., **downsampling/decimation**) and integer rate increase (ie.e,
  **interpolation**). 

## Downsampling by factor $D$
* Given $x[n] \stackrel{z}{\longleftrightarrow} X(z)$. Consider the
  *downsampled* signal $x_D[n] = x[Dn]$, where $D$ is a positive
  integer. That is, we obtain $x_D[n]$ by sampling $x[n]$ every $D$
  time instants: 
  ```{image} ../figs/downsample.jpg
  :alt: Downsampling
  :width: 500px
  :align: center
  ```
  The rate of $x_D[n]$ is $\frac{1}{D}$ times that of $x[n]$. That is,
  every $D$ samples of $x[n]$ gives $1$ sample pf $x_D[n]$.

* Recall, from {numref}`sec:imtr` and {numref}`sec:dfs`, the impulse
  train $\displaystyle \delta_D[n] = \sum_{k=-\infty}^{\infty}
  \delta[n-kD]$ of period $D$ and its DFS expansion $\displaystyle
  \delta_D[n] = \sum_{k=0}^{D-1} e^{j\frac{2\pi k n}{D}}$. Let
  $\tilde{x}[n] = x[n] \delta_D[n]$. Then, it is trivial to check
  that $x_D[n] = \tilde{x}[Dn]$.  
