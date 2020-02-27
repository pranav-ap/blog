---
title: "An Introduction to Gradient Descent"
date: "2020-2-22"
template: "post"
draft: false
slug: "/posts/gradient-descent-intro/"
category: "Deep Learning"
tags:
   - ""
description: ""
---

Let $f$ be a function with domain $D$. Then $f$ has an **global maximum** value at a point $c$ within $D$ if

$$
f(x) \le f(c) \qquad \text{for all x in D}
$$

and an **global minimum** at point $c$ within $D$ if

$$
f(x) \ge f(c) \qquad \text{for all x in D}
$$

<figure style="width: 750px">
	<img src="/media/calculus/maxima-minima.png" alt="Sign of a slope">
	<figcaption>Extremes of a function</figcaption>
</figure>

Maximum and minimum values are called **extreme values** of function $f$. Extreme values that are not *global* maxima or minima are called **local** maxima or minima.

The places where a function can have extreme values are:

- interior points where $f'(x) = 0$
- interior points where $f'(x)$ is undefined
- domain endpoints of $f$

Note that an interior point of a $f$ where $f'(x)$ is zero or undefined is called a **critical point** of $f$.

# First Derivative Test for Local Extrema

In optimization problems, it is useful to detect minima and maxima of a function $f$. This can be done by examining the sign of the function's derivative $f'$ at various points in its domain.

<figure style="width: 900px">
	<img src="/media/calculus/first-derivative-test.png" alt="First Derivative Test">
	<figcaption>First Derivative Test</figcaption>
</figure>

If $f$ has a local minima at an *interior* point $c$ then $f' < 0$ for points immediately to the left of $c$ and $f' > 0$ for points immediately to the right.

If $f$ has a local maxima at an *interior* point $c$ then $f' > 0$ for points immediately to the left of $c$ and $f' < 0$ for points immediately to the right.

The test for local extrema at endpoints is similar, but there is only one side to consider.

<figure style="width: 800px">
	<img src="/media/deep learning/slope-signs.png" alt="Sign of a slope">
	<figcaption>Sign of a slope</figcaption>
</figure>

In summary, if $f'(c)$ changes from positive to negative, then $c$ is a local maxima. If $f'(c)$ changes from negative to positive, then $c$ is a local minima. If the sign remains the same on both the sides of point $c$, then there is no local extreme at $c$.

# Gradient descent

<figure style="width: 1000px">
	<img src="/media/deep learning/simple-gradient-descent.gif" alt="Gradient Descent">
	<figcaption>Gradient Descent</figcaption>
</figure>

Gradient descent is an optimization algorithm used to find the parameters of a function $f$ that lead to a minima. It is used when the parameters cannot be calculated [analytically](https://math.stackexchange.com/questions/567014/what-does-it-mean-to-solve-a-math-problem-analytically).

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

- Compute the gradient for $f(x, y)$ wrt $x$ and $y$.
- Choose a random initial values for parameters $x$ and $y$.
- Repeat for each parameter until it reaches a minima,

$$
Q_{new} = Q_{old} - \underbrace{ \alpha \underbrace{ \frac {\partial f(x, y)} {\partial Q} }_{\text{slope}} }_{\text{step}}
$$

where $Q$ represents a function parameter, and $\alpha$ is the learning rate.

# Learning Rate

The **learning rate** is a small positive number between $0$ to $1$ that controls the magnitude of the step.

<figure style="width: 500px">
	<img src="/media/deep learning/learning-rate.png" alt="Learning Rate">
	<figcaption>Learning Rate</figcaption>
</figure>

If the learning rate is too high, gradient descent might jump over the minima, but a tiny learning rate will take too long to reach the minima.

<figure style="width: 800px">
	<img src="/media/deep learning/slope-signs-2.jpg" alt="Sign of a slope">
	<figcaption>Sign of the slope</figcaption>
</figure>

The sign of the partial derivative decides the direction of the step. If the slope is positive, then the step is positive, and the parameter value is decreased.

$$
Q_{new} = Q_{old} - \underbrace{ \alpha \underbrace{ \text { positive} }_{\text{slope}} }_{\text{step}}
$$

If the slope is negative, then the step is negative, and the parameter value is increased.

$$
Q_{new} = Q_{old} - \underbrace{ \alpha \underbrace{ \text { negative} }_{\text{slope}} }_{\text{step}}
$$

The optimal learning rate will be dependent on the shape of the function $f$. In deep learning, the shape of $f$ depends on the examples available in the dataset and how it gets processes by the model architecture.

It is important to note that the step size decreases as we go through the iterations, due to the decrease in slope as we get closer to the minima. This reduces the chance of overshooting the minima.

# Improvements

Gradient Descent is designed to find a minima, but it does not *necessarily* find a global minima.

It works well with smooth functions like the one used above. But if the function is very complex with many local minima, then ensuring that gradient descent finds the *global* minima is difficult.

One approach to this problem is *momentum*.

## Gradient Descent with Momentum

In standard gradient descent we use the immediate gradient at each iteration. Instead, we can use the average gradient over the previous $n$ steps, to maintain  we're able to keep momentum when we approach local optima.

As you approach the minima the gradient will get smaller but not as drastically as when using the immediate gradient. This improves the speed of convergence.

# References

- [Gradient](https://en.wikipedia.org/wiki/Gradient)
- [Gradient descent, Jeremy Jordan](https://www.jeremyjordan.me/gradient-descent/)
- [Gradient Descent, Step-by-Step](https://youtu.be/sDv4f4s2SB8)
- [Michael Nielsen](http://neuralnetworksanddeeplearning.com)
- [Wikipedia: Learning rate](https://en.wikipedia.org/wiki/Learning_rate)
