# ➰ Recurrent Neural Networks

## 🔎 Definition
A class of neural networks that allow previous outputs to be used as inputs to the next layers
> They remember things they learnt during training ✨

## 🧱 Structure

<img src="../res/RNNStructure.png" width="600"  />

## ⏩ Forward Propagation
**To find a<sup><<i>t</i>></sup>:**

<img src="../res/RNNForwardA.png" height="25"  />

**To find ŷ<sup><<i>t</i>></sup>:**

<img src="../res/RNNForwardY.png" height="25"  />

## ⏪ Back Propagation
**Loss Function is defined like the following**

<img src="../res/RNNOneLoss.png" height="25"  />

</br>

<img src="../res/RNNLoss.png" height="60"  />

## 🎨 Types of RNNs
- **One-to-One** (Traditional ANN)
- **One-to-Many** (Music Generation)
- **Many-to-One** (Semantic Analysis)
- **Many-to-Many** T<sub>x</sub> = T<sub>y</sub> (Speech Recognition)
- **Many-to-Many** T<sub>x</sub> != T<sub>y</sub> (Machine Translation)

<img src="../res/RNNTypes.png" width="600"  />

## ❌ Problem: Vanishing Gradients with RNNs
- An RNN that process a sequence data with the size of 10,000 time steps, has 10,000 deep layers which is very hard to optimize 🙄
- Same in Deep Neural Networks, deeper networks are getting into the vanishing gradient problem. 
- That also happens with RNNs with a long sequence size 🐛

### 🧙‍♀️ Solution
Adding _Gated Recurrent Unit_ 

### 🚪 Gated Recurrent Unit (GRU)
GRUs are improved version of standard recurrent neural network ✨, GRU uses _update gate and reset gate_ . 
- Basically, these are two vectors which decide what information should be passed to the output. 
- The special thing about them is that they can be trained to keep information from long ago
  - Without washing it through time or remove information which is irrelevant to the prediction.

| Gate           | Description                                 |
| -------------- |---------------------------------------------|
| 🔁 Update Gate | Helps the model to determine how much of the past information (from previous time steps) needs to be passed along to the future |
| 0️⃣ Reset Gate  | Helps the model to decide how much of the past information to **forget** |

#### 🔁 Update Gate
Given this gate the issue of the vanishing gradient is eliminated since the model on its own learn how much of the past information to pass to the future.
> In short: How much past should matter now? 🙄

#### 0️⃣ Reset Gate
This gate has the opposite functionality in comparison with the update gate since it is used by the model to decide how much of the past information to forget.
> In short: Drop previous information? 🙄

#### 💬 Current Memory Content
Memory content which will use the reset gate to store the relevant information from the past.

#### 🎈 Final Memory at Current Time Step
A vector which holds information for the current unit and it will pass it further down to the network.

#### 👀 Visualization 

<img src="../res/GRU.png" width="600"  />

### 🎉 GRU Conclusion
A solution to eliminate the vanishing gradient problem since the model is not washing out the new input every single time but keeps the relevant information and passes it down to the next time steps of the network


## 🧐 Read More
- [Recurrent Neural Networks Cheatsheet ✨](https://stanford.edu/~shervine/teaching/cs-230/cheatsheet-recurrent-neural-networks#)
- [What are RNNs and GRUs](https://towardsdatascience.com/what-is-a-recurrent-nns-and-gated-recurrent-unit-grus-ea71d2a05a69)
- [Understanding GRU Networks](https://towardsdatascience.com/understanding-gru-networks-2ef37df6c9be)
