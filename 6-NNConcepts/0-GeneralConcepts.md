# The Problem in General 
Given a dataset like:

{(x<sup>(1)</sup>, y<sup>(1)</sup>), (x<sup>(2)</sup>, y<sup>(2)</sup>), (x<sup>(m)</sup>, y<sup>(m)</sup>)}

We want:

ŷ<sup>(i)</sup> ≈ y

## Basic Concepts and Notations

| Concept         | Description   |
| --------------- |---------------|
| `m`             | Number of examples in dataset |
| x<sup>(i)</sup> | `i`th example in the dataset  |
| `ŷ`             | Predicted output |
| Loss Function `𝓛(ŷ, y)` | A function to compute the error for a **single** training example |
| Cost Gunction `𝙹(w, b)` | The average of the loss functions of the **entire** training set  |
| Convex Function | A function that has one local value |
| Non-Convex Function | A function that has lots of different local values |
| Gradient Descent | An iterative optimization method that we use to converge to the global optimum of `Cost Function` |

> In other words: The `Cost Function` measures how well our parameters `w` and `b` are doing on the training set, so the best `w` and `b` are the values that minimize `𝙹(w, b)` as possible

## Gradient Descent
General Formula:
<p float="left">
    <img src="https://github.com/asmaamirkhan/TensorflowGuide/blob/master/res/GradientDescentW.png" width="400"  />
    <img src="https://github.com/asmaamirkhan/TensorflowGuide/blob/master/res/GradientDescentB.png" width="400"  />
</p>

> `α` _(alpha)_ is the **Learning Rate** which is a positive scalar determining the size of the step of each iteration of gradient descent due to the corresponded estimated error each time the model weights are updated, so, it controls how quickly or slowly a neural network model learns a problem

## References
* [Introduction to Artificial Neural Networks (ANN)](https://searchenterpriseai.techtarget.com/definition/neural-network)
* [More on Learning Rate](https://machinelearningmastery.com/learning-rate-for-deep-learning-neural-networks/)