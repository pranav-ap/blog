---
title: "The Fundamentals of Probability Theory"
date: "2019-11-1"
template: "post"
draft: false
slug: "/posts/probability-theory-fundamentals/"
category: "Statistics and Probability Theory"
tags:
 - ""
description: ""
---

**Probability theory** is a mathematical framework for quantifying uncertainty. It is widely in game theory and artificial intelligence.

# Table of Contents

- Random Experiment
- Types of Events
- Probability of an Event
- Conditional Probability
- Sum and Product Rules
- Total Probability Theorem
- Independence
- Bayes Theorem
- Random Variables
- Probability Distribution Functions
	- Probability Mass Function
	- Probability Density Function
	- Cumulative Distribution Function
- Expectation of a function
- Variance of a function
- Total Expectation Theorem
- Covariance

# Random Experiment

A **random experiment** is an trial or observation that can be repeated multiple times under the same set of conditions.

All possible outcomes are *known* in advance. The occurrence of each of these outcomes depend on *random chance* and are *independent* of previous outcomes.

A **sample space** or **possibility space** is a set of elements that represent *all* possible outcomes of a random experiment.

<figure style="width: 420px">
	<img src="/media/statistics and probability theory/sample-space.png" alt="Sample space">
	<figcaption>Sample space</figcaption>
</figure>

A sample space is denoted using set $S$, where all possible outcomes are listed as its elements. The sample space for rolling a single six-sided die is $\{ 1, 2, 3, 4, 5, 6 \}$.

Each element of the sample space is called a **sample point**. Any subset of sample points is collectively called an **event** $E$.

# Types of Events

An **independent event** is an event that is not affected by any other events. A coin does not "know" that it came up heads previously. Each coin toss is a isolated event.

A **dependent event** is an event that is affected by other events. For example, consider removing colored marbles from a bag. Each time you remove a marble the chances of drawing out a certain color will change.

Two events A and B are **mutually exclusive** if both events can't happen at the same time. For example, on tossing a coin, heads and tails are mutually exclusive events.

# Probability of an Event

The **probability** of an event is a number indicating how likely that event is to occur. This number is always between $0$ and $1$, where $0$ indicates impossibility and $1$ indicates certainty.

When a single die is thrown, there are $6$ possibilities and the all of them are equally likely to occur. We need a formula that assigns a numeric value to each of them.

Since a probability of $1$ represents certainty, this formula must divide certainty *equally* among all the sample points.

<figure style="width: 420px">
	<img src="/media/statistics and probability theory/discrete-uniform-law.png" alt="Discrete uniform law">
	<figcaption>Discrete uniform law</figcaption>
</figure>

In general, if all sample points are equally likely to occur, the probability of an event $A$ is,

$$
P(A) = \frac {\text{Number of occurrences of A}} {\text{Total number of Trials}}
$$

So, the probability of getting a $5$ on throw of a die, is $1 / 6$.

# Conditional Probability

The probability that event $A$ occurs, given that event $B$ has occurred, is called **conditional probability**. The conditional probability of $A$, given $B$, is denoted by $P(A \mid B)$.

<figure style="width: 420px">
	<img src="/media/statistics and probability theory/conditional-discrete-uniform-law.png" alt="Conditional discrete uniform law">
	<figcaption>Conditional discrete uniform law</figcaption>
</figure>

In the above venn diagram, $P(A) = 4 / 10$ and $P(B) = 2 / 10$. But once we know that $A$ has occurred we must only consider the sample points in the red circle. This is our new sample space. Therefore, the $P(B \mid A) = 2 / 4$.

Generally, it can be written as,

$$
P(B \mid A) = \frac {P(A \cap B)} {P(A)}
$$

Note that conditional probability is not defined if $A$ has no chance of occurring.

# Sum and Product Rules

Consider two random variables $X$ and $Y$, that take some value $x_i$ and $y_j$ respectively.

<figure style="width: 390px">
	<img src="/media/statistics and probability theory/sum-product-rules.png" alt="Grid of probabilities">
	<figcaption>Grid of probabilities</figcaption>
</figure>

We can draw a grid where each box holds the number of trials where $X = x_i$ and $Y = y_j$. The number of trials in each box is denoted by $n_\text{ij}$.

The probability that $X$ will take value $x_i$, and $Y$ will take value $y_i$ simultaneously is called **joint probability**. It is denoted as $P(X = x_i, Y = y_i)$ or $P(x, y)$.

$$
P(X = x_i, Y = y_i) = \frac { n_\text{ ij} } {N}
$$

where $N$ is the total number of trials.

Note that joint probability is symmetric. This means

$$
P(X = x_i, Y = y_i) = P(Y = y_i, X = x_i)
$$

This is because both of them point to the same box in the grid.

Sometimes we know the joint probability distribution over a set of variables, and may want to know the probability of a subset of these random variables taking on some values. The is calculated using **marginal probability**. It is denoted by $P(X = x_i)$ and is informally represented by,

$$
P(X = x_i) = \frac { c_i } {N}
$$

Formally, it can be represented as a simple summation,

$$
P(X = x_i) = \sum_y P(X = x_i, Y = y_i)
$$

Marginal probability is also called the **sum rule** of probability.

We now derive the **product rule**. Lets start with the formula for joint probability,

$$
\begin{aligned}
   P(X = x_i, Y = y_i) &= \frac { n_\text{ ij} } {N} \\\\
   &= \frac {n_\text{ ij}} {c_i} \cdot \frac {c_i} {N}
\end{aligned}
$$

Here, we substitute the formula for conditional and marginal probability,

$$
P (X = x_i, Y = y_i) = P (Y = y_i \mid X = x_i) \space P (X = x_i)
$$

The product can be generalized to $n$ number of terms. This is called the **chain rule**. It is a way to split a joint probability into a condition probability and a smaller joint probability. This smaller joint probability can again be split.

$$
P (X_n, \ldots, X_0)
=
P (X_n \mid X_{n-1}, \ldots, X_0) \space
P (X_{n-1} \mid X_{n-2}, \ldots, X_0)
\ldots
P (X_0)
$$

# Total Probability Theorem

<figure style="width: 420px">
	<img src="/media/statistics and probability theory/total-probability-theorem.png" alt="Total Probability Theorem">
	<figcaption>Total Probability Theorem</figcaption>
</figure>

The total probability theorem tells us the probability of an event $B$ that is partitioned into multiple other events $A_i$.

<figure style="width: 420px">
	<img src="/media/statistics and probability theory/total-probability-theorem-tree.png" alt="Total Probability Theorem Tree">
	<figcaption>Total Probability Theorem Tree</figcaption>
</figure>

$$
P(B) = P(B \cap A_1) + P(B \cap A_2) + P(B \cap A_3)
$$

This can be expressed in terms of conditional probabilities.

$$
P(B) = P(A_1) P(B \mid A_1) + P(A_2) P(B \mid A_2) + P(A_3) P(B \mid A_3)
$$

More generally $P(B)$ is written as,

$$
P(B) = \sum_i P(A_i) \space P(B \mid A_i)
$$

# Independence

Two events $A$ and $B$ are **independent** if the occurrence of one does not affect the probability of occurrence of the other. It is denoted by $A \perp B$.

$$
P(A \mid B) = P(A)
$$

Because of this, the probability of them occurring simultaneously is,

$$
P(A \cap B) = P(A) \space P(B)
$$

This can be extended for multiple independent events,

$$
P(A \cap B \cap C \cap \cdots) = P(A) \space P(B) \space P(C) \space \cdots
$$

# Bayes Theorem

**Bayes theorem** lets us update our beliefs based on new evidence.

We know that the probability of $B$ given $A$ is,

$$
P(B \mid A) = \frac {P(A \cap B)} {P(A)}
$$

The probability of $A$ given $B$ is,

$$
P(A \mid B) = \frac {P(B \cap A)} {P(B)}
$$

Due to symmetry of joint probabilities, $P(A \cap B) = P(B \cap A)$, we can expand and get,

$$
\begin{aligned}
P(B \mid A) \space P(A) &= P(A \mid B) \space P(B) \\\\
P(A \mid B) &= \frac { P(B \mid A) \space P(A) }{P(B)}
\end{aligned}
$$

where $A$ and $B$ are events, and $P(B) \ne 0$

Note that $P(B)$ can be represented in terms of the quantities appearing in the numerator, using the total probability theorem.

So Bayes theorem is defined as,

$$
P (A \mid B) = \frac { P(A) \space P(B \mid A) } { \sum_i P(A_i) \space P(B \mid A_i) }
$$

- $P(A)$ is called the **prior probability** of $A$. This is the probability of $A$ before we consider the evidence.
- $P (A \mid B)$ is called the **posterior**. This is the updated probability of $A$.
- $P (B \mid A)$ is called the **likelihood**. This is the probability of observing the new evidence, given our initial hypothesis.
- $P(B)$ is the probability of observing the evidence $B$.

Let $A$ be an event where you have malaria, and $B$ an event where you have high fever as a symptom.

$P(A)$ is the probability of any person in the population having malaria. $P(B)$ is the probability of any person in the population getting high fever.

$P (A \mid B)$ is the probability of you having malaria given that you have a fever. $P (B \mid A)$ is the probability that you will have high fever, in case you have malaria.

# Random Variables

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

# Probability Distribution Functions

A **probability distribution** is a function that gives the probability of occurrence of the different possible outcomes of an experiment.

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

# Covariance

**Covariance** tells us the direction of the linear relationship between two random variables. It is denoted by $\text{Cov}_{X \sim P, Y \sim P}(X, Y)$.

<figure style="width: 460px">
	<img src="/media/statistics and probability theory/covariance.png" alt="Covariance">
	<figcaption>Covariance</figcaption>
</figure>

A **positive** covariance means that when one variable increases the other also increases. A **negative** covariance means that when one variable increases the other decreases. It is defined as,

$$
\text{Cov}(X, Y) = E[(X - E[X])(Y - E[Y])]
$$

You can simplify this,

$$
\begin{aligned}
\text{Cov}(X, Y) &= E[XY - X \space E[Y] - Y \space E[X] + E[X] E[Y]]
\\
&= E[XY] - E[X \space E[Y]] - E[Y \space E[X]] + E[E[X] \space E[Y]]
\\
&= E[XY] - E[X] E[Y] - E[Y] E[X] + E[X] E[Y]
\\
&= E[XY] - E[X] E[Y]
\end{aligned}
$$





# References

- [MIT Introduction to Probability](https://www.youtube.com/playlist?list=PLUl4u3cNGP60hI9ATjSFgLZpbNJ7myAg6)
- [Math is Fun : Random Variables](https://www.mathsisfun.com/data/random-variables.html)
- [Stat Trek : Probability](https://stattrek.com/probability/probability-rules.aspx?tutorial=prob)
- [Math Antics : Basic Probability](https://www.youtube.com/watch?v=KzfWUEJjG18)
- [Conditional probability explained visually (Bayes' Theorem)](https://www.youtube.com/watch?v=Zxm4Xxvzohk)
- [Bayes theorem](https://www.youtube.com/watch?v=OqmJhPQYRc8)
- [Random Variables: Khan Academy](https://www.youtube.com/watch?v=3v9w79NhsfI)
- [Discrete Probability Distribution: Khan Academy](https://www.khanacademy.org/math/statistics-probability/random-variables-stats-library/random-variables-discrete/v/discrete-probability-distribution)
- [Expected value of a discrete random variable](https://www.khanacademy.org/math/statistics-probability/random-variables-stats-library/random-variables-discrete/v/expected-value-of-a-discrete-random-variable)
- [Variance and standard deviation of a discrete random variable](https://www.khanacademy.org/math/statistics-probability/random-variables-stats-library/random-variables-discrete/v/variance-and-standard-deviation-of-a-discrete-random-variable)
- [Stack Overflow : Chain rule](https://math.stackexchange.com/questions/228811/understanding-the-chain-rule-in-probability-theory)
- [MIT : Expectation](https://youtu.be/_yJsO5955ZE?list=PLUl4u3cNGP60hI9ATjSFgLZpbNJ7myAg6)
