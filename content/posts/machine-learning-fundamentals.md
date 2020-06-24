---
title: "The Fundamentals of Machine Learning"
date: "2020-6-22"
template: "post"
draft: false
slug: "/posts/machine-learning-fundamentals/"
category: "Machine Learning"
tags:
- ""
description: ""
---

**Machine learning** is a set of mathematical tools for developing accurate statistical models of real-world events. The models are used to predict, classify and explore relationships.

# Table of Contents

- Types of learning algorithms
	- Supervised vs Unsupervised Learning
	- Regression vs Classification
	- Prediction vs Interpretation
- Statistical model
	- Errors in Estimation
- How to estimate $f$?
	- Parametric Methods
	- Non-Parametric Methods
- Calculating Model Performance
	- Mean Squared Error
	- Error Rate
- Capacity and Generalization
	- Flexibility and MSE
	- Bias-Variance Tradeoff
	- Bias-Variance Decomposition

# Types of Learning Algorithms

Learning algorithms enable computers to gain the ability to perform tasks that are difficult to solve by handwritten rule-based programs. Algorithms differ in their approach, type of input and output or task they are intended to solve.

## Supervised vs Unsupervised Learning

Most statistical learning problems fall into two categories: *supervised* and *unsupervised*. **Supervised learning** attempts to fit a model to a dataset with inputs $X$ leading to a response $Y$, such that the model works well with unseen inputs. Examples include linear and logistic regression.

In contrast, **unsupervised learning** algorithms work with datasets without a response variable $Y$. So, what kind of analysis is possible? One possibility is *cluster analysis*. Its goal is to categorize a dataset into multiple classes based on a set of features. If used for predictions, the input must be placed under the proper class.

<figure style="width: 600px">
	<img src="/media/machine learning/basics/sup-unsup.png" alt="Supervised vs Unsupervised Learning">
	<figcaption>Supervised vs Unsupervised Learning</figcaption>
</figure>

## Regression vs Classification

Problems involving continuous response variables are named **regression problems**, and problems involving categorical response variable are **classification problems**.

**Continuous variables** take on numerical values such as integers or floating point values. For example, a house may be predicted to sell for 200,000 dollars.

In contrast, **categorical variables** take on one of many classes or categories. For example, brand of shoe purchased.

<figure style="width: 600px">
	<img src="/media/machine learning/basics/classification-vs-regression.png" alt="Regression vs Classification">
	<figcaption>Regression vs Classification</figcaption>
</figure>

## Prediction vs Interpretation

Some models, like linear models, are much less flexible compared to models using thin-plane splines.

**So, why would we ever choose a model with low flexibility?** This is because *restrictive models are much more interpretable.* As the flexibility of models decrease, the interpretablity increases.

The goal of **interpretation** is to understand the relationship between $Y$ and $X$; not to make a prediction for $Y$ given $X$. We ask questions like:

- **Which predictors are associated with the response?** Often only a small subset of available predictors are substantially associated with $Y$. Identifying them simplifies the task.
- **What is the relationship between the response and each predictor?** The value of $Y$ may increase as a predictor $X_i$ is increased in value. This is a *positive relationship*. Other predictors may have a *negative relationship* with the response. The relationship between a response and a predictor might also depend on other predictors.

<figure style="width: 600px">
	<img src="/media/machine learning/basics/flexibility-interpretability.png" alt="Flexibility Interpretability">
	<figcaption>Flexibility Interpretability</figcaption>
</figure>

For prediction tasks, one might think that the most flexible model will provide the best predictive model. This is not necessarily the case. This has to do with the concept of overfitting, which is explained later.

# Statistical model

A **statistical model** is a function $f$ consisting of a set of adjustable parameters that maps the relationship between *input variables* or **predictors** to an *output variable* or a **response**. Finding the function $f$ and the values for its parameters is known as **learning**.

The response is denoted by $Y$, and the set of $p$ predictors $\lbrace X_1, X_2, ... , X_p\rbrace$ are denoted by $X$. The true relationship $f$ between $Y$ and $X$ in the most general form is written as:

$$
Y = f(X) + \epsilon
$$

Here $f$ is the true and unknown function we need to find. It encodes systematic information about the relationship between $X$ and $Y$. For example, it states whether the relationship is linear, polynomial or exponential.

## Errors in Estimation

The true relationship $f$ cannot be known even if we have a huge dataset. We can only *estimate* the relationship. It is denoted by $\hat{f}$.

$$
\hat{Y} = \hat{f}(X) + \epsilon
$$

The accuracy of $\hat{Y}$ as a estimation of $Y$ depends on two quantities: *reducible error* and *irreducible error*.

Some learning methods ask us to assume the general functional shape of the relationship $f$. Our assumption could be incorrect but can potentially be improved. Thus it is known as a **reducible error**.

Even if our assumption is fairly close to the truth, our model will still have some inaccuracies. This could be because we missed out some useful predictors or due to unmeasured variation and dependencies in predictors already considered by $\hat{f}$. It is denoted by $\epsilon$ and is called the **irreducible error**.

The irreducible error will always provide an upper bound to the accuracy of our predictions.

# How to estimate $f$?

There are two categories of statistical methods for estimating $f$:

- Parametric methods
- Non-parametric methods

## Parametric Methods

Parametric methods make an assumption about the functional form of $f$. A simple assumption is that $f$ is linear.

$$
f(X) = \beta_0 + \beta_1 X_1 + ... + \beta_p X_p
$$

This is a linear model. Once this is assumed, the problem of estimating $f$ is greatly simplified. Instead of trying to estimate an arbitrary p-dimensional *function* $f(X)$, we only need to estimate $p + 1$ *coefficients* $\beta_0, \beta_1, ... \beta_p$.

Then we estimate the parameters $\beta_0, \beta_1, ... \beta_p$ using a training dataset such that

$$
Y \approx \beta_0 + \beta_1 X_1 + ... + \beta_p X_p
$$

This is called **fitting a model** to a dataset.

The parametric method reduces the problem of estimating $f$ to estimating a set of parameters, greatly simplifying the learning process. It is computationally faster than non-parametric methods.

<figure style="width: 500px">
	<img src="/media/machine learning/basics/parametric-method.png" alt="Parametric Method - Fitting a Linear Model">
	<figcaption>Parametric Method - Fitting a Linear Model</figcaption>
</figure>

The disadvantage is that if the assumption of $f$ is incorrect, then our model accuracy will be poor regardless of how much data you have.

## Non-Parametric Methods

This approach does not make any explicit assumptions about the functional form of $f$. Thus, it avoids the danger of a bad assumption and has the potential to fit a wider range of possible shapes for $f$ from the training data.

With more training data, these models increase in complexity. Whereas parametric models stay within the confines of the assumed general functional shape.

As non-parametric methods make fewer assumptions, they are more robust and thus can be applied unfamiliar situations.

<figure style="width: 500px">
	<img src="/media/machine learning/basics/non-parametric-method.png" alt="Non-Parametric Method - Fitting a Thin-Plate Spline">
	<figcaption>Non-Parametric Method - Fitting a Thin-Plate Spline</figcaption>
</figure>

Since non-parametric methods don't make any major assumptions, they require a larger number of examples to estimate $f$ compared to parametric methods.

They are computationally slower than parametric methods since they have more parameters to learn.

# Calculating Model Performance

In order to evaluate performance of a learning method on a given dataset, we need a way to measure how well its prediction responses actually match true responses in observed data.

## Mean Squared Error

In regression problems, the most commonly used measure is the **mean squared error** (MSE).

$$
MSE = \frac{1}{n}\sum_\text{i = 1}(y_i - \hat{f}(x_i))^2
$$

where $\hat{f}(x_i)$ provides the prediction for ith observation, and $y_i$ is the actual response variable for ith observation. The MSE value will be small if the predicted responses are very close to true responses.

<figure style="width: 800px">
	<img src="/media/machine learning/basics/mse.png" alt="MSE">
	<figcaption>MSE</figcaption>
</figure>

If training data is used to compute MSE, it is called **training MSE**, and if test data is used, it is **test MSE**.

Since our goal is to build a model that works accurately with previously unseen inputs (test data), we prefer models with the lowest test MSE as opposed to one with the lowest training MSE.

## Error Rate

In the classification setting, the most common approach to quantify accuracy of $\hat{f}$ is the error rate. It calculates the fraction of incorrect classifications.

$$
\text{Error rate}
=
\frac {1} {n} \sum_{i = 1}^n I (y_i \ne \hat{y_i})
$$

where, $I$ is an indicator variable,

$$
I = \begin{cases}
   1 &\text{if } y_i \ne \hat{y_i}\\
   0 &\text{if } y_i = \hat{y_i}
\end{cases}
$$

A good classifier has a very small error rate.

# Capacity and Generalization

The ability to perform well on previously unseen inputs is called **generalization**. The need to have a low generalization error or test error is the difference between machine learning and optimization.

A good model accurately *captures the regularities* in its training data and also *generalizes well* to unseen data. An important hurdle in achieving this is finding the appropriate model flexibility.

<figure style="width: 600px">
	<img src="/media/machine learning/basics/flexibility.png" alt="Flexibility">
	<figcaption>Flexibility</figcaption>
</figure>

When a model is highly flexible, it hugs the data points very tightly. This makes it a good representation of the training dataset. But it does not generalize well to unseen inputs. This is because they are fitting the fringe and noisy data points too. This error is called **overfitting**.

When the model is inflexible it is incapable of representing the regularities in the dataset. Since it cannot representing the training dataset, it cannot be expected to generalize well to unseen inputs. This error is called **underfitting**.

We can control whether a model is more likely to overfit or underfit by altering its capacity. A model's **capacity** is its ability to fit a wide variety of functions. Models with low capacity are not very flexible and may struggle to fit the training set. Models with high capacity may overfit the training set.

One way to control capacity, is to restrict the types of functions that the learning algorithm is allowed to choose as the model. This is called the **hypothesis space**.

For example, the linear regression algorithm has a set of all linear functions as its hypothesis space. To increase the model capacity, we can let the algorithm generalize the model to include polynomials.

Models perform best when their capacity is appropriate for the complexity of the task.

## Flexibility and MSE

Let us see how the test and training MSE of a model changes based on varying degrees of flexibility.

<figure style="width: 900px">
	<img src="/media/machine learning/basics/u-shape.png" alt="Flexibility vs MSE">
	<figcaption>Flexibility vs MSE. The gray curve is the training MSE and red curve is the test MSE.</figcaption>
</figure>

When the model flexibility is very low, it suffers from underfitting. So the training MSE will be very high. Since underfitting contributes to bad generalization, the test MSE is also high.

As we increase the flexibility, the model can capture more of the regularities in the dataset, so both the training and test MSE decrease.

But if the model flexibility is too high, the training MSE inches closer and closer to $0$ because it suffers from overfitting. The test MSE on the other hand increases after a certain point. This is due to the fact that noisy data points are being learnt, causing bad generalization.

Note that we expect the training MSE to almost always be smaller than the test MSE, as most learning methods either directly or indirectly seek to minimize the training MSE.

The same line of reasoning can be applied to any of the alternatives to MSE.

## Bias-Variance Tradeoff

The **bias–variance tradeoff** is central in the conflict to prevent overfitting and underfitting.

Ideally, we want a model that both accurately captures the regularities in its training data and also generalizes well to unseen data. Unfortunately, it is impossible to do both simultaneously.

**Bias** is the inability of a learning algorithm to capture the true relationship between the predictors and the response. It is exhibited by relatively inflexible methods like linear regression.

**Variance** is the error caused by sensitivity to small fluctuations in the dataset. High variance is exhibited by highly flexible methods like polynomial regression. If a model has *high* variance, it means small changes in the training data will result in large changes in MSE, which in turn causes large changes in $\hat{f}$.

Variance and bias are two opposing forces.

- Increasing bias will decrease variance
- Increasing variance will decrease bias

The challenge lies in finding a method for which we both variance and bias are low.

<figure style="width: 700px">
	<img src="/media/machine learning/basics/bias-variance.png" alt="Bias-Variance Tradeoff">
	<figcaption>Bias-Variance Tradeoff</figcaption>
</figure>

## Bias-Variance Decomposition

[Proof](https://youtu.be/C3nIFH649wY)

$$
\text{MSE} (\hat{\theta}) = (\text{bias} \space \hat{\theta})^2 + \text{var} \space \hat{\theta}
$$

# References

- [StatQuest : Bias and Variance](https://www.youtube.com/watch?v=EuBBz3bI-aA)
- [Introduction to Statistical Learning](http://faculty.marshall.usc.edu/gareth-james/ISL/)
- [What is the “capacity” of a machine learning model?](https://stats.stackexchange.com/questions/312424/what-is-the-capacity-of-a-machine-learning-model/312578)
- [What exactly is a hypothesis space in machine learning?](https://stats.stackexchange.com/questions/183989/what-exactly-is-a-hypothesis-space-in-machine-learning)
