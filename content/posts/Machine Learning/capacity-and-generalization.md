---
title: "Capacity and Generalization"
date: "2020-6-22"
template: "post"
draft: false
slug: "/posts/capacity-and-generalization/"
category: "Machine Learning"
tags:
- ""
description: ""
---

A **statistical model** is a function $f$ consisting of a set of adjustable parameters that maps the relationship between *input variables* or **predictors** to an *output variable* or a **response**. Finding the function $f$ and the values for its parameters is known as **learning**.

The response is denoted by $Y$, and the set of $p$ predictors $\lbrace X_1, X_2, ... , X_p\rbrace$ are denoted by $X$. The true relationship $f$ between $Y$ and $X$ in the most general form is written as:

$$
Y = f(X) + \epsilon
$$

Here $f$ is the true and unknown function we need to find. It encodes systematic information about the relationship between $X$ and $Y$. For example, it states whether the relationship is linear, polynomial or exponential.

<figure style="width: 900px">
	<img src="/media/machine learning/basics/learning model.svg" alt="Learning Model">
	<figcaption>Learning Model</figcaption>
</figure>

# Table of Contents

- Errors in Estimation
- Capacity and Generalization
	- Flexibility and MSE
	- Bias-Variance Tradeoff
	- Bias-Variance Decomposition

# Errors in Estimation

The true relationship $f$ cannot be known even if we have a huge dataset. We can only *estimate* the relationship. It is denoted by $\hat{f}$.

$$
\hat{Y} = \hat{f}(X) + \epsilon
$$

The accuracy of $\hat{Y}$ as a estimation of $Y$ depends on two quantities: *reducible error* and *irreducible error*.

Some learning methods ask us to assume the general functional shape of the relationship $f$. Our assumption could be incorrect but can potentially be improved. Thus it is known as a **reducible error**.

Even if our assumption is fairly close to the truth, our model will still have some inaccuracies. This could be because we missed out some useful predictors or due to unmeasured variation and dependencies in predictors already considered by $\hat{f}$. It is denoted by $\epsilon$ and is called the **irreducible error**.

The irreducible error will always provide an upper bound to the accuracy of our predictions.

# Capacity and Generalization

The ability to perform well on previously unseen inputs is called **generalization**. The need to have a low generalization error or test error is the difference between machine learning and optimization.

A good model accurately *captures the regularities* in its training data and also *generalizes well* to unseen data. An important hurdle in achieving this is finding the appropriate model flexibility.

<figure style="width: 600px">
	<img src="/media/machine learning/basics/flexibility.png" alt="Flexibility">
	<figcaption>Flexibility</figcaption>
</figure>

When a model is highly flexible, it hugs the data points very tightly. This makes it a good representation of the training dataset. But it does not generalize well to unseen inputs. This is because they are fitting the fringe and noisy data points too. This error is called **overfitting**.

When the model is inflexible it is incapable of representing the regularities in the dataset. Since it cannot representing the training dataset, it cannot be expected to generalize well to unseen inputs. This error is called **underfitting**.

We can control whether a model is more likely to overfit or underfit by altering its capacity. A model's **capacity** is its ability to fit a wide variety of functions. Models with low capacity are not very flexible and may struggle to fit the training set. Models with high capacity may overfit the training set.

One way to control capacity, is to restrict the types of functions that the learning algorithm is allowed to choose as the model. This is called the **hypothesis space**.

For example, the linear regression algorithm has a set of all linear functions as its hypothesis space. To increase the model capacity, we can let the algorithm generalize the model to include polynomials.

Models perform best when their capacity is appropriate for the complexity of the task.

## Flexibility and MSE

Let us see how the test and training MSE of a model changes based on varying degrees of flexibility.

<figure style="width: 900px">
	<img src="/media/machine learning/basics/u-shape.png" alt="Flexibility vs MSE">
	<figcaption>Flexibility vs MSE. The gray curve is the training MSE and red curve is the test MSE.</figcaption>
</figure>

When the model flexibility is very low, it suffers from underfitting. So the training MSE will be very high. Since underfitting contributes to bad generalization, the test MSE is also high.

As we increase the flexibility, the model can capture more of the regularities in the dataset, so both the training and test MSE decrease.

But if the model flexibility is too high, the training MSE inches closer and closer to $0$ because it suffers from overfitting. The test MSE on the other hand increases after a certain point. This is due to the fact that noisy data points are being learnt, causing bad generalization.

Note that we expect the training MSE to almost always be smaller than the test MSE, as most learning methods either directly or indirectly seek to minimize the training MSE.

The same line of reasoning can be applied to any of the alternatives to MSE.

## Bias-Variance Tradeoff

The **bias–variance tradeoff** is central in the conflict to prevent overfitting and underfitting.

Ideally, we want a model that both accurately captures the regularities in its training data and also generalizes well to unseen data. Unfortunately, it is impossible to do both simultaneously.

**Bias** is the inability of a learning algorithm to capture the true relationship between the predictors and the response. It is exhibited by relatively inflexible methods like linear regression.

**Variance** is the error caused by sensitivity to small fluctuations in the dataset. High variance is exhibited by highly flexible methods like polynomial regression. If a model has *high* variance, it means small changes in the training data will result in large changes in MSE, which in turn causes large changes in $\hat{f}$.

Variance and bias are two opposing forces.

- Increasing bias will decrease variance
- Increasing variance will decrease bias

The challenge lies in finding a method for which we both variance and bias are low.

<figure style="width: 700px">
	<img src="/media/machine learning/basics/bias-variance.png" alt="Bias-Variance Tradeoff">
	<figcaption>Bias-Variance Tradeoff</figcaption>
</figure>

## Bias-Variance Decomposition

[Proof](https://youtu.be/C3nIFH649wY)

$$
\text{MSE} (\hat{\theta}) = (\text{bias} \space \hat{\theta})^2 + \text{var} \space \hat{\theta}
$$

# References

- [StatQuest : Bias and Variance](https://www.youtube.com/watch?v=EuBBz3bI-aA)
- [Introduction to Statistical Learning](http://faculty.marshall.usc.edu/gareth-james/ISL/)
- [What is the “capacity” of a machine learning model?](https://stats.stackexchange.com/questions/312424/what-is-the-capacity-of-a-machine-learning-model/312578)
- [What exactly is a hypothesis space in machine learning?](https://stats.stackexchange.com/questions/183989/what-exactly-is-a-hypothesis-space-in-machine-learning)
