---
title: "The Fundamentals of Statistics"
date: "2019-11-7"
template: "post"
draft: false
slug: "/posts/statistics-fundamentals/"
category: "Statistics and Probability Theory"
tags:
 - ""
description: ""
---

**Statistics** is concerned with the collection, analysis and presentation of data.

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

# Sampling Methods

A **sampling method** is a procedure for selecting sample elements from a population. Some methods are given below:

## Simple Random Sampling

In **simple random sampling**, each member of the population has an equal probability of being included in the sample. We *randomly* choose $N$ elements to get a sample.

## Stratified sampling

In **stratified sampling**, we divide the population into groups based on some characteristic. Then, within each group, we select a random sample. These groups are called **strata**.

Suppose we conduct a national survey, we might divide the population into strata based on gender. Then within each stratum, we might randomly select survey respondents.

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

# References

- [Statistical Distribution](https://youtu.be/oI3hZJqXJuc?list=PLblh5JKOoLUK0FLuzwntyYI10UQFUhsY9)
- [StatQuest: Maximum Likelihood](https://youtu.be/XepXtl9YKwc?list=PLblh5JKOoLUK0FLuzwntyYI10UQFUhsY9)
- [The Sample Variance: Why Divide by n-1?](https://youtu.be/9ONRMymR2Eg)
- [StatQuickie: Standard Deviation vs Standard Error](https://youtu.be/A82brFpdr9g?list=PLblh5JKOoLUK0FLuzwntyYI10UQFUhsY9)
- [The Central Limit Theorem](https://youtu.be/YAlJCEDH2uY?list=PLblh5JKOoLUK0FLuzwntyYI10UQFUhsY9)
