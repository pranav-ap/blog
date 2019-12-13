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

**Probability theory** is a mathematical framework for quantifying uncertainty. It is used widely in game theory and artificial intelligence.

# Random experiment

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

Since a probability of $1$ represents certainty, this formula must divide certainty *equally* among all the sample points like a pie.

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

Note that we can have multiple random variables defined over a sample space.

## Types of random variables

A random variable can be **discrete** or **continuous**.

A **discrete random variable** can only take on certain discrete values. For example, an element from a set of numbers or names.

A **continuous random variable** can take any value within a range of values. For example, a person's height or weight.

# Probability Mass Function

The probability distribution of discrete random variables is described using a **probability mass function** (PMF).

The PMF of a random variable $X$ is denoted by $P(X)$. The probability of $X$ taking on a value $x$ is denoted by $P(X = x)$ or $P(x)$.

- The domain of $P(X)$ is the set of all possible states of $X$.
- $\forall x \in X$, $P(x) \le 1$. An impossible event has a probability of $0$ and a guaranteed event has a probability of $1$, and everything else falls in between.
- $\sum_{x \in X} P(x) = 1$. This ensures that the probabilities of various values are normalized.

<figure style="width: 700px">
	<img src="/media/statistics and probability theory/pmf-example.png" alt="PMF Example">
	<figcaption>PMF Example</figcaption>
</figure>

# Probability Density Function

The probability distribution of continuous random variables is described using a **probability density function** (PDF).

The PDF of a random variable $X$ is denoted by $p(X)$. The probability of $X$ taking on a value $x$ is denoted by $p(X = x)$ or $p(X)$.

- The domain of $p(X)$ is the set of all possible states of $X$.
- $\forall x \in X$, $p(x) \le 1$. An impossible event has a probability of $0$ and a guaranteed event has a probability of $1$, and everything else falls in between.
- $\int p(x) \space dx = 1$. This ensures that the probabilities of various values are normalized.

<figure style="width: 700px">
	<img src="/media/statistics and probability theory/pdf-example.png" alt="PDF Example">
	<figcaption>PDF Example</figcaption>
</figure>

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
P(X = x_i, Y = y_i) = (Y = y_i, X = x_i)
$$

This is because both of them point to the same box in the grid.

Sometimes we know the joint probability distribution over a set of variables, and may want to know the probability of a subset of these random variables taking on some values. The is calculated using **marginal probability**. It is denoted by $P(X = x_i)$.

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

Imagine that we are trying to find the probability that a person has cancer. Initially, we say it is whatever percent of the population has cancer. However, given new evidence that the person is a smoker, we can improve our probability estimation.

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

# Expectation, Variance and Standard Deviation of a Random Variable

**Expectation** or **expected value** of a random variable $X$ is the *mean* value that it is most likely to hold after the associated trial. It is denoted by $E(X)$ or $\mu_x$.

In case of discrete random variables, it is the probability-weighted average of all its possible values.

$$
E(X) = \sum_i x_i \space p(x_i)
$$

And for continuous random variables,

$$
E(X) = \int x \space p(x) \space dx
$$

**Variance** is a measure of spread of the values of a random variable around $E(X)$. It is denoted by $Var(X)$ or $\sigma^2$.

$$
\begin{aligned}
   Var (X) &= E [(X - \mu)^2] \\\\

	&= \sum_i ( x_i - \mu )^2 \space p(x_i)
\end{aligned}
$$

**Standard deviation** is simply the square root of the variance. It is denoted by $\sigma$.

$$
\sigma_X = \sqrt {Var(X)}
$$

<figure style="width: 650px">
	<img src="/media/statistics and probability theory/expectation-variance-discrete.png" alt="Expectation, Variance and Standard Deviation of RV">
	<figcaption>Expectation, Variance and Standard Deviation of a RV</figcaption>
</figure>

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
