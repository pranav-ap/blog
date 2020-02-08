---
title: "Neural Networks"
date: "2020-1-9"
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

Every neural net has three types of layers: input, hidden, and output. Each layer has a set of nodes. The arrangement of the layers and nodes in the network is called its **architecture**.

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

If a single hidden layer can learn any problem, why bother with multiple hidden layers? While a neural net with a single hidden layer *can* learn anything, it may not always be *easy* to learn it.

One or two hidden layers is sufficient for a large majority of problems.

Adding more hidden layers helps in learning hierarchical representations of the input data and generalize better
to unseen data.

But this does increase computational costs and learning time, due to the increase in number of parameters to be learned during the learning phase.

# References

- [Michael Nielsen](http://neuralnetworksanddeeplearning.com)
- [Wikipedia: Artificial neural network](https://en.wikipedia.org/wiki/Artificial_neural_network)
- [Wikipedia: Feature engineering](https://en.wikipedia.org/wiki/Feature_engineering)
- [Wikipedia: Feature learning](https://en.wikipedia.org/wiki/Feature_learning)
- [Wikipedia: Deep learning](https://en.wikipedia.org/wiki/Deep_learning)
- [StackOverflow: How to choose the number of hidden layers and nodes in a feedforward neural network?](https://stats.stackexchange.com/questions/181/how-to-choose-the-number-of-hidden-layers-and-nodes-in-a-feedforward-neural-netw)
