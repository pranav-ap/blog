---
title: "Regularization"
date: "2019-12-30"
template: "post"
draft: false
slug: "/posts/regularization/"
category: "Deep Learning"
tags:
   - ""
description: ""
---

**Regularization** is the process of modifying a learning algorithm to prevent overfitting.

# Early Stopping

Early stopping is probably the most commonly used form of regularization in deep learning. Its popularity is due to both effectiveness and simplicity.

Methods such as gradient descent reduce the training error with each iteration. *Too little* training produces a model that will underfit both the *training* and *test* sets. *Too much* training will mean that the model will overfit the training dataset and have poor performance on the test set.

<figure style="width: 550px">
	<img src="/media/deep learning/early-stopping.png" alt="Early Stopping">
	<figcaption>Early Stopping</figcaption>
</figure>

Here, we train the model on the training set as we always do, but stop training when performance on the *validation* set starts to degrade. This method is called **early stopping**.

It is common to use about 30% of the training set as a validation dataset. This is used to monitor performance of the model during training. The validation set is not used to train the model.

Performance of the model is evaluated on the validation set at the end of each epoch. This adds an additional computational cost during training. This can be reduced by evaluating the model less frequently.

Every time the error on the validation set improves, we store a copy of the model parameters. When the training algorithm terminates, we return these parameters, rather than the latest parameters.

<figure style="width: 700px">
	<img src="/media/deep learning/early-stopping-1.png" alt="Early Stopping">
	<figcaption>Early Stopping</figcaption>
</figure>

Note that the performance of a model on a validation set may go up and down many times. This means that the first sign of overfitting may not be a good place to stop training.

There is no way to predict how many epochs it will take for overfitting to start. So it is important to keep an eye on the graph while training the model.

# L1 Regularization

This expression is commonly used for feature selection as it tends to produce sparse parameter vectors where only the important features take on non-zero values.

# L2 Regularization

This expression doesn't tend to push less important weights to zero and typically produces better results when training a model.

# References

- [Michael Nielsen](http://neuralnetworksanddeeplearning.com)
- [Wikipedia: Feedforward neural network](https://en.wikipedia.org/wiki/Feedforward_neural_network)
- [Wikipedia: Multilayer perceptron](https://en.wikipedia.org/wiki/Multilayer_perceptron)
- [Wikipedia: Early stopping](https://en.wikipedia.org/wiki/Early_stopping)
- [Wikipedia: Artificial neural network](https://en.wikipedia.org/wiki/Artificial_neural_network)
- [A Gentle Introduction to Early Stopping to Avoid Overtraining Neural Networks](https://machinelearningmastery.com/early-stopping-to-avoid-overtraining-neural-network-models/)