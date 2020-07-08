---
title: "Estimator"
date: "2019-11-1"
template: "post"
draft: false
slug: "/posts/estimator/"
category: "Statistics and Probability Theory"
tags:
 - ""
description: ""
---

An **estimator** is a function that estimates a property of a population based on sample data. This property does not need to be a distribution parameter.

For example, the sample mean $\overline{x}$ is an estimator of the population mean $\mu$. A different estimator can try to estimate $\mu^2$, which is not a distribution parameter.

If $X$ denotes a random variable that holds the sample data, and if we are supposed to estimate a parameter $\theta$, we denote an estimator by $\hat{\theta}(X)$ or just $\hat{\theta}$. A estimate for a sample data point $X = x$ is denoted by $\hat{\theta}(x)$.

## Error

For a given sample $x$, the **error** of an estimator $\hat{\theta}$ is defined as,

$$
e(x) = \hat{\theta}(x) - \theta(x)
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

# References

- [Estimators - the basics](https://youtu.be/qvR7sSGphQ4)
- [Estimator properties](https://youtu.be/UxbY85Cm9SQ)
- [What is the difference between an estimator and a statistic?](https://stats.stackexchange.com/questions/47728/what-is-the-difference-between-an-estimator-and-a-statistic)
- [Errors and residuals](https://en.wikipedia.org/wiki/Errors_and_residuals)
