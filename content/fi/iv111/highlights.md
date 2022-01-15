---
url: iv111/exam
title: iv111
---

Events A1, A2, . . . An are (mutually) independent iff for any set {i1, i2, . . . ik }⊆{1 . . . n} (2 ≤k ≤n) of distinct indices it holds that P (Ai1 ∩Ai2 ∩···∩Aik ) = P (Ai1 )P (Ai2 ) . . . P (Aik ).

Events A1, A2, . . . An are pairwise independent iff for all distinct indices i , j ∈{1 . . . n} it holds that P (Ai ∩Aj ) = P (Ai )P (Aj ).

# Law of Total Probability

prob of A given event space, gives prob of A

Let A be an event and {B1, . . . , Bn } be an event space. Then \\( P(A) = \sum_{i=1}^{n} P(A|B_i) P(B_i) \\)

# Random Variable

to each sample point (HEAD/TAIL) assigns a real number.

def: A (discrete) random variable X on a sample space S is a function X : S→R that assigns a real number X(s) to each sample point s∈S.

{{<image src="/images/iv111/random_variable.jpg" position="center" alt="random variable">}}

---

For a random variable X and a real number x , we define **inverse image** of x to be the event

\\( [X = x] = {s \in S | X(s) = x} \\)

i.e. the set of all sample points from S to which X assigns the value x.

# Probability Mass Function PMF

probability for discrete

def: Probability mass function (or probability distribution) of a random variable X is a function pX : R → [0,1] given by

\\( p_X(x) = P(X = x) = \sum_{s:X(s)=x} P(s) \\)


# Cumulative Distribution Function - CDF

def: The cumulative distribution function (probability distribution function or simply distribution functiona) of a random variable X is a function FX : R→[0,1] given by

\\( F_X(x) = P (X \leq x) = \sum_{t \leq x} p_X(t) \\)


# Probability Density Function

def: (or density) of a random variable X is a derivative function of the cumulative distribution function.


# Discrete Random Vectors

The joint (or compound) probability distribution of a random vector X is defined to be

\\( p_X(x) = P(X=x) = P(X_1 = x_1 \wedge X_2 = x_2 \wedge ...) \\)

The joint (or compound) distribution functionaof a random vector X is defined to be

\\( F_X(x) = P(X_1 \leq x_1 \wedge X_2 \leq x_2 \wedge ...) \\)



Let pX(x) be a joint probability distribution of a random variable X = (X1,X2). The marginal probability distribution of X1 is defined as

\\( p_{X_{1}}(x) = P(X1=x) = \sum_{x_2 \in lm(X_2)} p_X((x ,x2))  \\)

# Independent Random Variables

X and Y are independent:

\\( p_{X,Y}(x, y) = p_X(x)p_Y(y) \\) for all x and y

we can use there also F instead of p

# Expectation

Expectation of a random variable X is defined as

E(X) = \sum_{x \in lm(X)} x \cdot P(X=x)

provided the sum is absolutely convergent. In case the sum is convergent, but not absolutely convergent, we say that no finite expectation exists.
In case the sum is not convergent, the expectation has no meaning.


# Linearity of Expectation

## Expectation of sum
Let X and Y be random variables. Then \\( E(X+Y) = E(X) + E(Y) \\)

## Multiplication by a constant

Let X be random variable and c be a real number. Then \\( E(cX) = cE(X) \\)

## Expectation of Independent Random Variables

If X and Y are independent random variables, then \\( E(XY) = E(X)E(Y) \\)

## Jensons Inequality

\\( E[f(X)] \geq f(E(X)) \\)

## Observation

If Im(X) \in N then \\( E(X) = \sum_{i=1}^{\inf} P(X \geq i) \\)


# Conditional probability

\\( p_{X|Y}(x|y) = P(X=x|Y=y) = \frac{P(X=x, Y=y)}{P(Y=y)} = \frac{p_{X,Y}(x,y)}{p_Y(y)} \\)


# Markov inequality

def: Let X be a nonnegative random variable with finite mean value E(X). Then for all t > 0 it holds that:

\\( P(X \geq t) \leq \frac{E(X)}{t} \\)


# Moments

The k th moment of a random variable X is defined as E (X^k).
Note that for k = 1 we get the expectation of X

Usually we center the expected value to 0 – we use moments of X - E(X)
i.e. \\( μ_k = E([X-E(X)]^k) \\)

# Variance

The second central moment is known as the variance

\\( Var(X) = E(X^2) - [E(X)]^2 \\)

If X and Y are independent random variables, then Var (X + Y) = Var (X) + Var (Y)

If X and Y are (not independent) random variables, we obtain
\\( Var(X + Y) = Var(X) + Var(Y) + 2Cov(X,Y) \\)


# Covariance

Cov(X,Y) = E(XY) − E(X)E(Y)

Covariance measures linear dependence between two random variables

We define the correlation coefficient ρ(X ,Y ) as the normalized covariance, i.e.

\\( ρ(X,Y) = \frac{Cov(X,Y)}{\sqrt{Var(X)Var(Y)}} \\)

For independent random variables X and Y , it holds that Cov (X ,Y ) = 0.


\\( X and Y independent \Rightarrow Cov(X,Y) = 0 \\)
\\( X and Y independent \not\Leftarrow Cov(X,Y) = 0 \\)



# Chebyshev Inequality

In case we know both mean value and variance of a random variable, we can use much more accurate estimation

\\( P[(X - E(X))^2 \geq t^2] \leq \frac{E([X - E(X)]^2)}{t^2} = \frac{Var(X)}{t^2} \\)



# Overview: Moments and Bounds

- Markov inequality uses E (X).
- Chebyshev inequality uses Var (X).
- Chernoff bound uses moment generating functions.

The k th moment of a random variable X is defined as \\( E(X^k) \\)

The moment generating function of a random variable X is: \\( M_X(t) = E(e^{tX})  \\)


# Moment Generating Function and Moments

> The moment generating function captures all moments

Let \\( M_X(t) = E(e^{tX}) be a moment generating function of X. Assuming that exchanging the expectation and differentiation operands is legitimate, for all n >1 we have:

E(X^n) = M_X^{(n)} (0), 

M_X^{(n)} (0) is the n-th derivative of M_X(t) evaluated at 0


If X and Y are independent random variables, then: \\( M_{X+Y}(t) = M_X(t)M_Y(t) \\)


# Chernoff Bounds

The Chernoff bound for random variable X is obtained by applying the Markov inequality to e^{tX} for some suitably chosen t.

For any t > 0:
\\( P(X \geq a) = P(tX \geq ta) = P(e^{tX} \geq e^{ta}) \leq \frac{E(e^{tX})}{e^{ta}}


Similarly, for any `t < 0` (just first inequality will be switched):
\\( P(X \leq a) = P(tX \geq ta) = P(e^{tX} \geq e^{ta}) \leq \frac{E(e^{tX})}{e^{ta}}


# Law of Large Numbers

## Weak LoLN

> the expected value is really expected as average of the repeated experiments

If X1,X2,...is a sequence of independent identically distributed random variables with expectation μ = E (X_k), then for every ε >0

\\( lim_{n -> \inf} P(\abs{\frac{X1 + .. Xn}{n} - \u } > \epsilon) = 0 \\)


Law of Large Numbers proves formally that the mathematically defined statement of probability corresponds to our motivation based on frequencies in repeated experiments


## Strong LoLN

If X1,X2,...is a sequence of independent identically distributed random variables with expectation μ = E (X_k), then

The (weak) law of large numbers implies that large errors in “experimentally obtained expectation” occur infrequently

In many practical situations, we require the stronger statement that the error remains small for all sufficiently large n, i.e. infinite sequences with average difference from the mean have zero probability

\\( P(lim_{n -> \inf} \frac{X1 + .. Xn}{n} - n}  = \u ) = 1 \\)


# Stochastic Process

A stochastic process is a collection of random variables \\( X = {X_t |t \in T} \\). The index t often represents time; X_t is called the state of X at time t.

Classification:
 - the time domain T can be either countable, or uncountable - representing discrete-time or continuous-time process, resp.
 - the state space of Xt can be finite, countable, or uncountable - representing finite-state, discrete-state, or continuous-state process.


Markova Chain is a discrete-time stochastic process iff 
\\( P(X_t = a |X_{t−1} = b) = p_{b,a} \\)

That is, the value of Xt should depend on the value of Xt−1, but does not depend on the history of how we arrived at Xt−1. This is called Markov or memoryless property

Every (discrete-time finite-state) Markov chain can be alternatively (uniquely) defined by an initial vector ~λ(0) and a transition matrix P .


# Hiting time

The hitting time of a subset A of states of a Markov chain is a random variable H^A : S -> {0,1,2,...} \cup {\inf} given by

\\( H^A = inf{n \geq 0| X_n \in A} \\)

hitting time = hitting probability + 1

# Hitting probability


# Long-run Analysis

> A state of a Markov chain is said to be absorbing iff it cannot be left, once it is entered, i.e. pi,i = 1.

> A state i of a Markov chain is said to be recurrent iff, starting from state i, the process eventually returns to state i with probability 1.

> A state of a Markov chain is said to be transient (or non-recurrent) iff there is a positive probability that the process will not return to this state.


In a finite-state Markov chain, a state is recurrent if and only if it is in a bottom strongly connected component of the Markov chain graph representation. All other states are transient.


A Markov chain is irreducible if and only if its graph representation is a single strongly connected component

All states of a finite-state irreducible Markov chain are recurrent.


# Mean Portion of Visited States and Inter Visit Time

## Expected long-run frequency

Let us have a finite-state irreducible Markov chain and the unique stationary distribution \pi. It holds that

\\( \pi_i = lim_{n => \inf} \frac{E(number of visits of state i during the first n steps)}{n} \\)


## Mean inter visit time

Let us have a finite-state irreducible Markov chain and the unique \pi_i = 1 / m_i

where m_i is the mean inter visit time (or expected return time) of state i.

## Limit of transient distributions

Let us have a finite-state aperiodic irreducible Markov chain and the unique stationary distribution ~\pi. It holds that

\\( \pi = lim_{n -> \inf} \lambda P^n \\)


# Finite-state Markov Chains - Overview

- Vector of expected long-run frequencies is a stationary distribution
- If it is irreducible:
 - All states are recurrent
 - There is a unique stationary distribution
 - it is 1/(mean inter visit time)
 - if it is aperiodic:
  - \pi is a limit of transient distributions


# Event Driven System

- we are staying in a state and waiting for events
- the system changes its state when the first event occurs
- the subsequent state depends on the event that occurs first

## Markovian Property
We would like to have a Markovian model - where the subsequent behavior depends on the current state only

 - It depends neither on where we were going through nor when we did the (last) step(s).
 - It also does not depend on the time we have been waiting for the next step.

We are looking for a continuous-time variant of the geometric distribution



# Continuous-Time Markov Chain (CTMC)

Continuous-Time Markov Chain (CTMC) is an event-driven system with exponentially distributed events.

In each state, we are waiting for exponentially distributed events (with arbitrary rates).

## Properties of Exponential Distribution

- waiting time: for exponentially distributed E1, E2 with rates λ1, λ2; min(E1,E2) is exponentially distributed with rate λ1 + λ2.
- mean waiting time: 1/λ; for an exponentially distributed event with rate λ
- probability that E1 wins: `P (E1 <E2) = λ1/(λ1 + λ2)` for exponential distributions E1, E2 with rates λ1, λ2.
- probability that E1 wins for a given winning time: `∀t .P (E1 <E2|min(E1,E2) = t ) = λ1/(λ1 + λ2)` for exponential distributions E1, E2 with rates λ1, λ2.


# Kendall Notation

A/S/n/B/K queue where:

A - inter-arrival time distribution
S - service time distribution
n - number of servers
B - buffer size, implicit \inf
K - population size, implicit \inf

# CTMC formally

CTMC is defined by (an initial distribution λ(0) and) a rate matrix Q where Q [i ,j ] is the rate of an event leading from state i to state j.

A distribution π on states of a CTMC is called stationary iff π=λ(t), for every time t≥0, when starting the CTMC in π=λ(0).

## Important Questions

What is the distribution on states at a given time?
 - It is to compute λ(t ), for a given time t≥0.

Does the distribution converge to a stationary distribution?
 - Is \\( lim_{t→∞}λ(t) = π \\) where πis a stationary distribution?

What is the continuous (time) frequency, i.e. fraction of time spent?
 - \\( F_s = lim_{t-> \inf} T_s (t) / t where T_s(t) is time spent in s from start to time t 

What is the queue-server utilization and the mean queue length?
 - The utilization is a probability that the server is in use, i.e. 1 −F0 as the server is idle only in state so.
 - The mean queue length is defined by \sum_s s \cdot F_s


# Dual View on CTMC

As the winning event does not depend on the winning time and vice versa, we can separately choose the winner and the winning time.

The rate λ= λ1 + λ2 + λ3 is called exit rate of the state s and the probabilities p1,p2,p3 are called exit probabilities.


## Discretization

- transform the CTMC to a DTMC (e.g. based on exit probabilities)
- analyses the CTMC using the properties of the DTMC
- useful for long-run average (steady-state) properties

1. discrete (time-abstract) frequency
2. continuous (time) frequency
3. utilization and mean length of a queue


## Uniformization Technique

Thanks to the memoryless property: Adding a self-loop does not change the behavior of a CTMC!

- Every CTMC can be transformed to the one with uniform exit rates. (Find a state with the highest exit rate and added appropriate self-loops to all others.)

- Uniform exit rates allow for easier discretization and enables analysis of distribution on states at a given time.


# Uncertainty

- Given a random experiment it is natural to ask how uncertain we are about an outcome of the experiment.
- The most uncertain is the experiment with the uniform probability distribution
- Permutation of probability distribution does not change the uncertainty
- Uncertainty should be nonnegative and equals to zero if and only if we are sure about the outcome of the experiment.
- If we include into an experiment an outcome with zero probability, this does not change our uncertainty
- As justified before, having the uniform probability distribution on n outcomes cannot be more uncertain than having the uniform probability distribution on n + 1 outcomes
- H (p1,...,pn ) is a continuous function of its parameters
- Uncertainty of an experiment consisting of a simultaneous throw of m and n sided die is as uncertain as an independent throw of m and n sided die implying


# (Shannon) entropy
of the random variable X is defined as

\\( H(X) = \sum_{x\in Im(X)} p(x) \cdot log 1/p(x) \\)

\\( H(X, Y) = H(Y) + H(X|Y) \\)

\\( H(X,Y|Z) = H(Y|Z) + H(X|Y,Z) \\)


# Cross-Entropy

cross-entropy, which measures ”entropy” of q in the probability space defined by p.

The cross-entropy of the distribution q relative to a distribution p (on a common set of sample points Im(X)) is defined as

\\( H_p(q) = - \sum_{x \in Im(X)} p(x) log q(x) = -E_p(log q(X)) \\)


# Relative entropy or Kullback-Leibler divergence

measures inefficiency of assuming that a given distribution is q when the true distribution is p.

between two probability distributions p(x) and q(x) (on a common set of sample points Im(X)) is defined as

\\( D(p||q) = \sum_{x \in Im(X)} p(x) log \frac{p(x)}{q(x)} = E_p[log \frac{p(X)}{q(X)}]

\\( D(p||q) = H_p(q) - H(p) \\)

It is not a distance, it is not symmetric, it does not satisfy the triangle inequality.

# Mutual information

measures the shared information between two random variables

\\( I(X;Y) = H(X) − H(X|Y) \\)
\\( I(X;X) = H(X)



# Information Inequality

Let p(x) and q(x), be two probability distributions. Then

\\( D(p||q) \geq 0 \\)

with equality if and only if p(x ) = q(x ) for all x.

## Nonnegativity of mutual information

I(X;Y) >= 0

with equality iff X and Y are independent


### Corollary

\\( D(p(y|x)||q(y|x)) \geq 0 \\)

with equality if and only if p(y|x) = q(y|x) for all y and x with p(x) > 0


### Corollary

I(X;Y|Z) >= 0

with equality iff X and Y are conditionally independent given Z.

# Consequences of Information Inequality


Let X be a random variable, then

\\( H(X) \leq log|Im(X)| \\)

## Conditioning reduces entropy

H(X|Y) \leq H(X)

with equality iff X and Y are independent.

\\( 0 \leq I(X;Y) = H(X) −H(X|Y) \\)

with equality iff X and Y are independent


# Code

A code C for a random variable (memoryless source) X is a mapping C: Im(X) -> D*, where D* is the set of all finite length strings over the alphabet D. With |D| = d, we say the code is d-ary.
C(x) is the codeword assigned to x and I_C(x) denotes the length of C(x).

The expected length L_C(X) of a code C for a random variable X is given by


# Non-singular Code

A code C is said to be non-singular if it maps every element in the range of X to different string in D∗, i.e.

\forall_{x,y} \in Im(X) x != y \Rightarrow C(x) != C(y).


# Uniquely Decodable Code

A code is uniquely decodable iff its extension is non-singular.

# Prefix Code

A code is called prefix code (or instantaneous code) if no codeword is a prefix of any other codeword.


# Kraft Inequality

For any prefix code over an alphabet of size d , the codeword lengths (including multiplicities) l1,l2,...lm satisfy the inequality

\sum_{i=1}^m d^{-I_i} \leq 1

Conversely, given a sequence of codeword lengths that satisfy this inequality, there exists a prefix code with these codeword lengths.


# McMillan Inequality

The codeword lengths of any uniquely decodable code must satisfy the Kraft inequality, i.e.

\sum_i d^{-I_i} \leq 1

Conversely, given a set of codeword lengths that satisfy the inequality it is possible to construct a uniquely decodable code with these codeword lengths.


# Optimal Codes

The expected length of any prefix d–ary code C for a random variable X is greater than or equal to the entropy H_d(X) (d is the base of the logarithm), i.e.

\\( L_C(X) \geq H_d(X) \\)

with equality iff for all x_i P(X=x_i) = p_i = d^{-I_i} for some integer I_i

A probability distribution is called d –adic if each of the probabilities is equal to d^−n for some integer n

# Shannon-Fano

top-down construction

Shannon-Fano coding is not optimal!

# Huffman
down-top
is optimal


# Discrete Distribution

For any algorithm generating X , the expected number of fair bits used is at least the entropy H (X ), i.e. E(T) >= H(X)


# Channels

A discrete channel is a system consisting of an input alphabet X, output alphabet Y, and a probability transition matrix p(y|x) specifying the probability we observe y \in Y when x \in X was sent.

Binary symmetric channel preserves its input with probability 1 −p and it outputs the negation of the input with probability p

Probability of an error for the code (M ,n) and the channel provided the i th message was sent is:

\\( \lambda_i = \sum p(y^n|f(i)) \\)

## Average Error Probability

The (arithmetic) average probability of error for an (M ,n) code is defined as

\\( P_e^n = 1/M \cdot \sum_{i=1}^{M} \lambda_i \\)

## Code Rate

The rate R of an (M,n) code is

\\( R = \frac{log_2 M}{n} \\) bits per transmission

Intuitively, the rate expresses the ratio between the number of message bits and the number of channel uses, i.e. it expresses the number of non-redundant bits per transmission

Intuitively, channel capacity is the noiseless throughput of the channel
it specifies the highest rate (number of non-redundant bits per channel use) at which information can be sent with arbitrarily low error.
















