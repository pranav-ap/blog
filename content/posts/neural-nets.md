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

# Layers

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

# Training phase in Feedforward networks

The feedforward neural net is a simple network where the nodes and links don't form closed loops. Every net including this one, has two operations defined on it: the forward pass and the backward pass.

The **forward pass** is how a network processes the given input. It takes the input vector $\bold{x}$ and performs the calculations specified by the hidden and output layers to obtain the result. Once your model is trained, this is the only operation you will need in production.

For the training phase however, we need both the passes. The forward pass gives you an output, and the **backward pass** uses it to optimize the weights to make the network more precise.

A forward pass followed by a backward pass, together is called an **iteration**.

We will use the following simple neural net to demonstrate the passes.

<figure style="width: 550px">
	<img src="/media/deep learning/pass-calculation-network.png" alt="Network Pass Calculation">
	<figcaption>Network Pass Calculation</figcaption>
</figure>

### Notation

The inputs $x_1$ and $x_2$ are from the vector $\bold{x}$. $\theta^{(p)}$ is a two-dimensional matrix that holds the weights of links starting from layer $p$. In the diagram, $\theta^{(1)}$ holds the weights for links starting from the input layer.

To denote a specific link that starts from layer $p$ node $q$ to layer $p + 1$ node $r$, we use subscripts as follows: $\theta^{(p)}_{r q}$.

$$
\begin{bmatrix}
   \textcolor{#ffa366}{\theta^{(p)}_{1 1}} & \textcolor{#ffa366}{\theta^{(p)}_{1 2}} \\
   \textcolor{blue}{\theta^{(p)}_{2 1}} & \textcolor{blue}{\theta^{(p)}_{2 2}}
\end{bmatrix}
$$

Finally, $a^{(2)}_1$ represents the activation function for the first node in layer $2$. For convenience, the activations of a layer $p$ can be denoted by a one-dimensional vector $\bold{a}^{(p)}$.

$$
\bold{a}^{(2)}

=

\begin{bmatrix}
   a^{(2)}_1 \\
   a^{(2)}_2
\end{bmatrix}
$$

## Forward Pass Calculation

The goal of forward pass is to calculate the output vector $\bold{a}^{(3)}$ of this network. Let's start by calculating $\bold{a}^{(2)}_{1}$ and $\bold{a}^{(2)}_{2}$.

$$
\bold{a}^{(2)}_{1}
=
g ( \theta^{(1)}_{1 1} x_1 + \theta^{(1)}_{1 2} x_2 + b_1 )
$$

$$
\bold{a}^{(2)}_{2}
=
g ( \theta^{(1)}_{2 1} x_1 + \theta^{(1)}_{2 2} x_2 + b_2 )
$$

For ease, we can represent the activations of the entire layer using the matrix notation,

$$
\begin{bmatrix}
   a^{(2)}_1 \\
   a^{(2)}_2
\end{bmatrix}

=

g \Bigg(

\begin{bmatrix}
   \textcolor{#ffa366}{\theta^{(p)}_{1 1}} & \textcolor{#ffa366}{\theta^{(p)}_{1 2}} \\
   \textcolor{blue}{\theta^{(p)}_{2 1}} & \textcolor{blue}{\theta^{(p)}_{2 2}}
\end{bmatrix}

\begin{bmatrix}
   x_1 \\
   x_2
\end{bmatrix}

+

\begin{bmatrix}
   b_1 \\
   b_2
\end{bmatrix}

\Bigg)
$$

$$
\bold{a}^{(1)} = g (\theta^{(1)} \bold{x} + \bold{b})
$$

Similarly, we can find $\bold{a}^{(3)}$.

$$
\bold{a}^{(3)} =  g (\theta^{(2)} \bold{a}^{(1)} + \bold{b})
$$

## Calculate the Error

Now, we need to calculate how wrong our output was compared to the true value.

## Backward Pass Calculation

# References

- [Michael Nielsen](http://neuralnetworksanddeeplearning.com)
- [Wikipedia: Artificial neural network](https://en.wikipedia.org/wiki/Artificial_neural_network)
- [Wikipedia: Feature engineering](https://en.wikipedia.org/wiki/Feature_engineering)
- [Wikipedia: Feature learning](https://en.wikipedia.org/wiki/Feature_learning)
- [Wikipedia: Deep learning](https://en.wikipedia.org/wiki/Deep_learning)
- [StackOverflow: How to choose the number of hidden layers and nodes in a feedforward neural network?](https://stats.stackexchange.com/questions/181/how-to-choose-the-number-of-hidden-layers-and-nodes-in-a-feedforward-neural-netw)
