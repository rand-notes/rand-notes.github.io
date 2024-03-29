---
date: "2021-01-01T00:00:00Z"
url: dl2
title: DL2
---


# TOC

- [Learning algorithms](#learning-algorithms)

    - [The Task, T](#the-task,-t)

        - [Classification](#classification)

        - [Classification with missing inputs](#classification-with-missing-inputs)

        - [Regression](#regression)

        - [Transcription](#transcription)

        - [Machine translation](#machine-translation)

        - [Structured output](#structured-output)

        - [Anomaly detection](#anomaly-detection)

        - [Synthesis and sampling](#synthesis-and-sampling)

        - [Imputation of missing values](#imputation-of-missing-values)

        - [Denoising](#denoising)

        - [Density estimation or probability mass function estimation](#density-estimation-or-probability-mass-function-estimation)

    - [The Performance Measure, P](#the-performance-measure,-p)
**accuracy**; **error rate**; 

    - [The Experience, E](#the-experience,-e)
**supervised**; **unsupervised**; **Dataset**; **data points**; 

        - [Unsupervised Learning Algorithm](#unsupervised-learning-algorithm)

        - [Supervised Learning Algorithm](#supervised-learning-algorithm)
**label**; **target**; 

        - [Overview](#overview)
**semi-supervised**; **multi-instance**; **Reinforcement learning**; 

        - [Dataset](#dataset)
**design matrix**; 
- [Capacity, Overfitting and Underfitting](#capacity,-overfitting-and-underfitting)
**generalization**; **training error**; **generalization error**; **test error**; **test set**; **Statistical learning theory**; **data generating process**; **data generating distribution**; **underfitting**; **overfitting**; **capacity**; **hypothesis space**; **Representational capacity**; **effective capacity**; **Occam's razor**; **Vapnik-Chervonenkis dimension**; **nonparametric models**; **Bayes error**;

    - [Free lunch theorem](#free-lunch-theorem)

    - [Regularization](#regularization)
**weight decay**; **regularizer**; 
- [Hyperparameters and Validation Sets](#hyperparameters-and-validation-sets)
**validation set**; 
    - [Cross-validation](#cross-validation)

- [Estimators, Bias and Variance](#estimators,-bias-and-variance)

    - [Point and Function Estimation](#point-and-function-estimation)
**point estimator**; **statisctic**; 

    - [Bias](#bias)
**unbiased**; **asymptotically unbiased**; 

    - [Variance and Standard Error](#variance-and-standard-error)

    - [Trading off bias on variance to minimize MSE](#trading-off-bias-on-variance-to-minimize-mse)

        - [Consistency](#consistency)
**consistency**; **almost sure**; 
- [Maximum Likelihood Estimation](#maximum-likelihood-estimation)

    - [Conditional Log-likelihood and MSE](#conditional-log-likelihood-and-mse)

        - [Linear Regression as Maximum Likelihood](#linear-regression-as-maximum-likelihood)

        - [Properties of Maximum Likelihood](#properties-of-maximum-likelihood)
**statistical efficiency**; **parametric case**; 
- [Bayesian Statistics](#bayesian-statistics)
**frequentist statistics**; **prior probability distribution**; **the prior**; 

	- [Bayesian Linear Regression](#bayesian-linear-regression)
**posterior**; 

    - [Maximum a Posteriori (MAP) Estimation](#maximum-a-posteriori-(map)-estimation)
**maximum a posteriori**; 
- [Supervised Learning Algorithms](#supervised-learning-algorithms)

    - [Probabilistic Supervised Learning](#probabilistic-supervised-learning)

        - [Support Vector Machines](#support-vector-machines)
**kernel trick**; **Gaussian kernel**; **radial basis function**; **template matching**; **kernel machines**; **kernel methods**; **support vectors**; 
    - [Other Simple Supervised Learning Algorithms](#other-simple-supervised-learning-algorithms)

- [Unsupervised Learning Algorithms](#unsupervised-learning-algorithms)  
	
	- [Principal Components Analysis](#principal-components-analysis)

- [Stochaistic Gradient Descent](#stochaistic-gradient-descent)
**minibatch**; 
- [Building a Machine Learning Algorithm](#building-a-machine-learning-algorithm)

- [Challenges Motivating Deep Learning](#challenges-motivating-deep-learning)

    - [The Curse of Dimensionality](#the-curse-of-dimensionality)
**curse pf dimensionality**; 

    - [Local Constancy and Smoothness Regularization](#local-constancy-and-smoothness-regularization)
**smoothness prior**; **local constancy prior**; **local kernels**; 

    - [Manifold Learning](#manifold-learning)
**manifold**; **Manifold Learnign**; **manifold hypothesis**;



# Learning algorithms

Basically algorithm that is able to learn from data.

> A computer program is said to learn from experience E with respect to some class of tasks T and performance measure P, if its performance at tasks i T, as measured by P, improves with experience E.

## The Task, T

ML tasks are usually described in terms of how the machine learning system should process an example. An example is a collection of features that have been quantitatively measured from some object or
event that we want the ML system to process.


There are a lot of task types, some examples:

### Classification

In this type of thas the program is asked to specify which of k categories some input belongs to.
Algorithm usually produce a function `f: R^n -> {1, ..., k}`. 
When `y = f(x)`, the model assigns an input described by vector x to a category indentified by numeric y.
There are other variants of the classification task, eg where f outputs a probability distribution over classes.


### Classification with missing inputs

Classification becomes more challenging if the program is not guaranteed that every measurement in its input vector will always be provided.
In order to solve the classification task, the learning algorithm only has to define a single function mapping from a vector input to a categorical ouput.
when some of the inputs may be missing, rather than providing a single function, the learning algorithm must learn a set of functions.
Each function corresponds to classifying x with a different subset of its inputs missing.
This often arises in medical diagnosis, because many tests are invasive or expensive.
One way to efficiently define such a large set of functions is to learn a probability distribution over all of the relevant variables, then solve the classification task by marginalizing out the missing
variables. With n input variables, we can now obrain all 2^n different classification functions needed for each possible set of missing inputs, but we only need to learn a single function describing the
joint probability distribution.

### Regression

program predict a numerical value given some input. To solve this task, the learning algorithm, is asked to output a function `f: R^n -> R`.
eg. future prices of securities

### Transcription

ML system is asked to observe a relatively unstructured representation of some kind of data and transcribe it into discrete, textual form.

eg. OCR, speech recognition


### Machine translation

converting a sequence of symbols in some language into a sequence of symbols in another language.

eg. english -> french


### Structured output

Structured output tasks involve any task where the output is a vector (or other data structure containing multiple values) with important relationships between the different elements.
This is a broad category, and subsumes the transcription and translation tasks described above, but also many other tasks.
One examples is parsing, which is mapping a natural language into a tree that describe its grammatical structure  and tagging nodes as verbes, nouns, adverbs and so on.
The output need not have its form mirror the structure of the input as closely as in these annotation-style tasks.
These tasks are called structured output tasks because the program must output several values that are all tightly inter-related. eg. the words produced by an image captioning program must form a valid
sentence

### Anomaly detection

In this type of task, the computer program sifts through a set of events or objects, and flags some of them as being unusual or atypical.
detecting card fraud etc.

### Synthesis and sampling

Algorithm generate new examples that are similar to those in the training data.
Synthesis and smapling via machine learning can be useful for media application -- generating content like textures for large objects or landscape.
In speech synthesis task, we provide a written sentence and ask the program to emit an audio waveform containing a spoken version.
This is kind of structured ouput task, but with the added qualification that there is no single correct output for each input, and we explicitly desire a large amount of variation in the ouput, in order
for the output to seem more natural and realistic.

### Imputation of missing values

In this type of task, the ML algorithm is given a new example `x ∈ R^n`, but with some entries x_i of x missing. The algorithm must provide a prediction of the values of the missing entries.

### Denoising

In this type of task, the ML algorithm is given in input a corrupted example `x' ∈ R^n` obtained by an uknown corruption process from a clean example x ∈ R^n. The learner must predict the clean example x
from its corrupted version x', or more generally predict the conditional probability distribution `p(x|x')`


### Density estimation or probability mass function estimation

In density estimation problem, the ML algorithm is asked to learn a function `p_model: R^n -> R` where p_model(x) can be interpreted as a probability density function (if x is continuous) or a
probability mass function (if x is discrete) on the space that the examples were drawn from.

To do such tasks well the algorithm needs to learn the structure of the data it has seen. It must know where examples cluster tightly and where they are unlikely to occur.

Most of the tasks require to at least implicitly capture the structure of probability distribution. Density estimation allows us to explicitly capture that distribution. In principle, we can then perform
computations on that distribution in order to solve the other tasks as well. eg. ig we have performed density estimation to obtaion a probability distribution p(x), we can use that distribution to solve
the missing value imputation task. In practise, density estimation does not always allow us to solve all of these related tasks, because in many cases the required operations on p(x) are computationally
intractable.


## The Performance Measure, P

In order to evaluate the abilities of ML algorithm on (ussualy) specific task T, we must design a quantitative measure of its performance.

For task such as classification or transcription, we often measure the **accuracy** of the model. Accuracy is just the proportion of examples for which the model produces the correct output.

We can also obtain equivalent information by measuring the **error rate**, the proportion of examples for which the model produces an incorrect output. We often refer to the error rate as the expected
0-1 loss (0 if correctly classiffied, 1 if mistakenly).

For tasks such as density estimation it doesn't make sense to use these metrics and instead we use metrics with continuous-valued score for each example. The most common approach is to report the average
log probability the model assigns to some examples.

Performance measures using a test set of data that is separate from the data used for training ML system.

Sometimes it may not be clear what should be measured. Should be measured whole result atomically or should be model awarded for partially correct result. Sometimes we must to approximate measuring
because real measuring is computationally difficult.


## The Experience, E

ML algorithms can be divided as **supervised** and **unsupervised** by what kind of experience they are allowed to have during learning process.

**Dataset** is collection of many examples sometimes called **data points**

### Unsupervised Learning Algorithm

experience a dataset containing many features, then learn useful properties of the structure of this dataset. In DL context, we usually want to learn the entire probability distribution that generated a
dataset, wheter explicitly (density estimation) or implicitly (synthesis). Some other unsupervised learning algorithms perform other roles, like clustering, which constist of dividing the dataset into
clusters of similar examples.


### Supervised Learning Algorithm

experience a dataset containing features, but each  example is also associated with a **label** or **target**.

### Overview

Basically, unsupervised learning involvesobserving several examples of a random vector x and attempting to learn the probability distribution p(x) or some interesting properties of that distribution.
On the other hand supervised learning involves observing several examples of a random vector x and an associated value or vector y, and learning to predict y from x, ussualy by estimating p(y|x).
The line between these two are often blurred.

eg. chain rule of probability, which decomposition says that we can solve ostensibly unsupervised problem of modeling p(x) by splitting it into n supervised learning problems.

Even though the line is blur, traditionally, people refer to regression, classification and structured output problems as supervised learning. Density estimation in support of other tasks is usually
considered unsupervised learning.

There are also other variants of learning paradigm.

In **semi-supervised**, some examples include a supervision target but others do not.
In **multi-instance** learning, an entire collection of examples is labeled as containin gor not containing an example of class, but he individual members of the collection are not labeled.
Some ML algorithms do not experience a fixed dataset. eg. **Reinforcement learning** algorithms interact with an environment, so there is a feedback loop between the learning system and its experience.

### Dataset

Common way of describing a dataset is with a **design matrix**. A design matrix is a matrix containing a different example in each row. Each column corresponds to a different feature. If working with
heterogenous data we describe it as a set containing m elements. In supervised learning, design matrix of feature observations X, also contain a vector of labels y.


# Capacity, Overfitting and Underfitting

The ability to perform well on previously unobserved inputs is called **generalization**.

When training we have access to train set so we can compute some error measure on the training set called the **training error** and we reduce this training error.

What separates ML from optimization is that we want the **generalization error**, also called the **test error**, to be low.
The generalization error is defined as the expected value of the error on a new input.

We typically estimate the generalization error of a ML model by measuring its performance on a **test set** of examples that were collected separately from the training set.

**Statistical learning theory** can provide some answers on how can we affect performance on the test set we can observe only the training set.
If the sets weren't collected arbitrarily, we can make some assumptuions and make some progress.

The train and test data are generated by a probability distribution over datasets called the **data generating process**. We typically make a set of assumptions known collectively as the **i.i.d.
assumptions** (independent and identically distributed). This assumption allows us to describe the data generating process with a probability distribution over a single example. The same distribution is
then used to generate every train and test example. We call that shared underlying distribution the **data generating distribution**.

One immediate connection we can observe between the training and test erroris that the expected training error of a randomly selected model is equal to the expected test error of that model

However with ML algorithm, we do not fix parameters ahead of time, then sample both datasets. We sample training set, use it to choose parameters, then sample the test set. Under this process, the
expeted test error is greater than or equal to the expected value of training error.
The factors determining how well a machine learning algorithm will perform are its ability to:
 - make the training error small
 - make the gap between training and test error small

These two factors corresponds to the two central challenges in ML: **underfitting** **overfitting**.
Underfitting occurs when the model is not able to obtain a sufficiently low error value on the training set. 
Overfitting occurs when the gap between the training error and test error is too large.

We can control whether a model is more likely to overfit or underfit by altering its **capacity**

{{<image src="/images/capacity-error.png" alt="capacity-error" position="center" >}}

Informally, a model’s capacity is its ability to fit a wide variety of functions.
Models with low capacity may struggle to fit the training set.
Models with high capacity can overfit by memorizing properties of the training set that do not serve them well on the test set.

One way to control the capacity is by choosing its **hypothesis space**, the set of functions that the learning algorithm is allowed to select as being the solution.

For example, the linear regression algorithm has the set of all linear functions of its input as its hypothesis space.

If we generalize linear regression to include polynomials(eg quadratics or even more degree polynomials) we increase the models capacity. (By increasing degree of polynoms leads to different input but
output is still linear function). 

**Representational capacity** of model is changing according to function within family of functions of model. It's often very hard to find the best function withing this family. In practise we do not
find the best solution but rather use one that significantly reduce error. These additional limitations such as the imperfection fo the optimization, mean that the learning algorithm's **effective capacity**
may be less than the representational capacity of the model family.

**Occam's razor** This principle state sthat among competing hypotheses that explain known ovservations equally well, one should choose the "simplest one".

**Vapnik-Chervonenkis dimension** or VC dimension measures the capacity of a binary classifier. The VC dimension is defined as being the largest possible value of m for which there exists a training set
of m different x points that the classifier can label arbitrarily.

To reach the most extreme case of arbitrarily high capacity, we introduce the concept of **nonparametric models**. Sometimes, nonparametric models are just theoretical abstractions (such as
an algorithm that searches over all possible probability distributions) that cannot be implemented in practice. However, we can also design practical nonparametric models by making their complexity a
function of the training set size. One example of such an algorithm is nearest neighbor regression, where the model looks up the nearest entry in the training set and returns the
associated regression target.

Finally, we can also create a nonparametric learning algorithm by wrapping a parametric learning algorithm inside another algorithm that increases the number
of parameters as needed. For example, we could imagine an outer loop of learning that changes the degree of the polynomial learned by linear regression on top of a polynomial expansion of the input.

The ideal model is an oracle that simply knows the true probability distribution that generates the data (which still can incur some error because of noise in distribution). The error incurred by an
oracle making predictions from the true distribution p(x, y) is called the **Bayes error**.

Training and generalization error vary as the size of the training set varies. Expected generalization error can never increase as the number of training examples
increases. For nonparametric models, more data yield better generalization until the best possible error is achieved. Any fixed parametric model with less than
optimal capacity will asymptote to an error value that exceeds the Bayes error.

Note that it is possible for the model to have optimal capacity and yet still have a large gap between training and generalization
errors. In this situation, we may be able to reduce this gap by gathering more training examples

## Free lunch theorem

the no free lunch theorem for ML states that, averaged over alll possible data-generating distributions, every classification algorithm has the same error rate when classifying previously unobserved
points. 

Basically no ML algorithm is better than random predictor on all unobserved possible data, but we are ussually interested only in real-worlds distributions. 

## Regularization

The no free lunch theorem implies that we must design our machine learning algorithms to perform well on a speciffic task.

For example, we can modify the training criterion for linear regression to include **weight decay** denoted as \lambda. with \lambda = 0, we impose no preference, larger \lambda forces the weights to
become smaller. This gives us solutions that have a smaller slope, or that put weight on fewer of the features.

More generally, we can regularize a model that learns a function f(x; θ) by adding a penalty called a **regularizer** to the cost function. In the case of weight deacay.
There are many other ways of expressing preferences for different solutions, both implicitly and explicitly. Together, these different approaches are known as regularization.

# Hyperparameters and Validation Sets

Most machine learning algorithms have hyperparameters, settings that we can  to control the algorithm’s behavior.

Sometimes hyperparameters does not learn because it's difficult. More frequently, it's not appropriate to learn them on training set. If learned on the training set, such hyperparameters would always
choose the maximum possible capacity.

To solve this problem, we need a **validation set** of examples that the training algorithm does not observe.

It is important that the test examples are not used in any way to make choices about the model, including its hyperparameters. For this reason, no example from the test set can be used in the validation set.
Therefore, we always construct the validation set from the training data. Speciffically, we split the training data into two disjoint subsets.

Validation set is used to estimate the generalization error during or after training, allowing for the hyperparameters to be updated accordingly.
Typically 80 - 20 -- training - validation set

Since the validation set is used to “train” the hyperparameters, the validation set error will underestimate the generalization error, though typically by a smaller amount than the training error does.
After all hyperparameter optimization is complete, the generalization error may be estimated using the test set.

## Cross-validation

If dataset is too small, there are procedures that are based on the idea of repeating the training and testing computation on different randomly chosen subset or splits of the original data.

Most common is k-fold cross validation, in which a partition of the dataset is formed by splitting it into k non-overlapping subsets.

On trial i, the i-th subset of the data is used as the test set and the rest as training set. The test error may then be estimated by taking the average test error across k trials.


# Estimators, Bias and Variance

## Point and Function Estimation

A **point estimator** or **statisctic** is any function of the data: `θ^^_m = g(x^(1), ..., x^(m))`, where θ is ground truth and θ^^ is estimation. Almost any function is estimator, but good estimator is
a function whose output is close to the true underlying θ that generated the training data.

A function estimation is basically point estimator in function space, denoted as: f^^.

## Bias

The bias of an estimator is defined as: `bias(θ^^_m) = E(θ^^_m) - θ`.

An estimator θ^_m is said to be **unbiased** if `bias(θ^^_m) = 0` which implies that `E(θ^^_m) = θ`
An estimator θ^_m is said to be **asymptotically unbiased** if `lim_(m->\inf) bias(θ^^_m) = 0`, which implies that: `lim_(m->\inf) E(θ^^_m) = θ`

## Variance and Standard Error

The variance of an estimator is simply the variance `Var(θ^^)`, where the random variable is the training set.

Alternately, the square root of the variance is called the standard error, denoted `SE(θ)`

We often estimate the generalization error by computing the sample mean of the error on the test set.

## Trading off bias on variance to minimize MSE

Bias and variance measure two different sources of error in an estimator. Bias measeures the expected deviation from the true value of the function or parameter.
Variance on the other hand, provides a measure of the deviation from the expected estimator value that any particular sampling of the data is likely to cause.


Hot to choose between estimator with high bias and high variance? The most common way to negotiate this trade-off is to use cross-validation. Alternatively, we can also compare the mean squared error
(MSE) of the estimates.

{{<image src="/images/bias-var.png" alt="bias-var" position="center" >}}

### Consistency

We would like for our estimator to converge to the true as our training dataset grow. More formally, we would like that

`plim_(m->/inf) θ^^_m = θ`
where plim indicates convergence in probability.

This condition is known as **consistency**. It's sometimes referred to as weak consistency, with strong consistency referring to the **almost sure** convergence of θ^^ to θ. Almost sure convergence of a
sqeuemce of random variables x ... x_n to value x occurs when `p(lim_(m->\inf) x_m = x) = 1`

Consistency ensures that the bias induced by the estimator diminishes as the number of data examples grows. However, the reverse is not true - asymptotic unbiasedness does not imply consistency.


# Maximum Likelihood Estimation

MLE is most common principle for deriving specific functions that are good estimator for different models.

One way to interpret MLE is to view it as minimizing the dissimilarity between the emprirical distribution p_data defined bu the training set and the model distribution, with degree od dissimilarity the
two measured by the KL divergence.

`D_KL(p^^_data||p_model) = E x∼p^^data [log p^^_data(x) − log p_model(x)]`

The term on the left is a function only of the data-generating process, not the model. This means when we train the model to minimize the KL divergence, we need only minimize
`-E_(x~p^^_data) [log p_model(x)]`

Minimizing this KL divergence corresponds exactly to minimizing the cross-entropy between the distributions. Any loss consisting of a negative log-likelihood is a cross-entropy between the empirical
distribution deffined by the training set and the probability distribution deffined by model. e.g. MSE is the cross-entropy between the empirical distribution and a Gaussian model.

We can thus see maximum likelihood as an attempt to make the model distribution match the empirical distribution p^^_match. Ideally, we would like to match the true data-generating distribution p_data.

While the optimal θ is the same regardless of whether we are maximizing the likelihood or minimizing the KL divergence, the values of the objective functions are different. In software, we often phrase
both as minimizing a cost function.

Maximum likelihood thus becomes minimization of the negative log-likelihood (NLL), or equivalently, minimization of the cross-entropy. The perspective of maximum likelihood as minimum KL divergence
becomes helpful in this case because the KL divergence has a known minimum value of zero. The negative log-likelihood can actually become negative when x is real-valued.

## Conditional Log-likelihood and MSE

The MLE can readily be generalized to estimate a conditional probability P(y|x; θ) in order to predict y given x. This is actually the most common situation because it forms the basis for most supervised
learning. if X represents all our inputs and Y all our observed targets, then the conditional MLE is:

`θ_ML = argmax_θ P(Y|X;θ)`

If the examples are assumed to be i.i.d. then this can be decomposed into:

`θ_ML = argmax_θ \sum^m_i=1 log P(y_i|x_i;θ)`


### Linear Regression as Maximum Likelihood


Instead of producing a single prediction y^^, we now think of the model as producing a conditional distribution p(y|x). We can imagine that with an inffinitely large training set, we might see several
training examples with the same input value x but different values of y. The goal of the learning algorithm is now to fit the distribution p(y|x) to all those different y values that are all compatible
with x. derive the same linear regression algorithm we obtained before, we define p(y|x) = N(y;y^^(x;w), o^2), where o^2 is dispersion(σ). The function y^^(x;w)gives the prediction of the mean of the
Gaussian.


### Properties of Maximum Likelihood

MLE is that it can be shown to be the best estimator asymptotically, as the number of examples goes to infinite.
Under appropriate conditions, the MLE has the property of consistency meaning that as the number of training examples approaches infinity, the maximum likelihood estimate of a parameter converges to the true
value of the parameter. These conditions are as follows:
 - The true distribution p_data must lie within the model family p_model(.;θ). Otherwise, no estimator can recover p_data.
 - The true distribution p_data must correspond to exactly one value of θ. Otherwise, maximum likelihood can recover the correct p_data but will not be able to determine which value of θ was used by the 
 data-generating process.
 
There are other inductive principles besides the MLE, many of which share the property of being consistent estimators. Consistent estimators can differ, however, in their **statistical efficiency**, meaning
that one consistent estimator may obtain lower generalization error for a fixed number of samples or equivalently, may require fewer examples to obtain a fixed level of generalization error.

Statistical efficiency is typically studied in the **parametric case** (as in linear regression), where our goal is to estimate the value of a parameter (assuming it is possible to identify the true
parameter), not the value of a function. A way to measure how close we are to the true parameter is by the expected MSE, computing the squared difference between the estimated and true parameter alues,
where the expectation is over m training samples from the data-generating distribution. That parametric mean squared error decreases as m increases, and for m large, the Cramer-Rao lower bound shows that
no consistent estimator has a lower MSE than MLE.

For these reasons (consistency and efficiency), maximum likelihood is often considered the preferred estimator to use for machine learning. When the number of examples is small enough to yield overffitting
behavior, regularization strategies such as weight decay may be used to obtain a biased version of maximum likelihood that has less variance when training data is limited.

# Bayesian Statistics

So far we have discussed **frequentist statistics** and approaches based on estimating single value of O, then making all predictions thereafter base on that one estimate. Another approach is to consider
all possible values of θ when making a prediction. Another approach is to cnsider all possible values of θ when making a prediction which is domain of Bayesian statistics.

The Bayesian uses probability to reflect degrees of certainty in states of knowledge. The dataset is directly observed and so is not random. On the other hand, the true paramater θ is unkown or uncertain
and thus is represented as a random variable.

Before observing the data, we represent our knowledge of θ using the **prior probability distribution** sometimes called just **the prior**, p(θ). Generally, the ML practitioner selects a prior
distribution that is quite broad (i.e. with high entropy) to reflet a high degree of uncertainty in the value of θ before observing any data. e.g. one might assume a priori that θ lies in some finite
range or volume, with a uniform distribution. Many priors instead reflect a preference for "simplee" solutions (such as smaller magnitude coefficients, or a function that is close to being constant)


Now consider that we have a set of data samples {x_1, ..., x_n}. We can recover the effect of data on our belief about θ by combining the data likelihood p(x_1, ..., x_m| θ) with the prior via Bayes
rule:

`p(θ|x_1, ..., x_m) = p(x_1,...,x_m|θ)p(θ) / p(x_1,...,x_m)`


In the scenarios where Bayesian estimation is typically used, the prior begins as a relatively uniform or Gaussian distribution with high entropy, and the observation of the data usually causes the
posterior to lose entropy and concentrate around a few highly likely values of the parameters.

> Unlike the maximum likelihood approach that makes predictions using a point estimate of O, the Bayesian approach is to make predictions using a full distribution over O.

e.g., after observing m examples the predicted distribution over the next data sample, x_m+1, is given by:

`p(x_m+1 | x_1,...,x_m) = \int{p(x_m+1 | θpθ | x_1, ... x_m)} dθ`

Frequentist approach addresses the uncertainty in a given point estimate of θ by evaluating its variance. The variance of the estimator is an assessment of how the estimate might change with alternative
samplings of the observed data. The Bayesian answer to the question of how to deal with the uncertainty in the estimator is to simply integrate over it, which tends to protect well against overffitting.

Second difference between Bayesian and maximum likelihood approach is due to Bayesian prior contribution. The prior has an influence by shifting probability mass density ards regions of the parameter
space that are preferred a priori. In practice the prior often expresses a preference for models that are simpler or more smooth. Critics of the Bayesian approach identify the prior as a source of
subjective human judgment affecting the predictions.

Bayesian methods typically generalize much better when limited training data is available but typically suffer from high computational cost when the number of training examples is large.

## Bayesian Linear Regression

Expressed as a Gaussian conditional distribution on y_train, we have:

`p(y_train | X_train, w) = N(y_train; X_train w, I) ∝ exp(-1/2(y_train - X_train w)^T (y_train - X_train w))`

where we follow the standard MSE formulation in assuming that the Gaussian variance on y is one.

For real-valued parameters it is common to use a Gaussian as a prior distribution:

`p(w) = N(w; µ_0, Λ_0)`

where µ_0 and Λ_0 are the prior distribution mean vector and covariance matrix respectively.

With the prior thus specified, we can now proceed in determining the **posterior** distribution over the model paramater

`p(w | X, y) ∝ p(y| X, w)p(w)`


## Maximum a Posteriori (MAP) Estimation

Most principled approach is to use posterior distribution to make predictions but sometimes we also want a single point estimate. One common reason for desiring a point estimate is that most operations
involving the Bayesian posterior for most interesting models are intractable, and a point estimate offers a tractable approximation. Rather than simply returning to the maximum likelihood estimate, we
can still gain some of the benefit of the Bayesian approach by allowing the prior to influence the choice of the point estimate. One rational way to do this is to choose the **maximum a posteriori**
point estimate. The MAP estimate chooses the point of maximal posterior probability (or maximal probability density in the more common case of continous θ:
`θ_MAP = arg max_θ p(θ|x) = arg max log p(x|θ) + log p(θ)`.

we recognize, on the righthand side, `log p(x|0)`, that is, the standard log-likelihood term, and `log p(θ)`, corresponding to the prior distribution. Becasuse 

# Supervised Learning Algorithms

Learning algorithms that learn to associate some input with some output, given a training set of examples of inputs x and outputs y. In many cases the outputs y must be provided by a human "supervisor",
but the term still applies ven when the training set targets were collected automatically.

## Probabilistic Supervised Learning

A lot of supervised learning algorithms are based on estimating a probability distribution p(y|x). We can do this simply by using maximum likelihood estimation to find the best parameter vector θ for a
parametric family of distributions p(y|x;θ)

e.g. linear regression corresponds to te family
`p(y|x;θ) = N(y; θ^T x, I)`

We can generalize linear regression to the classification scenario by defining a differentfamily of probability distributions. If we have two classes, class 0 and class 1, then we need only specify the
probability of one of these classes. The probability of class 1 determines the probability of class 0, because these two values must add up to 1.

The normal distribution over real-valued numbers that we used for linear regression is parametrized in terms of a mean. Any value we supply for this mean is valid. A distribution over a binary variable
is slighty more complicated, because its mean must always be between 0 and 1. One way to solve this problem is to use the logistic sigmoid function to squash the output of the linear function into the
interval (0, 1) and interpret that value as probability:

`p(y = 1|x; θ) = σ(θ^T x)`

This approach is known as logistic regression (a somewhat strange name since we use the model for classification ratger than regression).


In the case of linear regression, we were able to find the optimal weights by solving the normal equations. Logistic regression is somewhat more difficult. There is no closed-form solution for its optimal
weights. Instead, we must search for them by maximizing the log-likelihood. We can do this by minimizing the negative log-likelihood using gradient descent.


This same strategy can be applied to essentially any supervised learning problem, by writing down a parametric family of conditional probability distributions over the right kind of input and output
variables.


### Support Vector Machines


> This model is similar to logistic regression in that it's driven by a linear function `w^T x + b` but does not provide probabilities, but only outputs a class identity. The SVM predicts positive class when `w^T x + b` is positive otherwise it's negative class.

One key innovation associated with SVM is the **kernel trick**.
The kernel trick consists of observing that many machine learning algorithms can be written exclusively in terms of dot products between examples.
e.g. it can be shown that the linear function used by the support vector machine can be rewritten as:
`w^T x + b = b + \sum^m_i=1 \alpha_i x^T x_i`,
where x_i is a training example, and \alpha is a vector of coefficients. Rewritting the learning algorithm this way enables us to replace x with the output of a given feature function φ(x) and the dot
product with a function `k(x, x_i) = φ(x) \cdot φ(x_i)`

After replacing dot products with kernel evaluations, we can make predictions using the function:
`f(x) = b + \sum_i \alpha_i k(x, x_i)`

This function is nonlinear with respect to x, but the relationship between φ(x) and f(x) is linear. Also, the relationship between \alpha and f(x) is linear. The kernel-based function is exactly
equivalent to preprocessing the data by applying φ(x) to all inputs, then learning a linear model in the new transformed space.

The kernel trick is powerful for two reasons. First, it enables us to learn models that are nonlinear as a function of x using convex optimization techniques that are guaranteed to converge effictiently.
This is possible because we consider φ fixed and optimze only \alpha, that is, the optimization algorithm can view the decision function as being linear in different space. Second, the kernel function k
often admits an implementation that is significantly more computationally efficient than naively constructing two φ(x) vectors and explicitely taking their dot product.

In some cases φ(x) can even be infinite dimensional, which would result in an inffinite computational cost for the naive, explicit approach. In many cases, k(x, x') is a nonlinear, tractable function of x
even when φ(x) is intractable.

The most commonly used kernel is the **Gaussian kernel** also known as **radial basis function** (RBF) kernel, because its value decreases along lines in v space radiating outward from u. 
`k(u, v) = N(u - v; 0, σ^2 I)`

We can think of the Gaussian kernel as performing a kind of **template matching**. A training example x associated with training label y becomes a template for class y. When a test point x' is near x
accorfing to Euclidean distanc, the Gaussian kernel has a large response, indicating that x' is very similar to the x template. The model then puts a large weight on the associated training label y.
Overall, the prediction will combine many such training labels weighted by the similarity of the corresponding training examples.

SVM are not the only algorithm that can be enhanced using the kernel trick. Many other linear models can be enhanced in this way.

> The category of algorithms that employ the kernel trick is known as **kernel machines** or **kernel methods**

Training examples in kernel machines are known as **support vectors**.


Kernel machines also suffer from a high computational cost of training when the dataset is large. Kernel machines with generic kernels struggle to generalize well. 


## Other Simple Supervised Learning Algorithms

We ussually think of k-nearest neighbors as not having any parameters and just implementing a simple function. We can turn it into a supervised learning algorithm by just taking from the training set
the nearest neigbours class. Problem is that it cannot learn that one feature is more discriminative than another.

Another type of learning algorithm that also breaks the input space into regions and has separate parameters for each region is the decision tree and its many variants.


# Unsupervised Learning Algorithms

Unsupervised algorithms are those that experience only features but not a supervision signal.
A classic unsupervised learning task is to find the "best" rpresentation of the data. By best we can mean different things, but generally speaking we are looking for a representation that preserves as
much information about x as possible while eying some penalty or constraint aimed at keeping the representation simpler or more accessible than x itself.

There are multiple ways of defining a simpler representation. Three of the most common include lower-dimensional representations, sparse representations and independent representations.

Low-dimensional representations attempt to compress as much information about x as possible in a smaller representation. Often yield elements that have fewer or weaker endencies than the original
high-dimensional data. This is because one way to reduce the size of a representation is to find and remove redundancies. Identifying and removing more redundancy enables the dimensionality reduction
algorithm to hieve more compression while discarding less information.

Sparse representations embed the dataset into a representation whose entries are mostly zeros for most inputs. The use of sparse representations typically requires increasing the dimensionality of the
representation, so that the representation becoming mostly zeros does not discard too much information.

Independent representations attempt to disentangle the sources of variation underlying the data distribution such that the dimensions of the representation are statistically independent.


## Principal Components Analysis

PCA algorithm provides a means of compressing data. We can also view PCA as an unsupervised learning algorithm that learns a representation of data. This representation is based on two of the criteria
for a simple representation described above. PCA learns a representation that has lower dimensionality than the original input. It also learns a representation whose elements have no linear correlation
with each other. This is a first step toward the criterion of learning representations whose elements are statistically independent. To achieve full independence, a representation learning algorithm must
also remove the nonlinear relationships between variables.

PCA learns an orthogonal, linear transformation of the data that projects an input x to a representation z.


# Stochaistic Gradient Descent

Nearly all DL is powered by one very imporant algorithm: Stochaistic Gradient Descent (SGD). SGD is an extension of the gradient descent algorithm.

A recurring problem in machine learning is that large training sets are necessary for good generalization, but large training sets are also more computationally expensive.

The cost function used by a machine learning algorithm often decomposes as a sum over training examples of some per-example loss function. e.g. the negative conditional log-likelihood of the training
data can be written as:

`J(θ) = E_(x,y~p^^_data) L(x, y, θ) = 1/m \sum_i=1^m L(x_i, y_i, θ)`

where L is the per-example loss `L(x, y, θ) = -log p(y | x;θ)`

The computational cost of this operation is O(m). As the training set size grows to billions of examples, the time to take a single gradient step becomes prohibitively long.

The insight of SGD is that the gradient is an expectation. The expectation may be approximately estimated using a small set of samples. Specifically, on each step of the algorithm, we can sample a
**minibatch** of examples drawn uniformly from the training set. The minibatch size is typically chosen to be a relatively small, ranging from one to a few hundred. The minibatch size is usually held
fixed as the training set size grows. We may fit a training set with billions of examples using updates computed on only a hundred examples. 

The estimate of the gradient is formed as:

`g = 1/m' ∇_θ \sum_i=1^m' L(x_i, y_i, θ)`

where m' is minibatch size. The stochastic gradient descent algorithm then follows the estimated gradient downhill:

`θ <- θ - eg`

where e is learning rate.

Gradient descent in general has often been regarded as slow or unreliable. In the past, the application of gradient descent to nonconvex optimization problems was regarded as foolhardy or unprincipled.
day, we know that the machine work very well when trained with gradient descent. The optimization algorithm may not be guaranteed to arrive at even a cal minimum in a reasonable amount of time, but it
often finds a very low value of the cost function quickly enough to be useful.


SGD has many important uses outside the context of DL. It is the main way to train large linear models on very large datasets. For a fixed model size, the cost per SGD update does not depend on the
training set size m. In practice, we often use a larger model as the training set size increases, but we are not forced to do so. The number of updates required to reach convergence usually increases
with training set size. However, as m approaches infinity, the model will eventually converge to its best possible test error before SGD has sampled every example in the training set. Increasing m
further will not extend the amount of training time needed to reach the model’s best possible test error. From this point of view, one can argue that the asymptotic cost of training a model with SGD is
O(1) as a function of m.

# Building a Machine Learning Algorithm

Nearly all deep learning algorithms can be described as particular instances of a fairly simple recipe: combine a speciffication of a dataset, a cost function, an optimization procedure and a mdoel.

By realizing that we can replace any of these components mostly independently from the others, we can obtain a wide range of algorithms.

The cost function typically includes at least one term that causes the learning process to perform statistical estimation. The most common cost function is the negative log-likelihood, so that minimizing
the cost function causes maximum likelihood estimation.

The cost function may also include additional terms, such as regularization terms.

If we change the model to be nonlinear, then most cost functions can no longer be optimized in closed form. This requires us to choose an iterative numerical optimization procedure, such as gradient descent.

The recipe for constructing a learning algorithm by combining models, costs, and optimization algorithms supports both supervised and unsupervised learning. The linear regression example shows how to
support supervised learning. Unsupervised learning can be supported by defining a dataset that contains only X and providing an appropriate unsupervised cost and model.

In some cases, the cost function may be a function that we cannot actually aluate, for computational reasons. In these cases, we can still approximately minimize it using iterative numerical
optimization, as long as we have some way of approximating its gradients.

Most machine learning algorithms make use of this recipe, though it may not be immediately obvious. If a machine learning algorithm seems especially unique or hand designed, it can usually be understood
as using a special-case optimizer. Some models, such as decision trees and k-means, require special-case optimizers because their cost functions have flat regions that make them inappropriate for
minimization by gradient-based optimizers. Recognizing that most machine learning algorithms can be described using this recipe helps to see the different algorithms as part of a taxonomy of methods for
doing related tasks that work for similar reasons, rather than as a long list of algorithms that each have separate justifications.

# Challenges Motivating Deep Learning


The development of deep learning was motivated in part by the failure of traditional algorithms to generalize well on AI tasks such as speech/image recognition.

## The Curse of Dimensionality

Many machine learning problems become exceedingly difficult when the number of dimensions in the data is high. This phenomenon is known as the **curse pf dimensionality**. Of particular concern is that the
number of possible distinct configurations of a set of variables increases exponentially as the number of variables increses.

The curse of dimensionality arises in many places in computer science, especially in machine learning.
One challenge posed by the curse of dimensionality is a statistical challenge.

Statistical challenge arises because the number of possible configurations of x is much larger than the number of training examples. 

To understand the issue, let us consider that the input space is organized into a grid. We can describe low-dimensional space with a small number of grid cells that are mostly occupied by the data. When
generalizing to a new data point, we can usually tell what to do simply by inspecting the training examples that lie in the same cell as the new input.

For example, if estimating the probability density at some point x, we can just return the number of training examples in the same unit volume cell as x, divided by the total number of training examples.
If we wish to classify an example, we can return the most common class of training examples in the same cell. If we are doing regression, we can average the target values observed over the examples in
that cell. But what about the cells for which we have seen no example? Because in high-dimensional spaces, the number of configurations is huge, much larger than our number of examples, a typical grid
cell has no training example associated with it. How could we possibly say something meaningful about these new configurations? Many traditional machine learning algorithms simply assume that the output
at a new point should be approximately the same as the output at the nearest training point.


## Local Constancy and Smoothness Regularization

To generalize well, machine learning algorithms need to be guided by prior beliefs about what kind of function they should learn. We have seen these priors incorporated as explicit beliefs in the form of
probability distributions over parameters of the model. More informally, we may also discuss prior beliefs as directly influencing the function itself and influencing the parameters only indirectly, as a
result of the relationship between the parameters and the funtion.
Additionally, we informally discuss prior beliefs as being expressed implicitly by choosing algorithms that are biased toward choosing some class of functions over another, even though these biases may
not be expressed (or even be possible to express) in terms of a probability distribution representing our degree of belief in various functions.

> Among the most widely used of these implicit “priors” is the **smoothness prior** or **local constancy prior**. This prior states that the function we learn should not change very much within small region.

Many simpler algorithms rely exclusively on this prior to generalize well, and as a result, they fail to scale to the statistical challenges involved in solving AI level tasks.


There are many different ways to implicitly or explicitly express a prior belief that the learned function should be smooth or locally constant. All these different methods are designed to encourage the
learning process to learn a function f∗ that satisfies the condition.

`f^*(x) ≈ f^x(x + \eps)` for most configurations x and small change \eps (learning rate).

In other words, if we know a good answer for an input x (e.g. x is a labeled training example), then that answer is probably good in the neighborhood of x.  If we have several good answers in some
neighborhood, we would combine them (by some form of averaging or interpolation) to produce an answer that agrees with as many of them as much as possible.

An extreme example of the local constancy approach is the k-nearest neighbors family of learning algorithms. These predictors are literally constant over each region containing all the points x that have
the same set of k nearest neighbors in the training set. For k=1, the number of distinguishable regions cannot be more than the number of training examples.


While the k-nearest neighbors algorithm copies the output from nearby training examples, most kernel machines interpolate between training set outputs associated with nearby training examples.

An important class of kernels is the family of **local kernels**, where k(u, v) is large when u=v and decreses as u and v grown further apart from each other (both u and v are vectors). A local kernel
can be thought of as a similarity function that performs template matching, by measuring how closely a test example x resembles each training example x_i. Much of the modern motivation for deep learning
is derived from studying the limitations of local template matching and how deep models are able to succeed in cases where local template matching fails. 


Decision trees also suffer from the limitations of exclusively smoothness-based learning, because they break the input space into as many regions as there are leaves and use a separate parameter (or
sometimes many parameters for extensions of decision trees) in each region. If the target function requires a tree with at least n leaves to be represented accurately, then at least n training examples
are required to fit the tree. A multiple of n is needed to achieve some level of statistical confidence in the predicted output.

In general, to distinguish O(k) regions in input space, all these methods require O(k) examples. Typically there are O(k) parameters, with O(1) parameters associated with each of the O(k) regions.

Is there a way to represent a complex function that has many more regions to be distinguished than the number of training examples? Clearly, assuming only
smoothness of the underlying function will not allow a learner to do that. For example, imagine that the target function is a kind of checkerboard. A checkerboard
contains many variations, but there is a simple structure to them. Imagine what happens when the number of training examples is substantially smaller than the
number of black and white squares on the checkerboard. Based on only local generalization and the smoothness or local constancy prior, the learner would be
guaranteed to correctly guess the color of a new point if it lay within the same checkerboard square as a training example. There is no guarantee, however, that
the learner could correctly extend the checkerboard pattern to points lying in squares that do not contain training examples. With this prior alone, the only
information that an example tells us is the color of its square, and the only way to get the colors of the entire checkerboard right is to cover each of its cells with at least one example.


The smoothness assumption and the associated nonparametric learning algorithms work extremely well as long as there are enough examples for the learning
algorithm to observe high points on most peaks and low points on most valleys of the true underlying function to be learned. This is generally true when the
function to be learned is smooth enough and varies in few enough dimensions. In high dimensions, even a very smooth function can change smoothly but in a
different way along each dimension. If the function additionally behaves differently in various regions, it can become extremely complicated to describe with a set of
training examples. If the function is complicated (we want to distinguish a huge number of regions compared to the number of examples), is there any hope to generalize well?


The answer to both of these questions—whether it is possible to represent a complicated function eﬃciently, and whether it is possible for the estimated function to generalize well to new inputs—is yes.
The key insight is that a very large number of regions, such as O(2^k), can be defined with O(k) examples, so long as we duce some dependencies between the regions through additional assumptions about
the underlying data-generating distribution. In this way, we can actually generalize nonlocally. Many different deep learning algorithms provide implicit or explicit assumptions that are reasonable for a
broad range of AI tasks in order to capture these advantages.

Other approaches to machine learning often make stronger, task-specific assumptions. For example, we could easily solve the checkerboard task by providing
the assumption that the target function is periodic. Usually we do not include such strong, task-specific assumptions in neural networks so that they can generalize
to a much wider variety of structures. AI tasks have structure that is much too complex to be limited to simple, manually specified properties such as periodicity, so we want learning algorithms that
embody more general-purpose assumptions.
The core idea in deep learning is that we assume that the data was generated by the composition of factors, or features, potentially at multiple levels in a hierarchy. Many other similarly generic
assumptions can further improve deep learning algorithms. These apparently mild assumptions allow an exponential gain in the relationship between the number of examples and the number of regions that can
be distinguished.

The exponential advantages conferred by the use of deep distributed representations counter the exponential challenges posed by the curse of dimensionality.


## Manifold Learning

An important concept underlying many ideas in machine learning is that of a manifold. A **manifold** is connected region.  From any given point, the manifold locally appears to be a Euclidean space. In
everyday life, we experience the surface of the world as a 2-D plane, but it is in fact a spherical manifold in 3-D space.
The concept of a neighborhood surrounding each point implies the existence of transformations that can be applied to move on the manifold from one position to a neighboring one. In the example of the
world’s surface as a manifold, one can walk north, south, east, or west.

Although there is a formal mathematical meaning to the term “manifold,” in machine learning it tends to be used more loosely to designate a connected set of points that can be approximated well by
considering only a small number of degrees of freedom, or dimensions, embedded in a higher-dimensional space. Each dimension corresponds to a local direction of variation. 
In the context of machine learning, we allow the dimensionality of the manifold to vary from one point to another. This often happens when a
manifold intersects itself. For example, a figure eight is a manifold that has a single dimension in most places but two dimensions at the intersection at the center.

Many machine learning problems seem hopeless if we expect the machine learning algorithm to learn functions with interesting variations across all of R^n.
**Manifold Learnign** algorithms surmount this obstacle by assuming that most of R^n consists of invalid inputs, and that interesting inputs occur only along a collection of manifolds containing a small
subset of points, with interesting variations in the output of the learned function occurring only along directions that lie on the manifold, or with interesting variations happening only when we move
from one manifold to another. Manifold learning was introduced in the case of continuous-valued data and in the unsupervised learning setting, although this probability concentration idea can be
generalized to both discrete data and the supervised learning setting: the key assumption remains that probability mass is highly concentrated. 


The assumption that the data lies along a low-dimensional manifold may not always be correct or useful. We argue that in the context of AI tasks, such as those that involve processing images, sounds, or
text, the manifold assumption is at least approximately correct. The evidence in favor of this assumption consists of two categories of observations.

The first observation in favor of the **manifold hypothesis** is that the probability distribution over images, text strings, and sounds that occur in real life is highly concentrated. Uniform noise
essentially never resembles structured inputs from these domains. Similarly, if you generate a document by picking letters uniformly at random, what is the probability that you will get a meaningful
English-language text? Almost zero, again, because most of the long sequences of letters do not correspond to a natural language sequence: the distribution of natural language sequences occupies a very
little volume in the total space of sequences of letters.

Of course, concentrated probability distributions are not suﬃcient to show that the data lies on a reasonably small number of manifolds. We must also establish that the examples we encounter are
connected to each other by other examples with each example surrounded by other highly similar examples that can be reached y applying transformations to traverse the manifold. The second argument in favor
of the manifold hypothesis is that we can imagine such neighborhoods and transformations, at least informally.
In the case of images, we can certainly think of many possible transformations that allow us to trace out a manifold in image space: we can gradually dim or brighten the lights, gradually move or rotate
objects in the image, gradually alter the colors on the surfaces of objects, and so forth.
Multiple manifolds are likely involved in most applications. For example, the manifold of human face images may not be connected to the manifold of cat face images.


When the data lies on a low-dimensional manifold, it can be most natural for machine learning algorithms to represent the data in terms of coordinates on the
manifold, rather than in terms of coordinates in R^n. In everyday life, we can think of roads as 1-D manifolds embedded in 3-D space. We give directions to specific
addresses in terms of address numbers along these 1-D roads, not in terms of coordinates in 3-D space.

Extracting these manifold coordinates is challenging but holds the promise of improving many machine learning algorithms. This general principle is applied in many contexts.

{{<image src="/images/manifold.png" alt="manifold" position="center" >}}


