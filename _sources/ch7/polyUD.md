# Polyphase Implementation of $\frac{U}{D}$-rate Filter
Consider the general $\frac{U}{D}$-rate system as shown below with
an LTI filter
```{image} ../figs/polyUD1.jpg 
:alt: General $\frac{U}{D}$-rate filter
:width: 800px 
:align: center 
```
whose impulse response is $h[n] \stackrel{z}{\longleftrightarrow}
H(z)$:
  

1. As in {numref}`sec:polyinterp`, applying the transposed form of the
   {ref}`polyphase decomposition identity <sec:polyid>` to $H(z)$ with
   $e_k[n] = h[nU+k]$, for $k=0,1,\ldots, U-1$, and then the
   {ref}`upsampling identity <sec:upid>` to each branch gives
  ```{image} ../figs/polyUD2.jpg 
   :alt: Polyphase decomposition step 1
   :width: 800px 
   :align: center 
   ```

2. Next, applying the {ref}`upsample-downsample-mux identity <sec:UDid>` to the bank
   of upsamplers and the downsampler in step 1 gives
   ```{image} ../figs/polyUD3.jpg 
   :alt: Polyphase decomposition step 2
   :width: 800px 
   :align: center 
   ```

3. Then, for each $k=0,1,\ldots, U-1$, , as in {numref}`sec:polydown`,
   applying the direct form of the
   {ref}`polyphase decomposition identity <sec:polyid>`,
   {ref}`downsampling identity <sec:downid>`, and
   {ref}`downsample-demux identity <sec:DDid>` to the $k$th branch
   in step 2 gives
   ```{image} ../figs/polyUD4.jpg 
   :alt: Polyphase decomposition step 3
   :width: 800px 
   :align: center 
   ```
   where the impulse response of the polyphase filter component
   $F_{k,l}$ is given by 
   \begin{align*}
   f_{k,l}[n] 
   &= 
   e_{kD\%U} \left[nD +
   \left\lfloor \frac{kD}{U} \right\rfloor + l \right]
   \\
   &=
   h \left[ \left(nD + \left\lfloor \frac{kD}{U} \right\rfloor + l
   \right) U + kD\%U \right]
   \\
   &=
   h[nUD + kD + lU]
   \end{align*}
   for $l=0,1,\ldots, D-1$.
   ```{caution}
   Note that some of the polyphase filter components $f_{l,k}[n]$ may
   be non-causal even if $h[n]$ is causal.
   ```

4. Finally, putting the polyphase implementation of the $k$th branch
   in step 3 back to the structure in step 2 gives the following overall
   polyphase implementation of the $\frac{U}{D}$-rate filter:    
   ```{image} ../figs/polyUD5.jpg 
   :alt: Polyphase decomposition step 4
   :width: 800px 
   :align: center 
   ```
   

* Note that all the polyphase component filters $F_{k,l}(z)$,
  $k=0,1,\ldots, U-1$ and $l=0,1,\ldots, D-1$, operate at
  $\frac{1}{D}$ times of the input rate. If $H(z)$ is an FIR filter of
  length $L$, then the length of $f_{k,l}[n]$ is at most $\lceil
  \frac{L}{UD} \rceil + 1$.

* Clearly, the polyphase structure allows simple parallel
  implementation of the polyphase componet filters. Assuming $NU \gg L
  \gg UD$ where $N$ is the length of the input signal, the
  computational complexity (number of multiplications) of the
  polyphase implementation is $\mathcal{O}(\frac{L}{D})$ per input
  sample, instead of $\mathcal{O}(\frac{UL}{D})$ per input sample for
  the direct implementation.
