---
date: 2021-10-04
title: lec 04
url: fi/iv111/4
---

{{<image src="/images/distrib_summ.png" position="center" alt="distributions summary" >}}

# Covariance

$$ E([X - E(X)][Y - E(Y)]) = \sum_{i, j} p_{x_i, y_j} [x_i - E(X)][y_j - E(Y)] $$ 

is called the covariance of X and Y and denoted Cov(X, Y)


Covariance measures **linear dependence** between two random variables. It is positive if the variables are correlated, and negative when anticorrelated.

e.g. when Y = aX, using E(Y) = aE(x) we have Cov(X, Y) = aVar(X)


we define the correlation coefficient \rho(X, Y) as the normalized covariance, i.e.

$$
\rho(X, Y) = \frac{Cov(X, Y)}{\sqrt{Var(X)Var(Y)}}
$$

For any two random variables X and Y it holds that

$$
0 \leq (Cov(X, Y))^2 \leq Var(X)Var(Y)
$$


i.e. \\( -1 \leq \rho(X, Y) \leq 1 \\)

----

Let X and Y be random variables. The the covariance is

$$
Cov(X, Y) = E(XY) - E(X)E(Y)
$$

Cov(X, Y) = E([X - E(X)][Y - E(Y)]) = ... = E(XY) - E(X)E(Y)

Corollary:

**For independent random variables X and Y, it holds that Cov(X, Y) = 0**

It may happen that X is completely dependent on Y and yet the covariance is 0.

Hence,

X and Y independent \\( \nRightarrow Cov(X, Y) \\)  
X and Y independent \\( \nLeftarrow Cov(X, Y) \\)



# Variance of Independent Variables


If X and Y are independent random variables, then

Var(X + Y) = Var(X) + Var(Y)

---

If X and Y are not independent random variables, we obtain

Var(X + Y) = Var(X) + Var(Y) + 2Cov(X, Y)


/todo example

# Conditional probability

Using the derivation of conditional probability of two events, we can derive conditional probability of a pair of random variables

The conditional probability distribution of random variable Y given random variable X (their joint distribution is \\( p_{X, Y} \\) is

$$
p_{Y|X} (y|x) = P(Y=y|X=x) = \frac{P(Y=y, X=x)}{P(X=x)} = \frac{p_{X, Y} (x,y)}{p_X(x)}
$$

provided the marginal probability p_X(x) != 0

# Conditional expectation

We may consider Y|(X=x) to be a new random variable that is given by the conditional probability distribution \\( p_{Y|X} \\). Therefore, we can define its mean and moments

The conditional expectation of Y given X = x is defined
$$
E(Y|X=x) = \sum_y yP(Y=y|X=x) = \sum_y yp_{Y|X} (y|x)
$$

Analogously, the **conditional variance** can be defined as:

$$
Var(Y|X=x) = E(Y^2|X=x) - [E(Y|X=x)]^2
$$

---

We can derive the expectation of Y from the conditional expectation.

## Theorem of total expectation

Let X and Y be random variables, then

$$E(Y) = \sum_x E(Y|X=x) p_X (x)$$


## Theorem of total moments

Let X and Y be random varibles, then

$$E(Y^k) = \sum_x E(Y^k|X=x)p_X (x)$$


# Chebyshev Inequality

In case we know both mean value and variance of a random variable, we can use much more accurate estimation

## Theorem

Let X be a random variable with finite variance. Then

$$
P[|X-E(X)|\geq t] \leq \frac{Var(X)}{t^2}, t \geq 0
$$

or, alternatively, substituting \\( t = k\sigma_k = k\sqrt{Var(X)} \\)

$$
P[|X-E(X)|\geq k\sigma_x] \leq \frac{1}{k^2}, t \geq 0
$$

or, alternatively, substituting \\( X' = X - E(X) \\) 

$$
P[|X'|\geq t] \leq \frac{E(X'^2)}{t^2}, t \geq 0
$$

## Proof

We apply the Markov inequality to the nonnegative vriable [X - E(X)]^2 and we replace t by t^2 to get

$$
P[(X - E(X))^2 \geq t^2] \leq \frac{E([X - E(X)]^2)}{t^2} = \frac{Var(X)}{t^2}
$$

We obtain the Chebyshev inequality using the fact that the events \\( [(X - E(X))^2 \geq t^2 ] = [|X - E(X)| \geq t] \\) are the same














