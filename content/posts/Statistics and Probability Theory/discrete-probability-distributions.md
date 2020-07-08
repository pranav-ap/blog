---
title: "Discrete Probability Distributions"
date: "2020-7-8"
template: "post"
draft: false
slug: "/posts/discrete-probability-distributions/"
category: "Statistics and Probability Theory"
tags:
 - ""
description: ""
---

A **probability distribution** is a function that gives the probability of occurrence for all possible outcomes of an experiment.

A **discrete probability distribution** is a probability distribution that can take on a countable number of values. They are described using a probability mass function.

Some examples of discrete probability distributions include:

- Bernoulli distribution
- Binomial distribution
- Geometric distribution

# Bernoulli distribution

Bernoulli distribution is used to model a *single trial* of an experiment with only *two* possible outcomes. The outcomes are often encoded as $1$ and $0$, success and failure.

A **bernoulli trial** is a random experiment with exactly two possible outcomes, "success" and "failure". The probability of success is the same every time the experiment is conducted.

A random variable $X$ describing a Bernoulli trial is given by,

$$
P(X = x) = p_X(x) =

\begin{cases}
   p &\text{if } x = 1 \\
   1 - p &\text{if } x = 0
\end{cases}
$$

This can also be written as,

$$
p_X(x) = p^k (1 - p)^{1 - k}
$$

The Bernoulli distribution is a special case of the binomial distribution where a single trial is conducted. Many distributions are built on the assumption of independent Bernoulli trials.

<figure style="width: 450px">
	<img src="/media/statistics and probability theory/random-variable.png" alt="Random Variable">
	<figcaption>Random Variable X for a coin toss experiment</figcaption>
</figure>

The expected value of a Bernoulli random variable $X$ is,

## Expectation

The expectation or mean can be easily derived as follows,

$$
\begin{aligned}
E[X] &= P(X = 1) \cdot 1 + P(X = 0) \cdot 0
\\
&= p \cdot 1 + (1 - p) \cdot 0
\\
&= p
\end{aligned}
$$

## Variance

The general formula for variance is,

$$
Var[X] = E[X^2] - E[X]^2
$$

First, let us find $E[X^2]$,

$$
\begin{aligned}
E[X^2] &= P(X = 1) \cdot 1^2 + P(X = 0) \cdot 0^2
\\
&= p \cdot 1 + (1 - p) \cdot 0
\\
&= p
\end{aligned}
$$

Substitute in the general equation,

$$
\begin{aligned}
Var[X] &= E[X^2] - E[X]^2
\\
&= p - p^2
\\
&= p(1 - p)
\end{aligned}
$$

# Binomial distribution

Binomial distribution models the number of successes $k$ in $n$ independent trials.

$$
P(X = k) = \begin{pmatrix} n \\ k \end{pmatrix} p^k (1 - p)^{n - k}
$$

where, the random variable $X$ holds the number of successes. $\begin{pmatrix} n \\ k \end{pmatrix}$ is called the **binomial coefficient** and is defined as,

$$
\begin{pmatrix} n \\ k \end{pmatrix} = \frac {n!} {k! (n - k)!}
$$

# Geometric distribution

# References

- [Wikipedia : Probability distribution](https://en.wikipedia.org/wiki/Probability_distribution)
- [JB statistics : Introduction to the Bernoulli Distribution](https://youtu.be/bT1p5tJwn_0)
- [Wikipedia : Bernoulli trial](https://en.wikipedia.org/wiki/Bernoulli_trial)
- [Wikipedia : Binomial coefficient](https://en.wikipedia.org/wiki/Binomial_coefficient)
