---
date: "2021-01-01T00:00:00Z"
url: dl1
title: DL1
---

 TOC

- [self-information](#self-information)
**nats**; **bits**; **shannons**; 
- [Shannon entropy](#shannon-entropy)

- [KL Divergence](#kl-divergence)

- [CrossEntropy](#crossentropy)

- [Factorization](#factorization)

- [Structured Probabilistic Model](#structured-probabilistic-model)

    - [Directed](#directed)

    - [Undirected](#undirected)
**The graph are just representation, any probability distribution can be described by both graphs. Graphs are not property of distributions**;



# Self-information

we rate information value much higher if information is less likely and independent.

`I(x) = -log(P(x))`

we are using natural logarithm with base `e` so I(x) is in units of **nats**. One nat is the amount fo information gained by observing an event of probability `1/e`. Other texts use base-2 logarithms and
units called **bits** or **shannons**. Information measured in bits is just a rescaling of information measured in nats.

# Shannon entropy

`H(x) = E[I(x) = E[log P(x)]]`

when x is continuous the Shannon entropy is known as the differential entropy.


# KL Divergence
we are basically measuring distance between two distributions.
`D_{KL}(P||Q) = E[log(P(x)/Q(x))]`

important is that `D(P||Q) != D(Q||P)` and `D(P||Q) >= 0`.

if both distributions are same than KL divergence is 0.

let's say we have distribution representing true labels and models predictions. We can rate model with KL divergence. 

`D(P||Q) = CrossEntropy(P, Q) - Entropy(P)`


# CrossEntropy

Similar to KL Divergence

`H(P, Q) = H(P) + D_{KL}(P||Q)`


# Factorization

Factoring consists of writing a number or another mathematical object as a product of several factors, usually smaller or simpler objects of the same kind

# Structured Probabilistic Model

In ML we are working with a large number of random variables. Often these distributions are involved in direct interactions between relatively few variables. And instead difficulty crafting single
function we can split distribution into many factors that we multiply together. These factorization can greatly reduce the number of parameters needed to describe the distribution.

We can describe these kinds of factorizations using graphs that we call Structured Probabilistic Model or Graphical Model.
Could be directed or undirected. Each node represents random variable and edge represents direct interactions between two random variables.

## Directed

with directed edges; represent factorization into conditional probability distributions. A directed model contains one factor for every random variable x_i in the distribution and that factor consits of
the conditional distribution over x_i given the parents of x_i, denoted P_ag(x_i):

pi - capital Pi for multiplication

`p(x) = pi(p(x_i | P_ag(x_i)))`

{{<image src="/images/directed.png" alt="Directed" position="center" >}}

## Undirected

with undirected edges; represent factorizations into a set of functions. Unlike in directed case, these functions are usually not probability distributions.
Any set of nodes that are all connected to each other i G is called clique. Each clique c_i is associated with a factor o_i. These factors are functions and the output of each factor must be
non-negative, but there is no constint that the factor must sum or integrate to 1 like probability distribution. 

{{<image src="/images/undirected.png" alt="undirected" position="center" >}}


The probability of a configuration of random variables is proportional to the product od all these factors. Because we have no guarantee that the product will sum to 1, we divide by a normalizing
constant Z, defined to be the sum or integral over all states of the prodcut of the o fcuntions in order to obtain a normalized probability distribution:

`p(x) = 1/Z * pi(o_i * (C_i))`

**The graph are just representation, any probability distribution can be described by both graphs. Graphs are not property of distributions**

