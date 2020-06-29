---
title: "Support Vector Machines"
date: "2019-12-24"
template: "post"
draft: false
slug: "/posts/svm/"
category: "Machine Learning"
tags:
  - ""
description: ""
---

Support vector machines are supervised learning models designed for binary classification problems. However, there are ways to extend them for multi-class problems.

The main goal of an SVM is to draw a *hyperplane* that best divides the training set into two classes.

# The Hyperplane

<figure style="width: 600px">
	<img src="/media/machine learning/svm/hyperplane.png" alt="Hyperplane">
	<figcaption>Hyperplane</figcaption>
</figure>

A **hyperplane** is a line that separates and classifies a set of data. A hyperplane is a subspace whose dimension is one less than that of its parent space.

So, the hyperplanes of a two-dimensional space are lines. The hyperplanes of a three-dimensional space are planes, and so on. The above diagram shows you a 1D hyperplane.

# Choosing an hyperplane

<figure style="width: 500px">
	<img src="/media/machine learning/svm/best-hyperplane.png" alt="Best Hyperplane">
	<figcaption>Best Hyperplane</figcaption>
</figure>

There are many possible ways to draw the hyperplane, but we need the one that cuts the dataset into two classes.

Hyperplane $A$ is clearly not a good classifier. $B$ and $C$ are good candidates, but which one is better?

Intuitively, the best hyperplane is one that has the largest distance to the nearest training data points of any class. This makes $C$ the best option.

These nearest training points to the hyperplane are called **support vectors**. The distance between the hyperplane and the support vectors from either class is known as the **margin**.

If any support vectors are removed, the position of the dividing hyperplane will also change. Hence, they are critical elements of a dataset.

The support vectors essentially define the position and orientation of the hyperplane. If these support vectors are outliers, then the hyperplane will not be good. This sensitivity to outliers is a disadvantage of SVMs.

These vectors are also the most ambiguous and difficult to classify observations of your dataset. If you are classifying cats and dogs, one of these support vectors might include a dog that kinda looks like a cat.

# Training on linearly non-separable datasets

<figure style="width: 750px">
	<img src="/media/machine learning/svm/separable.png" alt="Separable">
	<figcaption>Separable</figcaption>
</figure>

Datasets are rarely ever cleanly linearly separable. So, what happens when you cannot draw a hyperplane through your dataset? In order to draw it, we need to transform this **linearly non-separable dataset** into a **linearly separable dataset**.

This can be done by mapping all the points to a higher dimension.

Take a look at the following 1D dataset. In order to map these points to a higher dimension $y$ we need a function.

<figure style="width: 600px">
	<img src="/media/machine learning/svm/1D.png" alt="1D">
	<figcaption>1D</figcaption>
</figure>

Let's try a simple one : $y = x^2$.

<figure style="width: 550px">
	<img src="/media/machine learning/svm/2D.png" alt="2D">
	<figcaption>2D</figcaption>
</figure>

Now, the dataset is easily divided by a straight line within this two-dimensional space.

The disadvantage of mapping is that a single mapping might not be enough for separating the points. We must continue mapping them into higher and higher dimensions until a hyperplane can be formed to segregate it. This is very computationally expensive.

This is where kernel functions come in.

## Kernel Function

Kernel functions measure the similarity between objects. Some kernels include the RBF kernel and the polynomial kernel.

I don't know how they work yet. So, your gonna have to go somewhere else.

# References

- [Wikipedia](https://en.wikipedia.org/wiki/Support-vector_machine#Linear_SVM)
