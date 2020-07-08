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
\bold{z}^{(1)} = \bold{w^{(1)}} \cdot \bold{x} + b^{(1)}
$$

The outputs from the hidden layer's nodes is given by the matrix $\bold{a}^{(1)}$,

$$
\bold{a}^{(1)} = f(\bold{z}^{(1)})
$$

Since $f(z)$ is an identity function, we can expand this into,

$$
\bold{a}^{(1)} = \bold{w^{(1)}} \cdot \bold{x} + b^{(1)}
$$

The matrix $\bold{a}^{(1)}$ is the input for the output layer. The $\bold{z}^{(2)}$ for the output layer is,

$$
\bold{z}^{(2)} = \bold{w^{(2)}} \cdot \bold{a}^{(1)} + b^{(2)}
$$

The output matrix $\bold{a}^{(2)}$ can be calculated as,

$$
\bold{a}^{(2)} = f(\bold{z}^{(2)})	\\

\bold{a}^{(2)} = \bold{w^{(2)}} \cdot \bold{a}^{(1)} + b^{(2)}
$$

Expand the $\bold{a}^{(1)}$ variable,

$$
\bold{a}^{(2)} = \bold{w^{(2)}} \cdot (\bold{w^{(1)}} \cdot \bold{x} + b^{(1)}) + b^{(2)}
$$

Finally, we rearranging the variables,

$$
\bold{a}^{(2)} = (\bold{w^{(2)}} \cdot \bold{w^{(1)}}) \cdot \bold{x} + (\bold{w^{(2)}}  \cdot b^{(1)} + b^{(2)})
$$

We can now see that $\bold{a}^{(2)}$ is a linear function.

No matter how many nodes and layers you have you will always end up with a linear function if you use linear activations.

Apparently, there are rare cases where linear activation functions are useful. I don't know what they are.

## Why do we need *differentiable* activation functions ?

During backpropagation, we calculate the partial derivatives of the loss function wrt each of the weights and biases. This is required to update the network weights and biases.

## Why do we need *monotonic* activation functions ?

Backpropagation with gradient descent informs each neuron how much it should influence each neuron in the next layer through weights.

If the activation function isn't monotonic then increasing the neuron's weight might cause it to have less influence, the opposite of what was intended.

The result would be chaotic behavior during training, with the network unlikely to converge to a minima that yields an accurate model.

## Why do we need *zero-centered* activation functions ?

During backpropagation, the partial derivative can be positive or negative. This is used to increase or decrease weights in the neural net. With a non-zero centred activation function the above steps cannot be done in a single epoch.

# Types of Activation Functions

There are many types of activation functions, each with its own pros and cons. Choose one depending on your network's requirements.

## Sigmoid

<figure style="width: 700px">
	<img src="/media/deep learning/sigmoid.png" alt="Sigmoid activation function">
	<figcaption>Sigmoid activation function</figcaption>
</figure>

A sigmoid function is a family of functions having a "S"-shaped curve. The sigmoid curve shown in the figure is called a logistic function. It is defined by the formula,

$$
f(z) = \frac {1} {1 + e^{-z}}
$$

It takes in a real-valued number $z$ and squashes it into a range monotonically increasing from $0$ to $1$. So, the output can be interpreted as probabilities when it used as the activation function for the output layer.

Unlike the perceptron neuron, a sigmoid function does not abruptly change the output as we tune the input weights. But it has recently fallen out of favor and it is rarely ever used, due to some drawbacks.

The first of which is that a sigmoid function does not center output around zero. The second is the *vanishing gradient problem*.

## Vanishing Gradient Problem

For very high or very low values of $z$, there is almost no change in activation. In other words, the slope is very small on both ends of the curve.

$$
\tag {saturation at the tails} \frac {\partial a^{(l)}_{p}} {\partial z^{(l)}_{p}} \approx 0
$$

This saturation is the root cause for the vanishing gradient problem observed during backprop.

<figure style="width: 600px">
	<img src="/media/deep learning/simple-line-net.png" alt="">
	<figcaption></figcaption>
</figure>

The gradient of the loss function $J(\theta)$ for the parameter $\theta_{2}$ is given by,

$$
\frac {\partial J (\theta)} {\partial \theta_{2}}
=
\Bigg ( \frac {\partial J (\theta)} {\partial a^{(3)}} \Bigg)
\Bigg ( \frac {\partial a^{(3)}} {\partial z^{(3)}} \Bigg)
\Bigg ( \frac {\partial z^{(3)}} {\partial \theta_{2}} \Bigg)
$$

The update rule for $\theta_{2}$ during gradient descent is,

$$
\theta_{2}
=
\theta_{2}
-
\alpha
\frac {\partial J (\theta)} {\partial \theta_{2}}
$$

If the activation function $a^{(3)}$ returns values from the tail, then its slope $\partial a^{(3)} / \partial z^{(3)} \approx 0$. This means $\partial J (\theta) / \partial \theta_{2}$ will be a tiny number $< 1$. So, $\theta_{2}$ is updated at a snail's pace.

This problem gets worse as we pass through more layers. The gradient of the loss function $J(\theta)$ for the parameter $\theta_{1}$ is given by,

$$
\frac {\partial J (\theta)} {\partial \theta_{1}}
=
\Bigg ( \frac {\partial J (\theta)} {\partial a^{(3)}} \Bigg)
\Bigg ( \frac {\partial a^{(3)}} {\partial z^{(3)}} \Bigg)
\Bigg ( \frac {\partial z^{(3)}} {\partial a^{(2)}} \Bigg)
\Bigg ( \frac {\partial a^{(2)}} {\partial z^{(2)}} \Bigg)
\Bigg ( \frac {\partial z^{(2)}} {\partial \theta_{1}} \Bigg)
$$

The gradients for the weights in the front of the network have longer chains of small numbers. The gradient may be so small by the time it reaches them that it may have very little effect in the update rule. So these weights train very slowly.

## Hyperbolic tangent (tanh)

<figure style="width: 700px">
	<img src="/media/deep learning/tanh.png" alt="Tanh">
	<figcaption>Tanh</figcaption>
</figure>

The tanh function takes in a real-valued number $z$ and squashes it into a range monotonically increasing from $-1$ to $1$. It is defined by the formula,

$$
f(z)
=
\frac {2} {1 + e^{-2z}} + 1
$$

Unlike the sigmoid function, its output values are zero-centered. It can be thought of as a scaled and shifted sigmoid.

It is almost always preferable compared to the sigmoid function, even though it suffers from vanishing gradients.

## Rectified Linear Unit (ReLU)

<figure style="width: 700px">
	<img src="/media/deep learning/reLU.png" alt="Rectified Linear Unit (ReLU)">
	<figcaption>Rectified Linear Unit (ReLU)</figcaption>
</figure>

**ReLU** is the most widely used activation function. It is defined as,

$$
f(z) = max(0, z)
$$

It simply returns $z$ if it is positive and $0$ otherwise. So it is efficient and easy to compute, unlike the sigmoid or tanh where we need to calculate the exponential.

It does not suffer from the vanishing gradient problem. Thus, it allows for faster and effective training of deep neural architectures.

One drawback of ReLU is that it is non-differentiable at $0$. For a function to be differentiable at a given point $x$, the following conditions must be true.

1. The left-hand limit exists
1. The right-hand limit exists
1. The left-hand and right-hand limits are equal

The derivative for a function $f$ at $x$ at $0$ is given by,

$$
f'(x)
=
\lim\limits_{x \to 0}
\frac {f(x + \Delta x) - f(x)} {\Delta x}
$$

The derivative for ReLU  at $0$ is,

$$
f'(x)
=
\lim\limits_{x \to 0}
\frac {\text{max}(0, x + \Delta x) - \text{max}(0, x)} {\Delta x}
$$

The right hand limit is,

$$
\begin{aligned}

f'(x)
&=
\lim\limits_{x \to 0^{\text{+}}}
\frac {\text{max}(0, x + \Delta x) - \text{max}(0, x)} {\Delta x}

\\

&=
\lim\limits_{x \to 0^{\text{+}}}
\frac {x + \Delta x - x} {\Delta x}

\\

&= 1

\end{aligned}
$$

The left hand limit is,

$$
\begin{aligned}

f'(x)
&=
\lim\limits_{x \to 0^{\text{-}}}
\frac {\text{max}(0, x + \Delta x) - \text{max}(0, x)} {\Delta x}

\\

&=
\lim\limits_{x \to 0^{\text{-}}}
\frac {0 - 0} {\Delta x}

\\

&= 0

\end{aligned}
$$

As we can see, the left-hand limit and the right-hand limit are not equal at $0$, Hence, we say that the derivative $f'$ is undefined at $0$.

As a workaround, deep learning frameworks do not evaluate it at non-differentiable points and simply return some sensible output value for ReLU neurons and its variants.

Another drawback with ReLU is that it suffers from what is called the *dying ReLU problem*.

## Dying ReLU Problem

<figure style="width: 700px">
	<img src="/media/deep learning/inside-a-neuron.png" alt="Inside a Neuron">
	<figcaption>Inside a Neuron</figcaption>
</figure>

If a weight like $w_1$ or bias $b$ has a large negative value, then the sum $z$ will likely be a negative value for any input vector $\bold{x}$. In this case, ReLU will always output $0$ for any input.

$$
\tag{\text{a dying ReLU's output}} \bold{a}(z) = 0
$$

This has a terrible affect on backprop. The gradient of the loss function $J(\theta)$ for the parameter $w_1$ is given by,

$$
\frac {\partial J (W)} {\partial w_1}
=
\Bigg ( \frac {\partial J (W)} {\partial a(z)} \Bigg)
\Bigg ( \frac {\partial a(z)} {\partial z} \Bigg)
\Bigg ( \frac {\partial z} {\partial w_1} \Bigg)
$$

The update rule for $\theta_{2}$ during gradient descent is,

$$
w_1
=
w_1
-
\alpha
\frac {\partial J (\theta)} {\partial w_1}
$$

Since $\bold{a}(z) = 0$, its gradient $\partial a(z) / \partial z$ is also $0$, which means that $w_1$ will never again get updated during gradient descent optimization.

One reason why $w_1$ is highly negative in the first place could be because of bad initialization of weights. This is easily remedied by ensuring that only small values are assigned to all the weights.

Another reason is the use of a high learning rate $\alpha$. When $\alpha$ is large, then the update rule will assign a large negative value to $w_1$.

## Leaky ReLU

<figure style="width: 700px">
	<img src="/media/deep learning/leaky-and-parametric-relu.png" alt="Leaky ReLU and Parametric ReLU">
	<figcaption>Leaky ReLU and Parametric ReLU</figcaption>
</figure>

A dead ReLU does not take part in backprop. The **leaky ReLU** is a variant that alleviates this problem by adding a slight slope in the negative range. It is defined as,

$$
f(z) = max(0.01 \space z, z)
$$

## Parametric ReLU (PReLU)

Parametric ReLU is a type of leaky ReLU that, instead of having a predetermined slope like 0.01, makes it a parameter for the neural network to learn. It is defined as,

$$
f(z) = max(az, z)
$$

where, $a$ is the parameter for the slope.

## Softmax

The softmax activation function is used in the last layer of neural nets for multi-class classification.

It takes in a vector of real numbers and returns a vector of whose sum of elements is always $1$. So, it can be used for categorical probability distribution. It is defined as,

$$
f_{i}(\bold{x})
=
\frac {e^{x_i}} {\sum_{j = 1}^{n} e^{x_j}}
$$


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
- [Deeplizard : Vanishing & Exploding Gradient explained](https://youtu.be/qO_NLVjD6zE)
- [StackOverflow : What is the “dying ReLU” problem in neural networks?](https://datascience.stackexchange.com/questions/5706/what-is-the-dying-relu-problem-in-neural-networks)
- [Victor Zhou : Softmax](https://victorzhou.com/blog/softmax/)