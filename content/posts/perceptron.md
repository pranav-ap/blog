---
title: "Perceptron"
date: "2019-12-25"
template: "post"
draft: false
slug: "/posts/perceptron/"
category: "Deep Learning"
tags:
  - ""
description: ""
---

A **perceptron** is a binary classifier that linearly separates data. It takes in a vector of real numbers as input $x$ and spits out a binary classification of $1$ or $0$.

It is a very simple model that uses *linear regression* followed by a *threshold function*. Just like regular linear regression the weights and bias are calculated during the training phase.

<figure style="width: 580px">
	<img src="/media/deep learning/perceptron.png" alt="Perceptron">
	<figcaption>Perceptron</figcaption>
</figure>

Each component of the input vector has a weight associated with it. The **weight** expresses its relative importance while calculating the output. The weights are stored in the vector $w$.

# Calculating the Output Class

The output depends on whether the weighted sum $\sum_i w_i  x_i$ is greater than or less than a **threshold value**.

<figure style="width: 450px">
	<img src="/media/deep learning/step-function.jpeg" alt="Step Function">
	<figcaption>Step Function</figcaption>
</figure>

$$
\text{output} =
\begin{cases}
   1 &\text{if } \sum_i w_i x_i + b > threshold \\
   0 &\text{otherwise}
\end{cases}
$$

where, $b$ is the bias. The **bias** value shifts the decision boundary towards or away from the origin and is independent of any input value.

If $b$ is negative and threshold is $0$, then $\sum_i w_i  x_i$ must produce a positive value greater than $\mid b \mid$ in order to push get a positive response.

## Simplifying the notation

We can simplify the way we denote a perceptron by making two notational changes. The first is to rewrite $\sum_i w_i  x_i$ as a dot product $\bold{w} \cdot \bold{x}$.

The second is to remove the threshold variable, and simply use the bias $b$ for this purpose.

$$
\text{output} =
\begin{cases}
   1 &\text{if } \bold{w} \cdot \bold{x} + b > 0 \\
   0 &\text{otherwise}
\end{cases}
$$

You can think of the bias as a measure of how easy it is to get the perceptron to output a 1.

For a perceptron with a large positive bias value, it's extremely easy for the perceptron to output a 1. But if the bias is a large negative value, then it's difficult for the perceptron to output a 1.

# Learning algorithm

Small changes in weights and biases cause changes in the output. We can use this fact to modify the weights and biases to get our perceptron to behave more in the manner we want.

<figure style="width: 500px">
	<img src="/media/deep learning/learning-algorithm.gif" alt="Learning algorithm">
	<figcaption>Learning algorithm</figcaption>
</figure>

The general idea behind this learning algorithm is to initially draw a random decision boundary across the dataset, then move the boundary gradually to classify the training set accurately.

<figure style="width: 620px">
	<img src="/media/deep learning/perceptron-learning-algorithm.png" alt="Learning algorithm">
	<figcaption>Perceptron Learning algorithm</figcaption>
</figure>

Let's say we have a *random* initial boundary line,

$$
3 x_1 + 4 x_2 - 10 = 0
$$

We also have a misclassified point $(1, 1)$. In order to classify this point properly, we need to move the boundary line towards it. This can be done by modifying the weights and bias of the boundary line.

<figure style="width: 620px">
	<img src="/media/deep learning/perceptron-moving-the-line.png" alt="Moving the Boundary line">
	<figcaption>Moving the Boundary line</figcaption>
</figure>

$\alpha$ is the learning rate. It is a number between $0$ and $1$ that ensures that $\alpha x$ is a small number. This ensures that the boundary line does not take very large steps.

# Limitations

A perceptron is limited to classifying linearly separable data, due to the use of linear combination.

The use of the step function after summation also restricts it to binary classification problems.

To model non-linear relationships, we need to use multiple perceptrons in the form of [Multi Layer Perceptrons](https://en.wikipedia.org/wiki/Multilayer_perceptron).

# References

- [Michael Nielsen](http://neuralnetworksanddeeplearning.com/chap1.html)
- [Wikipedia: Perceptron](https://en.wikipedia.org/wiki/Perceptron)
- [Wikipedia: Multilayer perceptron](https://en.wikipedia.org/wiki/Multilayer_perceptron)
