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

The style of an painting includes the brush strokes, texture and the color palette. The content of the image is what objects are present in the image and their locations.

To blend these two images together, we need to separate the style and content information from both of the images. It turns out that this information is captured by the layers of a convolutional network.

### Isolating Content

When you train a CNN for classification, the feature maps in the convolution layers *learn* increasingly more complex features the deeper we go into the network, and the max pooling layers *discard* information irrelevant to classification.

This results in the deeper layers increasingly capture the *content* of the image rather than *style*. So, these layers are also referred to as the **content representation** of the image.

### Isolating Style

Consider the first convolution layer of the CNN. It contains $35$ feature maps. One could have detected


# References

