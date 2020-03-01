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

When training a neural net with high capacity, there will be a point when it stops generalizing and starts overfitting to the training set.

**Regularization** is a family of methods to prevent overfitting. Some of these methods include

- Early Stopping
- **L1** Regularization
- **L2** Regularization

**L1** and **L2** regularization are explicit methods that directly reduce the representational capacity of a neural net by adding a penalty term to the loss function. Implicit methods reduce overfitting indirectly.

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

This expression is commonly used for feature selection as it tends to produce sparse parameter vectors where Only the important features take on non-zero values.

When gradient descent uses **L1** regularization, it tends to reduce unimportant weights to $0$, completely removing some inputs to a neuron.


Lasso shrinks the less important feature’s coefficient to zero thus, removing some feature altogether. So, this works well for feature selection in case we have a huge number of features.

In other words, neurons with **L1** regularization end up using only a sparse subset of their most important inputs and become nearly invariant to the “noisy” inputs. In comparison, final weight vectors from **L2** regularization are usually diffuse, small numbers. In practice, if you are not concerned with explicit feature selection, **L2** regularization can be expected to give superior performance over **L1**.

# L2 Regularization

**L2** Regularization is the most common form of regularization. It adds a penalty term to the loss function to discourage the coefficients from holding large values. The penalty is simply the *sum of squares all coefficients*,

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

It encourages the network to use all of its inputs a little rather than some of its inputs a lot.

This expression doesn't tend to push less important weights to zero and typically produces better results when training a model.

Max norm constraints. Another form of regularization is to enforce an absolute upper bound on the magnitude of the weight vector for every neuron and use projected gradient descent to enforce the constraint. In practice, this corresponds to performing the parameter update as normal, and then enforcing the constraint by clamping the weight vector w⃗  of every neuron to satisfy ∥w⃗ ∥2<c. Typical values of c are on orders of 3 or 4. Some people report improvements when using this form of regularization. One of its appealing properties is that network cannot “explode” even when the learning rates are set too high because the updates are always bounded.

# Dropout

<figure style="width: 580px">
	<img src="/media/deep learning/dropout.png" alt="Dropout">
	<figcaption>Dropout</figcaption>
</figure>


# References

- [Wikipedia: Early stopping](https://en.wikipedia.org/wiki/Early_stopping)
- [A Gentle Introduction to Early Stopping to Avoid Overtraining Neural Networks](https://machinelearningmastery.com/early-stopping-to-avoid-overtraining-neural-network-models/)