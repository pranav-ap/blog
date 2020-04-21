---
title: "Random Forest for Classification and Regression"
date: "2019-11-24"
template: "post"
draft: false
slug: "/posts/random-forest/"
category: "Machine Learning"
tags:
  - ""
description: ""
---

**Random forest** is a supervised learning method for prediction that operates by constructing multiple decision trees during training.

Decision trees are easy to build and interpret, but suffer from inaccuracy. They do not generalize well to new data. Random forests solve this problem.

But first, we must learn *Bootstrapping* and *Bagging*.

# Bootstrapping

**Bootstrapping** is a way to create a new dataset based on an existing one.

The new dataset is created by randomly selecting $n$ rows with replacement. This means some rows in the new dataset may be duplicates.

<figure style="width: 850px">
	<img src="/media/machine learning/decision trees/bootstrapping.png" alt="Bootstrapping">
	<figcaption>Bootstrapping</figcaption>
</figure>

# Bootstrap Aggregation

The **Bootstrap Aggregation** algorithm creates multiple models of the same kind from a single training dataset. It is also called **Bagging**.

Consider the following algorithm to train a bundle of decision trees given a dataset of $n$ points:

<figure style="width: 600px">
	<img src="/media/machine learning/decision trees/bagging.png" alt="Bagging">
	<figcaption>Bagging</figcaption>
</figure>

# How to make a prediction?

To make a prediction using this model with $n$ trees, we aggregate the predictions from the individual decision trees.

<figure style="width: 650px">
	<img src="/media/machine learning/decision trees/bag-predict.png" alt="Bagging Prediction">
	<figcaption>Bagging Prediction</figcaption>
</figure>

- Take the *majority vote* if the trees produce class labels.
- Take the *average* if the trees produce numerical values.

Bagging is a special case of the *model averaging approach*. Although it is usually applied to decision tree methods, it can be used with any type of method.

# Building a Random Forest

The procedure to build a Random forest is almost the same as for Bagging. The difference is that Random forests have a parameter that controls how many features to try when finding the best split.

Suppose we had a dataset with $n$ features. Instead of trying all features every time we make a new decision node, we *only try a random subset of the features*, usually of size $\sqrt{n}$ or $\frac{n}{3}$. This technique is called **feature bagging**.

Using bootstrapped datasets and feature bagging introduces randomness that makes individual trees more unique and reduces correlation between them. This *variety* makes the Random forest more effective than individual trees for predicting new data.

# References

- [Artificial Intelligence: A Modern Approach](http://aima.cs.berkeley.edu/)
- [StatQuest: Random Forests Part 1 - Building, Using and Evaluating](https://www.youtube.com/watch?v=J4Wdy0Wc_xQ&t=277s)
- [Victor Zhou: Random Forests for Complete Beginners](https://victorzhou.com/blog/intro-to-random-forests/)
