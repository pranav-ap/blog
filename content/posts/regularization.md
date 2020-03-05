---
title: "Regularization"
date: "2020-1-9"
template: "post"
draft: false
slug: "/posts/regularization/"
category: "Deep Learning"
tags:
   - ""
description: ""
---

Consider a polynomial regression model. As you keep increasing its degree $M$, there will be a point when it stops generalizing and starts overfitting to the training set.

<figure style="width: 700px">
	<img src="/media/deep learning/increasing-model-flexibility.png" alt="Increasing Polynomial Model Flexibility">
	<figcaption>Increasing Polynomial Model Flexibility</figcaption>
</figure>

If you examine the coefficients of the model, you will find that they increase in magnitude as $M$ increases. So, in order to reduce overfitting the magnitude of these weights must be controlled.

**Regularization** is a family of methods that help learn small weights to prevent overfitting. Some of these methods include

- Early Stopping
- **L1** Regularization
- **L2** Regularization

**L1** and **L2** regularization are explicit methods that directly reduce the representational capacity of a neural net by adding a penalty term to the loss function. Implicit methods like early stopping reduce overfitting indirectly.

# Early Stopping

Early stopping is a widely used form of regularization, as it is both simple and effective.

During backprop, the model is evaluated on a validation set after each epoch. If the loss begins to increase, then the training process is stopped. This is called **early stopping**.

But the performance of a model on a validation set may swing up and down many times during training. This means that the first sign of overfitting may not be a good place to stop training. More elaborate triggers may be required in practice.

Multiple evaluations on a validation set adds an additional computational cost during training. This can be reduced by evaluating the model less frequently.

The number of epochs after which to test the model on the validation set is called **patience**.

<figure style="width: 600px">
	<img src="/media/deep learning/early stopping.png" alt="Early Stopping">
	<figcaption>Early Stopping</figcaption>
</figure>

Every time the error on the validation set improves, we store a copy of the model parameters. When the training algorithm terminates, we return these parameters, rather than the latest parameters.

<figure style="width: 700px">
	<img src="/media/deep learning/early-stopping-1.png" alt="Early Stopping">
	<figcaption>Early Stopping</figcaption>
</figure>

There is no way to predict how many epochs it will take for overfitting to start. So, keep an eye on the graph while training the model.

# L1 Regularization

**L1** Regularization adds a penalty term to the loss function to discourage the coefficients from holding large values. The penalty is simply the *sum of all coefficients*,

$$
\lambda \sum^n_{i = 1} \mid \theta_i \mid
$$

The modified form of the *MSE* loss function is,

$$
J (\theta)
=
\frac {1} {2 n} ( \bold{y} - \bold{a}^{(3)})^2
+
\lambda \sum^n_{i = 1} \mid \theta_i \mid
$$

where $\theta$ represents all the weights, and $\lambda$ governs the degree to which we penalize large parameters. $\lambda$ in effect controls the capacity of the network. It is called the **regularization parameter**.

If the weights $\theta$ are large, then $\lambda \sum^n_{i = 1} \mid \theta_i \mid$ will also be large, which leads to a large loss $J (\theta)$.

When gradient descent uses **L1** regularization, it tends to reduce unimportant weights to $0$, completely removing some inputs of some neurons.

This makes **L1** useful when you have many features that for feature selection.

# L2 Regularization

**L2** Regularization is the most common form of regularization. It adds a penalty term to the loss function to discourage the coefficients from holding large values. This is also called **weight decay**.

The penalty is simply the *sum of squares all coefficients*,

$$
\lambda \sum^n_{i = 1} \theta_i^2
$$

The modified form of the *MSE* loss function is,

$$
J (\theta)
=
\frac {1} {2 n} ( \bold{y} - \bold{a}^{(3)})^2
+
\lambda \sum^n_{i = 1} \theta_i^2
$$

where $\lambda$ governs the degree to which we penalize large parameters, and $\theta$ represents all the weights.

It encourages the neurons to use all of their inputs a little rather than some of its inputs a lot. It doesn't tend to push less important weights to zero and typically produces better results when training a model.

# Dropout

In dropout, we randomly ignore a subset of nodes *including* their incoming and outgoing links from the input and hidden layers for each epoch during backprop.

Ignoring some nodes results in a smaller network which reduces capacity. This in turn reduces chances of overfitting.

It also prevents the network from relying on a small segment of nodes for its task. It forces nodes within a layer to take on more responsibility for the inputs, making the network more robust.

For an epoch, each node is retained with a probability $p$ independent of other units. It can be chosen using a validation set or can simply be a fixed value. A common value for $p$ for nodes in hidden layers is around $0.5$ and for input nodes, it is closer to $1$.

<figure style="width: 560px">
	<img src="/media/deep learning/dropout.png" alt="Dropout">
	<figcaption>Dropout</figcaption>
</figure>

Due to dropout, the architecture of the network is different for every epoch.

A neural net with $n$ nodes can be seen as a collection of $2^n$ possible thinned neural networks with different architectures. Dropout approximates training a large number of neural networks with different architectures in parallel.

# References

- [Wikipedia: Early stopping](https://en.wikipedia.org/wiki/Early_stopping)
- [A Gentle Introduction to Early Stopping to Avoid Overtraining Neural Networks](https://machinelearningmastery.com/early-stopping-to-avoid-overtraining-neural-network-models/)
- [Use Weight Regularization to Reduce Overfitting of Deep Learning Models](https://machinelearningmastery.com/weight-regularization-to-reduce-overfitting-of-deep-learning-models/)
- [Dropout Paper](https://www.cs.toronto.edu/~hinton/absps/JMLRdropout.pdf)