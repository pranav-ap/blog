---
title: "Classic CNN Architectures"
date: "2020-3-19"
template: "post"
draft: false
slug: "/posts/classic-cnn-architectures/"
category: "Deep Learning"
tags:
   - ""
description: ""
---

# LeNet

**LeNet** is a ConvNet architecture proposed by Yann LeCun et al. in 1998. It was successfully used for recognizing handwritten zip code digits provided by the U.S. Postal Service.

<figure style="width: 750px">
	<img src="/media/vision/cnn/le-net.png" alt="LeNet">
	<figcaption>LeNet</figcaption>
</figure>

The LeNet architecture is simple. It has $2$ convolutional layers, each followed by an average-pooling layer.

The convolution layers use the *tanh* activation function on the filter weights to introduce non-linearity after every convolution operation. Current implementations might replace it with the more effective *ReLU*.

<figure class="float-right">
	<img src="/media/vision/cnn/lenet-vert.png" alt="LeNet">
	<figcaption>LeNet</figcaption>
</figure>

The first convolution layer uses $6$ filters with dimensions $5 \times 5$ with $2$ pixels of padding to compensate for the reduction to its original dimensions.

The second convolution layer uses $16$ filters with dimensions $5 \times 5$ without padding, resulting in a $4$ pixel reduction of both height and width.

Both pooling layers have a window size $2 \times 2$ and use a stride of $2$. So, they are non-overlapping and halves the height and width of the volume.

After the last pooling layer, we flatten the volume into a vector and pass it to the fully connected layers.

The network has $3$ fully-connected layers at the end; two hidden layers and one outer layer. The hidden layers use the *tanh* layers, while the outer layer uses *softmax* for classification. It uses L2-regularization in the fully-connected layers to prevent overfitting.

For training the LeNet to recognize handwritten digits, we can use the MNIST database. The input is gray scale images with dimensions $32 \times 32 \times 1$. Here, the softmax outer layer will contain $10$ neurons, each corresponding to the probability of the input image being the digits $0$ to $9$.

# AlexNet

<figure style="width: 850px">
	<img src="/media/vision/cnn/alex-net.png" alt="AlexNet">
	<figcaption>AlexNet</figcaption>
</figure>

LeNet achieved good results on small datasets. The success of this model convinced the computer vision community to take deep learning seriously.

The **AlexNet** paper's primary conclusion was that the depth of the model was essential for high performance. This is computationally expensive, but is made feasible due GPUs.

<figure class="float-right">
	<img src="/media/vision/cnn/alex-net-vert.png" alt="AlexNet">
	<figcaption>AlexNet</figcaption>
</figure>

The architectures of AlexNet and LeNet are very similar. AlexNet consists of five convolutional layers, some of them followed by max-pooling layers. The increase in depth increased the network's capacity to learn from the larger ImageNet.

The filters in the first layer have dimensions $11 \times 11$, while the filters in the second layer have dimensions $5 \times 5$. The filters in the deeper layers have dimensions $3 \times 3$. All the convolution layers use *ReLU* instead of *tanh*.

Maximum pooling with window size $3 \times 3$ is done after the first, second and fifth convolutional layers with a stride of $2$. So, it is overlapping.

Due to the limited memory in early GPUs, the original AlexNet was split between two separate GPUs. That is not required today.

Then we flatten the volume and pass it through three fully-connected layers. The output layer uses *softmax* to provide probabilities.

Its performance and feasibility of training on larger datasets was low.

# VGG

<figure style="width: 850px">
	<img src="/media/vision/cnn/vgg.png" alt="VGG">
	<figcaption>VGG</figcaption>
</figure>

**VGG** was developed by and named after the Visual Geometry Group. With the introduction of VGG-16, researchers moved from thinking in terms of layers to *blocks* of repeated layers.

One *VGG block* consists of a sequence of convolutional layers, followed by a max pooling layer for spatial reduction.

<figure style="width: 450px">
	<img src="/media/vision/cnn/vgg-vert.png" alt="VGG">
	<figcaption>VGG</figcaption>
</figure>

The original VGG network has $5$ blocks followed by $3$ fully-connected layers.

The first two blocks have *one* convolutional layer each. The other three blocks contain *two* convolutional layers each. All blocks end with *one* max pooling layer.

Convolution in all layers uses $3 \times 3$ filters with stride $1$ and same padding. Max pooling is done using $2 \times 2$ windows with stride $2$. This simplified the network architecture and reduced the number of hyperparameters.

The convolution layers in the first block uses $64$ filters *each*. Subsequent blocks *double* the number of filters used per convolution layer.

In this network, $11$ layers have weights; $8$ convolutional layers and $3$ fully-connected layers. So, it is often called **VGG-11**.

Empirically, VGG shows that several layers of deep networks with narrow filters are more effective than shallow networks with wider filters. The drawback of VGG is the large number of parameters. It is very slow to train.

# Network in Network

<figure style="width: 450px">
	<img src="/media/vision/cnn/network-in-network-vert.png" alt="Network in Network">
	<figcaption>Network in Network</figcaption>
</figure>

A **NiN block** consists of one convolutional layer followed by two $1 \times 1$ convolutional layers. They act as per-pixel fully-connected layers with ReLU activations. The convolution width of the first layer is typically set by the user. The subsequent widths are fixed to 1×1.

The original NiN network was proposed shortly after AlexNet and clearly draws some inspiration. NiN uses convolutional layers with window shapes of 11×11, 5×5, and 3×3, and the corresponding numbers of output channels are the same as in AlexNet. Each NiN block is followed by a maximum pooling layer with a stride of 2 and a window shape of 3×3.

<figure style="width: 200px">
	<img src="/media/vision/cnn/one by one conv.gif" alt="1 x 1 Convolution">
	<figcaption>1 x 1 Convolution</figcaption>
</figure>

Once significant difference between NiN and AlexNet is that NiN avoids dense connections altogether. Instead, NiN uses an NiN block with a number of output channels equal to the number of label classes, followed by a global average pooling layer, yielding a vector of logits. One advantage of NiN’s design is that it significantly reduces the number of required model parameters. However, in practice, this design sometimes requires increased model training time.

Removing the dense layers reduces overfitting. NiN has dramatically fewer parameters.

# References

- [Wikipedia : LeNet](https://en.wikipedia.org/wiki/LeNet)
- [Illustrated: 10 CNN Architectures](https://towardsdatascience.com/illustrated-10-cnn-architectures-95d78ace614d)
- [Convolutional Neural Networks (LeNet)](https://d2l.ai/chapter_convolutional-neural-networks/lenet.html)
- [Deep Convolutional Neural Networks (AlexNet)](https://d2l.ai/chapter_convolutional-modern/alexnet.html)
- [Networks Using Blocks (VGG)](https://d2l.ai/chapter_convolutional-modern/vgg.html)
- [Andrew Ng : Convolutional Neural Networks - Classic Networks](https://www.coursera.org/lecture/convolutional-neural-networks/classic-networks-MmYe2)
- [Common architectures in convolutional neural networks](https://www.jeremyjordan.me/convnet-architectures/)
