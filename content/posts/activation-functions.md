---
title: "Activation Functions"
date: "2020-1-26"
template: "post"
draft: false
slug: "/posts/activation-functions/"
category: "Deep Learning"
tags:
   - ""
description: ""
---

<figure style="width: 700px">
	<img src="/media/deep learning/inside-a-neuron.png" alt="Inside a Neuron">
	<figcaption>Inside a Neuron</figcaption>
</figure>

A neuron takes in a input vector $\bold{x}$, weights $\bold{w}$ and a bias value $b$, then first calculates a linear combination,

$$
z = \bold{w} \cdot \bold{x} + b
$$

where $z$ is a scalar value.

An activation function $f(z)$ defines the output of a node. In order to be useful, $f(z)$ must be *non-linear*, *monotonic* and *continuously differentiable*.

## Why do we need *non-linear* activation functions ?

<figure style="width: 700px">
	<img src="/media/deep learning/simple-net.png" alt="Simple Neural Net">
	<figcaption>Simple Neural Net</figcaption>
</figure>

Imagine we have a simple neural net that uses the identity function $f(x) = x$ as its linear activation function.

We will now show that even though we have *two* layers of linear activation functions, the result is just another linear activation function.

The $z$ linear combination value for the hidden layer is given by the matrix $\bold{z}^{[1]}$,

$$
\bold{z}^{[1]} = \bold{w^{[1]}} \cdot \bold{x} + b^{[1]}
$$

The outputs from the hidden layer's nodes is given by the matrix $\bold{a}^{[1]}$,

$$
\bold{a}^{[1]} = f(\bold{z}^{[1]})
$$

Since $f(z)$ is an identity function, we can expand this into,

$$
\bold{a}^{[1]} = \bold{w^{[1]}} \cdot \bold{x} + b^{[1]}
$$

The matrix $\bold{a}^{[1]}$ is the input for the output layer. The $\bold{z}^{[2]}$ for the output layer is,

$$
\bold{z}^{[2]} = \bold{w^{[2]}} \cdot \bold{a}^{[1]} + b^{[2]}
$$

The output matrix $\bold{a}^{[2]}$ can be calculated as,

$$
\bold{a}^{[2]} = f(\bold{z}^{[2]})	\\

\bold{a}^{[2]} = \bold{w^{[2]}} \cdot \bold{a}^{[1]} + b^{[2]}
$$

Expand the $\bold{a}^{[1]}$ variable,

$$
\bold{a}^{[2]} = \bold{w^{[2]}} \cdot (\bold{w^{[1]}} \cdot \bold{x} + b^{[1]}) + b^{[2]}
$$

Finally, we rearranging the variables,

$$
\bold{a}^{[2]} = (\bold{w^{[2]}} \cdot \bold{w^{[1]}}) \cdot \bold{x} + (\bold{w^{[2]}}  \cdot b^{[1]} + b^{[2]})
$$

We can now see that $\bold{a}^{[2]}$ is a linear function.

No matter how many nodes and layers you have you will always end up with a linear function if you use linear activations.

Apparently, there are rare cases where linear activation functions are useful. I don't know what they are.

## Continuously differentiable

During backpropagation, we use the derivative of the activation functions. This property is required to compute the gradients we use to tune the network weights.

# Types of Activation Functions

There are many types of activation functions, each with its own pros and cons. Choose one depending on your needs.

## Sigmoid

<figure style="width: 700px">
	<img src="/media/deep learning/sigmoid.png" alt="Sigmoid activation function">
	<figcaption>Sigmoid activation function</figcaption>
</figure>

The sigmoid function squashes $z$ into the range 0 and 1. The sigmoid is rarely used any longer, except in the outer layer for binary classifications.

Drawback #1: the sigmoid function does not center output around zero
Drawback #2: small local gradients can mute the gradient and disallow the forward propagation of a useful signal
Drawback #3: incorrect weight initialization can lead to saturation, where most neurons of the network then become saturated and almost no learning will take place (see [1])

Vanishing gradient—for very high or very low values of X, there is almost no change to the prediction, causing a vanishing gradient problem. This can result in the network refusing to learn further, or being too slow to reach an accurate prediction.

## Tanh

<figure style="width: 700px">
	<img src="/media/deep learning/tanh.png" alt="Tanh">
	<figcaption>Tanh</figcaption>
</figure>

The tanh function "squashes" values to the range -1 and 1. Output values are, therefore, centered around zero
Can be thought of as a scaled, or shifted, sigmoid, and is almost always preferable to the sigmoid function

## Rectified Linear Unit (ReLU)

<figure style="width: 700px">
	<img src="/media/deep learning/reLU.png" alt="Rectified Linear Unit (ReLU)">
	<figcaption>Rectified Linear Unit (ReLU)</figcaption>
</figure>

Function takes the form of f(x) = max(0, x)
Transformation leads positive values to be 1, and negative values to be zero
Shown to accelerate convergence of gradient descent compared to above functions
Can lead to neuron death, which can be combated using Leaky ReLU modification (see [1])
ReLU is has become the default activation function for hidden layers (see [3])

Computationally efficient—allows the network to converge very quickly
Non-linear—although it looks like a linear function, ReLU has a derivative function and allows for backpropagation

## Leaky ReLU

The Dying ReLU problem—when inputs approach zero, or are negative, the gradient of the function becomes zero, the network cannot perform backpropagation and cannot learn.

Prevents dying ReLU problem—this variation of ReLU has a small positive slope in the negative area, so it does enable backpropagation, even for negative input values
Otherwise like ReLU

Results not consistent—leaky ReLU does not provide consistent predictions for negative input values.

## Softmax

Able to handle multiple classes only one class in other activation functions—normalizes the outputs for each class between 0 and 1, and divides by their sum, giving the probability of the input value being in a specific class.

Useful for output neurons—typically Softmax is used only for the output layer, for neural networks that need to
classify inputs into multiple categories.

Derivatives or Gradients of Activation Functions

The derivative—also known as a gradient—of an activation function is extremely important for training the neural network.

Neural networks are trained using a process called backpropagation—this is an algorithm which traces back from the output of the model, through the different neurons which were involved in generating that output, back to the original weight applied to each neuron. Backpropagation suggests an optimal weight for each neuron which results in the most accurate prediction.

# References

- [Wikipedia: Activation Function](https://en.wikipedia.org/wiki/Activation_function)
- [Michael Nielsen](http://neuralnetworksanddeeplearning.com)
- [Wikipedia: Artificial neural network](https://en.wikipedia.org/wiki/Artificial_neural_network)
- [Why Non-linear Activation Functions (C1W3L07)](https://www.youtube.com/watch?v=NkOv_k7r6no)
- [Derivatives Of Activation Functions (C1W3L08)](https://www.youtube.com/watch?v=P7_jFxTtJEo)
