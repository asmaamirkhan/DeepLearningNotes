# Notes on Applied Machine Learning

## Orthogonalisation
One of the challenges with building machine learning systems is that there are so many things we could try. Including, for example, so many hyperparameters we could tune. **The art of knowing what parameter to tune to get what effect, is called orthogonalisation**.

What should we pay attention to while evaluating an ML project? How to optimize it? How to speed up? Since there are a lot of parameters how to know where to fix and which parameter to tune? 🤔🤕

Before answering these question let's take a look at the whole process 🧐

## Chain of assumptions in ML
**The model should:**

Fit **training** set well on cost function  (Human level performance ❌❌)

⬇

Fit **dev** set well on cost function 

⬇

Fit **test** set well on cost function 

⬇

Perform well in **real world** ✨

> Figuring out what is exactly wrong can help us to choose a suitable solution and then to fix that part without affecting the whole project  👩‍🔧

## Table of Contents
0. [Notes on Evalution](0-Evaluation.md)