# FIR Filter Design

* We discuss two common approaches to design FIR filters that
  approximate the frequency responses of the ideal filters. We focus
  on the design of lowpass filter. The design approaches extend almost
  trivially to other types of filters. One may also use the frequency
  transformation methods in {numref}`sec:freqtrans` to convert the
  lowpass filter to other types of filters.




## Filter Specifications
* The first step in the filter design process is to specify in what
way we are to approximate the frequency response of an ideal lowpass
filter. 

* In the following discussion, we consider the specification of the
  magnitude response shown in the figure below:
  ```{image} ../figs/fspec.png
  :alt: Lowpass filter specification
  :width: 800px
  :align: center
  ```
  This specification is quantified by the quadruple 
  $(\hat\omega_p, \hat\omega_s, \delta_1, \delta_2)$.

* For the phase response, we impose the restriction that the group
  delay of the filter must be a constant. That is, the filter must be
  a generalized linear-phase FIR filter.
