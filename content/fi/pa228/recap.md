---
title: recap 0
url: /pa228/1
---


# Recap

- Is it static or dynamic?
- What are the objects of interest?
- What is our a priori knowledge? E.g., object appearance, position, pose.
- Can we control the scene?

Scene adaptation may be significantly cheaper  than development of a general image processing method!

# Point Spread Function - PSF

In fluorescence microscopy, the acquired image is always a blurred representation of the actual object under the microscope. This blurring is described by the so-called Point Spread Function (PSF). The PSF describes what a single point in the object looks like in the image.


basically: Response of the imaging system to an infinitesimal point source

In general, it is space variant and depends on the illumination source (e.g., light wavelength)

If the PSF is known, it can be used to bring the acquired microscopy image closer to the true object through a deconvolution.

Deconvolution reverses the imaging convolution in an iterative fashion: a model of the object is made and iteratively improved upon by convolving it with the PSF and comparing the result to the actual image.

At the end of the process, the model of the object is an accurate representation of the true object, with improved resolution and signal-to-noise ratio relative to the acquired image. Notably, deconvolution can re-separate neighboring particles with overlapping PSFs, which is not possible with simple deblurring operations.


A multi-channel image requires a multi-channel PSF for deconvolution as the PSFs often differ between channels.


# Optical Transfer Function

- Characterizes spatial frequencies transmitted through the optical system
- Formally Fourier transform of the PSF (in general a complex function)
- In real systems, it is finite, i.e., band-limited
- The largest transmitted frequency is called cut-off frequency
- is a complex-valued function describing the response of an imaging system as a function of spatial frequency
- 


# Linear Shift-Invariant System

PSF ----fourier transform---> MTF = |OTF|

PSF and OTF are related – convolution theorem

LSI has two properties:
- Linearity
- invariance: this means that if we shift the input in time (or shift the entries in a vector) then the output is shifted by the same amount


LSI systems are characterized by their “impulse response”


# Quantization

Process of reducing the number of values

e.g. grayscale image -> we can have 8bit or 4 or 1bit (or whatever), these are levels -> the lower we go the less values(memory) is needed but also image is getting degrading 


# Spatial filters


we can apply gaussian or laplacian(gauss-like but sharper /\). Applying Gaussian filter will blurr image. It is a widely
used effect in graphics software, typically to reduce image noise and reduce detail. The visual effect of this blurring technique is a smooth blur resembling that of viewing the image through a translucent screen, distinctly different from the bokeh effect produced by an out-of-focus lens or the shadow of an object under usual illumination. 

Gaussian smoothing is also used as a pre-processing stage in computer vision algorithms in order to enhance image structures at different scales—see scale space representation and scale space implementation.

Gaussian blur is a low-pass filter, attenuating high frequency signals

There are also filters like LoG filtering (Laplacian of Gaussian).

Gaussian smoothing is commonly used with edge detection. Most edge-detection algorithms are sensitive to noise; the 2-D Laplacian filter, built from a discretization of the Laplace operator, is highly sensitive to noisy environments.

Using a Gaussian Blur filter before edge detection aims to reduce the level of noise in the image, which improves the result of the following edge-detection algorithm. This approach is commonly referred to as Laplacian of Gaussian, or LoG filtering


A high pass filter can be used for sharpening image.

A Band-pass filter passes only frequencies in certain range.

# Steerable filter

A steerable filter is an orientation-selective convolution kernel used for image enhancement and feature extraction that
can be expressed via a linear combination of a small set of rotated versions of itself.

Steerable filters may be designed as approximations of a given filter shape up to a desired error or computational complexity

The steerable filters refer to a class of arbitrary orientation filters that can be synthesized into a linear combination of base filters

Allow synthetization of filters of arbitrary orientation from basis oriented filters


# Filter banks

In signal processing, a filter bank (or filterbank) is an array of bandpass filters that separates the input signal into multiple components, each one carrying a single frequency sub-band of the original signal

Several filters are applied and combined
- Maximum
- Sum
- Average

# Pyramids

at the bottom highest resolution -blur and subsample -> lower resolution -> repeat

implementation of a multi-scale, multi-orientation band-pass filter bank used for applications including image
compression, texture synthesis, and object recognition. It can be thought of as an orientation selective version of a
Laplacian pyramid, in which a bank of steerable filters are used at each level of the pyramid instead of a single
Laplacian or Gaussian filter.

# Adaptive Histogram Equalization

- Histogram equalization in local windows. 
- Applied only from a certain contrast to avoid noise amplification
- Popular normalization method in deep learning


# Transformations

Geometrical Transformations: Common for augmentation of the training datasets and camera calibration

Local Transforms (or Also Filters): Pixel values are changed based on a local region around each pixel

Shift Invariant Linear Filtering by Convolution: Relation to frequency domain filtering:
 - Low-pass filters (smoothing)
 - High-pass filters (details)
 - Band-pass filters (difference filters, e.g., DoG)



# Regional Maxima

A connected set of pixels M_t is a regional maximum of function g at level t, iff all external boundary pixels have a value
strictly smaller than t nad all pixels in M_t have a value equal to t


High Regional Maxima by Thresholding: Select only the high ones


# Extrema Dynamics

Dynamic of a regional maximum is the minimum descent we have to do to reach a regional maximum at higher elevation

# H-Extrema

Extrema with height (depth) higher than or equal to h

Also called extrema with a high local contrast or dynamic

Regional maxima from which we can reach a regional maximum with a higher elevation only along paths descending more than
or equal to h.

Background Correction: Low-pass filter or white (or black) top-hat

Uneven Illumination Correction: Could be measured or estimated from images



# How images are represented in the frequency domain

similarly as 1d signal, 2d image can be represented as a sum of rotated sines and cosines.
If represented in frequency domain, convolution can be easily computed, also for image compression.

Similar to Fourrier Transform, we got Gabor Transform and Wavelets.


Time series: I know where the signal is at each time but I don't know anything about frequencies
Fourier transform: a tool for converting signals/images from time or spatial domain to the frequency domain
Gabor Transform: compute spectogram that contain info when each frequencies get turn on and off but with small resolution
Wavelets: similar to gabor transforms, but we are using knowledge that most low frequencies last longer so we create
hierchical grading of time and frequencies information.


Wavelet Transform: Calculates the approximation and detail coefficients in the wavelet series expansion

# Wavelet Scattering

Wavelet scattering is an equivalent deep convolutional network 
formed by cascade of wavelets, modulus non-linearities, and low-pass filters to enable you to derive, with minimal
configuration, low-variance features from real-valued time series and image data for use in machine learning applications

Wavelet Scattering Network: repeated wavelet blocks
wavelet block: Wavelet Convolution -> Non-linearity -> averaging

Key differences w.r.t. CNNs: 1. kernels are fixed not learned, 2. modulus and averaging instead of ReLU and pooling

why modulus?
absolute value of a complex value.
Kind of pooling – combines real and imaginary parts.
It calculates a lower frequency envelope.
Modulus is L1 norm, which is invariant to translations

## Continuous Wavelet Transform

CWT measures similarity of the signal with wavelets of varying frequency and scale
Highly redundant function of two continuous variables–translation and scale

Wavelet scattering transform (WST) has architectural similarities with deep convolutional networks


The filters in WST are pre-defined and fixed
WST can produce robust representations of data for learning
Works well also for small data sets
The scattering features are invariant to translation, rotation, scaling, and small deformations

# Mathematical Morphology

Non-linear theory for analysis of spatial structures

Many useful operators
- Dilation, erosion, hit-or-miss
- Opening, closing, granulometry
- Reconstruction, connected filtering
- Extrema extraction
- Watershed

dilatation: lines get thicker
erosion: lines get thinner
opening: first erosion then dilation
closing: first dilation then erosion


# Gabor Filter

is a linear filter used for texture analysis, which essentially means that it analyzes whether there is any specific frequency content in the image in specific directions in a localized region around the point or region of analysis

In the spatial domain, a 2-D Gabor filter is a Gaussian kernel function modulated by a sinusoidal plane wave (see Gabor transform).

Usually different scales and orientations


# Connected Component Trees

Extremely useful image representation for connected filtering (attribute filters)

father wavelets are lowpass filters
mother wavelets are highpass filters

# Discrete Wavelet Transform

Wavelet was originally meant for compression. With correct configuration we can have most of signal 0s so its easier to
compress. It could be lossless or for higher efficiency lossy.

we can decompose in multiple levels. Back we are doing reconstruction.

# Undecimated Wavelet Transform

- DWT is not translation/shift invariant
- UWT does not incorporate down sampling
- inherently redundant scheme
- useful for feature extraction


# Feature Map

A feature map, or activation map, is the output activations for a given filter

# Generalization problem

- Large memorization capacity of networks
- Prone to overfitting and overlearning


# Adversarial fragility problem

The neural networks can be tricked into producing completely different outputs after the application of imperceptible perturbations to their inputs

# Scale-Space Theory

The stack of images as a function of increasing inner scale is coined a linear ’scale-space’.

Formal theory for handling image structures at different scales

Scale-space method attempts to represent data at all scales simultaneously

Image represented as one-parameter family of smoothed images

Why Gaussian?

Comes from so-called scale-space axioms.
Non-enhancement of local extrema, linearity, shift-, rotational-, scale-invariance, semigroup structure

# Feature Extraction in Scale-Space

Set of scale-space derivatives up to order N = N-jet

Features expressed as a polynomial combinations of normalized Gaussian derivatives

# Image Pyramids

What are they good for? improve search, precomputation, image blending etc.

Conceptually simple structure for representing images at more than one resolution

Originally designed for image compression applications

Used in computer graphics as well as image analysis

In the early days of computer vision, pyramids were used as the main type of multi-scale representation for computing
multi-scale image features from real-world image data. More recent techniques include scale-space representation, which
has been popular among some researchers due to its theoretical foundation.

# Laplacian Pyramid

created from gaussian pyramid.

Take original image and substract it with gaussian image.

# Smoothing as low-pass filtering

High frequencies lead to trouble with sampling
suppress high frequencies before sampling:
solution: truncate high frequencies in FT or convolve with a low-pass filter


# Features Extraction 

Local features and their descriptors, which are a compact vector representations of a local neighborhood

The general idea is to transform image content into local feature coordinates invariant to translation, rotation, scale, and other imaging parameters

algos like: SIFT


# Scale Invariant Feature Transform (SIFT)

Scale space peak selection
- Potential locations for finding features
Key point localization
- Accurately locating the feature key points
Orientation Assignment
- Assigning orientation to the key points
Key point descriptor
- Describing the key point as a high dimensional vector

LoG acts as a blob detector which detects blobs in various sizes due to change in o, where o acts as a scaling parameter. It's often used DoG (approximation of Log) because it's quicker

key localization/scale/rotation, solution: Difference of Gaussians / scale-space pyramid / orientation assignment


## Key Point Localization

Precise peak localization by fitting a 3D quadratic function
- Location, scale, and principle curvatures

Outlier rejection in case of:
 - Small contrast
 - Large ratio or principle curvatures


## Orientation Assignment

- Local orientation is calculated for each key point based on the orientation histogram in a surrounding region from local image gradient directions
- In ambiguous cases with multiple peaks multiple key points are created
- The location, scale, and orientation define a local coordinate system for each feature

## The Local Image Descriptor

- Feature vector with 4 x 4 x 8 = 128 elements
- Gradient magnitude and orientation at each sample point
- Samples are weighted by a Gaussian window and accumulated into orientation histograms summarizing content over 4 x 4 subregions in 8 directions


# One Times One Convolutions

Used for changing depth -> “dimensionality” reduction

CWH format: 64x56x56 --1x1conv-> 32 filters (64x1x1) ---> 32x1x1

A feature map, or activation map, is the output activations for a given filter, so the feature map has no channels!


# Blur Pooling

- applying a spatial low-pass filter before pooling operations
- maxpool has heavy aliasing, by bluring before downsampling we reduce aliasing a bit.
- maxblurpool = max(dense) + anti-aliasing filter + subsampling

# SURF – Speeded Up Robust Features

Feature Detection
 - Basic Hessian matrix approximation by box filters
 - Faster calculation of the DoG(difference of gaussian) pyramid
Feature Description:
 - Identify reproducible orientation by Haar wavelet responses
 - Calculate wavelet responses dx and dy in local 4x4 subregion

# ORB – Oriented FAST and Rotated BRIEF 

- Fast and accurate orientation component to FAST
- The efficient computation of oriented BRIEF
- Analysis of variance and correlation of oriented BRIEF
- A learning method for decorrelating BRIEF features under rotational invariance, leading to better performance in nearest-neighbor applications


# Maximally Stable Extremal Regions

- MSER features
- Go through thresholds, grab regions which stay nearly the same through a wide range of thresholds





