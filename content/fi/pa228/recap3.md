---
title: recap 3
url: /pa228/3
---

# Error function

regularization function: technique used for tuning the function by adding an additional penalty term in the error function.

Loss function L – penalization of dissimilar results



# Categorical Loss Functions

Typical for classification problems

Cross entropy applied to Softmax is often called Softmax Loss


# Focal Loss

softmax for one object or sigmoid for multiple objects

Generalization of cross entropy: Designed for Retina-Net to alleviate class imbalance problem.

Focal loss (FL) adopts another approach to reduce loss for well-trained class. So whenever the model is good at detecting background, it will reduce its loss and reemphasize the training on the object


# Segmentation Losses

Distribution-based: CE, TopK loss, Focal Loss
Compounded: ELL, Combo
Region-based: IoU, SS, Dice, Tversky
Boundary-based: Boundary Loss


# Region-based Loses

Precision = TP / (TP + FP)
Recall = TP / (TP + FN)
IoU = TP / (TP + FN + FP)
F1 = Dice

Tversky(0,1) = Precision
Tversky(1,0) = Recall
Tversky(1,1) = IoU
Tversky(0.5,0.5) = IoU

# Regression Loss Functions

MAE, MSE, MSLE

# Object detection

Object detection is treated like Classification + Localization. Use multitask loss (softmax for class + l2 for bounding box)


# Multiple Objects Detection: Idea

take every possible window and slide over image. 

# Viola & Jones Face Detection

First real-time object detector: Developed for faces and often still in use

Three key improvements:
 - Integral image for fast calculation of Haar-like features (Just three arithmetic operations regardless of window size!)
 - Selection of important visual features using AdaBoost 
 - Focus-of-attention mechanism: Combination of classifiers in cascades

# HOG for Human Detection

Dense grids of histograms of oriented gradients

Counts occurrences of gradient orientations in localized image portions

The essential thought behind the histogram of oriented gradients descriptor is that local object appearance and shape within an image can be described by the distribution of intensity gradients or edge directions. The image is divided into small connected regions called cells, and for the pixels within each cell, a histogram of gradient directions is compiled.


# Deformable Part Models

Objects represented by a collection of parts arranged in a deformable configuration
Spring-like connections between some pairs of parts
Models are defined by subwindows of a feature pyramids


# Modern Object Detectors

One-stage detector:
 - Input (Image, Patch, Pyramid)
 - Backbone (VGG16, ResNets, ...)
 - Neck (SPP, FPN, ...)
 - Dense Prediction (YOLO, RetinaNet)
Two-stage detector:
 - One-stage detector
 - Sparse Prediction (R-CNN family, ...)


# Multi-scale processing

ImagePyramid can create a multi-resolution representation of an image to facilitate efficient multiscale processing. Typical image pyramids are Gaussian and Laplacian pyramids.

# Spatial Pyramid Pooling (SPP)

Spatial Pyramid Pooling (SPP) is a pooling layer that removes the fixed-size constraint of the network, i.e. a CNN does not require a fixed-size input image. Specifically, we add an SPP layer on top of
the last convolutional layer. The SPP layer pools the features and generates fixed-length outputs, which are then fed into the fully-connected layers (or other classifiers). In other words, we perform
some information aggregation at a deeper stage of the network hierarchy (between convolutional layers and fully-connected layers) to avoid the need for cropping or warping at the beginning.

Basically: we can have arbitrary image -> cnn -> and we have output wxhx256 -> we make e.g. 3 pyramids: one for max-global pooling 1x1x256, one with 2x2x256 and one with output 4x4x256 -> this vectors we
concatanate and pass to fully-connected layer.


# Feature Pyramid Networks (FPN)

Feature Pyramid Network (FPN) is a feature extractor designed for such pyramid concept with accuracy and speed in mind. It replaces the feature extractor of detectors like Faster R-CNN and generates
multiple feature map layers (multi-scale feature maps) with better quality information than the regular feature pyramid for object detection.

FPN composes of a bottom-up and a top-down pathway. The bottom-up pathway is the usual convolutional network for feature extraction. As we go up, the spatial resolution decreases. With more high-level
structures detected, the semantic value for each layer increases.

SSD makes detection from multiple feature maps. However, the bottom layers are not selected for object detection. They are in high resolution but the semantic value is not high enough to justify its use
as the speed slow-down is significant. So SSD only uses upper layers for detection and therefore performs much worse for small objects.


overview:
- Down-sampling path
- Up-sampling path
- Corresponding levels connected by 1×1 bottlenecks
- Leads to better detection of small objects
- Similar to U-Net (feature maps cropped and copied)


# R-CNN

R-CNN uses selective search (SS) and on each region it applies big CNN (e.g. VGG)

# Fast R-CNN

First run whole image on VGG, then run SS on image features, on each region then run lightweight CNN.

# Faster R-CNN

Instead of SS uses Region Proposal Network.

# Region Proposal Network

takes feature maps as input and pass them to some CNN (ZF or VGG), which results in e.g. 1x256 vector. We then use two FC layers to predict coordinates and objectness.

The objectness measures whether the box contains an object (2 classes, background and object)
For each location in the feature maps, RPN makes k guesses. Therefore RPN outputs 4×k coordinates and 2×k scores per location
RPN only guess offsets for anchors for given point.

Faster R-CNN deploys 9 anchor boxes: 3 different scales (size of anchors) at 3 different aspect ratio (width:height of anchor). Using 9 anchors per location, it generates 2 × 9 objectness scores and 4 × 9 coordinates per location.

# ROI Pooling

we often use CNN that needs fixed size input. ROI pooling allows us to warp(resize) ROIs to predefined shape.

Divide into a grid of roughly equal subregions (sometimes cannot be same sizes) and then practically same as normal max pooling

Region features have always the same size even if input regions have different sizes!

Problem: Slight misalignment due to snapping; different-sized subregions is weird

Let's have a region 6x6 and we need to have ROI of size 2x2. So we take region 3x3 max pool it and use for ouput.

# ROI Align

Divide into equal sized subregions (may not be aligned to grid!)

Sample features at regularly-spaced points in each subregion using bilinear interpolation

It removes the harsh quantization of RoI Pool


# Mask R-CNN

- Object Detection Without Anchors
- Faster R-CNN extended by mask network that operates on each RoI and predicts a 28x28 binary mask.
- Only small overhead over Faster R-CNN
- Conceptually very simple and general idea
- Masks predicted for each class

# Non-max suppression

- object detectors often output many overlapping detections
- solution: post-process raw detections using non-max suppression (NMS)
 -- select next highest scoring box 
 -- eliminate lower-scoring boxes with IoU threshold e.g. 0.7
 -- if any boxes remain GOTO 1
- problem: NMS may eliminate "good" boxes when objects are highly overlapping ... no good solution


# Single Shot Detectors

Predicts both classes and boundary boxes at the same time


# Evaluation

TP = True Positives (Predicted as positive as was correct)
FP = False Positives (Predicted as positive but was incorrect); if `IoU < 0.5`
FN = False Negatives (Failed to predict an object that was there)

Precision = TP / (TP + FP)
Recall = TP / (TP + FN)
IoU = Area of overlap / area of union

The mean Average Precision or mAP score is calculated by taking the mean AP over all classes and/or overall IoU
thresholds, depending on different detection challenges that exist.

recall - there are 10 persons in image, but net found only 7, then recall is 0.7

AP - area under precision-recall curve - to plot we are lowering the threshold for object to be classified (at the end of
net)

Mean average precision (mAP) = Mean over all classes








