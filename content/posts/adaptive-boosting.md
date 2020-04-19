---
title: "Adaptive Boosting"
date: "2019-12-4"
template: "post"
draft: false

category: "Machine Learning"
tags:
  - ""
description: ""
---

Ensemble methods are algorithms that use multiple learning algorithms to obtain better predictive performance than could be obtained from any of the algorithms individually.

The trained ensemble represents a single model, and tends to yield better results when there is significant diversity among its constituent models. Thus, many ensemble methods seek to promote diversity among the constituent models.

**Boosting** and **Bagging** are two major families of algorithms that fall under the umbrella of ensemble methods. Here we will cover a form of Boosting called Adaptive Boosting, also known as AdaBoost.

# The weak learner

A **learner** is a program takes the training dataset $(X, Y)$, fits a model to it and producing a predictor. A **predictor** takes a single observation $X'$ and produces $Y'$. A predictor can be a classifier or a regressor.

A **weak learner** produces a predictor that is only slightly better than random guessing. In contrast, a strong learner produces a accurate predictor.

The key idea behind boosting is to train *sequence* of weak predictors, each trying to correct the inaccurate predictions made by it predecessor.

<figure style="width: 600px">
	<img src="/media/machine learning/boosting/boosting.png" alt="Boosting">
	<figcaption>Boosting</figcaption>
</figure>

The most widely used weak learner in AdaBoost are **decision stumps**. A decision stump is a decision tree that makes a prediction based on the value of a *single* input feature. A stump contains one decision node and two or more leaves.

<figure style="width: 500px">
	<img src="/media/machine learning/boosting/decision-stump.png" alt="Decision Stump">
	<figcaption>Decision Stump</figcaption>
</figure>

## Why use decision stumps?

Decision trees are reasonably fast to train. And since we are going to be hundreds or thousands of them, this is a good thing. They also give out their prediction very quickly, since they have only one decision node.

A weak learner needs to be *consistently* better than random guessing. You don't normally need to do any parameter tuning to a decision tree to get this behavior. But training a SVM model, on the other hand, requires a parameter search. And since the data is re-weighted on each iteration, you will need to do a parameter search for each iteration.

# Building the strong predictor

<figure style="width: 900px">
	<img src="/media/machine learning/boosting/adaptive-boosting.png" alt="Adaptive Boosting">
	<figcaption>Adaptive Boosting</figcaption>
</figure>

## Choosing the best stump

For choosing the best stump, we can use the Gini gain.

## The Purpose of assigning Observation weights

<figure style="width: 700px">
	<img src="/media/machine learning/boosting/initial-weights.png" alt="Initial Weights">
	<figcaption>Initial Weights</figcaption>
</figure>

Initially, all observations are given the same normalized weight. The formula for this initial weight is:

$$
w_i = \frac {1} {n}
$$

where $n$ is the no of observations.

The weight of an observation represents its importance to a learner $l$. The observation with the higher weight is given more importance by $l$. This improves the chance that $l$ correctly predicts the value.

If the current learner $l_c$ predicts an observation $o_i$ inaccurately, then it's weight must be increased. This signals the next learner $l_n$ to give $o_i$ more importance, since it is yet to be accurately predicted.

The formula to get the *increased weight* of an incorrectly predicted observation is:

$$
w_i = w_i \times e^{w_s}
$$

where, $w_s$ is the weight of the stump and $w_i$ is the weight of $o_i$.

If the current learner $l_c$ predicts an observation $o_i$ accurately, then it's weight is decreased. This signals the next learner $l_n$ to not lay too much importance on $o_i$, since it is already accurately predicted.

The formula to get the *reduced weight* of an accurately predicted observation is:

$$
w_i = w_i \times e^{- w_s}
$$

where, $w_s$ is the weight of the stump and $w_i$ is the weight of $o_i$.

## The Purpose of assigning stump weights

The result of boosting is a *forest of stumps*. When it is time for the ensemble to make a prediction, each stump gets a vote, ie. each stump makes a prediction.

But some stumps are better at prediction, so their vote is more important. A stump's weight quantifies its importance.

### Calculating stump weight

There are two steps to calculate stump weight. First, we must calculate the total error made by the stump.

$$
\text{Total Error} (s) = \sum w_{ipo}
$$

where, $w_{ipo}$ is the weight associated with an *incorrectly predicted observation*.

Since all the sample weights add upto $1$, total error for a stump will always be between $0$ and $1$, with $0$ total error for the perfect stump and $1$ for a horrible stump.

We can now use the $\text{total error}$ to calculate stump weight. Stump weight needs to be high if it is a good predictor; small otherwise.

$$
w_s = \frac {1} {2} \, log (\frac {1 - {\text{total error}}_s} {{\text{total error}}_s})
$$

This formula gives us the required relationship between $\text{total error}$ and $\text{weight}$. As the total error moves closer to 1, the importance *(weight)* of the stump is given a large negative value. As the total error moves closer to 0, the weight of the stump moves towards a large positive value.

This behavior can be seen in the graph.

<figure style="width: 450px">
	<img src="/media/machine learning/boosting/stump-weight-graph.png" alt="Stump Weight Graph">
	<figcaption>Stump Weight Graph</figcaption>
</figure>

# Weighed voting

Now we have a forest of stumps, each with its own weight. How do we make a prediction on a new observation?

We run the observation through each of the stumps. Each stump outputs a class or a value, depending on the type of the problem.

In a classification setting, we simply calculate the sum of the stump weights for each class. The class with the largest stump weight is the final ensemble prediction.

In the example below, it is clear that the class *Has Heart Disease* has a weight of $0.6 + 0.2 = 1.0$ behind it. Thus it is the final prediction.

<figure style="width: 600px">
	<img src="/media/machine learning/boosting/classification-voting.png" alt="Classification Voting">
	<figcaption>Classification Voting</figcaption>
</figure>

# Drawbacks of Boosting

**Computational Complexity :** The most obvious drawback of boosting is the *computational complexity*. Generating multiple models requires a lot of computations and time. However, using decision stumps instead of more complex constituent models helps to mitigate this problem.

**Sensitivity :** The biggest criticism for Boosting comes from its *sensitivity to noisy data*. At each iteration, Boosting tries to improve the output for data points that have not been predicted well until now. If your dataset happens to have a lot of outlier points, boosting will try very hard to fit subsequent weak learners to these noisy samples. As a result, overfitting is likely to occur.

# References

- [StatQuest : AdaBoost](https://www.youtube.com/watch?v=LsK-xG1cLYA&list=WL&index=15)
- [Stack Overflow : Why AdaBoost wth Decision Trees?](https://stats.stackexchange.com/questions/124628/why-adaboost-with-decision-trees?rq=1)
- [Artificial Intelligence: A Modern Approach](http://aima.cs.berkeley.edu/)
