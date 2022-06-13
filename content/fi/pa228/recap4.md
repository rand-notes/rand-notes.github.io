---
title: recap 0
url: /pa228/4
---


Discriminative Model: p(y|x)
Generative Model: p(x)
Conditional Generative Model p(x|y)

# Generative Models

Explicit density vs Implicit Density

# Autoregressive models

Explicit and tractable(careful construction) density

with these models I cannot say what it should generate. It just generate picture
useful for e.g. inpainting - I have a picture with blank square and I want to fill it.

PixelRNN - RNN that color pixel by pixel. Every pixel is dependent only on left and top neighbor. Slow
PixelCNN - Quicker than PixelRNN but not so good. Instead of RNN, used CNN, every pixel is dependent on context region of filter.

Explicit Density: Autoregression:

p(x) = p(x_1) * p(x_2|x1) ... = \mul p(x_t | x1, ... , x_{t-1})


# Autoencoders (non-variational)

No labels needed just raw data.

Features need to be lower dimensional than the data

from input data we encode features (encoder), then using decoder we decode features into reconstructed input data. Then L2 loss over reconstructed input and input.

We are learning net to "compress" data

After training throw away decoder and use encoder for a downstream task e.g. classification

These encoders can be used to initialize a supervised model -- training on final data will be quicker and there will be no need to have many data


# Variational Encoders

The difference from non-variational is that instead of decoding directly z, we decode \u and \Sigma (parameter to gaussian distribution  from which we will drawn), this allows us to sample from latent space to obtain z (embedding), we can then use z as input to
decoder. Decoder again doesn't output exact y, but values with which we sample from y
distribution.

training process:
1. trained by maximizing the variational lower bound:
2. encoder output should mathe the prior p(z)
3. sample code z from encoder output
4. run sampled code through decoder to get a distribtion over data sample
5. original input data should be likely under the distribution from (4)
6. can sample a reconstruction from (4)

generating data process:
1. sample z from prior(z)
2. run sampled z through decoder to get distribution over data x
3. sample from distribution in (2) to generate data


edit image process:
1. run input data through encoder to get a distribution over latent codes
2. sample code z from encoder output
3. modify some dimensions of sample code 
4. run modified z through decoder to get a distribution over data samples
5. sample new data from (4)

the idea is that the z is vector where each attribute mean something. e.g. while generating face
first attribute decides size of smile, second if person has beard etc.


# Summary

Probabilistic spin to traditional autoencoders => allows generating data
defines an intractable density => derive and optimize a (variational) lower bound

Pros:
- Principled approach to generative models
- Allows inference of q(z|x) can be useful feature representation for other tasks
Cons:
- Maximizes lower bound of likelihood: okay, but not as good evaluation as PixelRNN
- Samples blurrier and lower quality compared to SOTA GANs

# Autoregressive vs. Variational

Autoregressive:
- directly maximize p(data)
- high-quzlity generated images
- slow to generate
- no explicit latent codes

Variational:
- Maximize lower-bound on p(data)
- Very dast to generate images
- Learn rich latent codes


# Vector-Quantized VAE

Combining VAE & Autoregressive


# Generative Adversarial Networks

give up on modeling p(x), but allow us to draw samples from p(x)

jointly train generator G and discriminator D with minmax game

discriminator wants D(x) = 1 for real data and D(x) = 0 for fake data
generator wants D(x) = 1 for fake data

we are not minimizing any overall loss. No training curves to look at.

at start of training, generator is very bad and discriminator easily tell apart real/fake, so the gradient is very small - vanishing.

solution: right now G is trained to minize log(1 - D(G(Z))). Instead, train G to minimize -log(D(G(z))). Then G gets strong gradients at start of training.

caveats:

- G and D are nets with fixed architecture. we dont know whether they can actually represent the optimal D and G.
- This tells us nothing about convergence to the optimal solution

DC-GAN - GAN with use of Deep nets


Conditional GAN that can generate MNIST handwritten digits conditioned on a given class. Such a model can have various useful applications:
cGANs are not strictly unsupervised learning algorithms because they require labeled data as input to the additional layer.


This is where the cGANs come in as we can add an additional input layer of one-hot-encoded image labels. This additional layer guides the generator in terms of which image to produce.

The input to the additional layer can be a feature vector derived either an image that encodes the class or a set of specific characteristics we expect from the image.


# Attention

Dynamic selection process
Assists in analyzing complex scenes

# Attention in DL

RNNs to construct attention
explicit predition of important regions
implicit attention process
self-attention


Channel Attention e.g. SENet
Channel & Spatial Attention
Spation Attention
Spation & Temporal Attention
Temporal Attention
Branch Attention e.g. SKNet


# Channel Attention SE Net

Squeeze & Excitation
Channels that often represent diifferent features are weighted
More importatnt features get higher weights
The general idea is always same: emphasize more important features

# Spatial Attention

RAM, Self-Attention

# RAM - recurrent attention model

1. glimpse sensor: extraction of retina-like representation with multiresolution patches centered at l_{t-1}
2. glimpse network: glimpse network + MLPs
3. RNN model

basically RNN model consisting of glimpse networks

idea:

The Recurrent Attention Model (RAM) is a neural network that processes inputs sequentially, attending to different locations within the image one at a time, and incrementally combining information from these fixations to build up a dynamic internal representation of the image.



# Attention Layer

Inputs:
- Query vector Q 
- Input vectors X
- Key matrix W_k
- Value matrix W_v
Computation:
- Key vectors K = X * W_k
- Value vectors V = X * W_v
- Similarities E = q_i * k_j / \sqrt(D_q)
- Attention weights A = softmax(E)
- Output vector Y = AV



# Self Attention

Inputs:
- Input vectors X
- Query matrix W_q
- Key matrix W_k
- Value matrix W_v

Computation:
- Query Vectors Q = X * W_q
- Key Vectors K = X * W_k
- Value Vectors V = X * W_v
- Similarities E = q_i * k_j / \sqrt(D_q)
- Attention Weights A = softmax(E)
- Output vector Y = A*V


Self attention is permutation equivariant
Self attention layer works on sets of vectors

Self attention knows nothing about the order of vectors that is processing!


# Masked Self-Attention Layer

Don’t let vectors to “look ahead” in the sequence.

Used for language modelling to predict next word


# The Transformer

Transformer Block:
Input: Set of vectors x
Output: Set of vectors y

Self-Attention is the only interaction between vectors

Layer norm and MLP work independently per vector

Highly scalable, highly parallelizable

Transformer Block:
X -> Self-Attention -> (skip connection) -> Layer Normalization -> multiple MLPs -> (skip) ->
Layer Normalization -> Y


# Post-Norm vs Pre-Norm Transformer

Layer normalization is after residual connections
or
Layer normalization is inside residual connections (Gives more stable training, used in practice)

A transformer is a sequence of transformer blocks

A new neural network model that only uses attention

Usage:

Add Attention to Existing CNN
Replace Convolution with “Local Attention”
 - Map center of receptive field to a query
 - Map each element in receptive field to key and value
 - Compute output by attention
Standard Transformer on Pixels
Standard Transformer on Patches


# Vision Transformer (ViT)

Vision Transformer (ViT) Computer vision model with no convolutions!

process:
- take patches
- flatten patches
- Produce lower-dimensional linear embeddings from the flattened patches
- Add positional embeddings
- pass to transformer encoder
- MLP Head

# Summary 

Attention is inspired by human/animal vision

Vision transformers have been super hot topic in 1-2 last years

Very different architecture than CNNs

Application to many tasks

Vision transformers are evolution not revolution















