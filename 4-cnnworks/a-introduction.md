---
description: "\U0001F526 Convolutional Neural Networks Codes"
---

# 🌱 Introduction

This section will be filled by codes and notes gradually

## 👩‍💻 Codes

1. [👶 Basic CNNs](https://github.com/asmaamirkhan/DeepLearningNotes/tree/8e6115ccd68cd00bb957c3c9aca2ea6b7e818822/4-CNNWorks/0-CNN.ipynb)
2. [👀 CNN Visualization](https://github.com/asmaamirkhan/DeepLearningNotes/tree/8e6115ccd68cd00bb957c3c9aca2ea6b7e818822/4-CNNWorks/1-CNNVisualization.ipynb)
3. [👨‍👩‍👧‍👧 Human vs Horse Classifier with CNN](https://github.com/asmaamirkhan/DeepLearningNotes/tree/8e6115ccd68cd00bb957c3c9aca2ea6b7e818822/4-CNNWorks/2-HorseHumanClassifier.ipynb)
4. [🐱 Dog vs Cat Classifier with CNN](https://github.com/asmaamirkhan/DeepLearningNotes/tree/8e6115ccd68cd00bb957c3c9aca2ea6b7e818822/4-CNNWorks/3-DogCatClassifier.ipynb) 
5. [🎨 Multi-Class Classification](https://github.com/asmaamirkhan/DeepLearningNotes/tree/8e6115ccd68cd00bb957c3c9aca2ea6b7e818822/4-CNNWorks/4-MultiClassRPS.ipynb)
6. 🌐 Tensorflow.js based hand written digit recognizer
   1. [`Classifier.js`](https://github.com/asmaamirkhan/DeepLearningNotes/tree/8e6115ccd68cd00bb957c3c9aca2ea6b7e818822/4-CNNWorks/HandDigitClassifier/classifier.js)
   2. [`MNISTData.js`](https://github.com/asmaamirkhan/DeepLearningNotes/tree/8e6115ccd68cd00bb957c3c9aca2ea6b7e818822/4-CNNWorks/HandDigitClassifier/MNISTData.js)
   3. [`index.html`](https://github.com/asmaamirkhan/DeepLearningNotes/tree/8e6115ccd68cd00bb957c3c9aca2ea6b7e818822/4-CNNWorks/HandDigitClassifier/index.html)

## ✋ RPS Dataset

* Rock Paper Scissors is an available dataset containing 2,892 images of diverse hands in Rock/Paper/Scissors poses.
* Rock Paper Scissors contains images from a variety of different hands, from different races, ages and genders, posed into Rock / Paper or Scissors and labelled as such.

> 🔎 All of this data is posed against a white background. Each image is 300×300 pixels in 24-bit color

## 🐛 CNN Debugging

We can get info about our CNN by

```python
model.summary()
```

And the output will be like:

```text
Layer (type)                 Output Shape              Param #   
=================================================================
conv2d_18 (Conv2D)           (None, 26, 26, 64)        640       
_________________________________________________________________
max_pooling2d_18 (MaxPooling (None, 13, 13, 64)        0         
_________________________________________________________________
conv2d_19 (Conv2D)           (None, 11, 11, 64)        36928     
_________________________________________________________________
max_pooling2d_19 (MaxPooling (None, 5, 5, 64)          0         
_________________________________________________________________
flatten_9 (Flatten)          (None, 1600)              0         
_________________________________________________________________
dense_14 (Dense)             (None, 128)               204928    
_________________________________________________________________
dense_15 (Dense)             (None, 10)                1290      
=================================================================
```

👩‍💻 For code in the notebook:

> [Here](https://github.com/asmaamirkhan/DeepLearningNotes/tree/8e6115ccd68cd00bb957c3c9aca2ea6b7e818822/4-CNNWorks/0-CNN.ipynb) 🐾

* 🔎 The original dimensions of the images were 28x28 px
* 1️⃣ 1st layer: The filter can not be applied on the pixels on the edges 
  * The output of first layer has 26x26 px
* 2️⃣ 2nd layer: After applying `2x2 max pooling` the dimensions will be divided by 2
  * The output of this layer has 13x13 px
* 3️⃣ 3rd layer: The filter can not be applied on the pixels on the edges 
  * The output of this layer has 11x11 px
* 4️⃣ 4th layer: After applying `2x2 max pooling` the dimensions will be divided by 2
  * The output of this layer has 5x5 px
* 5️⃣ 5th layer: The output of the previous layer will be flattened
  * This layer has `5x5x64=1600` units
* 6️⃣ 6th layer: We set it to contain 128 units
* 7️⃣ 7th layer: Since we have 10 categories it consists of 10 units

> 😵 😵

## 👀 Visualization

The visualization of the output of each layer is available [here](https://github.com/asmaamirkhan/DeepLearningNotes/tree/8e6115ccd68cd00bb957c3c9aca2ea6b7e818822/4-CNNWorks/1-CNNVisualization.ipynb) 🔎

## 👷‍♀️ Network Visualization Tool

[Netron ✨✨](https://github.com/lutzroeder/netron)

## 🧐 References

* [Binary Cross-Entropy](https://gombru.github.io/2018/05/23/cross_entropy_loss/)
* [RMSProp Explained](http://www.cs.toronto.edu/~tijmen/csc321/slides/lecture_slides_lec6.pdf)
* [RMSProp in Tensorflow](https://www.tensorflow.org/api_docs/python/tf/train/RMSPropOptimizer)
* [Binary Classification](https://www.youtube.com/watch?v=eqEc66RFY0I&t=6s)
* [TensorFlow: an ML platform for solving impactful and challenging problems](https://www.youtube.com/watch?v=NlpS-DhayQA)
* [Rock Paper Scissors Dataset](http://www.laurencemoroney.com/rock-paper-scissors-dataset/)

