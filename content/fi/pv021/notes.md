---
title: pv021
url: /pv021/exam
---

# Net separation

if output is step function (1 or 0) the neuron divide space into halves. We can then combine
these half spaces with and/or neurons etc.

# Non linear separation

- Three layer nets are capable of "approximating" any "reasonable" subset A of the input space R^k.
- Each hypercube K can be separated using a two layer network NK.
- Hypercube is equivalent to square or cube in any dimension

representing any shapes using nn:
 - we can "fill" the shape with hypercubes (and combine them with or)
 - i.e. we need 3 layers -- 2 to define square (hypercubes) and one to connect them.


## Theorem - Cybenko

> two layers for any space (returns 1 if in space else 0)

- for set A \in [0, 1]^n there is two layer network with sigmoidal activation and linear outputs such that: for most vectors v \in [0, 1]^n we have that v \in A iff the net output is `>` 0 for the input v.
 

# Function approximation

> three layer net to approximate any continuous function using summing up the sigmoidal functions 

For every continuous function f: [0,1]^n -> [0,1] and \eps > 0 there is a three layer net
computing a function F: [0, 1]^n -> [0, 1]

- neurons have the logistic sigmoid as their activation, only outputs are linear.

process:
 - two layers to construct hill from two sigmoidal functions
 - one layer to sum the hills


## Theorem - Cybenko

> two layer networks can approximate any continuous function

For every continuous function and every \eps > 0 there is a function F computed by a two layer
network where each hidden neuron sigmoidal activation function and outputs are linear that
satisfies `|f(v) - F(v)| < \eps` i.e. f and F are ~same


# Computability

we have a word w from {0, 1}+ alphabet. Encoding w into numbers as follows:
\\( \sum_i=1^|w| (w(i)/2^i) + 1/2^{|w|+1} \\)

A network recognize a language L \in {0, 1}+ if it computes a function F: A -> R (A \in R) such
that:

\\( w \in L iff δ(w) \in A and F(δ(w)) > 0 \\)

where δ(w) is the code of the word
eg. w = 11001 that gives us δ(w) = 0.110011 in binary form

- Recurrent networks with rational weights are equivalent to Turing machines
- Recurrent networks are super-Turing powerful


# Computability Overview

- All Boolean functions can be expressed using two-layer networks.
- Two-layer networks may approximate any continuous function.
- Recurrent networks are at least as strong as Turing machines


# Online algorithm (Delta-rule, Widrow-Hoff rule)
 - weights in ~w(0) initialized randomly close to 0


# Complexity of the batch algorithm

computation of E/wji stops in time linear in the size of the network + the size of the training
set

Proof sketch: The algorithm does the following p times:
 - forward pass
 - backpropagation
 - gradient descent

# Gradient Descent in Large Networks

assume:
 - activation functions: "smooth" ReLU (softplus)
 - inputs ~xk of Euclidean norm equal to 1, desired values dk satisfying |dk| ∈ O(1),
 - the number of hidden neurons per layer sufficiently large
 - the learning rate constant and sufficiently small

/TODO

The gradient descent converges (with high probability) to a global
minimum with zero error at linear rate.

# Issues in computing the gradient

inexact gradient computation:
 - Minibatch gradient is only an estimate of the true gradient
 - Note that the variance of the estimate is (roughly) σ/√m where m is the size of the minibatch and σ is the variance of the gradient estimate for a single training example.

# Minibatch size

- Larger batches provide a more accurate estimate
- Multicore architectures are usually underutilized by small batches
- It is common for power of 2 batch
- Small batches can offer a regularizing effect, perhaps due to the noise they add to the learning process


# Generalization

Generalization = ability to cope with new unseen instances

more formally:
It is typically assumed that the training set has been generated as follows:

d_kj = g_j(x_k) + \theta_kj

where gj is the "underlying" function corresponding to the output neuron j ∈ Y and theta is random noise.

> Methods improving generalization are called regularization methods.


# Regularization

## Early stopping

## Size of the network

- Too small network is not able to capture intrinsic properties of the training set.
- I Large networks overfit faster.

## Feature extraction

basically reducing dimensionality like PCA


## Ensemble methods

## Dropout

## Weight decay and L2 regularization

Generalization can be improved by removing "unimportant" weights.

Penalising large weights gives stronger indication about their importance

Intuition: Unimportant weights will be pushed to 0, important weights will survive the decay.

E′(~w) = E(~w) + ζ/(2ε) (~w · ~w)

Here ζ/(2ε) (~w · ~w) is the L2 regularization that penalizes large weights.


# Maximizing INput

A maximum image computed using gradient ascent.
We can use backprop, but instead of weights we are changing inputs.
Gives the most "representative" image of the class c.

# Image specific saliency maps

- Let us fix an output neuron i and an image I0.
- Rank pixels in I0 based on their influence on the value y_i(I_0)
- Note that we can approximate yi locally around I0 with the linear part of the Taylor series:
- for every pixel we compute how much it affects output
- Heuristics: The magnitude of the derivative indicates which pixels need to be changed the least to affect the score most
- we can also take max gradient from saliency map and overlay it with default image, so we can clearly see which pixels are important.


# SmoothGrad

- Make a several noisy copies of image and than average saliency maps of these noisy copies.

# Occlusion
- Systematically cover parts of the input image.
- Observe the effect on the output value.
- Find regions with the largest effect


# LIME

Let us fix an image I_0 to be explained.

Outline:
- Consider superpixels of I0 as interpretable components.
- Construct a linear model approximating the network aroung the image I0 with weights corresponding to the superpixels.
- Select the superpixels with weights of large magnitude as the important ones.

superpixels:
- Denote by P1,..., P_l all superpixels of I0.
- Consider binary vectors ~x = (x1, . . . , xl) ∈ {0, 1}^l.
- Each such vector x determines a "subimage" I[x] of I_0 obtained by removing all Pk with xk = 0.















