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

An activation function $f(z)$ defines the output of a node. In order to be useful, $f(z)$ must be *non-linear*, [*monotonic*](https://en.wikipedia.org/wiki/Monotonic_function), *continuous* and *differentiable*.

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

## Why do we need *differentiable* activation functions ?

During backpropagation, we calculate the partial derivatives of the error wrt each of the weights. This is required to tune the network weights.

## Why do we need *monotonic* activation functions ?

During the training phase, backpropagation informs each neuron how much it should influence each neuron in the next layer. If the activation function isn't monotonic then increasing the neuron's weight might cause it to have less influence, the opposite of what was intended. The result would be choatic behavior during training, with the network unlikely to converge to a state that yields an accurate classifier.



## Why do we need *zero-centered* activation functions ?

This property is important in deep learning because it has been empirically shown that models operating on normalized data enjoy faster convergence.

Unfortunately, zero-centered activation functions like tanh saturate at their asymptotes––the gradients within this region get vanishingly smaller over time, leading to a weak training signal. ReLU avoids this problem but it is not zero-centered. So, deep learning practitioners have invented a myriad of normalization layers (batch norm, layer norm, weight norm, etc.) to mitigate this issue.

During back propagation, the derivative can be positive or negative  i.e We might want to increase a particular weight and decrease another weight in the same neural network at the same time. With non-zero centred activation function the above steps cannot be done in a single epoch, this is the reason why we are going for zero centred activation function. Zero centred activation functions can do the above task in fewer steps and thus faster convergence.

# Types of Activation Functions

There are many types of activation functions, each with its own pros and cons. Choose one depending on your needs.

## Sigmoid

<figure style="width: 700px">
	<img src="/media/deep learning/sigmoid.png" alt="Sigmoid activation function">
	<figcaption>Sigmoid activation function</figcaption>
</figure>

A sigmoid function is a family of functions having a "S"-shaped curve. The sigmoid curve shown in the figure is called a logistic function. It is defined by the formula,

$$
f(z) = \frac {1} {1 + e^{-z}}
$$

It takes in a real-valued number $z$ and squashes it into a range monotonically increasing from $0$ to $1$. The output is thus, often interpreted as probabilities.

Unlike the perceptron neuron, a sigmoid function does not abruptly change the output as we tune the input weights. This made is widely used until it was replaced by others due to the following disadvantages.

The sigmoid function does not center output around zero, ie. the mean is not $0$.

### Vanishing gradient

For very high or very low values of $z$, there is almost no change in activation. This can result in the network refusing to learn further, or being too slow to reach an accurate prediction.

## Hyperbolic tangent (Tanh)

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
Non-linear—although it looks like a linear function, ReLU has a derivative function and allows for backpropagation.

Functions like ReLU are used in neural networks due to the computational advantages of using these simple equations over more traditional activation functions like tanh or the logistic sigmoid function. The back-propagation algorithm used to optimise neural networks works under the pre-condition that all of the functions contained within the system are differentiable. As discussed ReLU and other variants are non-differentiable at specific points, so how are they used? Essentially, at the points at which they are non-differentiable the function is not evaluated and the output is replaced with a sensible value. For example for ReLU at 𝑓ʹ(𝑥) we just specify the output to be zero or one, which is reasonable given our usage. In Theano [ 3] for example it specified that 𝑥 is not evaluated and taken to be 1 for 𝑥 >= 0. This is not mathematically pure and one could imagine scenarios where this would cause problems, the reality is however that the neural networks that comprise of these functions work well and are stable and so this issue is over-looked in favour of computational efficiency.

## Leaky ReLU

<figure style="width: 700px">
	<img src="/media/deep learning/leaky-and-parametric-relu.png" alt="Leaky ReLU and Parametric ReLU">
	<figcaption>Leaky ReLU and Parametric ReLU</figcaption>
</figure>

The Dying ReLU problem—when inputs approach zero, or are negative, the gradient of the function becomes zero, the network cannot perform backpropagation and cannot learn.

Prevents dying ReLU problem—this variation of ReLU has a small positive slope in the negative area, so it does enable backpropagation, even for negative input values
Otherwise like ReLU

Results not consistent—leaky ReLU does not provide consistent predictions for negative input values.

## Parametric ReLU (PReLU)

## Exponential Linear Unit (ELU)

<figure style="width: 700px">
	<img src="/media/deep learning/elu.png" alt="Exponential Linear Unit">
	<figcaption>Exponential Linear Unit</figcaption>
</figure>

## ReLU-6

<figure style="width: 700px">
	<img src="/media/deep learning/relu-6.png" alt="ReLU-6">
	<figcaption>ReLU-6</figcaption>
</figure>

## Softmax

Able to handle multiple classes only one class in other activation functions—normalizes the outputs for each class between 0 and 1, and divides by their sum, giving the probability of the input value being in a specific class.

Useful for output neurons—typically Softmax is used only for the output layer, for neural networks that need to
classify inputs into multiple categories.

# References

- [Wikipedia: Activation Function](https://en.wikipedia.org/wiki/Activation_function)
- [Michael Nielsen](http://neuralnetworksanddeeplearning.com)
- [Wikipedia: Artificial neural network](https://en.wikipedia.org/wiki/Artificial_neural_network)
- [Why Non-linear Activation Functions (C1W3L07)](https://www.youtube.com/watch?v=NkOv_k7r6no)
- [Derivatives Of Activation Functions (C1W3L08)](https://www.youtube.com/watch?v=P7_jFxTtJEo)
- [Wikipedia: Sigmoid function](https://en.wikipedia.org/wiki/Sigmoid_function)
- [Derivative of the Sigmoid function](https://towardsdatascience.com/derivative-of-the-sigmoid-function-536880cf918e)
- [Why is the ReLU function not differentiable at x=0?](https://sebastianraschka.com/faq/docs/relu-derivative.html)
- [StackOverflow : Pros and Cons](https://stats.stackexchange.com/questions/115258/comprehensive-list-of-activation-functions-in-neural-networks-with-pros-cons/229015#229015)
