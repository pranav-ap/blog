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

Classical machine learning algorithms like Linear regression and SVMs require us to design the features before training can begin. Their performance depends heavily on the *representation* of the data they are given.

A **feature** is a measurable property of some phenomenon. Choosing informative and independent features is a crucial step for effective algorithms.

Coming up with features is difficult, time-consuming, requires expert knowledge.

A feature is an attribute or property shared by all of the independent units on which analysis or prediction is to be done. Any attribute could be a feature, as long as it is useful to the model.

The purpose of a feature, other than being an attribute, would be much easier to understand in the context of a problem. A feature is a characteristic that might help when solving the problem.

choosing the right features is still very important. Better features can produce simpler and more flexible models, and they often yield better results.

<figure style="width: 530px">
	<img src="/media/deep learning/ml-vs-dl.jpg" alt="ML vs DL">
	<figcaption>ML vs DL</figcaption>
</figure>

You can improve the quality of your dataset’s features with processes like feature selection and feature engineering, which are notoriously difficult and tedious. If these techniques are done well, the resulting optimal dataset will contain all of the essential features that might have bearing on your specific business problem, leading to the best possible model outcomes and the most beneficial insights.

Feature engineering is the process of creating features (also called "attributes") that don't already exist in the dataset. This means that if your dataset already contains enough "useful" features, you don't necessarily need to engineer additional features.

The performance of machine learning algorithms depends heavily on the representation of the given raw data. Raw data is in the form of a table

If the features in the raw data are relevant, then the algorithm ca.

<figure style="width: 550px">
	<img src="/media/deep learning/learning-features.png" alt="Learning Features">
	<figcaption>Learning Features</figcaption>
</figure>

In machine learning, feature learning or representation learning[1] is a set of techniques that allows a system to automatically discover the representations needed for feature detection or classification from raw data. This replaces manual feature engineering and allows a machine to both learn the features and use them to perform a specific task.

Feature learning is motivated by the fact that machine learning tasks such as classification often require input that is mathematically and computationally convenient to process. However, real-world data such as images, video, and sensor data has not yielded to attempts to algorithmically define specific features. An alternative is to discover such features or representations through examination, without relying on explicit algorithms.

Feature learning can be either supervised or unsupervised.

In supervised feature learning, features are learned using labeled input data. Examples include supervised neural networks, multilayer perceptron and (supervised) dictionary learning.
In unsupervised feature learning, features are learned with unlabeled input data. Examples include dictionary learning, independent component analysis, autoencoders, matrix factorization[2] and various forms of clustering.

# References

- [Michael Nielsen](http://neuralnetworksanddeeplearning.com)
- [Wikipedia: Artificial neural network](https://en.wikipedia.org/wiki/Artificial_neural_network)
- [Wikipedia: Feature engineering](https://en.wikipedia.org/wiki/Feature_engineering)
- [Wikipedia: Feature learning](https://en.wikipedia.org/wiki/Feature_learning)
- [Wikipedia: Deep learning](https://en.wikipedia.org/wiki/Deep_learning)