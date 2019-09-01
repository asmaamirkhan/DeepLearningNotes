# Optimization Algorithms
Having fast and good optimization algorithms can speed up the efficiency of the whole work ✨

## Batch Gradient Descent
In batch gradient we use the **entire** dataset to compute the gradient of the cost function for each iteration of the gradient descent and then update the weights.

* Since we use the entire dataset to compute the gradient convergence is slow.

### Stochastic Gradient Descent (SGD)
In stochastic gradient descent we use a single datapoint or example to calculate the gradient and update the weights with **every** iteration, we first need to shuffle the dataset so that we get a completely randomized dataset.

Random sample helps to arrive at a global minima and avoids getting stuck at a local minima.

* Learning is much faster and convergence is quick for a very large dataset.

### Mini Batch Gradient Descent
Mini-batch gradient is a variation of stochastic gradient descent where instead of single training example, mini-batch of samples is used.
Mini batch gradient descent is widely used and converges faster and is more stable.
Batch size can vary depending on the dataset.

> 1 ≤ batch-size ≤ m

### Comparison

* Very large batch-size (m or close to m): 
  * Too long per iteration
* Very small batch-size (1 or close to 1)
  * losing speed up of vectorization
* batch-size not too large/small
  * We can do vectorization
  * Good speed per iteration
  * The fastest learning 🤗✨   

### Guidlines for Choosing Batch-Size
* For a small (m ≤ 2000) dataset ➡ use batch gradient descent
* Typical mini batch-size: 64, 128, 256, 512, up to 1024
* Make sure mini batch-size fits in your CPU/GPU memory 

> It is better(faster) to choose mini batch size as a power of 2 (due to memory issues) 🧐


## References
* [Machine learning Gradient Descent](https://medium.com/datadriveninvestor/gradient-descent-5a13f385d403)