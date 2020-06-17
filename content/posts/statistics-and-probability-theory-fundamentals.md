---
title: "The Fundamentals of Statistics and Probability Theory"
date: "2019-11-1"
template: "post"
draft: false
slug: "/posts/statistics-and-probability-theory-fundamentals/"
category: "Statistics and Probability Theory"
tags:
 - ""
description: ""
---

Probability and statistics are two sides of the same coin. You cannot study one without the other. **Probability theory** is a mathematical framework for quantifying uncertainty, while **statistics** is concerned with the collection, analysis and presentation of data. They are widely in game theory and artificial intelligence.

# Table of Contents

- Statistics
	- Population and Samples
	- Statistical Distribution
	- Central Limit Theorem
	- Maximum Likelihood Estimation
- Probability Theory
	- Random Experiment
	- Types of Events
	- Probability of an Event
	- Conditional Probability
	- Sum and Product Rules
	- Total Probability Theorem
	- Independence
	- Bayes Theorem
	- Random Variables
	- Probability Mass Function
	- Probability Density Function
	- Expectation of a function
	- Variance of a function
	- Total Expectation Theorem
	- Cumulative Distribution Function
	- Covariance

# Population and Samples

The **population** is the complete set of observations or individuals that we *wish* to study. For example, if you want to know the average height of the Chinese, then all the Chinese people make up the population.

But it's impossible measure the heights of all these people. We can only measure the heights of some. A **sample** is a subset of the population, and is the set of observations we *actually use* for analysis. This sample is used to make estimations of the characteristics of the population.

<figure style="width: 900px">
    <img src="/media/statistics and probability theory/population-sample.png" alt="Sampling a Population">
    <figcaption>Sampling a Population</figcaption>
</figure>

There will be some inaccuracy in our conclusions about the population based upon a sample. This should be obvious - we have fewer members in our sample than our population therefore we have lost some information.

A characteristic of a population, such as the mean or standard deviation, is called a **parameter**; whereas a characteristic of a sample is called a **statistic**.

Parameters hold the true values of a real world distribution. A statistic is an estimate of a population parameter. In most cases, we only have access to a portion of the population distribution, so we almost always work with statistics.

# Statistical Distribution

It is important to remember that the sample we draw from the population is only one from a large number of *potential samples*. If ten researchers were all studying the same population, each will draw a different sample and thus may obtain different results after analysis.

<figure style="width: 700px">
    <img src="/media/statistics and probability theory/mean-and-std-dev.png" alt="Mean and Standard Deviation">
    <figcaption>Mean and Standard Deviation</figcaption>
</figure>

Data can be spread out or distributed in different ways and can have all kinds of interesting shapes. Distributions are defined by statistics like mean, variance and standard deviation.

## Mean

The **mean** tells you where the middle of distribution is. It is the sum of all measurements divided by the number of observations $N$ in the data set.

The population mean is denoted by $\mu$, and calculated using,

$$
\mu = \frac {\sum_i x_i} {N}
$$

The sample mean is denoted by $\overline{x}$, and estimated using,

$$
\overline{x} = \frac {\sum_i x_i} {N}
$$

## Variance

The variance measures how far the observations are spread out from their average observation. It is the average of the *squared differences* from the mean.

The population variance is denoted by $\sigma^2$. It is calculated using,

$$
\sigma^2 = \frac {\sum_i ( x_i - \mu )^2 } {N}
$$

The difference tells you how far away $x_i$ is from the mean, and squaring each term makes sure the distance is positive.

The sample variance is estimated using,

$$
s^2 = \frac { \sum_i ( x_i - \overline{x} )^2 } {N - 1}
$$

**Bessel's correction**

It refers to the use of $N - 1$ instead of $N$ in the formula for sample variance to get an better estimate of the population variance.

Lets start with,

$$
s^2 = \frac { \sum_i ( x_i - \overline{x} )^2 } {N}
$$

Using $\overline{x}$ in the square of differences will result in the smallest possible value. This is because it is equidistant from all other sample points $x_i$. Using any other value instead of $\overline{x}$ will result in a larger value.

Since $\mu \ne \overline{x}$, our current estimation $s^2$ is smaller than the population variance. Dividing by $n - 1$ increases $s^2$ to compensate for our use of $\overline{x}$.

[watch this](https://youtu.be/92s7IVS6A34?list=WL)

## Standard Deviation

Variance is measured in square units. This makes it difficult to reason with. So, we define the **standard deviation**, to measure the spread of data. It is simply the square root of the variance.

The population standard deviation is denoted by $\sigma$. It is calculated using,

$$
\sigma = \sqrt { \frac {\sum_i ( x_i - \mu )^2 } {N} }
$$

The sample standard deviation is denoted by $s$. It is estimated using,

$$
s = \sqrt { \frac {\sum_i ( x_i - \overline{x} )^2 } {N - 1} }
$$

## Standard Error

**Standard Error** measures the variation of a statistic calculated from multiple samples. It is simply the standard deviation of the distribution of a statistic.

The *standard error of the mean* is visualized below. You can calculate standard error for any statistic you wish.

<figure style="width: 600px">
    <img src="/media/statistics and probability theory/standard-error-of-mean.png" alt="Standard Error of Mean">
    <figcaption>Standard Error of Mean</figcaption>
</figure>

When the standard error increases, the means are more spread out; and it becomes more likely that any given mean is far from the population mean.

# Central Limit Theorem

The **Central Limit Theorem** states that the sample means $\overline{x}$ will be normally distributed for large samples from a population distribution; regardless of the type of the population distribution.

<figure style="width: 880px">
    <img src="/media/statistics and probability theory/central-limit-theorem.png" alt="Central Limit Theorem  demonstrated by various distributions">
    <figcaption>Central Limit Theorem demonstrated by various distributions</figcaption>
</figure>

Consider the following experiment,

1. Roll a die $20$ times and count the number of heads
2. Note down the sample mean
3. Repeat this multiple times

As this experiment is repeated, ie. the more samples we take, the graph showing the sample means will increasingly look normal.

The central limit theorem lets us continue performing statistical analysis even if we do not know the true form of the population distribution.

# Maximum Likelihood Estimation

**Likelihood** tells you how probable it is for a set of observations $O$ to came from a distribution $D$. It is denoted by $L ( D \mid O )$.

Since a distribution is described by its parameters or statistics like the mean and standard deviation we write likelihood as $L ( \mu = 15, \sigma = 2 \mid O )$. This denotes the likelihood of a distribution with a mean of $15$ and a standard deviation of $2$ given observations $O$.

<figure style="width: 650px">
	<img src="/media/statistics and probability theory/probability-vs-likelihood.png" alt="Probability vs Likelihood">
	<figcaption>Probability vs Likelihood</figcaption>
</figure>

Given a set of observations, **maximum likelihood estimation** (MLE) finds a distribution from which they were most likely sampled from. We must perform MLE for each and every statistic we wish to estimate.

## MLE for Mean

First we choose a distribution with a constant standard deviation $\sigma$. Then we vary the mean $\mu$, and calculate the likelihood. The mean that gives the maximum likelihood is called the *maximum likelihood estimate for the mean* $\mu_\text{MSE}$.

<figure style="width: 650px">
	<img src="/media/statistics and probability theory/mle.gif" alt="Maximum Likelihood Estimation for the mean">
	<figcaption>Maximum Likelihood Estimation for the Mean</figcaption>
</figure>

## MLE for Standard Deviation

Now that we have found the MLE for the mean, we can move onto estimating the standard deviation. Here we hold the $\mu_\text{MSE}$ constant and vary $\sigma$.

The standard deviation that results in the maximum likelihood is called *maximum likelihood estimate for standard deviation* $\sigma_\text{MSE}$.

<figure style="width: 650px">
	<img src="/media/statistics and probability theory/mle-std.png" alt="Maximum Likelihood Estimation for the Standard Deviation">
	<figcaption>Maximum Likelihood Estimation for the Standard Deviation</figcaption>
</figure>

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

# Probability Mass Function

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

# Probability Density Function

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

# Expectation of a function

The **expectation** of a function $g(x)$ with respect to a probability distribution $P(x)$ is the mean value that $g$ takes on when $x$ is drawn from $P$. It is denoted by $E_{x \in P}[g(x)]$ or $\mu_X$.

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

### Properties of Expectation

- **Non-negativity** : If $\forall x \in X \ge 0$, then $E_{X \sim P}[X] \ge 0$
- **Monotonicity** : If $X \le Y$, then $E[X] \le E[Y]$
- **Expectation of a constant** : $E_{X \sim P}[c] = c$, where $c$ is a constant
- **Range of an expectation** : If $a \le X \le b$, then $a \le E_{X \sim P}[X] \le b$

**Linearity of Expectations**

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
   Var (f(x)) &= E [(f(x) - E[f(x)])^2] \\\\

	&= \sum_x ( f(x) - E[f(x)] )^2 \space p(x)
\end{aligned}
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



# Cumulative Distribution Function

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

# Covariance

**Covariance**

# References

- [Statistical Distribution](https://youtu.be/oI3hZJqXJuc?list=PLblh5JKOoLUK0FLuzwntyYI10UQFUhsY9)
- [StatQuest: Maximum Likelihood](https://youtu.be/XepXtl9YKwc?list=PLblh5JKOoLUK0FLuzwntyYI10UQFUhsY9)
- [The Sample Variance: Why Divide by n-1?](https://youtu.be/9ONRMymR2Eg)
- [StatQuickie: Standard Deviation vs Standard Error](https://youtu.be/A82brFpdr9g?list=PLblh5JKOoLUK0FLuzwntyYI10UQFUhsY9)
- [The Central Limit Theorem](https://youtu.be/YAlJCEDH2uY?list=PLblh5JKOoLUK0FLuzwntyYI10UQFUhsY9)
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
