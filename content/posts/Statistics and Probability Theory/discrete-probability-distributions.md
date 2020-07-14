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
- Multinomial Distribution
- Hypergeometric distribution
- Multivariate Hypergeometric distribution
- Geometric distribution
- Poisson Distribution

# Bernoulli distribution

Bernoulli distribution is used to model a *single trial* of an experiment with only *two* possible outcomes. The outcomes are often encoded as $1$ and $0$, success and failure.

A **bernoulli trial** is a random experiment with exactly two possible outcomes, "success" and "failure". The probability of success is the same every time the experiment is conducted.

The PMF of a random variable $X$ describing a Bernoulli trial is given by,

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

Binomial distribution models the number of successes $x$ in $n$ independent trials. The PMF of a binomial random variable $X$ is given by,

$$
P(X = x) = \begin{pmatrix} n \\ x \end{pmatrix} p^x (1 - p)^{n - x}
$$

where, the random variable $X$ holds the number of successes. $\begin{pmatrix} n \\ x \end{pmatrix}$ is called the **binomial coefficient** and is defined as,

$$
\begin{pmatrix} n \\ x \end{pmatrix} = \frac {n!} {x! (n - x)!}
$$

The second part, $p^x (1 - p)^{n - x}$, gives you the probability for a particular sequence of successes and failures. Multiplying this by the binomial coefficient gives the total probability for any sequence with the same number of successes and failures.

## Expectation

Let $U_1, U_2, \cdots, U_n$ be independent Bernoulli random variables.

$$
\begin{aligned}
E[U_i] &= p
\\\\
Var[U_i] &= p (1 - p)
\end{aligned}
$$

The binomial random variable can be thought of as the sum of $n$ Bernoulli random variables.

$$
\begin{aligned}
X &= U_1 + U_2 + \cdots + U_n
\\\\
E[X] &= E[U_1 + U_2 + \cdots + U_n]
\\
&= E[U_1] + E[U_2] + \cdots + E[U_n]
\\
&= p + p + \cdots + p
\\
&= np
\end{aligned}
$$

## Variance

Variance follows similar reasoning,

$$
\begin{aligned}
X &= U_1 + U_2 + \cdots + U_n
\\\\
Var[X] &= Var[U_1 + U_2 + \cdots + U_n]
\\
&= Var[U_1] + Var[U_2] + \cdots + Var[U_n]
\\
&= p(1 - p) + p(1 - p) + \cdots + p(1 - p)
\\
&= np(1 - p)
\end{aligned}
$$

# Multinomial Distribution

The multinomial distribution is a generalization of the binomial distribution that allows for more than $2$ outcomes.

The multinomial random variable $X$ represents the number of occurrences of outcome $i$. The PMF is given by,

$$
P(X_1 = x_1, \cdots, X_n = x_n)
=
\frac {n!} {x_1! \cdots x_n!} p_1^{\normalsize x_1} \cdots p_k^{\normalsize x_k}
$$

# Hypergeometric distribution

Hypergeometric distribution models the probability of randomly selecting $x$ successes from a population size $N$ *without* replacement. Each draw is either a success or a failure. Since it is done without replacement, the probability of each successive draw changes.

This stands in contrast to binomial distribution which describes the probability of $x$ successes in $n$ trials *with* replacement. The probability in each trial remains constant.

The hypergeometric random variable $X$ holds the number of successes $x$ in the drawn sample. Its PMF is given by,

$$
P(X = x)
=
\frac
{\begin{pmatrix} a \\ x \end{pmatrix} \begin{pmatrix} N - a \\ n - x \end{pmatrix} }
{\begin{pmatrix} N \\ n \end{pmatrix}}
$$

where $a$ is the total number of successes in the population and $n$ is the number of draws.

# Multivariate Hypergeometric distribution

This is a generalization of hypergeometric distribution to support more than $2$ outcomes.

$$
P(X = x)
=
\frac
{ \Pi_i \begin{pmatrix} n_i \\ x_i \end{pmatrix}}
{\begin{pmatrix} N \\ x \end{pmatrix}}
$$

where $n_i$ is the total number of items of type $i$ available in the population, $x_i$ is the number of items of each type chosen, $N$ is the size of the population and $x$ is the total number of items chosen, $x_1 + x_2 + \cdots$.

# Geometric distribution

The geometric distribution models the number of trials needed to reach the first success in a series of independent Bernoulli trials.

The PMF of a geometric random variable is given by,

$$
P(X = x) = (1 - p)^{x - 1} p
$$

where $p$ is the probability of the success event.

The first part of the equation $(1 - p)^{x - 1}$ gives you the probability that the initial $x - 1$ trials are failures. The second part $p$ tells you the probability that the x*th* trial is a success.

Together, they tell you the probability of $x - 1$ failures followed by a success.

The expectation in defined by,

$$
E[X] = \frac {1}{p}
$$

[Proof](https://youtu.be/7br_-emGNec)

The variance is given by,

$$
Var[X] = \frac {1 - p} {p^2}
$$

# Poisson Distribution

The Poisson distribution expresses the probability of a given number of events occurring in a fixed interval of time, distance, etc.

$$
P(X = x) = \frac {\lambda^x e^{- \lambda}}{x!}
$$

where $\lambda = E[X] = Var[X]$ and $x$ is the number of events.

The expectation of a Poisson random variable is given by,

$$
\begin{aligned}
E[X] &= \sum_x x \space p(x)
\\\\
&= \sum_{x = 0}^\infty x \frac {\lambda^x e^{- \lambda}}{x!}
\\\\
&= e^{- \lambda} \sum_{x = 0}^\infty x \frac {\lambda^x}{x!}
\\\\
&= \lambda e^{- \lambda} \sum_{x = 1}^\infty \frac {\lambda^{\normalsize (x - 1)}}{(x - 1)!}
\end{aligned}
$$

Using the following series expansion,

$$
e^a = \sum_{y = 0}^{\infty} \frac {a^y} {y!}
$$

we simplify the expectation,

$$
\begin{aligned}
E[X] &= \lambda e^{- \lambda} e^{\lambda}
\\
&= \lambda e^{- \lambda + \lambda}
\\
&= \lambda e^0
\\
&= \lambda
\end{aligned}
$$

## Variance

$$
Var[X] = \lambda
$$

- [Deriving the Mean and Variance](https://youtu.be/65n_v92JZeE)
- [The Relationship Between the Binomial and Poisson Distributions](https://youtu.be/eexQyHj6hEA)

# References

- [Wikipedia : Probability distribution](https://en.wikipedia.org/wiki/Probability_distribution)
- [JB statistics : Introduction to the Bernoulli Distribution](https://youtu.be/bT1p5tJwn_0)
- [Wikipedia : Bernoulli trial](https://en.wikipedia.org/wiki/Bernoulli_trial)
- [Wikipedia : Binomial coefficient](https://en.wikipedia.org/wiki/Binomial_coefficient)
- [JB statistics : An Introduction to the Binomial Distribution](https://youtu.be/qIzC1-9PwQo)
- [JB statistics : Introduction to the Multinomial Distribution](https://youtu.be/syVW7DgvUaY)
- [The Normal Approximation to the Binomial Distribution](https://youtu.be/CCqWkJ_pqNU)