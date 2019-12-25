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

It is a very simple model that uses linear regression followed by a threshold function. Just like regular linear regression the weights and bias are calculated during the training phase.

<figure style="width: 580px">
	<img src="/media/deep learning/perceptron.png" alt="Perceptron">
	<figcaption>Perceptron</figcaption>
</figure>

Each component of the input vector has a weight associated with it. The **weight** expresses its relative importance in calculating the output. The weights are stored in the vector $w$.

# Calculating the Classification

Now, calculate the weighted sum $\sum_i w_i  x_i$. The output depends on whether this sum is greater than or less than a **threshold value**.

$$
\text{output} =
\begin{cases}
   1 &\text{if } \sum_i w_i x_i + b > threshold \\
   0 &\text{otherwise}
\end{cases}
$$

where, $b$ is the bias. The **bias** value shifts the decision boundary away from the origin and is independent of any input value.

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

You can think of the bias as a measure of how easy it is to get the perceptron to output a 1. For a perceptron with a really big bias, it's extremely easy for the perceptron to output a 1. But if the bias is very negative, then it's difficult for the perceptron to output a 1.

# Learning algorithm

Small changes in weights and biases cause changes in the output. We can use this fact to modify the weights and biases to get our perceptron to behave more in the manner we want.

<figure style="width: 500px">
	<img src="/media/deep learning/learning-algorithm.gif" alt="Learning algorithm">
	<figcaption>Learning algorithm</figcaption>
</figure>

The general idea behind this learning algorithm is to initially draw a random decision boundary across the dataset, then move the boundary to classify the training set properly.

1. Initialize the weights and the threshold with small random values
1. For each example *misclassified* example $(\bold{x}, y)$ in our training set
   1. If the $\bold{x}$ is classified positive, but $y$ is a negative label
         1. Subtract $\alpha x$ from $x$
         1. Subtract $\alpha$ from $b$
   1. If the $\bold{x}$ is classified negative, but $y$ has a positive label
         1. Add $\alpha x$ to $x$
         1. Add $\alpha$ to $b$

$\alpha$ is the learning rate. It is a number between 0 and 1 that ensures that $\alpha x$ is a small number. In turn, it ensures that the boundary line does not take very large steps.

# Multilayer perceptron

A multilayer perceptron (MLP) is a class of feedforward artificial neural network (ANN). The term MLP is used ambiguously, sometimes loosely to refer to any feedforward ANN, sometimes strictly to refer to networks composed of multiple layers of perceptrons (with threshold activation); see § Terminology. Multilayer perceptrons are sometimes colloquially referred to as "vanilla" neural networks, especially when they have a single hidden layer.[1]

An MLP consists of at least three layers of nodes: an input layer, a hidden layer and an output layer. Except for the input nodes, each node is a neuron that uses a nonlinear activation function. MLP utilizes a supervised learning technique called backpropagation for training.[2][3] Its multiple layers and non-linear activation distinguish MLP from a linear perceptron. It can distinguish data that is not linearly separable.[4] 

# References

- [Michael Nielsen](http://neuralnetworksanddeeplearning.com/chap1.html)
- [Wikipedia](https://en.wikipedia.org/wiki/Perceptron)
