---
title: "The Fundamentals of Statistics"
date: "2019-11-1"
template: "post"
draft: false
slug: "/posts/statistics-fundamentals/"
category: "Statistics and Probability Theory"
tags:
 - ""
description: ""
---

**Statistics** is concerned with the collection, analysis and presentation of data.

# Table of Contents

- Population and Samples
- Estimator
    - Error
    - Mean Squared Error
    - Sampling Deviation
    - Variance
    - Bias
    - Consistency
    - Relationship between Bias and Consistency
- Common Statistical Distributions
	- Normal Distribution
	- Standard Normal Distribution
- Maximum Likelihood Estimation
- Central Limit Theorem

# Population and Samples

The **population** is the complete set of observations or individuals that we *wish* to study. For example, if you want to know the average height of the Chinese, then all the Chinese people make up the population.

But it's impossible measure the heights of all these people. A **sample** is a subset of the population and is what we actually use for analysis. It is used to make estimations of the characteristics of the population.

<figure style="width: 900px">
    <img src="/media/statistics and probability theory/population-sample.png" alt="Sampling a Population">
    <figcaption>Sampling a Population</figcaption>
</figure>

There will be some inaccuracy in our conclusions about the population based upon a sample. This should be obvious - we have fewer members in our sample than the population, therefore we have lost some information.

A characteristic of a population, such as the mean or standard deviation, is called a **parameter**; whereas a characteristic of a sample is called a **statistic**.

Parameters hold the true values of a real world distribution. Since we only have samples and not the entire population, we always work with statistics.

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

### Bessel's correction

It refers to the use of $N - 1$ instead of $N$ in the formula for sample variance to get an better estimate of the population variance.

Lets start with,

$$
s^2 = \frac { \sum_i ( x_i - \overline{x} )^2 } {N}
$$

Using $\overline{x}$ in the square of differences will result in the smallest possible value. This is because it is equidistant from all other sample points $x_i$. Using any other value instead of $\overline{x}$ will result in a larger value.

Since $\mu \ne \overline{x}$, our current estimation $s^2$ is smaller than the population variance. Dividing by $n - 1$ increases $s^2$ to compensate for our use of $\overline{x}$.

[Why are degrees of freedom (n-1) used in Variance and Standard Deviation?](https://youtu.be/92s7IVS6A34)

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


# Estimator

An **estimator** is a function that estimates a property of a population based on sample data. This property does not need to be a distribution parameter.

For example, the sample mean $\overline{x}$ is an estimator of the population mean $\mu$. A different estimator can try to estimate $\mu^2$, which is not a distribution parameter.

If $X$ denotes a random variable that holds the sample data, and if we are supposed to estimate a parameter $\theta$, we denote an estimator by $\hat{\theta}(X)$ or just $\hat{\theta}$. A estimate for a sample data point $X = x$ is denoted by $\hat{\theta}(x)$.

## Error

For a given sample $x$, the **error** of an estimator $\hat{\theta}$ is defined as,

$$
e(x) = \hat{\theta}(x) - \theta
$$

## Mean Squared Error

The mean squared error of $\hat{\theta}$ is defined as the expected value of all the squared errors,

$$
\text{MSE}(\hat{\theta}) = E[(\hat{\theta} - \theta)^2]
$$

## Sampling Deviation

For a given sample $x$, the sampling deviation of $\hat{\theta}$ is defined as,

$$
d(x) = \hat{\theta}(x) - E[\hat{\theta}]
$$

## Variance

The variance is the expected value of all the squared sampling deviations,

$$
\text{var}(\hat{\theta}) = E[(\hat{\theta} - E[\hat{\theta}])^2]
$$

## Bias

Bias measures how far the expected value of the estimate is from the population property. It is denoted by $B(\hat{\theta})$.

$$
B(\hat{\theta}) = E(\hat{\theta}) - \theta
$$

If a statistic over or under estimates a property for a distribution then it is said to be **biased** *for* that distribution. Otherwise, it is **unbiased** for the distribution.

Sample mean as an estimator for distribution mean has zero bias. But sample mean as an estimator for distribution variance is biased for most distributions.

## Consistency

As we increase the sample size, the expectation of the estimation moves towards the population parameter value. This is called **consistency**. An estimator that exhibits this is called a **consistent estimator**.

## Relationship between Bias and Consistency

[Relationship between Bias and Consistency](https://youtu.be/21lXGc02XwM) <br/>
[Example](https://youtu.be/6i7mqDJICzQ)

<figure style="width: 900px">
    <img src="/media/statistics and probability theory/bias-consistency-1.png" alt="Unbiased and Consistent">
    <figcaption>Unbiased and Consistent</figcaption>
</figure>

<figure style="width: 900px">
    <img src="/media/statistics and probability theory/bias-consistency-2.png" alt="Biased and Consistent">
    <figcaption>Biased and Consistent</figcaption>
</figure>

<figure style="width: 900px">
    <img src="/media/statistics and probability theory/bias-consistency-3.png" alt="Biased and Inconsistent">
    <figcaption>Biased and Inconsistent</figcaption>
</figure>

# Common Statistical Distributions

Some common types of data distributions are described below.

## Normal Distribution

The **Gaussian** or **normal distribution** is a continuous probability distribution for a real-valued random variable. Its shape is defined by its mean and variance, just like any other distribution. It is also called a *bell shaped curve* because it is shaped like a bell.

<figure style="width: 900px">
    <img src="/media/statistics and probability theory/normal-distro.png" alt="Normal Distribution">
    <figcaption>Normal Distribution</figcaption>
</figure>

Its general form is given by,

$$
\tag{1}
\mathcal{N} (x \mid \mu, \sigma^2)
=
\frac {1} {\sqrt{2 \pi} \sigma} e^{\normalsize - \frac {\normalsize 1} {\normalsize 2 \sigma^2} (x - \mu)^2}
$$

It can be shown that,

$$
\begin{aligned}
	\mathcal{N} (x \mid \mu, \sigma^2) &> 0
	\\
	\int_{- \infty}^{\infty} \mathcal{N} (x \mid \mu, \sigma^2) dx &= 1
\end{aligned}
$$

This allows us to treat equation $(1)$ as a valid probability density function.

The data that follows normal distribution is symmetric around the mean. The mean, [median](https://www.mathsisfun.com/median.html) and [mode](https://www.mathsisfun.com/mode.html) are also the same.

<figure style="width: 900px">
    <img src="/media/statistics and probability theory/normal symmetry.svg" alt="Normal Distribution Symmetry">
    <figcaption>Normal Distribution Symmetry</figcaption>
</figure>

You will also find $68 %$ of the values within $1$ standard deviation of the mean. $95 %$ of the values will be found within $2$ standard deviations and $99.7 %$ of the values will be found within $3$ standard deviations.

<figure style="width: 900px">
    <img src="/media/statistics and probability theory/normal distro std dev.png" alt="Normal Distribution Standard Deviation">
    <figcaption>Normal Distribution Standard Deviation</figcaption>
</figure>

## Standard Normal Distribution

The standard normal distribution is a normal distribution with mean $\mu = 0$ and variance $\sigma^2 = 1$.

### z-score

The **standard score** or **z-score** of a standard normal distribution is the number of standard deviations a value $x$ is away from the mean value $\mu$.

$$
\tag{2} z = \frac {x - \mu} {\sigma}
$$

A z-score of $1$ represents a data point that is $1$ standard deviation greater than the mean. A z-score of $-2.3$ represents a data point that is $2.3$ standard deviations less than the mean.

z-scores are used to standardize normal distributions and find the area under a certain region of a standard normal distribution using the [z-table](https://youtu.be/-UljIcq_rfc). You can also use the area to find the corresponding z-scores.

### Standardization

Any random variable with a non-standard normal distribution can be converted into a random variable with standard distribution. This is done by translating all data points $X = x$ into $z$ values using equation $(2)$.

<figure style="width: 900px">
    <img src="/media/statistics and probability theory/standardizing normal distro.svg" alt="Standardization">
    <figcaption>Standardization</figcaption>
</figure>

[Standardizing Normally Distributed Random Variables](https://youtu.be/4R8xm19DmPM)

# Maximum Likelihood Estimation

**Likelihood** tells you how probable it is for a set of observations $O$ to came from a distribution $D$. It is denoted by $L ( D \mid O )$.

Since a distribution is described by its parameters or statistics like the mean and standard deviation we write likelihood as $L ( \mu = 15, \sigma = 2 \mid O )$. This denotes the likelihood of a distribution with a mean of $15$ and a standard deviation of $2$ given observations $O$.

<figure style="width: 650px">
	<img src="/media/statistics and probability theory/probability-vs-likelihood.png" alt="Probability vs Likelihood">
	<figcaption>Probability vs Likelihood</figcaption>
</figure>

Given a set of observations, **maximum likelihood estimation** (MLE) finds a distribution from which they were most likely sampled from. We must perform MLE for each and every statistic we wish to estimate.

<figure style="width: 550px">
	<img src="/media/statistics and probability theory/likelihood.png" alt="Likelihood">
	<figcaption>Likelihood</figcaption>
</figure>

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

# Central Limit Theorem

The **Central Limit Theorem** states that the sample mean $\overline{x}$ of a large number of samples from a population will approximately be normally distributed, regardless of the type of the population distribution.

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

# References

- [The Sample Variance: Why divide by n-1?](https://youtu.be/9ONRMymR2Eg)
- [StatQuickie: Standard Deviation vs Standard Error](https://youtu.be/A82brFpdr9g)
- [Estimators - the basics](https://youtu.be/qvR7sSGphQ4)
- [Estimator properties](https://youtu.be/UxbY85Cm9SQ)
- [Statistical Distribution](https://youtu.be/oI3hZJqXJuc)
- [StatQuest: Maximum Likelihood](https://youtu.be/XepXtl9YKwc)
- [The Central Limit Theorem](https://youtu.be/YAlJCEDH2uY)
- [Math is fun : Normal Distribution](https://www.mathsisfun.com/data/standard-normal-distribution.html)
- [JB Statistics : An Introduction to the Normal Distribution](https://youtu.be/iYiOVISWXS4)
- [Stattrek : z-score](https://stattrek.com/statistics/dictionary.aspx?definition=z-score)
- [Z-Scores, Standardization and the Standard Normal Distribution](https://youtu.be/2tuBREK_mgE)
- [Central limit theorem : Khan Academy](https://youtu.be/JNm3M9cqWyc)
- [What is the difference between an estimator and a statistic?](https://stats.stackexchange.com/questions/47728/what-is-the-difference-between-an-estimator-and-a-statistic)
