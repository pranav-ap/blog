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

Convolutional architectures make the explicit assumption that the inputs are images, which allows us to encode certain properties into the architecture.

Each layer is a volume of neurons instead of a vector of neurons as in ordinary neural nets. We can use *parameter sharing* between some neurons within the same layer and *local connectivity* between neurons of different layers.

There are three main types of layers in a convolutional nets: *Convolutional layer*, *Pooling layer*, and *Fully-Connected layer*. They are stacked together in different number and order to form its architecture.

<figure style="width: 650px">
	<img src="/media/vision/cnn/simple-cnn.png" alt="Convolutional Neural Network">
	<figcaption>Convolutional Neural Network</figcaption>
</figure>

The layers of a ConvNet are volumes of neurons that act on an input volume of feature maps to produce an output volume of feature maps.

A volume of neurons of any ConvNet layer with dimensions $3 \times 3 \times 4$ is shown below. This layer has $3 \times 3 \times 4 = 36$ neurons. A layer of neurons within this volume at some depth is called a **depth slice**.

<figure style="width: 550px">
	<img src="/media/vision/cnn/conv-layer-as-neurons.png" alt="Volume of Neurons">
	<figcaption>Volume of Neurons</figcaption>
</figure>

A single column of neurons across all depth slices is called a **depth column**.

# Convolution

The *convolution* operation is the workhorse of convolutional nets. Convolution is used to transform an image to make it easier to identify primitive shapes within it. The primary tool for convolution is the **filter** or **kernel**. They are matrices that can detect lines, curves and edges within an image, while some can blur or sharpen the image.

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

The output matrix is called a **feature map** or an **activation map** and represents the filtered image. If an element is large, it means that the filter has found a good candidate for the feature it was looking for.

<figure style="width: 600px">
	<img src="/media/vision/cnn/conv-calc.jpg" alt="Convolution Calculation">
	<figcaption>Convolution Calculation</figcaption>
</figure>

The height and width of a filter are usually odd numbers like $3 \times 3$ or $5 \times 5$. This ensures that the filter has a proper center position, which in turn decides the location of the filtered pixel value.

The values inside a kernel are the *weight* parameters. One $3 \times 3$ filter introduces $9$ weight parameters. A kernel also has a *bias* parameter associated with it. Both weight and bias parameters are learnt via backprop. *None* of the filters are hand-engineered by the designer.

<figure style="width: 400px">
	<img src="/media/vision/cnn/convolution.gif" alt="Convolution Operation">
	<figcaption>Convolution Operation</figcaption>
</figure>

The filter acts on every depth slice of the input volume and resizes it spatially. This is called [downsampling](https://en.wikipedia.org/wiki/Downsampling_(signal_processing)). So a filter can be considered a three dimensional volume, with a depth equal to the number of feature maps in the incoming layer.

<figure style="width: 700px">
	<img src="/media/vision/cnn/k filters with depth C.png" alt="K filters with depth C">
	<figcaption>K filters with depth C</figcaption>
</figure>

# Output volume dimensions for Convolution

<figure style="width: 450px">
	<img src="/media/vision/cnn/dim-change.png" alt="Changes in Dimension">
	<figcaption>Changes in Dimension</figcaption>
</figure>

A convolution layer accepts a volume of feature maps of size $W_1 \times H_1 \times D_1$. It transforms this into an output volume of size $W_2 \times H_2 \times D_2$. The dimensions of the output volume changes depending on four hyperparameters:

- Number of filters **K**
- Spatial extent **F**
- Stride **S**
- Amount of padding **P**

**Number of filters** Typically, a convolution layer uses multiple filters, say $32$ filters. Each of them will produce a separate $2$-dimensional feature map. We will stack them to produce an *volume of feature maps* of depth $32$.

**Spatial extent** It refers to the height or width of a filter. Filters are square matrices, so they are both the same.

**Stride** The number of pixels a filter moves across in a single step is called the **stride**. When the stride is $1$ then we move the filters one pixel at a time. When the stride is $2$ then the filters jump $2$ pixels at a time as we slide them around. This will produce smaller output volumes spatially.

**Padding** Convolution reduces the height and width of the input matrix washing away the information from pixels at the image border. If we want to use a very deep ConvNet we will need to retain the original height and width.

The most common way to deal with this is to border the image or input feature map with one or more layers of $0$’s so that we can perfectly overlay a kernel on all the pixel values in the original image. It provides a way for us to control the spatial size of the output volumes. This is called **padding**.

<figure style="width: 1000px">
	<img src="/media/vision/cnn/padding.png" alt="Padding">
	<figcaption>Padding</figcaption>
</figure>

The dimensions of the output volume is given by,

$$
\begin{aligned}
W_2 &= \frac {W_1 - F + 2P} {S} + 1
\\
H_2 &= \frac {H_1 - F + 2P} {S} + 1
\\
D_2 &= K
\end{aligned}
$$

## Example

Consider a CONV layer that accepts an input volume of size $W_1 = 5$, $H_1 = 5$, $D_1 = 3$ and let its parameters be as follows: number of filters $K = 2$, spatial extent $F = 3$, stride $S = 2$ and zero padding $P = 1$.

<figure style="width: 1100px">
	<img src="/media/vision/cnn/conv-dim-calc.gif" alt="Calculating Output Volume Dimensions">
	<figcaption>Calculating Output Volume Dimensions</figcaption>
</figure>

Using the above formulas, we find the output volume size to be,

$$
\begin{aligned}
W_2 &= \frac {W_1 - F + 2P} {S} + 1
\\
&= \frac {5 - 3 + 2 \times 1} {2} + 1
\\
&= \frac {4} {2} + 1 = 3
\\
H_2 &= \frac {H_1 - F + 2P} {S} + 1
\\
&= \frac {5 - 3 + 2 \times 1} {2} + 1
\\
&= \frac {4} {2} + 1 = 3
\\
D_2 &= K = 3
\end{aligned}
$$

# Pooling

A limitation of feature maps is that they record the precise position of features in the input image. This means small movements in the position of the feature in the input image will result in a different feature map. Pooling makes a network resistant to small pixel value changes in the input image.

Another purpose of pooling is to reduce the dimensionality of feature maps.

<figure style="width: 450px">
	<img src="/media/vision/cnn/max pooling.png" alt="Max Pooling with stride 2">
	<figcaption>Max Pooling with stride 2</figcaption>
</figure>

All pooling operations first break an image into smaller patches, often $2 \times 2$ pixel areas. The actual operation happens within the patches. Two common types of pooling operations are:

- Max Pooling
- Average Pooling

For each $2 \times 2$ patch, a **max pooling** layer looks at each value and selects only the maximum value. In the pink patch, it selects $20$ and so on until we are left with four values from the four patches. For similar images, even if a patch has some slightly different pixel values, the maximum values extracted in successive pooling layers, should be similar.

On the other hand, an **average pooling** layer takes the average of the values in a patch. Empirically, averaging is not as effective as max pooling.

Pooling changes the height and width depending on the stride and window size. It does not change the depth because it does not create or remove feature maps.

<figure style="width: 400px">
	<img src="/media/vision/cnn/downsampling.jpeg" alt="Downsampling">
	<figcaption>Downsampling</figcaption>
</figure>

**Zooming effect of Pooling** The pooling layer mimics an increase in the *field of view* for later layers. For example, a $3 \times 3$ kernel placed over an original input image will see a $3 \times 3$ pixel area at a time.

When you apply a kernel of the same size to a pooled version of the original input image, it will see the same number of pixels, but the $3 \times 3$ area corresponds to a larger area in the original input image. This allows later convolutional layers to detect features in a larger region of the input image.

<figure style="width: 570px">
	<img src="/media/vision/cnn/pooling-zoom-effect.png" alt="Increase in Field of View">
	<figcaption>Increase in Field of View</figcaption>
</figure>

# Output volume dimensions for Pooling

<figure style="width: 450px">
	<img src="/media/vision/cnn/dim-change.png" alt="Changes in Dimension">
	<figcaption>Changes in Dimension</figcaption>
</figure>

A pooling layer accepts a volume of feature maps of size $W_1 \times H_1 \times D_1$. It transforms this into an output volume of size $W_2 \times H_2 \times D_2$. The dimensions of the output volume changes depending on four hyperparameters:

- Spatial extent **F**
- Stride **S**

The dimensions of the output volume is given by,

$$
\begin{aligned}
W_2 &= \frac {W_1 - F} {S} + 1
\\
H_2 &= \frac {H_1 - F} {S} + 1
\\
D_2 &= K
\end{aligned}
$$

In practice, we only use two variations of the max pooling layer: A pooling layer with $F = 3$, $S = 2$, also called *overlapping pooling*, and more commonly $F = 2$, $S = 2$, which is non-overlapping. Pooling sizes with larger receptive fields $F$ are too destructive.

# Local Connectivity and Parameter Sharing

When dealing with high-dimensional inputs such as images, it is impractical to use fully connected layers, since it introduces a large number of weights.

Instead, we will connect each neuron to only a local region of the input volume. The spatial extent (height and width) of this connectivity is a hyperparameter called the **receptive field** of the neuron. The connections are local in along width and height, but extends along the entire depth of the input volume. This is called **local connectivity**.

<figure style="width: 600px">
	<img src="/media/vision/cnn/conv-layer-as-neurons-2.png" alt="Convolutional layer as Neurons">
	<figcaption>Convolutional layer as Neurons</figcaption>
</figure>

Consider the neuron $n_1$ from the first layer of the depth column. It is connected to a local region in the input volume as defined by its receptive field.

For example, for an input image of dimensions $28 \times 28 \times 3$, if the receptive field is $5 \times 5$, then each neuron is connected to a region of $5 \times 5 \times 3$ in the input volume. Hence, the neuron $n_1$ will have $75$ weights.

Other neurons in the same depth slice as $n_1$ looks at different local regions in the input volume, and they too will introduce $75$ weights *each*. This gives us another opportunity to optimize.

Instead of every neuron using a different set of weights, they could use the same set of weights by sharing the same set of weights. These weights $\bold{w}$ are stored as values in the three-dimensional filter matrix. This is called **parameter sharing** and this allows us to use a convolution.

Sharing parameters gives the network the ability to look for a given feature everywhere in the image, rather than in just a certain area.
<!--
Now let’s say you have some prior knowledge about the structure of your images—for instance, your task is to classify images of four-legged animals, where the animals will always be scaled to the same size, will always be centered and will always face directly right. In such a scenario, the neurons assigned to the left of the image will always be looking at the butt of the animals and the neurons assigned to the top-right corner will always be looking at the head of the animals. It no longer makes sense to share parameters since forcing these neurons to look for the same thing is now inefficient. -->

# Introducing Non-linearity with ReLU

ReLU is typically applied immediately after every convolution layer. It aims at introducing non-linearity into the network by removing all the negative elements from the input volume.

It is done to offset the linear operations, element-wise multiplications and summations, executed in the convolution layers

<figure style="width: 1000px">
	<img src="/media/vision/cnn/relu.png" alt="ReLU">
	<figcaption>ReLU</figcaption>
</figure>

In the past, activation functions like tanh and sigmoid were used, but ReLU layers are more computationally efficient since it is just a thresholding function.

# Classification using Fully-Connected Layers

Once the previous layers have learned a meaningful, low-dimensional set of features from the image dataset, we can use them for classification. To do this we first flatten the last volume into a vector.

For example, for a final convolution or pooling layer that produces a volume $5 \times 5 \times 10$, the fully-connected layer has to accept a vector of length $5 \times 5 \times 10 = 250$.

This vector is treated as an input to a standard neural net. It responsible for learning a function $f$ and produce a list of class scores based on image features that have been extracted by the earlier convolutional and pooling layers. So, the last fully-connected layer will have as many nodes as there are classes.

# References

- [CS231n Convolutional Neural Networks for Visual Recognition](http://cs231n.github.io/convolutional-networks/)
- [Conv Nets: A Modular Perspective](https://colah.github.io/posts/2014-07-Conv-Nets-Modular/)
- [Brandon Rohrer: How Convolutional Neural Networks work](https://youtu.be/FmpDIaiMIeA?list=LLm-oVeNttHguGRcnMcWtZRg)
- [A Gentle Introduction to Pooling Layers for Convolutional Neural Networks](https://machinelearningmastery.com/pooling-layers-for-convolutional-neural-networks/)
- [Convolutional Neural Networks](https://cezannec.github.io/Convolutional_Neural_Networks/)
- [CNNs, Part 1: An Introduction to Convolutional Neural Networks](https://victorzhou.com/blog/intro-to-cnns-part-1/)
- [CNNs, Part 2: Training a Convolutional Neural Network](https://victorzhou.com/blog/intro-to-cnns-part-2/)
- [Wikipedia: Kernel (image processing)](https://en.wikipedia.org/wiki/Kernel_(image_processing))
- [Basics of convolutions](https://aishack.in/tutorials/convolutions/)
- [Image convolution examples](https://aishack.in/tutorials/image-convolution-examples/)
- [Convolutional Neural Networks cheatsheet](https://stanford.edu/~shervine/teaching/cs-230/cheatsheet-convolutional-neural-networks#)
- [Convolutional Neural Networks (CNNs): An Illustrated Explanation](https://blog.xrds.acm.org/2016/06/convolutional-neural-networks-cnns-illustrated-explanation/)
