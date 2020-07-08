---
title: "Basic Probability Theory"
date: "2019-11-1"
template: "post"
draft: false
slug: "/posts/probability-theory-basic/"
category: "Statistics and Probability Theory"
tags:
 - ""
description: ""
---

**Probability theory** is a mathematical framework for quantifying uncertainty. It is widely in game theory and artificial intelligence.

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
- [Stat Trek : Probability](https://stattrek.com/probability/probability-rules.aspx?tutorial=prob)
- [Math Antics : Basic Probability](https://www.youtube.com/watch?v=KzfWUEJjG18)
- [Conditional probability explained visually (Bayes' Theorem)](https://www.youtube.com/watch?v=Zxm4Xxvzohk)
- [Stack Overflow : Probability Chain rule](https://math.stackexchange.com/questions/228811/understanding-the-chain-rule-in-probability-theory)
