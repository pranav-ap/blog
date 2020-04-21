---
title: "Decision Trees for Classification and Regression"
date: "2019-11-24"
template: "post"
draft: false
slug: "/posts/decision-trees/"
category: "Machine Learning"
tags:
  - ""
description: ""
---
**Decision Trees** are a non-parametric supervised learning method used for both classification and regression tasks.

It learns simple decision rules from the data; and these rules are represented as nodes of a tree. Due to their tree structure, they are easy to interpret.

These trees form the basis for the *Random Forest algorithm* and are used often in ensemble algorithms like *bagging* or *boosting*.

Here, I will present a supervised learning algorithm for building a decision tree based on Gini impurities.

# Structure of the model

<figure style="width: 700px">
	<img src="/media/machine learning/decision trees/decision-tree.png" alt="Decision Tree">
	<figcaption>Decision Tree</figcaption>
</figure>

The model has a tree structure with interior nodes, edges and leaf nodes. The interior nodes of the tree represent the input features from the dataset. These are called **decision nodes**.

The **edges** leading out of a decision node represent all the possible values for the feature. In this case, all decisions have simple Yes or No branching.

Each **leaf node** represents the value of the output variable given the values of the input variables. The value depends on the path from the root to the leaf. This model tells us whether or not the person has a heart disease.

The leaf node is actually a subset of the original dataset. If this subset's target column has class $i$ as the majority, then any new observation that leads to this leaf is assigned class $i$.

# Calculating Gini Gain

Algorithms for constructing decision trees usually work by choosing a input variable that *best splits the dataset* on the target variable. Different algorithms use different metrics for measuring "best" input variable.

Generally, they measure the homogeneity of the target variable within the subsets. A dataset is said to be homogeneous if all observations lead to the same value for the target variable.

<figure style="width: 600px">
	<img src="/media/machine learning/decision trees/decision-tree-table.png" alt="Decision Tree Table">
	<figcaption>Decision Tree Table</figcaption>
</figure>

Look at the dataset given above.

It has three features and a target variable, *Heart disease*. The target variable column has four *yeses* and one *no*. Lets try splitting the dataset on the *Chest Pain* variable. This gives use the two following subsets.

<figure style="width: 600px">
	<img src="/media/machine learning/decision trees/split-table.png" alt="Decision Tree Split Table">
	<figcaption>Decision Tree Split Table</figcaption>
</figure>

Clearly, the first subset is not completely homogeneous. But how do we quantify partial homogeneity?

There are a bunch of methods to calculate homogeneity, but two of the most widely used methods are:

- Gini Impurity
- Entropy

Here, I will cover Gini Impurity.

## Gini Impurity

**Gini Impurity** is the probability of classifying an observation *incorrectly*.

If we have $C$ total classes and $p(i)$ is the fraction of target variables labeled with class $i$, then the **Gini Impurity** is calculated as:

$$
G = 1 - \sum_{i}^C p_i^2  \\
$$

A Gini Impurity of $0$ is the lowest and best possible impurity. It can only be achieved when everything in the target column is the same class.

## Gini Gain

**Gini gain** is the difference in impurity between a dataset and the subsets created after a split.

It is calculated by subtracting the weighted impurities of the branches from the original impurity.

$$
GG = G_{original} - (\frac {n_i} {n_{original}}) * G_i
$$

where, $G_i$ represents the Gini impurity of subset $i$ and $n_i$ is the number of observations in dataset $i$.

The reason we take the *weighted* impurities of the subsets is that the number of observations in the subsets can be different; and this must not affect the Gini gain.

# Constructing the tree

A decision tree is built progressively starting from the root node to the leaves, one node at a time. The steps involved are as follows:

<figure style="width: 800px">
	<img src="/media/machine learning/decision trees/building-tree.png" alt="Building a Decision Tree">
	<figcaption>Building a Decision Tree</figcaption>
</figure>

After one pass of this algorithm, we would have chosen one variable as the root node and it will have branches with one dataset each.

<figure style="width: 650px">
	<img src="/media/machine learning/decision trees/stump.png" alt="Stump">
	<figcaption>Stump</figcaption>
</figure>

Next we choose one of these subsets and perform the same operations again, creating another bunch of subsets.

## When do you stop constructing the tree?

If there were many input variables, then this construction process could go on for a long time. To stop, you can do any one of the following:

1. Use a *maximum depth value*. You can restrict the total length of any path in the tree.
1. If the *Gini gain decreases*, stop going deeper down a certain path. A decrease in Gini gain means that the impurity is increasing.
1. Stop if the number of instances in the subset is lower than a predefined threshold.
1. Stop if the standard deviation of the target column is lower than a predefined threshold.

The leaf nodes do not have to be pure for us to make predictions. If a new observation leads you to an impure node, simply assign the class that is the most common in the leaf node. The probability of this class within this leaf (subset) provides the confidence value for this prediction.

# Handling Continuous values

### What if the input variable is continuous?

Consider a new continuous feature, *weight* to predict heart disease.

<figure style="width: 650px">
	<img src="/media/machine learning/decision trees/weight-feature.png" alt="Weight Feature">
	<figcaption>Weight Feature</figcaption>
</figure>

In the case of categorical data, we can simply create one branch per class. We can't do that here. So we look for a way to split this column into two classes.

1. Arrange the rows in ascending order of weights.
1. Find the average between weights of successive rows.
1. Split the dataset into two on the average, to create multiple subset pairs.
1. Calculate Gini impurity for each split.
1. Choose the split that gives lowest Gini impurity.

The Gini gain of this split can be compared with other features like Chest Pain, Blocked Arteries, etc. The rest of the tree construction process remains the same.

### What if the target variable is continuous?

If the target variable is continuous, we calculate the average of the values in the target column as the value for the observation's target variable.

# References

- [Artificial Intelligence: A Modern Approach](http://aima.cs.berkeley.edu/)
- [StatQuest : Decision Trees](https://www.youtube.com/watch?v=7VeUPuFGJHk&list=LLm-oVeNttHguGRcnMcWtZRg&index=2&t=0s)
- [Wikipedia : Decision Tree Learning](https://en.wikipedia.org/wiki/Decision_tree_learning)
