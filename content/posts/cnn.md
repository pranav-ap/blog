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

<figure style="width: 680px">
	<img src="/media/vision/color-image.png" alt="Color Image">
	<figcaption>Color Image</figcaption>
</figure>

The challenge is to create an image classifier that looks at these pixel values and can classify this image as a car under *varying* light conditions, angles and positions.

# Convolutional Neural Networks

Convolutional neural networks represent a data-driven approach to image classification. It contains three main types of layers:

- Convolutional layer
- Pooling layer
- Fully-connected layer

<figure style="width: 650px">
	<img src="/media/vision/cnn/simple-cnn.png" alt="CNN">
	<figcaption>CNN</figcaption>
</figure>

# Convolution

The convolution operation is used to transform an image to make it easier to identify primitive shapes within the original image.

The general idea is that we use multiple filters to extract a different features from an input image and these features will be useful for classifying it.

<figure style="width: 600px">
	<img src="/media/vision/cnn/filter_in_action.gif" alt="Convolution Operation">
	<figcaption>Convolution Operation</figcaption>
</figure>

The primary tool for convolution is the **filter** or **kernel**. They are three-dimensional matrices that can detect lines, curves and edges within an image, while some can blur or sharpen images.

Different kernel matrices have different effects on an image. An example of matrix for edge detection is,

$$
\begin{bmatrix}
   -1 & -1 & -1 \\
   -1 & 8 & -1 \\
   -1 & -1 & -1 \\
\end{bmatrix}
$$

The values inside a kernel are called **weights**, because they determine how important a input pixel is in forming the filtered image. A kernel also has a **bias** parameter associated with it. Both weight and bias  parameters are learnt via backprop.

We execute a convolution by sliding the filter over the input image. At every location, calculate the *dot product* between the filter matrix and the underlying values in the image and add the *bias* to get the final pixel value. Write it into the output matrix.

If the final value large, then the filter has found a good candidate for the feature it was looking for.

<figure style="width: 600px">
	<img src="/media/vision/cnn/conv-calc.jpg" alt="Convolution Operation">
	<figcaption>Convolution Operation</figcaption>
</figure>

The output matrix is called a **feature map**. The number of pixels a filter moves across in a single step is called the **stride**.

The size of the output feature map changes depending on the stride and the filter size. The higher the stride, smaller the output feature map. Larger the filter size, smaller the output feature map.

<figure style="width: 400px">
	<img src="/media/vision/cnn/convolution.gif" alt="Convolution Operation">
	<figcaption>Convolution Operation</figcaption>
</figure>

The height and width of a filter are usually odd numbers like $3 \times 3$ or $5 \times 5$. This ensures that the filter has a proper center position, which in turn decides the location of the filtered pixel value.

## Padding

Convolution reduces the height and width of the input matrix. If we want to use a very deep ConvNet we may need to retain the original height and width.

<figure style="width: 1000px">
	<img src="/media/vision/cnn/padding.png" alt="Padding">
	<figcaption>Padding</figcaption>
</figure>

The most common way to deal with this is to surround this image with a border of $0$’s so that we can perfectly overlay a kernel on all the pixel values in the original image. This is called **padding**.

# Pooling

A limitation of feature maps is that they record the precise position of features in the input image. This means that small movements in the position of the feature in the input image will result in a different feature map. Pooling makes a network resistant to small pixel value changes in the input image.

Another purpose of pooling is to reduce the dimensionality of feature maps, which in turn, reduces the number of weight parameters. This improves training time and controls overfitting.

<figure style="width: 450px">
	<img src="/media/vision/cnn/max pooling.png" alt="Max Pooling with stride 2">
	<figcaption>Max Pooling with stride 2</figcaption>
</figure>

All pooling operations first break an image into smaller patches, often $2 \times 2$ pixel areas. The actual operation happens within the patches. Two common types of pooling operations are:

- Max Pooling
- Average Pooling

For each $2 \times 2$ patch, a **max pooling** layer looks at each value and selects only the maximum value. In the pink patch, it selects $20$ and so on until we are left with four values from the four patches. For similar images, even if a patch has some slightly different pixel values, the maximum values extracted in successive pooling layers, should be similar.

On the other hand, an **average pooling** layer takes the average of the values in a patch. But empirically, averaging is not as effective as max pooling.

<figure style="width: 450px">
	<img src="/media/vision/cnn/downsampling.jpeg" alt="Downsampling">
	<figcaption>Downsampling</figcaption>
</figure>

The pooling layer operates independently on every depth slice of the input volume and resizes it spatially. By reducing the width and height of an image ([downsampling](https://en.wikipedia.org/wiki/Downsampling_(signal_processing))) as it moves forward through the CNN, the pooling layer mimics an increase in the *field of view* for later layers.

For example, a $3 \times 3$ kernel placed over an original input image will see a $3 \times 3$ pixel area at a time. But that same kernel, when applied to a pooled version of the original input image, will see the same number of pixels, but the $3 \times 3$ area corresponds to a larger area in the original input image. This allows later convolutional layers to detect features in a larger region of the input image.

Many people dislike the pooling operation and think that we can get away without it. Some propose discarding pooling layer in favor of architecture that only consists of repeated convolution layers. To reduce the size of the representation they suggest using larger stride in the convolution layers once in a while.

Discarding pooling layers has also been found to be important in training models such as generative adversarial networks. It seems likely that future architectures will feature very few to no pooling layers.

# Changes in volume dimensions

Say you have an image with dimensions $28 \times 28$. As it passes through the network, it undergoes a lot of changes in its dimensions.

If you perform convolution on it using $8$ different filters, you will get $8$ feature maps. We stack them together and consider it a *volume* with depth $8$. The change in height and width depend on the stride and padding.

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