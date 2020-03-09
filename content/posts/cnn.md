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

Computers see an image as a matrix of numbers, where each element is called a **pixel**. For grayscale images, each pixel has a value between $0$ and $255$, where $0$ is black and $255$ is white; shades of gray fall in between.

<figure style="width: 650px">
	<img src="/media/vision/grayscale-image.png" alt="Grayscale Image">
	<figcaption>Grayscale Image</figcaption>
</figure>

Standard color images are represented using the **RGB** color model. It uses the summation of red, green, and blue light components in various ways to produce a broad array of colors.

Color images are seen as a stack of three images, one for each color component. A pixel in a color image is written as a list of three numerical values, one for each color component. For example, the RGB pixel value $[200, 0, 200]$ represents purple.

In this way, we can think of any image as a 3D matrix or volume with some width, height, and color depth. Grayscale images have a color depth of $1$.

<figure style="width: 650px">
	<img src="/media/vision/color-image.png" alt="Color Image">
	<figcaption>Color Image</figcaption>
</figure>

The challenge is to create an image classifier that looks at these pixel values and can classify this image as a car under *varying* light conditions, angles and positions.

# Convolutional Neural Networks

Convolutional neural networks represent a data-driven approach to image classification. Every CNN is made up of multiple layers, the three main types of layers are convolutional, pooling, and fully-connected, as pictured below.

<figure style="width: 650px">
	<img src="/media/vision/cnn/simple-cnn.png" alt="CNN">
	<figcaption>CNN</figcaption>
</figure>

# Convolution

In image processing, a kernel, convolution matrix, or mask is a small matrix. It is used for blurring, sharpening, embossing, edge detection, and more. This is accomplished by doing a convolution between a kernel and an image.

Depending on the element values, a kernel can cause a wide range of effects.

The convolution operation is used to transform an image to make it easier to identify primitive shapes within the original image.

The general idea is that we use multiple filters to extract a different features from an input image and these features will be useful for classifying it.

<figure style="width: 600px">
	<img src="/media/vision/cnn/conv-calc.jpg" alt="Convolution Operation">
	<figcaption>Convolution Operation</figcaption>
</figure>

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

A limitation of feature maps is that they record the precise position of features in the input. This means that small movements in the position of the feature in the input image will result in a different feature map. Pooling helps to retain features that do not change depe

Another purpose of pooling is to reduce the dimensionality of feature maps, which in turn, reduces the number of parameters. This shortens the training time and controls overfitting.

<figure style="width: 450px">
	<img src="/media/vision/cnn/max pooling.png" alt="Max Pooling with stride 2">
	<figcaption>Max Pooling with stride 2</figcaption>
</figure>

Two common types of pooling operations are:

- **Max Pooling** - Calculate the maximum value for each patch of the feature map
- **Average Pooling** - Calculate the average value for each patch on the feature map

# Changes in dimensions

Say you have an image with dimensions $28 \times 28$.

If you perform convolution on it using $8$ different filters, you will get $8$ feature maps. We stack them together and consider it a volume with depth $8$. The change in height and width depend on the stride and padding.

<figure style="width: 450px">
	<img src="/media/vision/cnn/dim-change.png" alt="Changes in Dimension">
	<figcaption>Changes in Dimension</figcaption>
</figure>

Next, we apply pooling. Pooling changes the height and width depending on the stride and window size. It does not change the depth, ie. it does not create or remove feature maps.

# References

- [Brandon Rohrer: How Convolutional Neural Networks work](https://youtu.be/FmpDIaiMIeA?list=LLm-oVeNttHguGRcnMcWtZRg)
- [A Gentle Introduction to Pooling Layers for Convolutional Neural Networks](https://machinelearningmastery.com/pooling-layers-for-convolutional-neural-networks/)
- [Convolutional Neural Networks](https://cezannec.github.io/Convolutional_Neural_Networks/)
- [CNNs, Part 1: An Introduction to Convolutional Neural Networks](https://victorzhou.com/blog/intro-to-cnns-part-1/)
- [CNNs, Part 2: Training a Convolutional Neural Network](https://victorzhou.com/blog/intro-to-cnns-part-2/)
- [Basics of convolutions](https://aishack.in/tutorials/convolutions/)
- [Image convolution examples](https://aishack.in/tutorials/image-convolution-examples/)
- [Wikipedia: Kernel (image processing)](https://en.wikipedia.org/wiki/Kernel_(image_processing))