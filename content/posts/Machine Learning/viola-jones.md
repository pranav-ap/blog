---
title: "Viola-Jones Framework : Rapid Object Detection using a Boosted Cascade of Simple Features"
date: "2019-12-1"
template: "post"
draft: false
slug: "/posts/viola-jones/"
category: "Vision"
tags:
  - ""
description: ""
---

The **Viola-Jones framework** is a machine learning approach to real-time object detection that processes images quickly and achieves high detection rates. It was primarily intended for frontal face detection, but this approach can be used for any object.

There are two stages in this framework - **training** and **detection**. I will start with detection.

# Detection

The input image is first converted to grayscale as they are easier to process. A small sliding detection window is moved across the grayscale image in small steps, top to bottom and left to right.

<figure style="width: 450px">
	<img src="/media/vision/viola jones/sliding-window.gif" alt="Sliding window">
	<figcaption>Sliding window</figcaption>
</figure>

All the computation required for detection happens inside this window.

The sliding window has access to a large collection of rectangular boxes with white and gray pixel-regions called **features**.

These features are moved across the window in small steps and each feature is tasked with finding a small portion of the object we wish to detect.

<figure style="width: 650px">
	<img src="/media/vision/viola jones/rect-features.png" alt="Types of Rectangular Features">
	<figcaption>Types of Rectangular Features</figcaption>
</figure>

In the figure, $A$ and $B$ are two-rectangle features or edge features. $C$ is a three-rectangle feature or line feature; and $D$ is a four-rectangle feature or diagonal feature.

Features can be stretched, scaled and oriented as required. They try to detect portions of an object by the variance in intensities that they exhibit.

For example, an edge-feature can capitalize on the observation that the eye region is often darker than the cheeks. The eye region corresponds to the gray rectangle and the cheeks correspond to the white rectangle of the feature. It can also compare intensity between the eyebrows and the forehead.

Of course, a human face will not have an exact white or black rectangular pixel region. The framework simply looks for regions that are similar.

## Feature Calculation

<figure style="width: 650px">
	<img src="/media/vision/viola jones/frontal-features.png" alt="Frontal Features">
	<figcaption>Frontal Features</figcaption>
</figure>

If the pixels under the feature are similar enough to it, then it means we have found a _good candidate_ for this portion. Each feature has a _value_ and a _threshold_ associated with it.

The **threshold** is determined during the training stage. It tells you how similar the underlying pixels must be to the rectangular feature in order to be a good candidate, for example, a nose.

Individually, these features are terrible, but the accuracy of the detector comes from using many features together.

The value is calculated for every step the feature traverses inside the sliding window. The value tells you how similar the underlying pixel group is to the feature. If the value surpasses the threshold, then the underlying pixels represent what the feature is looking for.

The **value** is the absolute difference between the sum of all pixel values in the gray and white rectangles. This is just a way to compare intensities.

For example, the value of a two-rectangle feature is,

$$
\text{value} = \left| \sum_\text{white region} \text{pixel} - \sum_\text{gray region} \text{pixel} \right|
$$

The figure below shows a edge-feature at some position inside the window.

<figure style="width: 450px">
	<img src="/media/vision/viola jones/nose-feature.png" alt="Nose Feature">
	<figcaption>Nose Feature</figcaption>
</figure>

For simplicity, the feature has been divided into a simple $4 \times 8$ grid of pixels. A pixel value ranges from $0$ to $1$, with $1$ being pure black and $0$ being pure white. The value can be found as follows:

$$
\sum_\text{gray region} = 0.568
$$

$$
\sum_\text{white region} = 0.166
$$

$$
\text{value} = \left| 0.568 - 0.166 \right| = 0.402
$$

Let's say that during training, the threshold for finding a nose using an edge-feature was found to be $0.3$. Since the value is larger than the threshold, this feature has found a good candidate representing a nose.

## Integral image

The summation of pixel values _(feature computation)_ needs to be done often and this requires a lot of compute. In order to make the computation faster, we use an integral image.

An **integral image** at a location $(x, y)$ is an image we get by cumulative addition of pixel values found in the top-left region from $(x, y)$ of a grayscale image. The integral mage can be calculated in one pass over the grayscale.

$$
s(x, y) = s(x, y - 1) + i(x, y) \\

ii(x, y) = ii(x- 1, y) + s(x, y)
$$

Here, $x$ is the row, $y$ is the column, $s(x, y)$ is the cumulative row sum, $i(x, y)$ is the original image at $(x, y)$ and $ii(x, y)$ is the integral image at $(x, y)$.

<figure style="width: 650px">
	<img src="/media/vision/viola jones/integral-image.png" alt="Integral image">
	<figcaption>Integral image</figcaption>
</figure>

## Using Integral image to calculate feature

Calculating a rectangular sum for any feature can be done using four array references in constant time, as shown below.

We see that $235$ is the sum over the entire region. The other values chip away at this region, leaving only the necessary rectangle's sum (feature value).

<figure style="width: 650px">
	<img src="/media/vision/viola jones/integral-feature-calc.png" alt="Integral image Feature Calculation">
	<figcaption>Integral image Feature Calculation</figcaption>
</figure>

## Cascade

The detector uses a series of classifiers in cascade. Each classifier uses a small number of features.

A single classifier of the cascade can use more than one feature. A positive outcome from the first classifier triggers the evaluation of a second classifier and so on. A negative outcome leads to immediate rejection of the sub-region.

<figure style="width: 650px">
	<img src="/media/vision/viola jones/cascade.png" alt="Attentional Cascade">
	<figcaption>Attentional Cascade</figcaption>
</figure>

The classifiers are arranged such that classifiers with simple features are used in the beginning to reject a majority of the image sub-regions, before more complex ones are called upon. This is called an **attentional cascade**.

**Multiple Detections.** Multiple sub-regions around a an object will probably have a positive outcome. So we combine overlapping detections into a single detection by averaging the corners of all detections.

# Training

Features can be scaled, oriented and stretched providing us with a variety of _combinations_. During training phase, we identify the combinations which are useful for detection and provide each of them with a threshold.

For a $24 \times 24$ pixel sliding window, there are $162,336$ possible features and it would be expensive to perform feature calculation for _all_ of them during detection.

So during the training stage, the framework uses the **AdaBoost algorithm** to both select a small set of important features and to train a classifier.

**How did we get the number $162,336$?**

```python
count = 0
for each feature in (edge, line, diagonal)
  for each position inside sliding window
    for each size
      for each orientation
        count++
```

**Why do we use a $24 \times 24$ sliding window during training?** If we do not scale down the images to this size, then the features will have to be scaled incrementally upto the size of the images. So, to reduce the combinations and for computational efficiency we scale down the images.

## Adaptive Boosting

The AdaBoost algorithm constructs a strong classifier as a linear combination of weighted weak classifiers.

A **weak classifier** is one that performs only slightly better than a random classifier and so its error rate is less than $0.5$. In our case, every weak classifier tries to detect an object based on just one feature.

**Why is it called "Adaptive"?**

Initially, all images are given the same weight. We now classify the images based on a single feature. An image is given more weight if it was classified incorrectly. This continues for a number of features.

This deliberate distortion of the dataset ensures that the next weak classifier focuses more on the misclassifications of the previous classifier and corrects these mistakes.

This is how it adapts to mistakes during training and this is why it is named _adaptive_ boosting.

<!-- *Write algorithm here* -->

**Code.** You can find a face detector built using OpenCV in my Github repo [here](https://github.com/pranav-ap/face-detection).

# References

- [Viola Jones Research Paper](https://www.cs.cmu.edu/~efros/courses/LBMV07/Papers/viola-cvpr-01.pdf)
- [Detecting Faces (Viola Jones Algorithm) - Computerphile](https://www.youtube.com/watch?v=uEJ71VlUmMQ)
- [Computer vision A-Z Udemy course](https://www.udemy.com/computer-vision-a-z/)
- [Artificial Intelligence: A Modern Approach](http://aima.cs.berkeley.edu/)
