# Notes on Implementation of Neural Networks


## Common Terms

| Term            | Description   |
| --------------- |---------------|
| Vectorization   |  A way to speed up the Python code **without using loop** |


## Vectorization
Vectorization is used to speed up the Python _(or Matlab)_ code without using loop. Using such a function can help in minimizing the running time of code efficiently. Various operations are being performed over vector such as _dot product_ of vectors, _outer products_ of vectors and _element wise multiplication_.

## Advantages
* Faster execution (allows parallel operations) 👨‍🔧
* Simpler and more readable code :sparkles:

### Simple Visualization
<img src="https://github.com/asmaamirkhan/TensorflowGuide/blob/master/res/Vectorization.png" width="400"  />


### Code Examples:
Finding the _dot product_ of two arrays:

```python
import numpy as np
array1 = np.random.rand(1000)
array2 = np.random.rand(1000)

# not vectorized version
result=0
for i in range(len(array1)):
  result += array1[i] * array2[i]
# result: 244.4311

# vectorized version
v_result = np.dot(array1, array2)
# v_result: 244.4311
``` 

<details>
<summary>Applying exponential operation on every element of an array (or matrix)</summary>

```python
array = np.random.rand(1000)
exp = np.exp(array)
```
</details>

<details>
<summary>Vectorized version of sigmoid function</summary>

```python
array = np.random.rand(1000)
sigmoid = 1 / (1 + np.exp(-array))
```
</details>

### Common Supported Operations in Numpy
<details>
<summary>Common single array functions</summary>

* Taking the square root of each element in the array
  * `np.sqrt(x)`
* Taking the sum over all of the array's elements
  * `np.sum(x)`
* Taking the absolute value of each element in the array
  * `np.abs(x)`
* Applying **trigonometric** functions on each element in the array
  * `np.sin(x)`, `np.cos(x)`, `np.tan(x)`
* Applying **logarithmic** functions on each element in the array
  * `np.log(x)`, `np.log10(x)`, `np.log2(x)`

</details>

<details>
<summary>Common nultiple array functions</summary>

* Applying **arithmetic** operations on corresponded elements in the arrays
  * `np.add(x, y)`, `np.subtract(x, y)`, `np.divide(x, y)`, `np.multiply(x, y)`
* Applying **power** operation on corresponded elements in the arrays
  * `np.power(x, y)`

</details>

<details>
<summary>Common sequential functions</summary>

* Getting **mean** of an array
  * `np.mean(x)`
* Getting **median** of an array
  * `np.median(x)`
* Getting **variance** of an array
  * `np.var(x)`
* Getting **standart deviation** of an array
  * `np.std(x)`
* Getting **maximum or minimum** value of an array
  * `np.max(x)`, `np.min(x)`
* Getting **index** of maximum or minimum value of an array
  * `np.argmax(x)`, `np.argmin(x)`

</details>