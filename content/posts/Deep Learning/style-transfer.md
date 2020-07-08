---
title: "Neural Style Transfer"
date: "2020-3-15"
template: "post"
draft: false
slug: "/posts/neural-style-transfer/"
category: "Deep Learning"
tags:
   - ""
description: ""
---

**Neural style transfer** is a technique used to take two images — a *content* image and a *style-reference* image — and blend them together so that the content image adopts the visual style of the style-reference image.

<figure style="width: 1000px">
	<img src="/media/vision/style transfer/style-transfer-example.png" alt="Style Transfer Example">
	<figcaption>Style Transfer Example</figcaption>
</figure>

The style of an painting includes the brush strokes, texture and the color palette. The content of the image is what objects are present in the image, including their locations.

To blend these two images together, we need to separate the style and content information from both of the images. It turns out that this information is captured by the layers of a convolutional network.

<figure style="width: 650px">
	<img src="/media/vision/cnn/simple-cnn.png" alt="Convolutional Neural Network">
	<figcaption>Convolutional Neural Network</figcaption>
</figure>

### Isolating Content

When you train a CNN for classification, the feature maps in the convolution layers *learn* increasingly more complex features the deeper we go into the network, and the max pooling layers *discard* information irrelevant to classification.

This results in the deeper layers increasingly capture the *content* of the image rather than *style*. So, these layers are also referred to as the **content representation** of the image.

### Isolating Style

Since style is stripped away in the deeper layers, we must look for it in the shallow layers.

Each feature map in, say the first convolution layer, is a different transformation to the original image but the style will remain common among them.

An example of style would be anything specific to image properties like texture, color, and so on - like a prominent use of a particular color within a drawing. Now the question is, how do you extract a style of an image? This is done by calculating correlations between the convolutional layers. Correlations give us a measure of how similar/related two or more variables are? To understand this, consider a learned convolutional layer which is composed of several feature maps. For each feature map, you can measure how strongly its detected features relate to the other feature maps in the same layer. This gives you an estimate of things like - is a certain color detected in the first feature map similar to a color in another map? Are there any shapes that are common across the feature maps? These traits/similarities define the style of an image. The process of measuring the similarity between the contents of several feature maps within a convolutional layer helps networks to learn a multi-scale representation of the given image that focuses on spatial features like texture and color.


We can directly visualise the information each layer contains about the input image by reconstructing the image only from the feature maps in that layer.

# Cost Function

$$
J (C, S) = J(C, G) + J(S, G)
$$

# References

