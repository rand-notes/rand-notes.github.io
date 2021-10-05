---
date: 2021-09-26
url: fi/iv111/3
title: IV111 lec 03
math: true
---

# Expectation of Random Variables

- Often we need a shorter description than PMF or CDF - single number, or a few number.
- First such characteristic describing a random variable is the **expectation**, also known as the **mean value**

Expectation of a random varialbe X is defined as:

$$E(X) = \sum_{x\in lm(X)} x \cdot P(X = x)$$

provided the sum is absolutely convergent. In case the sum is convergent, but not absoutely convergent, we say that no finite expectation exists. In case the sum is not convergent, the expectation has
not meaning.

for continuous variable:

$$E(X) = \int x \cdot f_X (x) dx$$


## Discrete Uniform Probability Distribution

e.g. value on 6-sided die

Let
\\(lm(X) = {x_1, x_2,..., x_n}\\)

The expectation of X is:
$$E(X) = \sum_{x\in lm(X)} x\cdot P(X=x) = \sum_{x\in lm(X)} x\cdot\frac{1}{n} = \frac{1}{n} \sum^n_{i=1} x_i $$

## Bernoulli Probability Distribution

Bernoulli probability distribution has one parameter p and models single Bernoulli trial or (biased) coin toss.

the distribution is given by:

$$p_X(x) = P(X = 0) = 1 -p$$
$$p_X(x) = P(X = 0) = p$$

the expectation is:

$$E(X) = 0 \cdot (1 - p) + 1 \cdot p = p$$


## Indicator Random Variable

Indicator random variable of an event A.

the indicator of an event A is the random variable \\(I_A\\) defined by:

\\( I_A(s) = 1\\) if \\(s \in A \\)

and

\\( I_A(s) = 0\\) if \\(s \notin A\\)

The probability distribution is:

$$p_{I_A}(0) = P(\overline{A}) = 1 - P(A)$$
$$p_{I_A}(1) = P(A)$$

the distribution function reads

$$
F_{I_A}(x) = 
\begin{cases}
\displaylines{0 \hskip 1em \text{for } x \lt 0 \\\ P(\overline{A}) \hskip 1em \text{for } 0 \leq x \geq 1) \\\ 1 \hskip 1em \text{for } x \geq 1}
\end{cases}
$$

It is a Bernoulli distribution, and so \\( E(I_A) = P(A) \\)


## Constant Random Variable


For \\(c \in \mathbb{R}\\) the function defined for all \\(s \in S \\) by \\(X(s) = c\\)

The probability distribution of this variable is:

$$
p_X(x) = 
\begin{cases}
\displaylines{1 \hskip 1em \text{ if } x = c \\\ 0 \hskip 1em \text{otherwise}}
\end{cases}
$$

The cumulative distribution function is:

$$
F_X(x) = 
\begin{cases}
\displaylines{0 \hskip 1em \text{ for } x \lt c \\\ 1 \hskip 1em \text{for} x \geq c}
\end{cases}
$$

The expectation:

$$E(X) = 1 \cdot c = c$$


## Geometric Probability Distribution

Geometric probability distribution has one parameter p and models the number of Bernoulli trials until the first 'success' occurs.

The probability function

$$p(x) = P(X = x) = (1 - p)^{x-1}p$$

The probability distribution function:

$$F(x) = P(X \leq x) = 1 - (1 - p)^{x}p$$

The expectation is

$$E(X) = \sum_{x \in lm(X)} x \cdot P(X = x)$$



## Binomial Probability Distribution

Binomial random variable X, denoted by B(n, p)

The probability distribution is:

$$
p_X(x) = P(x = x) = 
\begin{cases}
\displaylines{\binom{n}{x} p^x (1 - p)^{n-x} \hskip 1em \text{for } 0 \leq x \geq n \\\ 0 \hskip 5em \text{otherwise}}
\end{cases}
$$

the expectation is

$$E(X) = \sum_{x \in lm(X)} x \cdot P(X = x) = ... = np$$

or n independent Bernoulli trials = np. To use the easiest way, we need to define independence on random variables. Hence, we need more random variables.


# Functions of Random Variables


## Sum of Independent Random Variables


Let X and U be independent random variables. Let \\( Z = X + Y \\) is a new random variable defined as sum of X and Y. If X and Y are non-negative integer values, the probability distribution of Z is

$$ p_Z(t) = p_{X+Y}(t) = \sum^t_{x=0} p_X(x) p_Y(t-x)$$


> Observe that
> - Sum of two Bernoulli distributions with probability of success p is a binomial distribution B(2, p)
> - Sum of two binomial distributions B(n_1, p) and B(n_2, p) is a binomial distribution B(n_1 + n_2, p)


### Sums of Distributions

- Bernoulli + Bernoulli = Binomial
- Binomial + Binomial = Binomial
- Geometric + Geometric = Negative Binomial
- Negative Binomial + Negative Binomial = Negative Binomial
- Poisson + Poisson = Poisson
- Exponential + Exponential = Erlang
- Erlang + Erlang = Erlang

## Negative Binomial Distribution

Negative binomial distribution has two parameters p and r and expresses the number of Bernoulli trials to the r th success. Hence, it is a convolution of r geometric distributions.

The probability function 
$$
p_X(x) = P(X = x) =
\begin{cases}
\displaylines{\binom{x - 1}{r - 1} p^r (1 - p)^{x - r} \hskip 1em \text{ for } x \geq r \\\ 0 \hskip 2em \text{otherwise}}
\end{cases}
$$

The expectation is
$$
E(X) = \sum_{x \in lm(x)} xP(X = x) =
$$

The probability distribution - pr for r successes, \\( (1 −p)^{x −r} \\) failures, the last is successs, hence, \\( \binom{x −1}{r −1} \\) stands for placement of x − 1 successes in r − 1 trials.


## Linearity of Expectation

### Theorem (Expecation of sum)

Let X and Y be random variables. Then

$$E(X + Y) = E(X) + E(Y)$$

//TODO: proof

### Theorem (Multiplication by a constant)


Let X be random variable and c be a real number. Then
$$E(cX) = cE(X)$$

In general, the above theorem implies the following result for any linear combination of n random variables i.e.

### Corollary (Linearity of expectation)

Let \\( X_1, X_2,..., X_n \\) be random variables and \\(c_1,c_2,...,c_n \in \mathbb{R} \\). Then

$$
E(\sum^n_{i=1}c_i X_i) = \sum^n_{i=1} c_i E(X_i)
$$


## Jensen's inequality

Let X be a random variable. If f is a convex function, the

$$E[f(x)] \geq f(E(X))$$


## Expectation of Independent Random Variables

### Theorem

If X and Y are independent random variables, then:

$$
E(XY) = E(X) E(Y)
$$

//TODO: proof
//TODO: observation



# Conditional Expectation


Using the derivation of conditional probability of two events, we can derive conditional probability of (a pair of) random variables.

## Definition

The conditional probability distribution of random variable X given random variable Y (where \\( p_{X ,Y} (x , y) \\) is their joint distribution) is


$$p_{X|Y}(x|y) = P(X = x|Y = y) = \frac{P(X = x,Y = y)}{P(Y = y)} = \frac{p_{X, Y}(x, y)}{p_Y(y)}$$

provided the marginal probability \\( p_Y(y) \neq 0 \\)

---

We may consider \\( Y|(X = x) \\) to be a new random variable that is given by the conditional probability distribution \\( p_{Y|X} \\). therefore, we can define its mean.

## Definition

The **conditional expectation** of Y given X = x is defined

$$
E(Y|X = x) = \sum_y yP(Y = y|X = x) = \sum_y yp_{Y|X}(y|x)
$$

We can derive the expectation of Y from the conditional expectations.

## Theorem of total expectation

Let X and Y be random variables, then

$$
E(Y) = \sum E(Y|X = x)p_X(x)
$$

//TODO random sums example


# Markov Inequality

It is important to derive as much information as possible even from a partial description of random variable. The mean value already gives more information than one might expect, as captured by Markov
inequality.

## Theorem (Markov inequality)

Let X be a nonnegative random variable with finite mean value E(X). Then for all t >0 it holds that

$$
P(X \geq t) \leq \frac{E(X)}{t}
$$


//TODO: examples


## Proof

Let t > 0. We define a random variable \\( Y_t \\) (for fixed t ) as

$$
Y_t = 
\begin{cases}
\displaylines{0 \hskip 1em \text{ if } X \lt t \\\ t \hskip 1em X \geq t}
\end{cases}
$$

Then \\( Y_t \\) is a discrete random variable with probability distribution \\( p_{Y_{y}}(x) = P(X \lt t), p_{Y_{t}}(t) = P(X \geq t) \\) . We have

$$
E(Y_t) = tP(X \geq t)
$$


The observation \\( X \geq Y_t \\) gives

$$
E(X) \geq E(Y_y) = tP(X \geq t)
$$

what is the Markov Inequality


## Example

ex. Bound the probability of obtaining more than 75 heads in a sequence of 100 fair coin flips.

Let \\(X1, X_2, ..., X_100 \\) be random variables expressing

$$
\begin{cases}
\displaylines{1 \hskip 1em \text{if the i-th coin flip is head} \\\0 \hskip 6em otherwise}
\end{cases}
$$

Hence \\(X = \sum^100_{i=1} X_i \\) be the number of heads in 100 coin flips. Note that \\( E(X_i) = 1/2 \\) and \\( E(X) = 100/2 = 50\\)

Using the Markov inequality, we get
$$
P(X \geq 75) \leq \frac{E(X)}{75} = \frac{50}{75} = \frac{2}{3}
$$



# Moments

## Definition

> The k-th moment of a random variable X is defined as \\( E(X^k) \\)

Note that for k = 1 we get the expectation of X.

## Theorem

If X and Y are random variables with matching corresponding moments of all orders, i.e. \\( \forall k E(X^k) = E(Y^k) \\), then X and Y have the same distributions.

Usually we center the expected value to 0 - we use moments of \\( \phi(X) = X - E(X) \\)

\\( \phi \\) denotes normal distribution

i.e. we defined the k-th **central moment** of X as

$$\mu_k = E([X - E(X)]^k)$$


# Variance

The second central moment is known as the variance of X and defined as

$$
\mu_2 = E([X - E(X)]^2)
$$

The variance is usually denoted as Var(X) or \\( \mu^2_X \\)
The square root of Var(X) is known as the **standard deviation** \\( \mu_x \\)

---
variance - rozptyl  
standard deviation - smerodatna odchylka

---

Let Var(X) be the variance of the random variable X. Then \\( Var(X) = E(X^2) - [E(X)]^2 \\)

Proof:
$$
\displaylines{
Var(X) = E([X - E(X)]^2) = \\\ = E(X^2 - 2XE(X) + [E(X)]^2) = \\\ = E(X^2) - E[2XE(X)] + [E(X)]^2 = \\\ = E(X^2) - 2[E(X)]^2 + [E(X)]^2 = \\\ = E(X^2) - [E(X)]^2
}
$$

---

Let X be a random variable and a and b real numbers. Then

$$
Var(aX + b) = a^2 Var(X)
$$

/todo proof


