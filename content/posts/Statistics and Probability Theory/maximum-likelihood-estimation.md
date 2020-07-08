---
title: "Maximum Likelihood Estimation"
date: "2019-11-1"
template: "post"
draft: false
slug: "/posts/maximum-likelihood-estimation/"
category: "Statistics and Probability Theory"
tags:
 - ""
description: ""
---

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

# References

- [StatQuest: Maximum Likelihood](https://youtu.be/XepXtl9YKwc)
