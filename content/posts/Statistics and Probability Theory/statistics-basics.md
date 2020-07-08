---
title: "Basic Statistics"
date: "2019-11-1"
template: "post"
draft: false
slug: "/posts/statistics-basic/"
category: "Statistics and Probability Theory"
tags:
 - ""
description: ""
---

**Statistics** is concerned with the collection, analysis and presentation of data.

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

Using $\overline{x}$ in the square of differences will result in the smallest possible value. This is because it is equidistant from all other sample points $x_i$. Using any other value instead of $\overline{x}$ will result in a smaller numerator.

Since $\mu \ne \overline{x}$, our current estimation $s^2$ is smaller than the population variance. Dividing by $n - 1$ increases $s^2$ to compensate for our use of $\overline{x}$.

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

**Standard error** is the standard deviation of the distribution of a multiple instances of a statistic calculated from multiple samples.

- Collect five different samples.
- Calculate the mean of each of these samples.
- Plot the means on the number line.
- Now find the standard deviation of the mean around the mean of means.

This is the *standard error of the mean*. If the means are more spread out, then the standard error increases. You can calculate standard error for any statistic you wish.

<figure style="width: 550px">
    <img src="/media/statistics and probability theory/standard-error-of-mean.png" alt="Standard Error of Mean">
    <figcaption>Standard Error of Mean</figcaption>
</figure>

- [StatQuickie: Standard Deviation vs Standard Error](https://youtu.be/A82brFpdr9g)<br/>
- [Derivation](https://youtu.be/7mYDHbrLEQo)

# Common Statistical Distributions

Some common types of data distributions are described below.

## Normal Distribution

The **Gaussian** or **normal distribution** is a continuous probability distribution for a real-valued random variable. Its shape is defined by its mean and variance, just like any other distribution. It is also called a *bell shaped curve*.

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

You will also find $68 \%$ of the values within $1$ standard deviation of the mean. $95 \%$ of the values will be found within $2$ standard deviations and $99.7 \%$ of the values will be found within $3$ standard deviations.

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

z-scores are used to standardize normal distributions. It can also be used to find the area under a certain region of a standard normal distribution using the [z-table](https://youtu.be/-UljIcq_rfc).

### Standardization

Any random variable with a non-standard normal distribution can be converted into a random variable with standard distribution. This is done by translating all data points $X = x$ into $z$ values using equation $(2)$.

<figure style="width: 900px">
    <img src="/media/statistics and probability theory/standardizing normal distro.svg" alt="Standardization">
    <figcaption>Standardization</figcaption>
</figure>

[Standardizing Normally Distributed Random Variables](https://youtu.be/4R8xm19DmPM)

# Sampling Distribution

The sampling distribution of a statistic is the probability distribution of a statistic if we repeatedly draw samples from the population and calculate the statistic for this sample.

<figure style="width: 880px">
    <img src="/media/statistics and probability theory/sampling-distribution.png" alt="Sampling Distribution">
    <figcaption>Sampling Distribution</figcaption>
</figure>

[JB Statistics : Sampling Distribution](https://www.youtube.com/watch?v=Zbw-YvELsaM)

# References

- [Introduction to sampling distributions](https://youtu.be/z0Ry_3_qhDw)
- [The Sample Variance: Why divide by n-1?](https://youtu.be/9ONRMymR2Eg)
- [Why are degrees of freedom (n-1) used in Variance and Standard Deviation?](https://youtu.be/92s7IVS6A34)
- [Statistical Distribution](https://youtu.be/oI3hZJqXJuc)
- [Math is fun : Normal Distribution](https://www.mathsisfun.com/data/standard-normal-distribution.html)
- [JB Statistics : An Introduction to the Normal Distribution](https://youtu.be/iYiOVISWXS4)
- [Stattrek : z-score](https://stattrek.com/statistics/dictionary.aspx?definition=z-score)
- [Z-Scores, Standardization and the Standard Normal Distribution](https://youtu.be/2tuBREK_mgE)
