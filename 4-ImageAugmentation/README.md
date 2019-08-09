# Image Augmentation
Basics of Image Augmentation :boom:

## Important Terms
| Term            | Description   |
| --------------- |---------------|
| Image Augmentation | Image Augmentation is a very simple, but very powerful tool to help you avoid overfitting your data |
| Rotation Range | A value in degrees (0–180), a range within which to randomly **rotate** pictures    |
| Height and Width Shifting |  Randomly shifts pictures vertically or horizontally |
| Shear Range | Randomly applying shearing transformations |
| Zoom Range | Randomly zooming inside pictures. |
| Horizontal Flip | Randomly flipping half of the images horizontally |
|  Fill Mode | A strategy used for filling in newly created pixels, which can appear after a rotation or a width/height shift. |

> Note: Image augmentation is needed for both training and test set :sweat_smile:

## Basic Concept of Image Augmentation

The concept is very simple though: If we have limited data, then the chances of you having data to match potential future predictions is also limited, and logically, the less data we have, the less chance we have of getting accurate predictions for data that our model hasn't yet seen.
> If we are training a model to spot cats, and our model has never seen what a cat looks like when lying down, it might not recognize that in future.

Augmentation simply amends our images on-the-fly while training using **transforms** like rotation. So, it could 'simulate' an image of a cat lying down by rotating a 'standing' cat by 90 degrees. As such we get a cheap :sparkles: way of extending our dataset beyond what we have already.

> Note: Doing image augmentation in runtime is preferred more than doing it on memory to keep original data as it is :thinking:

## TODO
- [ ] Adding codes of Image Augmentation

## References
* [More About Image Augmentation](https://github.com/keras-team/keras-preprocessing)
* [More About Image Pre-processing](https://keras.io/preprocessing/image/)