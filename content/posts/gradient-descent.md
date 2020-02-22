---
title: "Gradient Descent"
date: "2020-2-22"
template: "post"
draft: false
slug: "/posts/gradient-descent/"
category: "Deep Learning"
tags:
   - ""
description: ""
---

Every function $f$ has a set of maximum and minimum values.

<figure style="width: 800px">
	<img src="/media/deep learning/slope-signs.png" alt="Sign of a slope">
	<figcaption>Sign of a slope</figcaption>
</figure>

<figure style="width: 500px">
	<img src="/media/deep learning/extrema.png" alt="Extrema of a function">
	<figcaption>Extrema of a function</figcaption>
</figure>

# Derivative Tests

## First Order Derivative Test

## Second Order Derivative Test

# Gradient descent

<figure style="width: 1000px">
	<img src="/media/deep learning/simple-gradient-descent.gif" alt="Gradient Descent">
	<figcaption>Gradient Descent</figcaption>
</figure>

Gradient descent is an optimization algorithm used to find the parameters of a function $f$ that lead to a local minima. It is used when the parameters cannot be calculated [analytically](https://math.stackexchange.com/questions/567014/what-does-it-mean-to-solve-a-math-problem-analytically).

Consider a function with two parameters $f(x, y)$. Our goal is to reach the local minima starting from a randomly chosen initial point $(x_0, y_0)$.

Gradient descent reaches a minima by iteratively moving in the direction with the *steepest slope*.

The slope of a function $f$ with a single parameter at a point $p$ is simply its derivative $d f(x)$ / $d x$ at $p$.

The slope of a function $f$ with more than one parameter at a point $p$ is defined by a vector called a **gradient**. The components of this vector hold the *partial derivatives* of $f(x, y)$ at the point $p$.

$$
\nabla f
=
\begin{bmatrix}
   \Large{\frac {\partial f (x, y)} {\partial x}}
   \\\\
   \Large{\frac {\partial f (x, y)} {\partial y}}
\end{bmatrix}
$$

The algorithm to minimize $f(x, y)$ is as follows,

- Choose a random initial point $(x_0, y_0)$.
- Repeat for each parameter until convergence,

$$
Q_{new} = Q_{old} - \alpha \frac {\partial f(x, y)} {\partial Q}
$$

where $Q$ represents a parameter, and $\alpha$ is the learning rate.

<figure style="width: 500px">
	<img src="/media/deep learning/learning-rate.png" alt="Learning Rate">
	<figcaption>Learning Rate</figcaption>
</figure>

# Badlands

step = slope x alpha

new parameter = old - step

# References

- [Gradient](https://en.wikipedia.org/wiki/Gradient)
- [Gradient Descent, Step-by-Step](https://youtu.be/sDv4f4s2SB8)
- [Michael Nielsen](http://neuralnetworksanddeeplearning.com)
