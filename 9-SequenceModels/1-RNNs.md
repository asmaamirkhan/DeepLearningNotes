# ➰ Recurrent Neural Networks

## 🔎 Definition
A class of neural networks that allow previous outputs to be used as inputs to the next layers
> They remember things they learnt during training ✨

## 🧱 Architecture

### 🔶 The Whole RNN Architecture
<img src="../res/RNNStructure2.png" width="600"  />

<img src="../res/RNNStructure.png" width="600"  />

### 🧩 An RNN Cell

<img src="../res/RNNCell.png" width="600"  />

Basic RNN cell. Takes as input x⟨t⟩ (current input) and a<sup>⟨t−1⟩</sup> (previous hidden state containing information from the past), and outputs a<sup>⟨t⟩</sup> which is given to the next RNN cell and also used to predict y<sup>⟨t⟩</sup>

## ⏩ Forward Propagation
**To find a<sup><<i>t</i>></sup>:**

<img src="../res/RNNForwardA.png" height="25"  />

**To find ŷ<sup><<i>t</i>></sup>:**

<img src="../res/RNNForwardY.png" height="25"  />

### 👀 Visualization

<img src="../res/RNNForwardVis.png" width="600"  />

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

### 🧙‍♀️ Solutions
- **GRU** _Gated Recurrent Unit_ 
- **LSTM** _Long Short-Term Memory_ 

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
- A solution to eliminate the **vanishing gradient** problem 
- The model is not washing out the new input every single time but keeps the relevant information and passes it down to the next time steps of the network.

### 🤸‍♀️ Long Short-Term Memory

#### 0️⃣ Forget Gate
- Let's assume we are reading words in a piece of text, and want use an LSTM to keep track of grammatical structures, such as whether the subject is singular or plural. 
- If the subject changes from a singular word to a plural word, we need to find a way to get rid of our previously stored memory value of the singular/plural state. 
- In an LSTM, the forget gate let's us do this:

<img src="../res/ForgetGate.png" width="300"  />

- Here,  W<sub>f</sub>  are weights that govern the forget gate's behavior. We concatenate  [a<sup>⟨t−1⟩</sup>,x<sup>⟨t⟩</sup>]  and multiply by  W<sub>f</sub>. The equation above results in a vector  Γ<sub><i>f</i></sub><sup>⟨t⟩</sup>  with values between 0 and 1. 
- This forget gate vector will be multiplied element-wise by the previous cell state c<sup>⟨t−1⟩</sup> . 
- So if one of the values of Γ<sub><i>f</i></sub><sup>⟨t⟩</sup> is 0 (or close to 0) then it means that the LSTM should remove that piece of information (e.g. the singular subject) in the corresponding component of  c<sup>⟨t−1⟩</sup> . 
- If one of the values is 1, then it will keep the information.

#### 🔄 Update Gate
Once we forget that the subject being discussed is singular, we need to find a way to update it to reflect that the new subject is now plural. Here is the formula for the update gate:

<img src="../res/UpdateGate.png" width="300"  />

Similar to the forget gate, here  Γ<sub><i>u</i></sub><sup>⟨t⟩</sup>  is again a vector of values between 0 and 1. This will be multiplied element-wise with  c̃<sup>⟨t⟩</sup>, in order to compute c<sup>⟨t⟩</sup>.

#### 👩‍🔧 Updating the Cell
To update the new subject we need to create a new vector of numbers that we can add to our previous cell state. The equation we use is:

<img src="../res/StateUpdate.png" width="300"  />

Finally, the new cell state is:

<img src="../res/NextState.png" width="300"  />

#### 🚪 Output Gate
To decide which outputs we will use, we will use the following two formulas:

<img src="../res/OutputGate1.png" width="300"  />

<img src="../res/OutputGate2.png" width="300"  />

Where in equation 5 you decide what to output using a sigmoid function and in equation 6 you multiply that by the _tanh_ of the previous state.

<img src="../res/RNNLSTM.png" width="600"  />

> GRU is newer than LSTM, LSTM is more powerful but GRU is easier to implement 🚧

## 🧐 Read More
- [Recurrent Neural Networks Cheatsheet ✨](https://stanford.edu/~shervine/teaching/cs-230/cheatsheet-recurrent-neural-networks#)
- [What are RNNs and GRUs](https://towardsdatascience.com/what-is-a-recurrent-nns-and-gated-recurrent-unit-grus-ea71d2a05a69)
- [Understanding GRU Networks](https://towardsdatascience.com/understanding-gru-networks-2ef37df6c9be)
- [Detailed LSTM](http://colah.github.io/posts/2015-08-Understanding-LSTMs/)
- [All About RNNs 🚀](https://medium.com/@jianqiangma/all-about-recurrent-neural-networks-9e5ae2936f6e)