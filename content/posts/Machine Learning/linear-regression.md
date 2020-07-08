---
title: "Linear Regression"
date: "2020-6-22"
template: "post"
draft: false
slug: "/posts/linear-regression/"
category: "Machine Learning"
tags:
- ""
description: ""
---

Regression analysis explores the relationship between a quantitative response variable and one or more explanatory variable.

Linear regression methods attempt to solve regression tasks by assuming that the response $y$ is a *linear* function of one or more explanatory variable $x_1, x_2, \cdots, x_n$.

The general form of a linear function or linear relationship is,

$$
y = \beta_0 + \beta_1 x_1 + \cdots + \beta_n x_n + \epsilon
$$

where $\epsilon$ is the irreducible error.

The relationship is estimated using,

$$
\hat{y} = \hat{\beta_0} + \hat{\beta_1} x_1 + \cdots + \hat{\beta_n} x_n
$$

The graph is a $n$-dimensional [hyperplane](https://en.wikipedia.org/wiki/Hyperplane) in a $n + 1$ dimensional space, where the extra dimension is reserved for the response variable $y$.

The goal of linear regression is to estimate the coefficients $\beta_0, \cdots, \beta_n$ such that the regression line closely fits the training data. The most common approach to measure closeness of fit is the least squares criterion.

# Table of Contents

- Simple Linear Regression
- Multiple Linear Regression
- Polynomial Linear Regression
- Fitting Criteria
	- Ordinary Least Squares
	- Ordinary Least Squares with **L1** penalty
	- Ordinary Least Squares with **L2** penalty
- Calculating Model Performance
	- Mean Squared Error

# Simple Linear Regression

The case with one explanatory variable is called *simple* linear regression. The graph forms a line,

$$
\hat{y} = \hat{\beta_0} + \hat{\beta_1} x_1
$$

<figure style="width: 800px">
	<img src="/media/machine learning/basics/mse.png" alt="MSE">
	<figcaption>Residual <b>e</b></figcaption>
</figure>

The **residual** $e_i$ is the difference between the observed response and the predicted response.

$$
\begin{aligned}
	e_i &= \text{Observed value} - \text{Predicted value}
	\\
	&= y_i - \hat{y_i}
\end{aligned}
$$

The points above the line have positive residuals while the points below the line have negative residuals. Intuitively we can tell that the best line through the data is one that has the smallest residuals.

To measure this we define the **sum of squared residues**,

$$
\begin{aligned}
	\text{SSR} &= \sum_i e_i^2
	\\
	&= \sum_i (y_i - \hat{y_i})^2
	\\
	&= \sum_i (y_i - \hat{\beta_0} - \hat{\beta_1} x_i)^2
\end{aligned}
$$

A small SSR indicates that the model is tightly fit to the data.

<figure style="width: 800px">
	<img src="/media/machine learning/linear regression/Reducing SSR.png" alt="Reducing SSR">
	<figcaption>Reducing SSR</figcaption>
</figure>

We need to find values for the coefficients $\beta_0$ and $\beta_1$ such that the SSR is minimized. Graphically these values are the coordinates at the red dot. The red dot has a slope of $0$.

Solve the following partial differential equations,

$$
\begin{aligned}
	\frac {\partial \text{ SSR}} {\partial \beta_0} &= 0
	\\\\
	\frac {\partial \text{ SSR}} {\partial \beta_1} &= 0
\end{aligned}
$$

to get the best values for $\beta_0$ and $\beta_1$,

$$
\begin{aligned}
	\hat{\beta_1} &= \frac {\sum_{i = 1}^n (x_i - \bar{x}) (y_i - \bar{y})} {\sum_{i = 1}^n (x_i - \bar{x})^2}
	\\\\
	\hat{\beta_0} &= \bar{y} - \hat{\beta_1} \bar{x}
\end{aligned}
$$

[Derivation](https://youtu.be/ewnc1cXJmGA)

# Multiple Linear Regression

The case with two or more predictor variables is called *multiple* linear regression. The graph for two predictor variables forms a plane.

$$
\hat{y} = \hat{\beta_0} + \hat{\beta_1} x_1 + \hat{\beta_2} x_2
$$

<figure style="width: 500px">
	<img src="/media/machine learning/basics/parametric-method.png" alt="Multiple Linear Regression">
	<figcaption>Multiple Linear Regression</figcaption>
</figure>

# Polynomial Linear Regression

# Fitting Criteria

# Calculating Model Performance

In order to evaluate performance of a learning method on a given dataset, we need a way to measure how well its prediction responses actually match true responses in observed data.

## Mean Squared Error

In regression problems, the most commonly used measure is the **mean squared error** (MSE).

$$
MSE = \frac{1}{n}\sum_\text{i = 1}(y_i - \hat{f}(x_i))^2
$$

where $\hat{f}(x_i)$ provides the prediction for ith observation, and $y_i$ is the actual response variable for ith observation. The MSE value will be small if the predicted responses are very close to true responses.

If training data is used to compute MSE, it is called **training MSE**, and if test data is used, it is **test MSE**.

Since our goal is to build a model that works accurately with previously unseen inputs (test data), we prefer models with the lowest test MSE as opposed to one with the lowest training MSE.

# References

- [Wikipedia : Linear regression](https://en.wikipedia.org/wiki/Linear_regression)
- [Simple Linear Regression: The Least Squares Regression Line](https://youtu.be/coQAAN4eY5s)
