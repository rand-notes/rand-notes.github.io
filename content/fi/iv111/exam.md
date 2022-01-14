---
title: exam
url: iv111/exam
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

\\( p_X(x) = P(X=x) = P(X_1 = x_1 \and X_2 = x_2 \and ...) \\)

The joint (or compound) distribution functionaof a random vector X is defined to be

\\( F_X(x) = P(X_1 \leq x_1 \and X_2 \leq x_2 \and ...) \\)



Let pX(x) be a joint probability distribution of a random variable X = (X1,X2). The marginal probability distribution of X1 is defined as

\\( p_X_1(x) = P(X1=x) = \sum_{x_2 \in lm(X_2)} p_X((x ,x2))  \\)

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

p_{X|Y}(x|y) = P(X=x|Y=y) = \frac{P(X=x, Y=y)}{P(Y=y)} = \frac{p_{X,Y}(x,y)}{p_Y(y)}


# Markov inequality

def: Let X be a nonnegative random variable with finite mean value E(X). Then for all t > 0 it holds that:

\\( P(X \geq t) \leq \frac{E(X)}{t} \\)


# Moments

The k th moment of a random variable X is defined as E (X^k).
Note that for k = 1 we get the expectation of X

Usually we center the expected value to 0 – we use moments of X - E(X)
i.e. μ_k = E([X-E(X)]^k)

# Variance

The second central moment is known as the variance

Var(X) = E(X^2) - [E(X)]^2


# Covariance

Cov(X,Y) = E(XY) − E(X)E(Y)

Covariance measures linear dependence between two random variables

We define the correlation coefficient ρ(X ,Y ) as the normalized covariance, i.e.

ρ(X,Y) = \frac{Cov(X,Y)}{\sqrt{Var(X)Var(Y)}}

For independent random variables X and Y , it holds that Cov (X ,Y ) = 0.


\( X and Y independent \Rightarrow Cov(X,Y) = 0 \)
\( X and Y independent \not\Leftarrow Cov(X,Y) = 0 \)


