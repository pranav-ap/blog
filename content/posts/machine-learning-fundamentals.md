---
title: "The Fundamentals of Machine Learning"
date: "2019-10-12"
template: "post"
draft: false
slug: "/posts/machine-learning-fundamentals/"
category: "Machine Learning"
tags:
- ""
description: ""
---

**Machine learning** is a set of mathematical tools for developing accurate statistical models of real-world events. The models are used to predict, classify and explore relationships.

A **statistical model** is a function $f$ consisting of a set of adjustable parameters that map *input variables* or **predictors** to an *output variable* or a **response**. Finding the function $f$ and the values for its parameters is known as **learning**.

The response is denoted by $Y$, and the set of $p$ predictors $\lbrace X_1, X_2, ... , X_p\rbrace$ are denoted by $X$. The true relationship $f$ between $Y$ and $X$ in the most general form is written as:

$$
Y = f(X) + \epsilon
$$

Here $f$ is the fixed, true, and unknown function. It encodes systematic information about the relationship between $X$ and $Y$. It states whether the relationship is linear, polynomial or exponential. In case it is linear; a unit change in $X$ causes a unit change in $Y$. In case it is exponential, a unit change in $X$ causes an exponential change in $Y$.

# Errors in Estimation

The true relationship $f$ cannot be known even if we have a huge dataset. We can only estimate the relationship. It is denoted by $$\hat{f}$$.

$$
\hat{Y} = \hat{f}(X) + \epsilon
$$

The accuracy of $$\hat{Y}$$ as a prediction of $$Y$$ depends on two quantities: *reducible error* and *irreducible error*.

Some methods of model learning ask us to assume the shape of $f$. This assumption of $f$ may be far away from the truth. But this assumption can potentially be made more accurate by choosing a more appropriate relationship. Thus, it is known as a **reducible error**.

Even if we do have assumed the true $f$, our model will still have some inaccuracies. This is because $$Y$$ is also a function of $$\epsilon$$, which is called the **irreducible error**.

It contains the error caused because $$\hat{f}$$ did not consider some useful predictors, or due to unmeasured variation in predictors already considered by $$\hat{f}$$. The irreducible error will always provide an upper bound to the accuracy of our predictions and classifications.

# How to estimate $f$?

There are two categories of statistical methods for estimating $f$:

- Parametric methods
- Non Parametric methods

## Parametric Methods

This is a two step approach:

- Make an assumption about the functional form or shape of $f$. A simple assumption is that $f$ is linear.

$$
f(X) = \beta_0 + \beta_1 X_1 + ... + \beta_p X_p
$$

This is a linear model. Once this is assumed, the problem of estimating $f$ is greatly simplified. Instead of trying to estimate an arbitrary p-dimensional *function* $f(X)$, we only need to estimate $p + 1$ *coefficients* $\beta_0, \beta_1, ... \beta_p$.

- Now we use estimate the parameters or coefficients $$\beta_0, \beta_1, ... \beta_p$$ using a training dataset such that:

$$
Y \approx \beta_0 + \beta_1 X_1 + ... + \beta_p X_p
$$

This is called **fitting a model** to a dataset. The most common approach for fitting a linear model is the ordinary least squares (OLS) method which will be discussed in another post.

This approach is called the parametric methods as it reduces the problem of estimating $f$ to simply estimating a set of parameters. The disadvantage is that if the model chosen for $f$ is far from the true $f$, then our model will be poor.

<figure style="width: 500px">
	<img src="/media/machine learning/basics/parametric-method.png" alt="Parametric Method - Fitting a Linear Model">
	<figcaption>Parametric Method - Fitting a Linear Model</figcaption>
</figure>

## Non-Parametric Methods

This approach does not make any explicit assumptions about the functional form of $f$. Thus, it avoids the danger of a bad assumption.

It tries to estimate a functional shape that gets close to the data points without being too wiggly. It has the potential to fit a wider range of possible shapes for $f$.

The disadvantage of this approach is that, compared to parametric methods, a dataset with a large number of examples is required to estimate $f$.

For example, we can use a thin-plate spline. The name thin plate spline refers to a thin sheet of metal. This spline can be bent to get close as possible to all the data points. The resulting shape is the functional shape of $f$.

<figure style="width: 500px">
	<img src="/media/machine learning/basics/non-parametric-method.png" alt="Non-Parametric Method - Fitting a Thin-Plate Spline">
	<figcaption>Non-Parametric Method - Fitting a Thin-Plate Spline</figcaption>
</figure>

# Prediction accuracy vs Model Interpretability

Some models, like linear models, are much less flexible compared to models using thin-plane splines. Linear regression is relatively inflexible and can only generate lines as functional shapes.

**So, why would we ever choose a model with low flexibility?** This is because *restrictive models are much more interpretable.* As the flexibility of models decrease, the interpretablity increases.

The goal of **interpretation** is to understand the relationship between $Y$ and $X$; not to make a prediction for $Y$ given $X$. We are simply asking questions like:

- **Which predictors are associated with the response?** Often only a small subset of available predictors are substantially associated with $Y$. Identifying them can be very useful.
- **What is the relationship between the response and each predictor?** The value of $Y$ may increase as a predictor $X_i$ is increased in value. This is a *positive relationship*. Other predictors may have a *negative relationship* with the response. The relationship between a response and a predictor might depend on other predictors.

<figure style="width: 500px">
	<img src="/media/machine learning/basics/flexibility-interpretability.png" alt="Flexibility Interpretability">
	<figcaption>Flexibility Interpretability</figcaption>
</figure>

One might think that the most flexible model will provide the best predictive model. This is not necessarily the case. This has to do with the concept of overfitting, which is explained later in this post.

# Supervised vs Unsupervised Learning

Most statistical learning problems fall into two categories: *supervised* and *unsupervised*. **Supervised learning** attempts to fit a model to a dataset with inputs $X$ leading to a response $Y$, such that the model works well with unseen inputs. Examples include Linear and logistic regression.

In contrast, **unsupervised learning** algorithms work with datasets without a response variable $Y$. We are in some sense blind, because there is nothing to supervise our analysis. Linear regression cannot be used with a dataset without a response variable.

So, what kind of analysis is possible? One possibility is *cluster analysis*. Its goal is to categorize a dataset into multiple classes based on a set of features. If used for predictions, any new input must be placed under the proper class.

# Regression vs Classification

Problems involving continuous response variables are named **regression problems**, and problems involving categorical response variable are **classification problems**.

**Continuous variables** take on numerical values such as integers or floating point values. For example, a house may be predicted to sell for 200,000 dollars.

In contrast, **categorical variables** take on one of many classes or categories. For example, brand of shoe purchased (Nike, Adidas Or Puma).

<figure style="width: 500px">
	<img src="/media/machine learning/basics/classification-vs-regression.png" alt="Regression vs Classification">
	<figcaption>Regression vs Classification</figcaption>
</figure>

# Calculating Model Accuracy

In order to evaluate performance of a learning method on a given dataset, we need a way to measure how well its prediction responses actually match true responses in observed data. In regression problems, the most commonly used measure is the **mean squared error** (MSE).

$$
MSE = \frac{1}{n}\sum_\text{i = 1}(y_i - \hat{f}(x_i))^2
$$

where $\hat{f}(x_i)$ provides the prediction for ith observation, and $y_i$ is the actual response variable for ith observation. The MSE value will be small if the predicted responses are very close to true responses.

<figure style="width: 500px">
	<img src="/media/machine learning/basics/mse.png" alt="MSE">
	<figcaption>MSE</figcaption>
</figure>

If training data is used to compute MSE, it is called **training MSE**, and if test data is used, it is **test MSE**.

Since our goal is to build a model that works accurately with previously unseen inputs (test data), we prefer models with the lowest test MSE as opposed to one with the lowest training MSE.

# Flexibility and Generalization

A good model accurately *captures the regularities* in its training data and also *generalizes well* to unseen data. An important hurdle in achieving this is finding the proper model flexibility.

<figure style="width: 500px">
	<img src="/media/machine learning/basics/flexibility.png" alt="Flexibility">
	<figcaption>Flexibility</figcaption>
</figure>

When a model is highly flexible, it hugs the data points very tightly, so it is a good representation of the training dataset. But it does not generalize well to unseen inputs. This is because they are fitting the fringe and noisy data points too. This error is called **overfitting**.

When the model is inflexible it is incapable of representing the regularities in the dataset. Since it cannot representing the training dataset, it cannot be expected to generalize well to unseen inputs. This error is called **underfitting**.

## Flexibility and MSE

We plot the test and training MSE of a model against varying degrees of flexibility.

<figure style="width: 700px">
	<img src="/media/machine learning/basics/u-shape.png" alt="Flexibility vs MSE">
	<figcaption>Flexibility vs MSE. The gray curve is the training MSE and red curve is the test MSE.</figcaption>
</figure>

When the model flexibility is very low, it suffers from underfitting. So the training MSE will be very high. Since underfitting contributes to bad generalization, the test MSE is also high.

As we increase the flexibility, the model can capture more of the regularities in the dataset, so both the training and test MSE decrease.

But if the model flexibility is too high, the training MSE inches closer and closer to $0$ because it suffers from overfitting. The test MSE on the other hand increases after a certain point. This is due to the fact that noisy data points are being learnt, causing bad generalization.

Note that we expect the training MSE to almost always be smaller than the test MSE, as most learning methods either directly or indirectly seek to minimize the training MSE.

## Bias-Variance Tradeoff

The **bias–variance tradeoff** is central in the conflict to prevent overfitting and underfitting.

**Bias** is the inability of a learning algorithm to capture the true relationship between the predictors and the response. It is exhibited by relatively inflexible methods like linear regression.

**Variance** is the error caused by sensitivity to small fluctuations in the dataset. High variance is exhibited by highly flexible methods like polynomial regression. If a model has *high* variance, it means small changes in the training data can result in large changes in $\hat{f}$.

Variance and bias are two opposing forces.

- Increasing bias will decrease variance
- Increasing variance will decrease bias

The challenge lies in finding a method for which we both variance and bias are low.

# Solving Overfitting and Underfitting

## Size of the data set

Given a fixed model flexibility, overfitting reduces as we increase the number of data points. This because as we increase the number of points it becomes more difficult for the regression line to hug all the points.

# References
- [StatQuest : Bias and Variance](https://www.youtube.com/watch?v=EuBBz3bI-aA&list=LLm-oVeNttHguGRcnMcWtZRg&index=2&t=0s)
- [Introduction to Statistical Learning](http://faculty.marshall.usc.edu/gareth-james/ISL/)
