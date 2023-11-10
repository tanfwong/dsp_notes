# Multi-rate Filtering
 * A **multi-rate filter** is one whose output and output rates
  differ.  That is, the filter outputs more/fewer than one sample per
  each input sample.

* In practice, a fixed-rate ADC (and/or DAC)  is often used. We may
  want to process the sampled signal at a rate different from the
  sampling rate of the ADC. In such cases, performing *rate
  conversion* in discrete time using a multi-rate filter would be
  convenient.

