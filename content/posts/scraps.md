---
title: "Scraps"
date: "2020-6-22"
template: "post"
draft: true
slug: "/posts/scraps/"
category: ""
tags:
- ""
description: ""
---

**Machine learning** is a set of mathematical tools for developing accurate statistical models of real-world events. The models are used to predict, classify and explore relationships. Learning is used when we cannot derive a complete mathematical relationship but we have a considerable amount of data.

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
