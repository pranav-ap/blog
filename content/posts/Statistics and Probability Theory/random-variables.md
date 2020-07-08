---
title: "Random Variables"
date: "2019-11-1"
template: "post"
draft: false
slug: "/posts/random-variables/"
category: "Statistics and Probability Theory"
tags:
 - ""
description: ""
---

A **random variable** is a variable that randomly takes on a value based on the outcome of a random experiment.

<figure style="width: 390px">
	<img src="/media/statistics and probability theory/random-variable.png" alt="Random Variable">
	<figcaption>Random Variable X for a coin toss experiment</figcaption>
</figure>

We can have a random variable $X$ that takes on the value of $0$ for a heads outcome, and $1$ for a tails outcome. The values $0$ and $1$ can be replaced by any number we want.

We define another random variable $Y$ where,

$$
Y = \text{number of heads after 5 flips of a fair coin}
$$

This takes on values from $\{ 0, 1, 2, 3, 4, 5 \}$.

We can define multiple random variables over the same sample space. These variables can also be dependent on each other. For example, for a random variable $X$ can be defined as $X = Y + 2$, where $Y$ is another random variable.

## Types of random variables

A random variable can be **discrete** or **continuous**.

A **discrete random variable** can only take on certain discrete values. For example, an element from a set of numbers or names.

A **continuous random variable** can take any value within a range of values. For example, a person's height or weight.

Some outcomes of an experiment are more likely than others, and similarly some values for a random variable are more likely than others. The PMF, PDF and CDF are ways to quantify that.

# Calculating Probability of Random Variables

You have three options:

- Probability Mass Function
- Probability Density Function
- Cumulative Distribution Function

## Probability Mass Function

The probability distribution of discrete random variables is described using a **probability mass function** (PMF).

<figure style="width: 700px">
	<img src="/media/statistics and probability theory/pmf balls.svg" alt="PMF">
	<figcaption>PMF</figcaption>
</figure>

In the above figure, we have two blue balls, a red ball and a yellow ball and the experiment is to just pick a ball at random blind-folded. The outcome of the experiment is stored in the random variable $X$. Since the outcome where we pick a blue ball is higher, this must get reflected in the PMF.

The PMF of a random variable $X$ taking on a value $x$ is denoted by $P(X = x)$ or $p_X(x)$.

- $\forall x \in X$, $p_X(x) \le 1$. An impossible event has a probability of $0$ and a guaranteed event has a probability of $1$, and everything else falls in between.
- $\underset{x}{\sum} p_X(x) = 1$. This ensures that the probabilities of various values are normalized.

<figure style="width: 700px">
	<img src="/media/statistics and probability theory/pmf-example.png" alt="PMF Example">
	<figcaption>PMF Example</figcaption>
</figure>

[Example](https://youtu.be/Qx2NKaUCUw0)

If you want to find the probability of a collection of discrete values, you just need to calculate the PMF for each discrete value and add them all up. It is denoted by,

$$
P(a < X < b)
=
\underset{x : a < x < b}{\sum} p_X(x)
$$

*Conditional* PMF works similar to normal conditional probability and is denoted by $P_{X \mid A} (x)$ and is defined by,

$$
P_{X \mid A} (x)
=
\underset{x}{\sum} p_X(x)
$$

## Probability Density Function

The probability distribution of continuous random variables is described using a **probability density function** (PDF).

<figure style="width: 700px">
	<img src="/media/statistics and probability theory/pdf.png" alt="PDF">
	<figcaption>PDF</figcaption>
</figure>

The PDF of a random variable $X$ is denoted by $f(X)$. Since it works on continuous random variables, $f(X)$ considers a range of values as its input.

The probability of $X$ taking on a value between $a$ and $b$ is,

$$
P(a < X < b)
=
\int_a^b f_X(x) \space dx
$$

- $\int_a^b f_X(x) \le 1$. An impossible event has a probability of $0$ and a guaranteed event has a probability of $1$, and everything else falls in between.
- $\int f_X(x) \space dx = 1$. This ensures that the probabilities of various values are normalized.

<figure style="width: 700px">
	<img src="/media/statistics and probability theory/pdf-example.png" alt="PDF Example">
	<figcaption>PDF Example</figcaption>
</figure>

## Cumulative Distribution Function

The **cumulative distribution function** provides the probability that $X$ will take a value less than or equal to $x$. It can be used by both discrete and continuous random variables. It is denoted by $F_X(x) = P(X \le x)$.

For a discrete random variable $X$,

$$
F_X(x) = P(X \le x) = \sum_{k \le x} p_X(k)
$$

For a continuous random variable $X$,

$$
F_X(x) = P(X \le x) = \int_{-\infty}^x f_X(t) \space dt
$$

[CDF MIT](https://youtu.be/4QeL1ma_XJ0)

# Expectation of a function

The **expectation** of a function $g(x)$ with respect to a probability distribution $P(x)$ is the mean value that $g$ takes on when $x$ is drawn from $P$. In other words, it is the probability weighted average of $g(x)$. It is denoted by $E_{x \in P}[g(x)]$ or $\mu_X$.

In case of discrete random variables, it is the probability-weighted average of all its possible values.

$$
E_{X \sim P}[g(x)] = \sum_x g(x) \space p_X(x)
$$

And for continuous random variables,

$$
E_{X \sim P}[g(x)] = \int g(x) \space f_X(x) \space dx
$$

[Khan Academy : Example](https://youtu.be/qafPcWNUiM8)
[Patrick JMT : Example](https://youtu.be/DAjVAEDil_Q)

Let's understand why this equation is the mean of a random variable.

<figure style="width: 700px">
	<img src="/media/statistics and probability theory/expectation derive.png" alt="Expectation informal derivation">
	<figcaption>Expectation informal derivation</figcaption>
</figure>

### Properties of Expectation

- **Non-negativity** : If $\forall x \in X \ge 0$, then $E_{X \sim P}[X] \ge 0$
- **Monotonicity** : If $X \le Y$, then $E[X] \le E[Y]$
- **Range of an expectation** : If $a \le X \le b$, then $a \le E_{X \sim P}[X] \le b$
- **Expectation of a constant** :

$E_{X \sim P}[c] = c$, where $c$ is a constant. Note that $E[E[X]] = E[c]$, since $E[X]$ is just a constant value.

[Khan Academy](https://youtu.be/ualmyZiPs9w)

- **Linearity of Expectations**

Expectations are linear. This means the a term like $E_{X \sim P}[\alpha \space g(x) + \beta]$ can be simplified as,

$$
E_{X \sim P}[\alpha \space g(x) + \beta]
=
\alpha \space E_{X \sim P}[g(x)]
+
\beta
$$

where $\alpha$ and $\beta$ are not dependent on $x$. This property even works for multiple random variables. For example,

$$
E_{X \sim P, Y \sim P}[X + Y] = E_{X \sim P}[X] + E_{Y \sim P}[Y]
$$

[Proof](https://youtu.be/0IJFBMIU6x4?list=PLUl4u3cNGP60hI9ATjSFgLZpbNJ7myAg6)

<figure style="width: 650px">
	<img src="/media/statistics and probability theory/expectation-variance-discrete.png" alt="Expectation, Variance and Standard Deviation of RV">
	<figcaption>Expectation, Variance and Standard Deviation of a RV</figcaption>
</figure>

# Variance of a function

**Variance** is a measure of spread of the values of a random variable around $E(X)$. It is denoted by $Var(X)$ or $\sigma_X^2$.

$$
\begin{aligned}
   Var (x) &= E [(x - E[x])^2] \\\\

	&= \sum_x (x - E[x] )^2 \space p(x)
\end{aligned}
$$

This can be written as,

$$
Var(x) = E[x^2] - E[x]^2
$$

**Standard deviation** is simply the square root of the variance. It is denoted by $\sigma_X$.

$$
\sigma_X = \sqrt {Var(X)}
$$

# Total Expectation Theorem

This is a random variable analogy to the Total Probability Theorem, which is,

$$
P(B) = P(A_1) P(B \mid A_1) + \cdots + P(A_n) P(B \mid A_n)
$$

Writing this in terms of PMF,

$$
p_X(x) = P(A_1) \space p_{X \mid A_1}(x) + \cdots + P(A_n) \space p_{X \mid A_n}(x)
$$

Multiply both sides by $\sum_x x$,

$$
\begin{aligned}

\sum_x x \space p_X(x)
&=
P(A_1) \sum_x x \space p_{X \mid A_1}(x)
+
\cdots
+
P(A_n) \sum_x x \space p_{X \mid A_n}(x)

\\\\

E_{X \sim P}[X]
&=
P(A_1) \space E_{X \sim P}[X \mid A_1]
+
\cdots
+
P(A_n) \space E_{X \sim P}[X \mid A_n]

\end{aligned}
$$

# References

- [Math is Fun : Random Variables](https://www.mathsisfun.com/data/random-variables.html)
- [Random Variables: Khan Academy](https://www.youtube.com/watch?v=3v9w79NhsfI)
- [Discrete Probability Distribution: Khan Academy](https://www.khanacademy.org/math/statistics-probability/random-variables-stats-library/random-variables-discrete/v/discrete-probability-distribution)
- [Expected value of a discrete random variable](https://www.khanacademy.org/math/statistics-probability/random-variables-stats-library/random-variables-discrete/v/expected-value-of-a-discrete-random-variable)
- [Variance and standard deviation of a discrete random variable](https://www.khanacademy.org/math/statistics-probability/random-variables-stats-library/random-variables-discrete/v/variance-and-standard-deviation-of-a-discrete-random-variable)
- [MIT : Expectation](https://youtu.be/_yJsO5955ZE?list=PLUl4u3cNGP60hI9ATjSFgLZpbNJ7myAg6)
