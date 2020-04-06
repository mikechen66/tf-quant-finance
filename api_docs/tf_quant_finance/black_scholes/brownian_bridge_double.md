<div itemscope itemtype="http://developers.google.com/ReferenceObject">
<meta itemprop="name" content="tf_quant_finance.black_scholes.brownian_bridge_double" />
<meta itemprop="path" content="Stable" />
</div>

# tf_quant_finance.black_scholes.brownian_bridge_double

<!-- Insert buttons and diff -->

<table class="tfo-notebook-buttons tfo-api" align="left">
</table>

<a target="_blank" href="https://github.com/google/tf-quant-finance/blob/master/tf_quant_finance/black_scholes/brownian_bridge.py">View source</a>



Computes probability of not touching the barriers for a 1D Brownian Bridge.

```python
tf_quant_finance.black_scholes.brownian_bridge_double(
    *, x_start, x_end, variance, upper_barrier, lower_barrier, n_cutoff=3,
    dtype=None, name=None
)
```



<!-- Placeholder for "Used in" -->

The Brownian bridge starts at `x_start`, ends at `x_end` and has a variance
`variance`. The no-touch probabilities are calculated assuming that `x_start`
and `x_end` are within the barriers 'lower_barrier' and 'upper_barrier'.
This can be used in Monte Carlo pricing for adjusting probability of
touching the barriers from discrete case to continuous case.
Typically in practice, the tensors `x_start`, `x_end` and `variance` should be
of rank 2 (with time steps and paths being the 2 dimensions).

#### Example

```python
x_start = np.asarray([[4.5, 4.5, 4.5], [4.5, 4.6, 4.7]])
x_end = np.asarray([[5.0, 4.9, 4.8], [4.8, 4.9, 5.0]])
variance = np.asarray([[0.1, 0.2, 0.1], [0.3, 0.1, 0.2]])
upper_barrier = 5.1
lower_barrier = 4.4

no_touch_proba = brownian_bridge_double(
  x_start=x_start,
  x_end=x_end,
  variance=variance,
  upper_barrier=upper_barrier,
  lower_barrier=lower_barrier,
  n_cutoff=3,
  )
# Expected print output of no_touch_proba:
#[[0.45842169 0.21510919 0.52704599]
#[0.09394963 0.73302813 0.22595022]]
```

#### References

[1] Emmanuel Gobet. Advanced Monte Carlo methods for barrier and related
exotic options.
https://papers.ssrn.com/sol3/papers.cfm?abstract_id=1265669

#### Args:


* <b>`x_start`</b>: A real `Tensor` of any shape and dtype.
* <b>`x_end`</b>: A real `Tensor` of the same dtype and compatible shape as
  `x_start`.
* <b>`variance`</b>: A real `Tensor` of the same dtype and compatible shape as
  `x_start`.
* <b>`upper_barrier`</b>: A scalar `Tensor` of the same dtype as `x_start`. Stands for
  the upper boundary for the Brownian Bridge.
* <b>`lower_barrier`</b>: A scalar `Tensor` of the same dtype as `x_start`. Stands for
  lower the boundary for the Brownian Bridge.
* <b>`n_cutoff`</b>: A positive scalar int32 `Tensor`. This controls when to cutoff
  the sum which would otherwise have an infinite number of terms.
  Default value: 3.
* <b>`dtype`</b>: Optional `tf.DType`. If supplied, the dtype to be used for conversion
  of any supplied non-`Tensor` arguments to `Tensor`.
  Default value: None which maps to the default dtype inferred by
  TensorFlow.
* <b>`name`</b>: str. The name for the ops created by this function.
  Default value: None which is mapped to the default name
  `brownian_bridge_double`.


#### Returns:

A `Tensor` of the same shape as the input data which is the probability
of not touching the upper and lower barrier.