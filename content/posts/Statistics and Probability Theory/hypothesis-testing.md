---
title: "Hypothesis Testing"
date: "2020-7-12"
template: "post"
draft: false
slug: "/posts/hypothesis-testing/"
category: "Statistics and Probability Theory"
tags:
 - ""
description: ""
---

A **hypothesis** is an assumption about a population parameter. **Hypothesis testing** uses sample data to check whether a hypothesis about a population parameter is likely to be true.

The two types of hypothesis are:

- Null hypothesis $H_0$
- Alternative hypothesis $H_a$

The **null hypothesis** is a statement about the population parameter that is assumed to be true, like a defendant is assumed to be innocent in court. It usually holds the status quo. Hypothesis testing tests whether the null hypothesis is likely to be true.

The **alternative hypothesis** is a statement that directly contradicts the null hypothesis by stating that that the actual value of a population parameter is less than, greater than or not equal to the value stated in the null hypothesis. It usually states that the results are influenced by some non-random cause.

The null and alternative hypothesis must be different. There cannot be any overlap.

For example, a null hypothesis could say that half of the coin tosses would result in Heads and the other half in Tails. The alternative hypothesis could be that the number of Heads and Tails would be very different.

Symbolically, these hypotheses would be expressed as,

$$
\begin{aligned}
H_0 : P &= 0.5
\\
H_a : P &\ne 0.5
\end{aligned}
$$

The hypothesis test will have one of two outcomes: *reject* or *fail to reject* the null hypothesis.

The decision making in hypothesis testing is similar to that made by a jury. The jury assumes that the defendant is innocent. We assume that the null hypothesis is true.

The prosecutor and the researcher present evidence to show guilt or falsehood. If there is enough strong evidence to show guilt, then the null hypothesis is rejected. It is better to accept the status quo null hypothesis, than to make false unproven alternative hypothesis.

# Decision Errors

A hypothesis test can have two types of errors

- Type **I** Error
- Type **II** Error

A **Type I error** occurs when you reject a true null hypothesis. The probability of committing a Type **I** error is called the **significance level** $\alpha$.

A **Type II error** occurs when you fail to reject a false null hypothesis. The probability of committing a Type **II** error is called **beta** $\beta$.

<figure style="width: 1000px">
    <img src="/media/statistics and probability theory/hyp-error.png" alt="Decision Errors">
    <figcaption>Decision Errors</figcaption>
</figure>

## Power

For example, consider a normally distributed population with a mean of $10$ and a standard deviation of $2$. This distribution indicates that $95.44 \%$ of the values in this population are between $6$ and $14$.

When you gather a sample from this population, it is possible that it has a mean of $4$. From such a sample you wouldn't know that the population mean is actually $10$.

Of course, the odds of getting such a sample are incredibly small, but it is nevertheless, possible. Improbable samples can lead you to the wrong conclusion. While you can't know when this will occur, you can estimate how often it will occur. That's where power comes in.

The **power** of a hypothesis test is the probability that the test correctly rejects the null hypothesis. It is the probability of *not* committing a Type **II** error.

- [Increase the power of a hypothesis test](https://support.minitab.com/en-us/minitab-express/1/help-and-how-to/basic-statistics/inference/supporting-topics/basics/increase-the-power-of-a-hypothesis-test/)

# Test statistic

A **test statistic** is a statistic of the sample used for a hypothesis test. In general, a test statistic is selected such that it distinguishes the null hypothesis from the alternative hypothesis.

In hypothesis testing, the test statistic is a value computed from sample data. The test statistic is used to assess the strength of evidence in support of a null hypothesis.

A test statistic contains information about the data that is relevant for deciding whether to reject the null hypothesis.

Suppose the test statistic in a hypothesis test is equal to S. If the probability of observing a test statistic as extreme as S is less than the significance level, we reject the null hypothesis.

The sampling distribution of the test statistic under the null hypothesis is called the **null distribution**.

Some test statistics have two forms depending on the type of test. **One-sample tests** are appropriate when a sample is being compared to the population. **Two-sample tests** are appropriate for comparing two samples, typically an experimental and a control sample.

# Hypothesis Testing Steps

The steps involved in hypothesis testing:

- State both of the hypotheses
- Choose a level of significance $\alpha$
- Choose and calculate the test statistic
- Calculate $p$-value

<figure style="width: 920px">
    <img src="/media/statistics and probability theory/hyp-test.png" alt="Hypothesis Testing">
    <figcaption>Hypothesis Testing</figcaption>
</figure>

- [Khan Academy : P-values and significance tests](https://youtu.be/KS6KEWaoOOE)
- [Understanding Hypothesis testing](https://youtu.be/0zZYBALbZgg)
- [Statistical and practical significance](https://support.minitab.com/en-us/minitab-express/1/help-and-how-to/basic-statistics/inference/supporting-topics/basics/statistical-and-practical-significance/)
- [How P-Values Help Us Test Hypotheses: Crash Course Statistics](https://youtu.be/bf3egy7TQ2Q)

# Level of Significance

The level of significance is the conditional probability of getting a certain sample statistic value assuming that the sample statistic is true. Often we choose $1 \%$ or $5 \%$.

- [Comparing P-values to different significance levels](https://youtu.be/DQCF4kTXf9Q)

# P-value

The $p$-value is a measure of the strength of the evidence against the null hypothesis. It is the probability of getting the observing value for the test statistic, if the null hypothesis is actually true.

If the $p$-value is less than the chosen significance level $\alpha$ then reject the null hypothesis.

# Region of acceptance

The region of acceptance is a range of values. If the test statistic falls within this range, the null hypothesis is not rejected. The region of acceptance is defined so that the chance of making a Type I error is equal to the significance level.

The set of values outside the region of acceptance is called the region of rejection. If the test statistic falls within the region of rejection, the null hypothesis is rejected. In such cases, we say that the hypothesis has been rejected at the α level of significance.

## One-Tailed and Two-Tailed Tests

A test of a statistical hypothesis, where the region of rejection is on only one side of the sampling distribution, is called a one-tailed test. For example, suppose the null hypothesis states that the mean is less than or equal to 10. The alternative hypothesis would be that the mean is greater than 10. The region of rejection would consist of a range of numbers located on the right side of sampling distribution; that is, a set of numbers greater than 10.

A test of a statistical hypothesis, where the region of rejection is on both sides of the sampling distribution, is called a two-tailed test. For example, suppose the null hypothesis states that the mean is equal to 10. The alternative hypothesis would be that the mean is less than 10 or greater than 10. The region of rejection would consist of a range of numbers located on both sides of sampling distribution; that is, the region of rejection would consist partly of numbers that were less than 10 and partly of numbers that were greater than 10.

# References

- [StatTrek : What is Hypothesis Testing?](https://stattrek.com/hypothesis-test/hypothesis-testing.aspx)
- [Wikipedia : Test statistic](https://en.wikipedia.org/wiki/Test_statistic)
- [Introduction to Type I and Type II errors](https://youtu.be/Hdbbx7DIweQ)
- [What is power?](https://support.minitab.com/en-us/minitab-express/1/help-and-how-to/basic-statistics/inference/supporting-topics/basics/what-is-power/)
