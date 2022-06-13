---
title: recap 2
url: /pa228/2
---

# LeNet-5

used for MNIST in 98. Conv and subsampling


# Bag Of Visual Words

Extract a set of local descriptors and assign each descriptor the closest entry in a visual vocabulary

The general idea of bag of visual words (BOVW) is to represent an image as a set of features. Features consists of
keypoints and descriptors. Keypoints are the “stand out” points in an image, so no matter the image is rotated, shrink, or
expand, its keypoints will always be the same. And descriptor is the description of the keypoint. We use the keypoints and
descriptors to construct vocabularies and represent each image as a frequency histogram of features that are in the image.
From the frequency histogram, later, we can find another similar images or predict the category of the image.

We detect features, extract descriptors from each image in the dataset, and build a visual dictionary. Detecting features
and extracting descriptors in an image can be done by using feature extractor algorithms (for example, SIFT, KAZE, etc).

# 2011 ILSVRC

Fisher Vectors + SIFT

- Generalization of BOVW
- Describe image by what makes it different from other images
- Probabilistic visual dictionary modeled by a Gaussian mixture model (GMM)

## Filter kernel/vector

The Fisher kernel can also be applied to image representation for classification or retrieval problems.
The Fisher kernel can result in a compact and dense representation, which is more desirable for image classification

The Fisher Vector (FV), a special, approximate, and improved case of the general Fisher kernel, is an image
representation obtained by pooling local image features. The FV encoding stores the mean and the covariance deviation
vectors per component k of the Gaussian-Mixture-Model (GMM).


# AlexNet

worked because ImageNet was introduced, optimized convolutions on GPU, ReLU, Batch Normalization, Pooling, data
augmentation, dropout, softmax at the end.

Batch Normalization (BN) within CNNs is a technique that standardizes and normalizes inputs by transforming a batch of
input data to have a mean of zero and a standard deviation of one. AlexNet architecture used a different method of
normalization within the network: Local Response Normalization (LRN).

LRN is a technique that maximizes the activation of neighbouring neurons. Neighbouring neurons describe neurons across several feature maps that share the same spatial position. By normalizing the activations of the neurons, neurons with high activations are highlighted; this essentially mimics the lateral inhibition that happens within neurobiology.


# ZFNet

Visualization of Features: the visualization of features, the authors use deconvolutional networks.

standard step in DL is to have a series of Conv > Rectification (Activation Function) > Pooling.

To visualize a deep layer feature, we need a set of decovnet techniques to reverse the above actions such that we can
visualize the feature in pixel domain.

Max pooling operation is non-invertible, however we can obtain an approximate inverse by recording the locations of the
maxima within each pooling region, as in the figure above.

## Layers

The first layer takes out the most simplistic of features like lines.

The second layer is modelling the various corners and edge/colour combinations. Think of it as learning the curves in the
images. Curves are formed from little lines.

The third layer learns more complex patterns such as meshes. Think of it as learning the combination of those curves i.e.
mesh. Curves come together to create meshes (think basket).

The fourth layer learns class-specific features such as dog faces. Think of it as getting the baskets shaped and painted into different things. Meshes can be transformed to resemble faces and various complex objects.

The fifth layers learn whole objects with some pose variation (side, front and others). Think of it like arranging all
those baskets into resembling different objects. Meshes resembling smaller artefacts of bigger objects can be arranged
together to make the whole shape.




# VGGNet

Smaller kernels on more layers have the same effective receptive field as a large kernel, but fewer parameters.

Vertical stacking = small kernels & more layers.


# GoogLeNet + Inception Module

Nine stacked inception modules with dimensionality reduction

Auxiliary classification outputs to inject additional gradient at lower layers -- dropedout after training

principles:
- Highly performant deep neural networks need to be large
- multi-scale convnet have the potential to learn more.
- Consideration of the Hebbian Principle — neurons that fire together, wire together.


## 1 x 1 Convolutions
purpose: Reduce the dimensions of data passing through the network, which provides the additional benefit of an increase
in the width and depth of the network.

A 1x1 convolution takes the element-wise product of all pixel values of an image.

## 3 x 3 and 5 x 5 Convolutions

purpose: Enables the network to learn various spatial patterns at different scales as a result of the varying conv filter sizes

1x1 learns patterns across the depth of the input
3x3 and 5x5 learns spatial patterns across all dimensional components (height, width and depth)of the input

Within an Inception module, we add padding(same) to the max-pooling layer to ensure it maintains the height and width as the other outputs(feature maps) of the convolutional layers within the same Inception module.

## Naive Inception

- Concatenate all filter responses channel-wise
- Apply parallel filter operations on the input from the previous layer
- Multiple receptive feature sizes
- Pooling operation

previous layer -> (1x1, 3x3, 5x5 conv, 3x3 maxpool)


## Inception module with dimensionality reduction

previous layer -> (1x1, 1x1 -> 3x3, 1x1 -> 5x5 conv, 3x3 maxpool -> 1x1)


# ResNet

Very deep network using residual connections

the problem is an optimization problem, deeper models are harder to optimize

A solution by construction is copying the learned layers from the shallower model and setting additional layers to identity mapping

Use network layers to fit a residual mapping instead of directly trying to fit a desired underlying mapping

ResConnection works because the gradient gets to every layer, with only a small number of layers in between it needs to differentiate through

It is a way to solve the vanishing gradient problem. And therefore models could be built even deeper.


# SENet

Squeeze and Excitation (SE) block

Adaptive recalibration of channel-wise feature responses

SE Block:
- The block has a convolutional block as an input.
- Each channel is "squeezed" into a single numeric value using average pooling.
- A dense layer followed by a ReLU adds non-linearity and output channel complexity is reduced by a ratio.
- Another dense layer followed by a sigmoid gives each channel a smooth gating function.
- Finally, we weight each feature map of the convolutional block based on the side network; the "excitation".


# EfficientNet

Balancing of network depth, width, and resolution lead to better performance

Compound scaling = width + depth + resolution scaling


# Object Detection

## Sliding Windows

Utilizing both a sliding window and an image pyramid we are able to detect objects in images at various scales and locations.
We take window and just slide it over image.

## Fully Convolutional Network

Direct idea: design a network with only convolutional layers without downsampling to make prediction for all pixels at once

Convolutions at the full image resolution are very expensive!

Reduce feature map sizes? But semantic segmentation requires the same output and input size => **upsampling**
Reduce the number of convolution operations? But how to keep a reasonable effective receptive field? => **atrous convolution**



# Invariance vs Equivariance

Invariance - applying transformation won't change output
Equivariance - Doesn't matter if transformation applied on input or output (of model)

Pooling layers are approximately shift invariant
Convolutional layers are (mostly) shift equivariant

Idea: design a network with downsampling and upsampling inside the network

Downsampling: Pooling or strided convolution
Upsampling: upsampling or upconvolution


# Upsampling

1. Interpolate discrete values f_k by a continuous function
2. make the geometric transformation (e.g. scaling)
3. resample the continuous function at new sample positions

## Interpolation

Continuous function f(x) can be created from discrete values f_k by convolving with a kernel o(x)

filters:
- Nearest neighbor: `_|-|_`
- linear: `_/\_`
- high orders: gaussian or whatever


## Interpolation of Scattered Data

Many different methods
- Triangulation based
- Inverse distance weighted
- Radial basis functions

## Usage In CNNs?

Direct up-sampling layers
- No learnable parameters
Learnable resampling layers
- Strided convolutions
- Transposed convolutions

## Direct up-sampling layers

- bed of nails: [1,2] => [0, 1, 0, 2]
- nearest neighbor: [1, 2] => [1, 1, 2, 2]
- Remember positions of maxima and Update activations at remembered positions

Strided Convolution -> Learnable Downsampling; Recall: strides higher than 1 lead to downsampling
Transposed Convolution -> Learnable upsampling


## Scattered data

Scattered data consists of a set of points X and corresponding values V , where the points have no structure or order
between their relative locations.

# Transposed Convolution

TODO

# U-Net

U-Net architecture is popular in biomedical imaging
V-shape architecture consisting of encoding and decoding part with skip connections between same levels.

Conv + MaxPool + Conv + MaxPool + Conv + UpConv + Conv + UpConv

# Atrous or Dilated Convolution

Dense evaluation of layers lead to shift-equivariance

The key application the dilated convolution authors have in mind is dense prediction: vision applications where the
predicted object that has similar size and structure to the input image.

In many such applications one wants to integrate information from different spatial scales and balance two properties:
- local, pixel-level accuracy, such as precise detection of edges, and
- integrating knowledge of the wider, global context

it allows for very large receptive fields while only growing the number of parameters logarithmically. 

networks using only diluted convolutions are fully equivariant under translation, which is great for dense prediction
applications.

Dense prediction = task of predicting a label for each pixel in the image


# Full DRN Architecture

Dilated Residual Networks: ResNet with dilated convolutions

Full DRN - 8 levels

The purpose of levels 7 and 8 is to reduce gridding artefacts

# Deformable Convolutional Networks

Based on deformable convolution: Generalization of the dilated convolution























