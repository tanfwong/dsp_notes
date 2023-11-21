# Polyphase Implementation of Interpolation
* Consider the interpolation system as shown below with an interpolation filter

  ```{image} ../figs/polyU1.jpg 
  :alt: Interpolation system
  :width: 800px 
  :align: center 
  ```
  whose impulse response is $h[n] \stackrel{z}{\longleftrightarrow}
  H(z)$.
  

* Applying the transposed form of the {ref}`polyphase decomposition identity <sec:polyid>` to
  $H(z)$ with $e_k[n] = h[nU+k]$, for $k=0,1,\ldots, U-1$, gives
  ```{image} ../figs/polyU2.jpg 
  :alt: Polyphase decomposition step 1
  :width: 800px 
  :align: center 
  ```

* Next, applying the {ref}`upsampling identity <sec:upid>` to each
  branch above gives
  ```{image} ../figs/polyU3.jpg 
  :alt: Polyphase decomposition step 2
  :width: 800px 
  :align: center 
  ```

* Finally, applying the {ref}`upsample-mux identity <sec:UMid>` to the bank
  of upsamplers gives the following polyphase implementation of the
  interpolation system:
  ```{image} ../figs/polyU4.jpg 
  :alt: Polyphase decomposition step 3
  :width: 800px 
  :align: center 
  ```

* Note that all the polyphase filters $E_k(z)$, $k=0,1,\ldots, U-1$,
  operate at the input rate. If $H(z)$ is an FIR filter of length $L$,
  then the length of each of the polyphase (FIR) filters is about
  $\frac{L}{U}$. 

* Clearly, the polyphase structure allows simple parallel
  implementation of the polyphase filters. Assuming $NU \gg L$ where
  $N$ is the length of the input signal, the computational complexity
  (number of multiplications) of the polyphase implementation is
  $\mathcal{O}(L)$ per input sample, instead of $\mathcal{O}(UL)$ per
  input sample for the direct implementation.
