# Practical Aspects of NN Impelemenation

## Things to think well before implementing NN
Number of layers, number of hidden units, learning rates, activation functions... 

It is too difficult to choose them all true at the first time so it is an iterative process

Idea ➡ Code ➡ Experiment ➡ Idea 🔁

> So the point here is how to go efficiently go around this cycle 🤔

## Train / Dev / Test Splitting
For good evaluation it is good to split dataset like the following:

| Part                         | Description                                                                |
| ---------------------------- | -------------------------------------------------------------------------- |
| Training Set                 |  Used to fit the model                                                     |
| Development (Validation) Set |  Used to provide an unbiased evaluation while tuning model hyperparameters |
| Test Set                     |  Used to provide an unbiased evaluation of a **final** model               |

### Training Set
The actual dataset that we use to train the model (weights and biases in the case of Neural Network). 

> The model **sees** and **learns** from this data 👶

### Validation (Development) Set
The sample of data used to provide an unbiased evaluation of a model fit on the training dataset while tuning model hyperparameters. The evaluation becomes more biased as skill on the validation dataset is incorporated into the model configuration.

> The model **sees** this data, but **never learns** from this 👨‍🚀

### Test Set
The sample of data used to provide an unbiased evaluation of a final model fit on the training dataset. It provides the gold standard used to evaluate the model.
**Implementation Note:** It should contain carefully sampled data that spans the various classes that the model would face, when used in the real world 🚩🚩🚩❗❗❗

> It is only used once a model is completely trained 👨‍🎓



## References
[About Train, Validation and Test Sets in Machine Learning](https://towardsdatascience.com/train-validation-and-test-sets-72cb40cba9e7)