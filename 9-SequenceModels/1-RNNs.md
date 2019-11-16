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

