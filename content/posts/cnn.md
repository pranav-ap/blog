---
title: "Convolutional Neural Networks"
date: "2020-3-6"
template: "post"
draft: false
slug: "/posts/cnn/"
category: "Deep Learning"
tags:
   - ""
description: ""
---

# Image representation

A gray scale image is a two-dimensional matrix of numbers, where each element, called a **pixel**, ranges from $0$ to $255$. Black pixels are encoded as $0$, and white pixels are encoded as $255$. Gray colors fall between them.

<figure style="width: 400px">
	<img src="/media/vision/grayscale-number.gif" alt="Grayscale Number">
	<figcaption>Grayscale Number</figcaption>
</figure>

Color images are represented using a three-dimensional matrix. Each dimension is called a **channel** and they hold the red, green and blue pixel values.

<figure style="width: 450px">
	<img src="/media/vision/color channels.png" alt="Color Channels">
	<figcaption>Color Channels</figcaption>
</figure>

Pixels of both gray scale and color images are usually normalized into the range $0$ to $1$ by dividing each by $255$ for use in training.

# Convolution

The convolution operation is used to transform an image to make it easier to identify primitive shapes within the original image.

The general idea is that we use multiple filters to extract a different features from an input image and these features will be useful for classifying it.

The primary tool for convolution is the **filter**. They are simple two-dimensional matrices that can detect horizontal or vertical lines, curves and edges within the image. Some filters are used to blur images, while others can smoothen rough edges.

<figure style="width: 600px">
	<img src="/media/vision/cnn/filter_in_action.gif" alt="Convolution Operation">
	<figcaption>Convolution Operation</figcaption>
</figure>

The matrix for edge detection is,

$$
\begin{bmatrix}
   -1 & -1 & -1 \\
   -1 & 8 & -1 \\
   -1 & -1 & -1 \\
\end{bmatrix}
$$

We can use an input image and a filter to produce an output image by convolving the filter with the input image.

We execute a convolution by sliding the filter over the input image. At every location, it performs an element-wise multiplication between the values in the filter and their corresponding values in the image, adds up the products and writes it into the output image matrix.

The number of pixels a filter moves in a single step is called the **stride**.

<figure style="width: 400px">
	<img src="/media/vision/cnn/convolution.gif" alt="Convolution Operation">
	<figcaption>Convolution Operation</figcaption>
</figure>

Sometimes the you may need to pad the input image with $0$'s to facilitate the element-wise multiplication.

# Pooling

Pooling is used to reduce the size of a feature map in order to decrease compute.

A limitation of feature maps is that they record the precise position of features in the input. This means that small movements in the position of the feature in the input image will result in a different feature map.

The size of the pooling filter is almost always 2×2 pixels applied with a stride of 2 pixels.

<figure style="width: 450px">
	<img src="/media/vision/cnn/max pooling.png" alt="Max Pooling with stride 2">
	<figcaption>Max Pooling with stride 2</figcaption>
</figure>

Two common functions used in the pooling operation are:

- Average Pooling: Calculate the average value for each patch on the feature map
- Max Pooling: Calculate the maximum value for each patch of the feature map

Pooling layers follow a sequence of one or more convolutional layers and are intended to consolidate the features learned and expressed in the previous layers feature map. As such, pooling may be consider a technique to compress or generalize feature representations and generally reduce the overfitting of the training data by the model.

They too have a receptive field, often much smaller than the convolutional layer. Their stride is often equal to the size of the receptive field to avoid any overlap.

The function of pooling is to continuously reduce the dimensionality to reduce the number of parameters and computation in the network. This shortens the training time and controls overfitting.

Pooling is a generalization process to reduce overfitting.

# References

- [Brandon Rohrer: How Convolutional Neural Networks work](https://youtu.be/FmpDIaiMIeA?list=LLm-oVeNttHguGRcnMcWtZRg)
- [A Gentle Introduction to Pooling Layers for Convolutional Neural Networks](https://machinelearningmastery.com/pooling-layers-for-convolutional-neural-networks/)
- [Convolutional Neural Networks](https://cezannec.github.io/Convolutional_Neural_Networks/)
