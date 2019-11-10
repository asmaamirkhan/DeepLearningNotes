# 📚 Concepts of Artificial Neural Networks

Basic Concepts of ANN

## 🍭 Basic Neural Network

<img src="../res/BasicANN.png" width="300"  />

> **Convention:** The NN in the image called to be a 2-layers NN since input layer is not being counted 📢❗

## 📚 Common Terms

| Term             | Description   |
| ---------------  |---------------|
| Input Layer      |  A layer that conatains the inputs to the NN |
| Hidden Layer     |  The layer(s) where computational operations are being done |
| Output Layer     |  The final layer of the NN and it is responsible for generating the predicted value ŷ |
| Neuron           |  A placeholder for a mathematical function, it applies a function on inputs and provides an output |
| Activation Function | A function that converts an input signal of a node to an output signal by applying some transformation |
| Shallow NN       |  NN with few number of hidden layers (one or two)  |
| Deep NN          |  NN with large number of hidden layers |
| n<sup>[l]</sup>  |  Number of units in _l_ layer |


## 🧠 What does an artificial neuron do?
It calculates a _weighted sum_ of its input, adds a bias and then decides whether it should be _fired_ or not due to an activaiton function
> My detailed notes on activaiton functions are [here](https://github.com/asmaamirkhan/DeepLearningNotes/tree/master/6-NNConcepts/3-ActivationFunctions.md) 👩‍🏫




## 👩‍🔧 Parameters Dimension Control

| Parameter        | Dimension     |
| ---------------  |---------------|
| w<sup>[<i>l</i>]</sup>   |  (n<sup>[<i>l</i>]</sup>,n<sup>[<i>l-1</i>]</sup>) |
| b<sup>[<i>l</i>]</sup>   |  (n<sup>[<i>l</i>]</sup>,1) |
| dw<sup>[<i>l</i>]</sup>  |  (n<sup>[<i>l</i>]</sup>,n<sup>[<i>l-1</i>]</sup>) |
| db<sup>[<i>l</i>]</sup>  |  (n<sup>[<i>l</i>]</sup>,1) |


> Making sure that these dimensions are true help us to write better and bug-free :bug: codes

## 🎈 Summary of Forward Propagation Process

|                  |                 |
| ---------------- | --------------- |
| **Input:**       |  a<sup>[<i>l</i>-1]</sup> |
| **Output:**      |  a<sup>[<i>l</i>]</sup>, chache (z<sup>[<i>l</i>]</sup>) |

**Vectorized Equations:**

<img src="../res/formulas/ForwardProp.png" height="80"  />

## 🎈 Summary of Back Propagation Process

|                  |                 |
| ---------------- | --------------- |
| **Input:**       |  da<sup>[<i>l</i>]</sup> |
| **Output:**      | da<sup>[<i>l</i>-1]</sup>, dW<sup>[<i>l</i>]</sup>, db<sup>[<i>l</i>]</sup> |

**Vectorized Equations:**

<img src="../res/formulas/BackProp1.png" height="30"  />
<br>
<img src="../res/formulas/BackProp2.png" height="50"  />
<br>
<img src="../res/formulas/BackProp3.png" height="50"  />
<br>
<img src="../res/formulas/BackProp4.png" height="30"  />

## ➰➰ To Put Forward Prop. and Back Prop. Together

<img src="../res/ForBackSummary.png" width="500"  />

> 😵🤕

## ✨ Parameters vs Hyperparameters

**Parameters:**
* W<sup>[<i>1</i>]</sup>, W<sup>[<i>2</i>]</sup>, W<sup>[<i>3</i>]</sup>
* b<sup>[<i>1</i>]</sup>, b<sup>[<i>2</i>]</sup>
* ......


**Hyperparameters:**

* Learning rate
* Number of iterations
* Number of hidden layers
* Number of hidden units
* Choice of activation function
* ......

> We can say that hyperparameters control parameters 🤔