---
title: "Neural Networks"
date: "2020-1-9"
template: "post"
draft: false
slug: "/posts/neural-networks/"
category: "Deep Learning"
tags:
   - ""
description: ""
---

Most knowledge required for tasks including speech and image recognition is informal, subjective and intuitive. This makes it difficult to encode into a program.

The performance of learning algorithms depends heavily on the *representation* of the data they are given. Classical machine learning algorithms like Linear regression and SVMs require us to design the features / columns before training can begin.

A **feature** is a measurable property of some phenomenon. Choosing informative and independent features is a crucial step for effective algorithms.

Coming up with features is difficult, time-consuming, requires expert knowledge. This is called **feature engineering**. If done well, the resulting dataset will lead us to the best possible model.

# Feature learning

**Feature learning** or **representation learning** is a set of techniques that automatically discover the features necessary for making a good model directly from raw data.

This replaces manual feature engineering and allows a machine to both learn useful features and use them to perform a task.

<figure style="width: 550px">
	<img src="/media/deep learning/learning-features.png" alt="Learning Features">
	<figcaption>Learning Features</figcaption>
</figure>

Feature learning can be either supervised or unsupervised. Examples of supervised feature learning include neural networks and multilayer perceptrons. Examples of unsupervised feature learning include Principal component analysis and K-means clustering.

# References

- [Michael Nielsen](http://neuralnetworksanddeeplearning.com)
- [Wikipedia: Artificial neural network](https://en.wikipedia.org/wiki/Artificial_neural_network)
- [Wikipedia: Feature engineering](https://en.wikipedia.org/wiki/Feature_engineering)
- [Wikipedia: Feature learning](https://en.wikipedia.org/wiki/Feature_learning)
- [Wikipedia: Deep learning](https://en.wikipedia.org/wiki/Deep_learning)
