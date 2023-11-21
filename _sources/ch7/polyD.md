(sec:polydown)=
# Polyphase Implementation of Downsampling 
Consider the downsampling system as shown below with an anti-aliasing filter
```{image} ../figs/polyD1.jpg 
:alt: Downsampling with anti-aliasing filter
:width: 800px 
:align: center 
```
whose impulse response is $h[n] \stackrel{z}{\longleftrightarrow}
H(z)$:
  

1. Applying the direct form of the {ref}`polyphase decomposition identity <sec:polyid>` to
   $H(z)$ with $e_k[n] = h[nD+k]$, for $k=0,1,\ldots, D-1$, gives
   ```{image} ../figs/polyD2.jpg 
   :alt: Polyphase decomposition step 1
   :width: 800px 
   :align: center 
   ```

2. Next, applying the {ref}`downsampling identity <sec:downid>` to each
   branch in step 1 gives
   ```{image} ../figs/polyD3.jpg 
   :alt: Polyphase decomposition step 2
   :width: 800px 
   :align: center 
   ```

3. Finally, applying the {ref}`downsample-demux identity <sec:DDid>` to the bank
   of downsamplers in step 2 gives the following polyphase implementation of the
   downsampling system:
   ```{image} ../figs/polyD4.jpg 
   :alt: Polyphase decomposition step 3
   :width: 800px 
   :align: center 
   ```

* Note that all the polyphase filters $E_k(z)$, $k=0,1,\ldots, D-1$,
  operate at $\frac{1}{D}$ times of the input rate. If $H(z)$ is an
  FIR filter of length $L$, then the length of each of the polyphase
  (FIR) filters is about $\frac{L}{D}$. 

* Clearly, the polyphase structure allows simple parallel
  implementation of the polyphase filters. Nevertheless, the
  computational complexity (number of multiplications) of the
  polyphase implementation remains $\mathcal{O}(\frac{L}{D})$ per
  input sample, assuming time-domain implementation for $h[n]$ and all
  polyphase component filters by convolution.
