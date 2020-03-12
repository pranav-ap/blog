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

Computers see an image as a matrix of numbers, where each element is called a **pixel**. For grayscale images, each pixel has a value between $0$ and $255$, where $0$ is black and $255$ is white; various shades of gray fall in between.

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

The challenge is to create an image classifier that looks at these pixel values and can classify the image as a car under *varying* light conditions, angles and positions.

# Challenges faced by ordinary neural networks

Ordinary feedforward neural nets receive a single input vector and transform it through a series of hidden layers. Each hidden layer is made up of a set of neurons, where each neuron is connected to *all* neurons in the previous layer. Neurons within a layer are completely independent of each other and do not share any connections.

**Scaling to large images** We could try to use a traditional feedforward net for image classification by *flattening* all the image pixels into a vector.

In CIFAR-10, images are only of size $32 \times 32 \times 3$, so a single fully-connected neuron in the first hidden layer of a regular neural net would have $32 \times 32 \times 3 = 3072$ weights. Clearly, fully connected layers cannot scale to larger images, since the number of weights would add up quickly!

<figure style="width: 650px">
	<img src="/media/vision/cnn/mlp-for-image.png" alt="Fully Connected Layer">
	<figcaption>Fully Connected Layer</figcaption>
</figure>

**Spatial information** Another important drawback is that after flattening, the spatial information within the image is now lost. So, normal neural nets are unable to perform well on complex image datasets.

# Convolutional Neural Networks

Convolutional neural networks are very similar to ordinary neural networks. They are made up of neurons that have learnable weights and biases. The whole network expresses a single function $f$ that takes raw image pixels and gives class scores. It uses backprop to learn the weights and biases based on a loss function $J(\theta)$.

ConvNet architectures make the explicit assumption that the inputs are images, which allows us to encode certain properties into the architecture. The *convolution* operation is at the heart of conv nets and gives rise to most of these properties.

<!-- gives rise to what properties ? -->

There are three main types of layers in a ConvNets: Convolutional Layer, Pooling Layer, and Fully-Connected Layer. They are stacked together to form a full ConvNet architecture.

## Convolution

Convolution is used to transform an image to make it easier to identify primitive shapes within it. The primary tool for convolution is the **filter** or **kernel**. They are matrices that can detect lines, curves and edges within an image, while some can blur or sharpen the image.

Filters are small *spatially* (along width and height), but extend through the full depth of the input image.

<figure style="width: 600px">
	<img src="/media/vision/cnn/filter_in_action.gif" alt="Convolution Operation">
	<figcaption>Convolution Operation</figcaption>
</figure>

Different kernel matrices have different effects on an image. An example of matrix for edge detection is,

$$
\begin{bmatrix}
   -1 & -1 & -1 \\
   -1 & 8 & -1 \\
   -1 & -1 & -1 \\
\end{bmatrix}
$$

We execute a convolution by sliding the filter over the input image. At every location, calculate perform *element-wise multiplication* between the filter matrix and the underlying values in the image and add the *bias* to get the final pixel value.

The output matrix is called a **feature map** and represents the filtered image. If an element is large, it means that the filter has found a good candidate for the feature it was looking for.

<figure style="width: 600px">
	<img src="/media/vision/cnn/conv-calc.jpg" alt="Convolution Operation">
	<figcaption>Convolution Operation</figcaption>
</figure>

The height and width of a filter are usually odd numbers like $3 \times 3$ or $5 \times 5$. This ensures that the filter has a proper center position, which in turn decides the location of the filtered pixel value.

The values inside a kernel are the *weight* parameters. One $3 \times 3$ filter introduces $9$ weight parameters. A kernel also has a *bias* parameter associated with it. Both weight and bias parameters are learnt via backprop. *None* of the filters are hand-engineered by the designer.

<figure style="width: 400px">
	<img src="/media/vision/cnn/convolution.gif" alt="Convolution Operation">
	<figcaption>Convolution Operation</figcaption>
</figure>

The size of the output feature map changes depending on three hyperparameters:

- Number of filters **F**
- Stride **S**
- Padding **P**

**Number of filters** Typically, a convolution layer uses multiple filters, say $32$ filters. Each of them will produce a separate $2$-dimensional feature map. We will stack them to produce an *volume of feature maps* of depth $32$.

**Stride** The number of pixels a filter moves across in a single step is called the **stride**. When the stride is $1$ then we move the filters one pixel at a time. When the stride is $2$ then the filters jump $2$ pixels at a time as we slide them around. This will produce smaller output volumes spatially.

**Padding** Convolution reduces the height and width of the input matrix. If we want to use a very deep ConvNet we will need to retain the original height and width.

The most common way to deal with this is to border the image or input feature map with $0$’s so that we can perfectly overlay a kernel on all the pixel values in the original image. It provides a way for us to control the spatial size of the output volumes. This is called **padding**.

<figure style="width: 1000px">
	<img src="/media/vision/cnn/padding.png" alt="Padding">
	<figcaption>Padding</figcaption>
</figure>

The number of elements in the output volume is given by the formula,

$$
\frac {W - F + 2P} {S + 1}
$$

where, $W$ is the number of elements in the input volume.

For example for a $7 \times 7$ input and a $3 \times 3$ filter with stride $1$ and padding $0$ we would get a $5 \times 5$ output. With stride 2 we would get a $3 \times 3$ output.

A ConvNet contains multiple convolution layers. The first convolution layer will use multiple filters to extract simple features from the original input image. Successive convolution layers will discover new features based on these simpler features. This creates an hierarchy of features that finally leads to the classes we wish to classify.

It contains three main types of layers:

- Convolutional layer
- Pooling layer
- Fully-connected layer

<figure style="width: 650px">
	<img src="/media/vision/cnn/simple-cnn.png" alt="CNN">
	<figcaption>Convolutional Neural Network</figcaption>
</figure>

The layers of a ConvNet have neurons arranged in 3 dimensions: width, height, depth. For example, the input images in CIFAR-10 are an input volume with dimensions $32 \times 32 \times 3$. The architecture will reduce this volume into a vector with dimensions $1 \times 1 \times 10$ class scores, arranged along the depth dimension.

<figure style="width: 600px">
	<img src="/media/vision/cnn/sparse-connections.png" alt="Locally connected layers">
	<figcaption>Locally connected layers</figcaption>
</figure>

The output layer can combine the findings of the each of the hidden nodes to make a prediction.

We can rearrange the input vector of pixels and the hidden layer as matrices.

<figure style="width: 600px">
	<img src="/media/vision/cnn/reorder-neurons-1.png" alt="CNN">
	<figcaption>CNN</figcaption>
</figure>

## Parameter Sharing

<figure style="width: 600px">
	<img src="/media/vision/cnn/reorder-multiple-filters.png" alt="CNN">
	<figcaption>CNN</figcaption>
</figure>

Local Connectivity. When dealing with high-dimensional inputs such as images, as we saw above it is impractical to connect neurons to all neurons in the previous volume. Instead, we will connect each neuron to only a local region of the input volume. The spatial extent of this connectivity is a hyperparameter called the receptive field of the neuron (equivalently this is the filter size). The extent of the connectivity along the depth axis is always equal to the depth of the input volume. It is important to emphasize again this asymmetry in how we treat the spatial dimensions (width and height) and the depth dimension: The connections are local in space (along width and height), but always full along the entire depth of the input volume.

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

Max-pooling layers kind of “zoom out”. They allow later convolutional layers to work on larger sections of the data, because a small patch after the pooling layer corresponds to a much larger patch before it.

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

- [CS231n Convolutional Neural Networks for Visual Recognition](http://cs231n.github.io/convolutional-networks/)
- [Conv Nets: A Modular Perspective](https://colah.github.io/posts/2014-07-Conv-Nets-Modular/)
- [Brandon Rohrer: How Convolutional Neural Networks work](https://youtu.be/FmpDIaiMIeA?list=LLm-oVeNttHguGRcnMcWtZRg)
- [A Gentle Introduction to Pooling Layers for Convolutional Neural Networks](https://machinelearningmastery.com/pooling-layers-for-convolutional-neural-networks/)
- [Convolutional Neural Networks](https://cezannec.github.io/Convolutional_Neural_Networks/)
- [CNNs, Part 1: An Introduction to Convolutional Neural Networks](https://victorzhou.com/blog/intro-to-cnns-part-1/)
- [CNNs, Part 2: Training a Convolutional Neural Network](https://victorzhou.com/blog/intro-to-cnns-part-2/)
- [Basics of convolutions](https://aishack.in/tutorials/convolutions/)
- [Image convolution examples](https://aishack.in/tutorials/image-convolution-examples/)
- [Wikipedia: Kernel (image processing)](https://en.wikipedia.org/wiki/Kernel_(image_processing))
