---
date: 2021-09-30
title: Confidence Intervals
url: fi/ma012/conf-intervals
---


# Statistical Inference

is the process of drawing conclusions about populations or scientific truths from data

There are two types of statistical inferences; estimation and statistical (hypothesis) tests

## Estimation

> Use information from the sample to estimate (or predict) the parameter of interest.
> 
> For instance, using the result of a poll about the president's current approval rating to estimate (or predict) his or her true current approval rating nationwide.

**Point Estimates**

An estimate for a parameter that is one numerical value. An example of a point estimate is the sample mean or the sample proportion.

**Interval Estimates**

Interval estimates give an interval as the estimate for a parameter. This is a new concept which is the focus of this lesson. Such intervals are built around point estimates which us why understatning
point estimates is important to understaning interval estimates.

**Confidence Interval**

An interval of values computed from sample data that is likely to cover the true parameter of interest.


## Properties of Good Estimator

- The center of the sampling distribution for the estimate is the same as that of the population. When this property is true, the estimate is said to be unbiased. The most often-used measure of the center
	is the mean.
- The estimate has the smallest standard error when compare to other estimators. For example, in the normal distribution, the mean and median are essentially the same. However, the standard error of the
	median is about 1.25 times that of the standard error of the mean. We know the standard error of the mean is \\( \frac{\sigma}{\sqrt{n}} \\). This is why the mean is a better estimator than the
	median when the data is normal (or approximately normal).

> We use estimated standard error because, typically, population is not known.


## General Format of a Confidence Interval

In putting the two properties above together, the center of our interval should be the point estimate for the parameter of interest. With the estimated standard error of the point estimate, we can
include a measure of confidence to our estimate by forming a margin of error.

e.g. survey where 44% of respondens approved President’s reaction has +-3.5% margin of error. We known that interval would be from 40.5% to 47.5%  
 
> **General Form of a confidence interval**:  
> sample statistic +- margin of error


The margin of error will consist of two pieces. One is the standard error of the sample statistic. The other is some multiplier, , of this standard error, based on how confident we want to be in our
estimate. This multiplier will come from the same distribution as the sampling distribution of the point estimate; for example, as we will see with the sample proportion this multiplier will come from
the standard normal distribution.

> **General form of the margin of error**  
> Margin of error = \\( M \times S^{\wedge}E\(estimate) \\)

the multiplier M depends on our level of confidence

## Interpretation of a Confidence Interval

The interpretation of a confidence interval has the basic template of: "We are 'some level of percent confident' that the 'population of interest' is from 'lower bound to upper bound'. The phrases in
single quotes are replaced with the specific language of the proble. We will discuss more about the interpretation of a confidence interval after we provide a few more examples.

Most confidence levels use ranges from 90% confidence to 99% confidence, with 95% being the most widely used. In fact, when you read a report that includes a margin of error, you can usually assume this
has a 95% confidence attached to it unless otherwise stated.


## Inference for the Popluation Proportion

### Point Estimate for the Population Proportion

> Point Estimate of the Population Proportion
> 
> \\( \hat{p} = \\# \\) of successes in the sample of size n

### Confidence Interval for the Population Proportion

Recall that: if np and n(1 - p) are greater than five, then \\(\hat{p}\\) is approximately normal with mean, p, standard error \\( \sqrt{\frac{p(1-p)}{n}} \\)

Under these conditions, the sampling ditribution of the sample proportion, pm is approximately Normal. The multiplier used in the confidence interval will come from the Standard Normal distribution.


### Construct and Interpret the CI

Constructing a CI (Confidence Interval) is done in 3 steps.

#### Check Conditions

Before doing the actual computations of the interval or test, it's important to check whether these conditions are met, otherwise the calculations and conclusions may not be correct.

> The conditions we need for inderence on a mean are random, normal, independent


##### Random Condition

> A random sample or randomized experiment should be used to obtain the data.


Random samples give us unbiased data from a population. When we don't use random selection, the resulting data usually has some form of bias, so using it to infer something about the population can be
risky.

More specifically, sample means are unbiased estimators of their population mean. For example, suppose we have a bag of ping pong balls individually numbered from  to 30, so the population mean
of the bag is 15. We could take random samples of balls from the bag and calculate the mean from each sample. Some samples would have a mean higher than 15 and some would be lower. But on
average, the mean of each sample will equal 15. We write this property as \\( \mu_{\overline{x}} = \mu \\)  which holds true as long as we are taking random samples.



##### Normal Condition

> The sampling distribution \\( \overline{x} \\) (the sample mean) need to be approximately normal. This is true if our parent population is normal or if our sample is reasonably large (n >= 30).

The sampling distribution of \\( \overline{x} \\) (a sample mean) is approximately normal in a few different cases. The shape of the sampling distribution of \\( \overline{x} \\) mostly dependes on the
shape of the parent population and the sample size n.

**case 1: parent population is normally distributed**  

If the parent population is normally distributed, then the sampling distribution of \\( \overline{x} \\) is approximately normal regardless of sample size. So if we know that the parent population is normally distributed, we pass this condition even if the sample size is small. In practice, however, we usually don't know if the parent population is normally distributed.


**case 2: Not normal or unknown parent population; sample size is large (n > 30)**  

The sampling distribution of \\( \overline{x} \\) is approximately normal as long as the sample size is reasonably large. Because of the CLT, when n > 30, we can treat the sampling distribution \\(
\overline{x} \\) as approximately normal.

There are a few rare cases where the parent population has such an unusual shape that the sampling distribution of the sample mean \\( \overline{x} \\) isn't quite normal for sample sizes near 30. These
cases are rate, so in practice, we are usually safe to assume approximately normality in the sampling distribution when n >= 30.


**case 3: Not normal or unknown parent population; sample size is small (n < 30)**

As long as the parent population doesn't have outliers or strong skew, even smaller samples will produce a sampling distribution of \\( \overline{x} \\) that is approximately normal. In
practice, we can't usually see the shape of the parent population, but we can try to infer shape based on the distribution of data in the sample. If the data in the sample shows skew or outliers, we
should doubt that the parent is approximately normal, and so the sampling distribution of \\( \overline{x} \\) may not be normal either. But if the sample data are roughly symmetric and don't show
outliers or strong skew, we can assume that the sampling distribution of \\( \overline{x} \\) will be approximately normal.

The big idea is that we need to graph our sample data when \\( n\lt 30 \\), is less than, 30 and then make a decision about the normal condition based on the appearance of the sample data.



##### Independent Condition

> Individual observations need to be independent. If sampling without replacement, our sample size shouldn't be more than 10% of the population.


To use formula for stadard deviation of \\( \overline{x} \\), we need individual observations to be independent. In an experiment, good design usually takes care of independence between subjects
(control, different treatments, randomization).

In an observational study that involves sampling without replacement, individual observations aren't technically independent since removing each observation changes the population. However the 10%
condition says that if we sample 1-% or less of the population, we can treat individual observations as independent since removing each observation doesn't change the population all that much as we
sample. For instance, if our sample size is n = 30, there should to be at least N = 300 members in the population for the sample to meet independence condition.

Assuming independence between observations allows us to use this formula for standard deviation of \\( \overline{x} \\) when we're making confidence intervals or doing significance tests:

$$ \mu_{\overline{x}} = \frac{\mu}{\sqrt{n}} $$

We usually don't know the population standard deviation \\( \mu \\), so we substitute the sample standard deviation \\(s_x\\) as an estimate for \\(\mu\\). When we do this, we call it the **standard
error** of \\(\overline{x}\\) to distinguish it from the standard deviation.

So our formula for standard error of \\(\overline{x}\\) is:

$$\mu_{\overline{x}} \approx \frac{s_x}{\sqrt{n}}$$




#### Construct The General Formm


The general form of the condifence interval is point estimate \\( \pm M \times \hat{SE}(estimate) \\). The point estimate is the sample proportion \\( \hat{p} \\), and the estimated standard error is
\\(  \hat{SE}(\hat{p}) = \sqrt{\frac{\hat{p}(1-\hat{p})}{n} } \\)

\\( 1 - \alpha 100\% \\) confidence interval for the population proportion, p

$$ \hat{p} \pm z_{\alpha/2} \sqrt{\frac{\hat{p}(1 - \hat{p})}{n}} $$

where z_{\alpha/2} represent a z-value with \\( \alpha / 2 \\) area to the right of it.

General notes about the confidence interval...
	- The \\( \pm \\) in the formula above means "plus or minus". It's shorthand way of writing \\( ( \hat{p} - ..., \hat{p} + ... ) \\)
	- It's centered at the point estimate \\( \hat{p} \\)
	- The width of the interval is determined by the margin of error.
	- You must determine the multiplier


#### Interpret the Confidence Interval


We can say we are \\( (1 - \alpha)100% \\) confident that the population proportion is in interval \\( \hat{p} \pm z_{\alpha/2} \sqrt{\frac{\hat{p}(1 - \hat{p})}{n}} \\)



## How to find the multiplier using the Standard Normal Distribution

\\( z_{\alpha} \\) is the z-value having a tail area of \\( \alpha \\) to its right. With some calculation, one can use the Standard Normal Cumulative Probability Table to find the value.

## Interpreting the CI

In the graph below, we show 10 replications (for each replication, we sample 30 students and ask them whether they are Democrats) and compute an 80% Confidence Interval each time. We are lucky in this
set of 10 replications and get exactly 8 out of 10 intervals that contain the parameter. Due to the small number of replications (only 10), it is quite possible that we get 9 out of 10 or 7 out of 10
that contain the true parameter. On the other hand, if we try it 10,000 (a large number of) times, the percentage that contains the true proportions will be very close to 80%.

{{<image src="/images/confidence_interval.png" alt="confidence interval" >}} 


If we repeatedly draw random samples of size n from the population where the proportion of success in the population is p and calculate the confidence interval each time, we would expect that \\(100(1 -
\alpha)%\\) of the intervals would contain the true parameter, p.

## Sample Size Computation for the Population Proportion Confidence Interval

An important part of obtaining desired results is to get a large enough sample size. We can use what we know about the margin of error and the desired level of confidence to determine an appropriate
sample size. 

Recall that the margin of error, E, is half of the width of the confidence interval. Therefore for a one sample proportion,

$$
E = z_{\alpha/2} \sqrt{\frac{\hat{p}(1 - \hat{p})}{n}}
$$

**Precision** - The wider the interval, the poorer the precision. Note that the higher the confidence level, the wider the width (or equivalently, half width) of the interval and thus the poorer the
precision.


## Statistical/Hypothesis Tests

> Use information from the sample to determine whether a certain statement about the parameter of interest is true.
> 
> For instance, suppose a news station claims that the President’s current approval rating is more than 75%. We want to determine whether that statement is supported by the poll data.









