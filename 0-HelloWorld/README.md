# Hello World of Deep Learning with Neural Networks
Like every first app we should start with something super simple that gives us an idea about the whole methodology. 

## What is Keras?
Keras is a high-level **neural networks API**, written in Python and capable of running on top of TensorFlow, CNTK, or Theano.

## Important Terms
| Term            | Description   |
| --------------- |---------------|
| Dense           | A layer of neurons in a neural network      |
| Loass Function  | A mathematical way of measuring how wrong your predictions are |
| Optimizer       | An algorithm to find parameter values which correspond to minimum value of loss function |

## The Simplest Neural Network
It contains one hidden layer with one neuron.

Code example:
```python
# initialize the model
model = Sequential()

# add a layer with one unit and set the dimension of input 
model.add(Dense(units=1, input_shape=[1]))

# set functional properties and compile the model
model.compile(optimizer='sgd', loss='mean_squared_error')
```

After building out neural network we can feed it with our sample data.

Code example:

```python
xs = np.array([-1.0,  0.0, 1.0, 2.0, 3.0, 4.0], dtype=float)
ys = np.array([-3.0, -1.0, 1.0, 3.0, 5.0, 7.0], dtype=float)
```
Then we have to start training process.

Code example:
```python
model.fit(xs, ys, epochs=500)
```
Every thing is done :sunglasses: ! Now we can test our neural network with new data.

Code example:
```python
print(model.predict([10.0]))
```

## Traditional Programming vs Machine Learning
<img src="https://github.com/asmaamirkhan/TensorflowGuide/blob/master/res/TraditionalProgvsML.JPG" width="350"  />

## References
* [Official Documentation of Keras](https://keras.io/)
* [More About Sequential model](https://keras.io/getting-started/sequential-model-guide/)
* [More About Optimizers in Keras](https://keras.io/optimizers/)
* [More About Loss Functions in Keras](https://keras.io/losses/)
