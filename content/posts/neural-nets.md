---
title: "Neural Networks"
date: "2020-2-9"
template: "post"
draft: false
slug: "/posts/neural-networks/"
category: "Deep Learning"
tags:
   - ""
description: ""
---

Most knowledge required for tasks including speech and image recognition is informal, subjective and intuitive. This makes it difficult to encode into a program.

The performance of learning algorithms depends heavily on the *representation* of the data they are given. Classical machine learning algorithms like Linear regression and SVMs require us to design the features / columns before training can begin.

A **feature** is a measurable property of some phenomenon. Choosing informative and independent features is a crucial step for effective algorithms.

However, for many tasks, coming up with features is difficult, time-consuming, requires expert knowledge. This is called **feature engineering**. If done well, the resulting dataset will lead us to the best possible model.

Say we want to detect a car in an image. We can try to use the presence of a wheel as a feature. But, even though a wheel has a simple geometric shape, factors like lighting and   create varieties of images.

These are called **factors of variation**. Factors of variation are some factors which determine varieties in observed data. If that factors change, the variety within the dataset will change.

One way to overcome this difficulty is to use *representation learning*.

# Representation learning

**Feature learning** or **representation learning** is a set of techniques that automatically discover the features necessary for making a good model directly from raw data.

This replaces manual feature engineering and allows a machine to both learn useful features and use them to perform a task.

<figure style="width: 550px">
	<img src="/media/deep learning/learning-features.png" alt="Learning Features">
	<figcaption>Learning Features</figcaption>
</figure>

Feature learning can be either *supervised* or *unsupervised*.

Examples of supervised feature learning include neural networks and multilayer perceptrons. Unsupervised feature learning includes principal component analysis and K-means clustering.

# Neural Networks

Every neural net has three types of *layers*: input, hidden, and output.

Each layer has a set of nodes connected to the nodes in other layers by *links*. Each link has a weight, which determines the strength of the current node's influence on the next.

The arrangement of the layers and nodes in the network is called its **architecture**.

<figure style="width: 700px">
	<img src="/media/deep learning/simple-net.png" alt="Simple Neural Net">
	<figcaption>A Simple Neural Net</figcaption>
</figure>

**Size** refers to the number of nodes in the model. **Width** is the number of nodes in a specific layer.
The number of layers in a neural net is called the **depth**.

The purpose of a neural network is to approximate a function with the help of a dataset. The type functions that can be learned by its architecture is called the **representational capacity**.

## The Input Layer

Every network has exactly one input layer. The number of layers equals the number of features/columns in your dataset. Usually we also include one additional node representing the bias term.

## The Output Layer

Every network has exactly one output layer.

If the network is used for regression, then the output layer has a single node. If the network is a classifier, then the number of nodes usually equals the number of classes we have in the dataset.

## The Hidden Layers

The configuration of the hidden layers decide the type of function we can approximate using the neural net.

A neural net with a single hidden layer containing a finite number of neurons, can approximate any continuous function $f(x)$. This is called the **universal approximation theorem**. This holds true for any number of inputs and outputs.

Note that the theorem doesn't say that a network can be used to *exactly* compute any function $f(x)$. Rather, we can get an *approximation* $g(x)$.

$$
\mid g(x) - f(x) \mid < \epsilon, \text{ for all inputs } x
$$

This approximation can be improved by increasing the number of hidden neurons.

Even though the architecture can closely represent $f(x)$, we don't have a guarantee that the training algorithm will be able to learn it. Learning can fail due to two reasons:

- The optimization algorithm may not be able to find the parameter values in $f(x)$
- Overfitting or underfitting will deviate $g(x)$ from reaching $f(x)$

The biggest obstacle to simply using a single hidden layer all the time, is that in the worst case it requires an exponential number of nodes. This makes learning more infeasible.

The solution is to use more hidden layers. This is empirically shown to reduce the number of hidden nodes required to estimate $f(x)$.

The more layers and nodes you add, the more representational capacity, your network will have.

# Feedforward networks

The feedforward neural net is a simple network where the nodes and links don't form closed loops. Every net including this one, has two operations defined on it: the forward pass and the backward pass.

The **forward pass** is how a network processes the given input. It takes the input vector $\bold{x}$ and performs the calculations specified by the hidden and output layers to obtain the result. Once your model is trained, this is the only operation you will need in production.

For the training phase however, we need both the passes. The forward pass gives you an output, and the **backward pass** uses it to optimize the weights to make the network more precise.

A forward pass followed by a backward pass, together is called an **iteration**.

## Forward Pass Calculation

<figure style="width: 600px">
	<img src="/media/deep learning/three-nodes.png" alt="Three nodes">
	<figcaption>Three nodes</figcaption>
</figure>

We have three layers with one node each. The weight of each link is denoted by $\theta$.

<figure style="width: 900px">
	<img src="/media/deep learning/three-nodes-detailed.png" alt="Three nodes - Detailed view">
	<figcaption>Three nodes - Detailed view</figcaption>
</figure>

## Backward Pass Calculation

# References

- [Michael Nielsen](http://neuralnetworksanddeeplearning.com)
- [Wikipedia: Artificial neural network](https://en.wikipedia.org/wiki/Artificial_neural_network)
- [Wikipedia: Feature engineering](https://en.wikipedia.org/wiki/Feature_engineering)
- [Wikipedia: Feature learning](https://en.wikipedia.org/wiki/Feature_learning)
- [Wikipedia: Deep learning](https://en.wikipedia.org/wiki/Deep_learning)
- [StackOverflow: How to choose the number of hidden layers and nodes in a feedforward neural network?](https://stats.stackexchange.com/questions/181/how-to-choose-the-number-of-hidden-layers-and-nodes-in-a-feedforward-neural-netw)