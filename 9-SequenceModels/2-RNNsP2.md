# 🔥 Advanced Recurrent Neural Networks

## 🔄 Bidirectional RNNs (BRNN)
- In many applications we want to output a prediction of y (t) which may depend on the whole input sequence
- Bidirectional RNNs combine an RNN that moves **forward** through time beginning from the start of the sequence with another RNN that moves **backward** through time beginning from the end of the sequence ✨

### 💬 In Other Words
- Bidirectional recurrent neural networks(RNN) are really just putting two independent RNNs together. 
- The input sequence is fed in normal time order for one network, and in reverse time order for another. 
- The outputs of the two networks are usually concatenated at each time step.
- 🎉 This structure allows the networks to have both backward and forward information about the sequence at every time step. 

### 👎 Disadvantages
We need the entire sequence of data efore you can make prediction anywhere.

>e.g: not suitable for real time speach recognition 

### 👀 Visualization

<img src="../res/BRNN.png" width="600"  />


## 🕸 Deep RNNs
The computation in most RNNs can be decomposed into three blocks of parameters and associated transformations:
1. From the input to the hidden state, x(t) ➡ a(t)
2. From the previous hidden state to the next hidden state, a(t-1) ➡ a(t)
3. From the hidden state to the output, a(t) ➡ y(t)

We can use multiple layers for each of the above transformations, which results in deep recurrent networks 😋

### 👀 Visualization

<img src="../res/DeepRNN.png" width="600"  />