# Introduction to Convolutional Neural Networks
Improving Neural Networks used in Computer Vision problems

## Important Terms
| Term            | Description   |
| --------------- |---------------|
| Convolutoin     | Applying some filter on an image so certain features in the image get emphasized |
| Pooling         | A way of compressing an image  |
| 2*2 max pooling | For every 4 neighbor pixels the biggest one will survive |

## Convolution Examples
<img src="https://github.com/asmaamirkhan/TensorflowGuide/blob/master/res/ConvolutionExH.JPG" width="450"  />

> Result: horizontal lines pop out

<img src="https://github.com/asmaamirkhan/TensorflowGuide/blob/master/res/ConvolutionExV.JPG" width="450"  />

> Result: vertical lines pop out

## Notes on performance :dizzy:
* Training speed of a CNN is too slower than plain NN because of its computational complexity :turtle:

## Better CNN Understanding

We can get info about our CNN by 
```python
model.summary()
``` 

And the output will be like:
``` 
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

For code in the notebook:
> [Here](https://github.com/asmaamirkhan/DeepLearningNotes/blob/master/2-Intro2CNN/0-CNN.ipynb) :feet:

* The orginal dimensions of the images were 28x28 px
* 1st layer: The filter can not be applied on the pixels on the edges 
  * The output from first layer has 26x26 px
* 2nd layer: After applying `2x2 max pooling` the dimensions will be divided by 2
  * The output from this layer has 13x13 px
* 3rd layer: The filter can not be applied on the pixels on the edges 
  * The output from first layer has 11x11 px
* 4th layer: After applying `2x2 max pooling` the dimensions will be divided by 2
  * The output from this layer has 5x5 px
* 5th layer: The output of the previous layer will be flattened
  * The output from this layer has `5x5x64=1600` neurons
* 6th layer: We set it to contain 128 neurons
* 7th layer: Since we have 10 categories it consists of 10 neurons

> :dizzy_face: :dizzy_face:

## Visualization
The visualization of the output of each layer is available [here](https://github.com/asmaamirkhan/DeepLearningNotes/blob/master/2-Intro2CNN/1-CNNVisualization.ipynb) :mag:

## References
* [More on Convolutional Neural Networks](https://www.youtube.com/playlist?list=PLkDaE6sCZn6Gl29AoE31iwdVwSG-KnDzF)
