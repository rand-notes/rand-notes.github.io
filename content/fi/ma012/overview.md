---
url: fi/ma012/cs
---
CPD - continuous probability distribution

T-distribution - CPD for astimating the mean of a normally distributed population with small size and unknown standard deviation
T-test - t-distribution under null hypothesis

F-distribution - CPD used as null hypothesis in ANOVA and other F-tests.
F-test -- F-distribution under null hypothesis

z-test - test whether two population means are different, when variances are known and sample size large



# Tests Overview

H_0 zamitneme pokud je p mensi nez alpha

# ANOVA

v pripade ze zamitneme H0, tedy rekneme ze stredni hodnoty se lisi, pouzijeme mnohonasobne pozorovani (Tukey, Scheffe) pro nalezeni dvojice ktere jsou odlisne.

jmeno anova rika ze analyzuje rozptyl ale actually to meri stredni hodnoty.


# Testo dobre shody

pouziva Chi-squared distribution

pocet stupnu volnosti je n - p, kde n je redukce stupnu volnosti. p je 3 pro normalni rozdeleni, 2 pro poisson, gen gamma 4


# Poradove testy

vsechny poradove testy testuji median ne stredni hodnoty


# Znamenkovy test

testujeme H0 ze median je X. 

S+ se rovna poctu hodnot ktere jsou nizsi nebo rovno nez testovany median.
n je pocet prvku.


asymptoticka testovaci statistika je

U = (2 * S+ - n)/sqrt(n)


# Correlation Analysis

parametric:
Pearson's r

nonparametric:
Spearsman's Rank Correlation


Post hoc testy vyrovnavaji rust chyby: Tukey's a Scheffe's

Partial Correlation, in contrast to Pearson Correlation, takes into account the existence of a third variable and “controlling” it.

Parametricky uvazuji ze data pochazi z nejake distribuce napr. normalniho rozdeleni

Pokud chceme overit ze ma nahodna velicina urcite predem dane (jakekoli) rozdeleni pravdepodobnosti pouzijeme **test dobre shody**

# Stupne volnosti

casto je N - 1, kde N je pocet vzorku, 1 se odecita protoze vetsinou nejaky parametr predpocitame napr. median.


# Yarnoldovo kriterium

podminka dobre aproximace.

pouziva se jako podminka pred testy dobre shody. Pokud nevyjde upravime kategorie jejich vhodnym sloucenim a podminku znovu overime.

# Pearsonuv test dobre shody

pocet volnosti je n - 1 - k neboli df - k, kde n je pocet vzorku (intervalu pokud vzorky rozdelujeme) a k je pocet odhadnutych parametru. k=3 pro normal

je pro katergorie. ze kterych ale muzeme udelat spojitou fci. takze je univerzalni na vse.

# ECDF

empiricka distrib fce. prochazime x osu ptame e kolik sledovanych dat je pod nimi.

# Kolmogorov Smirnov

testuje shodnost spojitych fci. merime vzdalenost bodu ECDF od testovane fce (merime svisle)

# Liliefors test

prakticky K-S test pro normalitu

# Shapiro Wilk test

test normality, vyuziva poradove statistiky.


# Test korelovanosti

pokud vyjde cca 0 - hypotezu nezamitame, rika nam ze data jsou linearne nezavisle = nekorelovanost
pokud vyjde cca 1 - hypotezu zamitame - souhlasna linearni zavislost - v korelogramu roustouci primka
pokud vyjde cca -1 - hypotezu zamitame - nesouhlasna linearni zavislost - v korelogramu klesajici primka

# Z transformace

Testuje rovnost korelacniho koeficientu p_{X,Y} nahodnych velicin X, Y konkretni zvolene hodnote p_o \in [-, 1].

H_0 : p_XY \eq p_0
H_1 : p_XY \neq p_0

# Spearmanuv poradovy korelacni koeficient

pocita korelaci na poradovych datech

# Kendallův

kvantifikuje ordinalni asociaci, nekouka se ani na poradi ani na hodnoty, jen porovnava dvojice

Konkordantni jsou, kdyz elementy rostou stejne
diskordantni kdyz rostou naopak (hodne zhruba receno)

tedy vektory X=(11, 22, 33, 44) a Y=(333,222,111,0) budou mit pouze diskordantni pary.

pokud by Y bylo (1,2,3,4) byly by ty pary konkondartni

# Korelogram

pokud korelogram obsahuje krizek, tak je to parcialni korelace, krize znamena ze nulova hypoteza nebyla zamitnuta


# T test

t test vyzaduje normalitu a symetrii rozdeleni pravdepodobnosti

# Parovy znamenkovy test

mam n dvojic, napr. velicina sledujici stav pred a po (napr. lekarskem zakroku).

basically udelame novou "fiktivni" velicinu do ktere ulozi rozdily a pak stejny jak basic
znamenkovy test.


# Testy o stredni hodnote

Wilcoxon == Man Whitney U

(mozna ne) pro normalni rozdeleni pouzijeme t-test pro libovolne spojite rozdeleni pouzijeme Wilcoxon

jeden vyber = jednovyberovy
parova pozorovani = parovy -- pouzivame jednovyberovy test

dva nezavisle vybery = dvouvyberovy


pri parovych datech pouzivame jednovyberovy test (sign)
dvouvyberovy se pouziva pokud jsou obe skupiny nezavisle







# title: MA120-0

---
date: "2021-09-28"
url: fi/ma012/0
title: ma012 lec0
math: true
---

> A bell curve is a graph depicting the normal distribution

# p-value

A p-value is a measure of the probability that an observed difference could have occurred just
by random chance. p-values are numbers in interval (0, 1) and commonly used threshold is 0.05.
The lower the p-value, the greater the statistical significance of the observed difference.
While a small p-value helps us decide if one group differs from another, it does not tell us how
different they are.

e.g.  
two groups (A: 73, B:125) and (A: 71, B: 127) results in p-value P=0.9. This means that the
difference is too small for us to be confident about it.

---

two groups (A: 60, B:138) and (A: 84, B: 114) - (30% vs 42%) results in p-value P=0.01, thus we
can say that these groups differs.

However it might be just an coincidence, if we get a small p-value when there is no difference,
it's called a **False Positive**

---

If we need to be really sure the results are correct, we use smaller threshold. e.g. using a
threshold 0.00001 means that we would get a False Positive only once every 100 000 experiments.


# Central Limit Theorem

The central limit theorem (CLT) states that the distribution of sample means approximates a normal distribution as the sample size gets larger, regardless of the population's distribution.

# Population Distribution

The population is the whole set of values, we are interested in.

# Sample Distribution

The sample is a subset of the population, and the set of values you actually use in your
estimation.

# Sampling Distribution

Researchers often use a sample to draw inferences about the population that sample is from. To
do that, they make use of a probability distribution that is very important in the world of
statistics: the sampling distribution.

# Descriptive statistics
- summarizes sample data via summarization techniques and indexes
- frequency tables, moments (mean, variance, skewness, kurtoisis) and quantiles (median, quartiles, interquartiles spans), contingency tables, correlation coefficients

# Frequency distribution i.e. frequency list/table
is a list, table or graph that display the frequency of various outcomes in a sample

# Exploratory Data Analysis (EDA)
- analysis of sample data, usually via visualization methods
- frequency plots, boxplots, histograms, scatter plots, PCA

# Statistical Inference
- derives probability properties (arguments, distribution) of population based on analysis of sample data
- requires a model - establishing a assumptions about population and data sample
- point and interval parameter estimates (confidence intervals), testing statistics hypothesis, predictions, classifications, clustering

# Parametric/Nonparametric

Parametric statistics are based on assumptions about the distribution of population from which the sample was taken. Nonparametric statistics are not based on assumptions, that is, the data can be
collected from a sample that does not follow a specific distribution.

# Parametric methods
- model establish probability distribution or some set, parameters are being examined via these probability distributions
- most of classic methods like t-test, linear regression model, Multivariate regression

# Nonparametric methods
or distribution-free statistical methods do not depend on having a normal distribution and can be used with skewed data or with categorical data (Spearman's rho, Mann-Whitney, Wilcoxon Test)

# Semiparametric methods
- combination of parametric and nonparametric mothods
- Cox model of proportional risks in survival analysis

# Nominal data (categorical)
distinguishes different categories for qualitative variables; 
dummy code: gender, ethnic background
R: factor

# Ordinal data
data exists in categories that are ordered but differences cannot be determined or they are meaningless. (Example: 1st, 2nd, 3rd)
R: ordered factor

# Interval data
Differences between values can be found, but there is no absolute 0. (Temp. and Time),
R: numeric

# Ratio Data
data with an absolute 0. Ratios are meaningful. (Length, Width, Weight, Distance)

# Null Hypothesis (H0)
a statement that the performance of treatment groups is so similar that the groups must belong to the same population; a way of saying that the experimental manipulation had no important effect

- all level factors have same mean values

# Alternative hypothesis (H1)
The hypothesis that states there is a difference between two or more sets of data.

- at least one pair of level factors differ in mean value

# significance level (alpha)
The acceptable level of error selected by the researcher, usually set at 0.05;
what we compare our p-value to

# Power of a test
- The probability of correctly detecting a false null hypothesis
- could be increased by increasing sample data size

# classical statistical hypothesis testing; according to critical field
- establish H0 and H1
- establish model - i.e. statistics assumptions
- choose test and testing statistics T with known probability distribution (under the validity of H0)
- choose significance level (α) - usually 0.05
- compute observed values *t* of testing statistics *T*
- establish critical region *W* according to *H1* and *t*
- H0 is rejected, if $$t \in W$$

# statistical hypothesis testing; via p-value
- compute p-value *p*
- H0 is rejected, if $$p \lt \alpha$$

# p-value
The probability level which forms basis for deciding if results are statistically significant (not due to chance).

# t-test
a statistical test used to evaluate the size and significance of the difference between two means

# multiple testing
the more statistical tests we do, the more likely we are to make an erroneous inference (unless we adjust our significance threshold).

# ANOVA (analysis of variance)
-differences among MEANS of continuous (numerical) variables
-more flexible than t-tests-->can analyze differences among MORE THAN 2 groups (even if diff sample sizes)

# multiple comparison tests
statistical tests used to make pairwise comparisons to find which means differ significantly from one another in a one-factor multilevel design

- Tukey or Scheffe method

# Tukey's method
it's preferred especially in case that all partial random selections have approximately same range

# Scheffe method
it's recommended especially in case that partial random selections have distinctly different ranges.

# The means / minimalni (nulovy) model
$$Y_{i,j} = \mu + \epsilon_{i,j}$$

- \mu (micro, u) - grand mean of Y, same for all levels of factor A
- eps - stochaistic independent random variables with probability distribution N(0, \o^2)

# The effect model / jednoducheho trideni
$$Y_{i,j} = \mu + \alpha + \epsilon_{i,j}$$

- alpha - effect of i-th level of factor A

# Grand mean / spolecna stredni hodnota
$$M: \mu^{\wedge} = Y^{\wedge}$$


# effect i-th category in model M
$$\alpha_{i}^{\wedge} = \overline{Y}_{i.} \overline{Y}_{..}$$

# mean value of i-th category in model M
$$\mu_{i}^{\wedge} = \mu^{\wedge} + \alpha^{\wedge}_{i} = \overline{Y}_{i.}$$

# common part of mean value in submodel M_0
$$\mu^{\wedge} = \overline{Y}$$

# Square sums describing variability
- Total sum of squares , SS / celkovy soucet ctvercu
- Between-groups SS / skupinovy soucet ctvercu
- Within-groups/error/residual SS / rezidualni soucet ctvercu

# Parameters estimates in models
- Gran mean / spolecna stredni hodnota
- effect i-th category in model M
- mean value of i-th category in model M
- common part of mean value in submodel M_0
# title: MA120-1

---
date: 2021-10-02
url: fi/ma012/1
title: "ma012 1"
---

- z method
- f distribution
- t test
- F test 


- Mnohonasobne porovnavani
- Tukeyho
- Scheffeho metoda
- Bartlettuv test
- Kruskal-Wallisuv Test
- Jednovyberovy Wilconxonuv test (signed rank test)
Dvouv ́ybˇerov ́y Wilcoxon ̊uv test (rank-sum test)



---

dvojne trideni 
hypotezy ve dvojnem trideni

linearni modely
Znam ́enkov ́y test (sign test)
Parovy znamenkovy test
ANOVA
Postup testovani ve dvojnem trideni
Dvojne trideni s interakcemi

Testovani v modelu s interakcemi
Interpretace indexu determinace R-squared

Index determinace

# Empirical distribution function

{{<image src="/images/edf.png" position="center" alt="edf">}}

# Error vs Residual

> Error (or disturbance) is theis the deviation of the observed value from the (unobservable) true value of quantity of interest

> Residual is the difference between the observed value and the estimated value of the quantity of interest

Residual = observed value - predicted value: \\(e = y - \hat{y}\\)

The distinction is most important in regression analysis, where the concepts are sometimes called the **regression errors** and **regression residuals** and were they lead to the concept of studentized
residuals.


# Degrees of freedom

> Degrees of freedom is the number of values in the final calculation of a statistic that are free to vary


# Z-test

> A z-test is a statistical test used to determine whether two population means are different when the variances are known and the sample size is large1.

The test statistic is assumed to have a normal distribution, and nuisance parameters such as standard deviation should be known in order for an accurate z-test to be performed.

- is a hypothesis test in which the z-statistic follows a normal distribution
- A **z-statistic**, or **z-score**, is a number representing the result from the z-test
- are closely related to t-tests, but t-tests are best performed when an experiment has a small sample size. 
- assume the standard deviation is known, while t-tests assume it is unknown.


# t-distribution

*or Student's t-distribution*

> is any continuous probability distribution that arise when astimating the mean of a **normally distributed** population in situations where the sample size is small and the population's standard
> deviation is unknown.

# t-test

*or student's t-test*
> is any statistical hypothesis test in which the test statistic follows a Student's t-dristribution under the null hypothesis.

Used to determine wheter the means of two groups are equal to each other. The assumption for the test is that both groups are sampled from normal distributions with equal variances. The null hypothesis
is that the two means are equal, and the alternative is that they are not. It is known that under the null hypothesis, we can calculate a t-statistic that will follow a t-distribution with \\( n1 + n2 -
2 \\) degrees of freedom.

There is also a widely used modification of the t-test, known as **Welch's t-test** that adjusts the number of degrees of freedom when the variances are thought not to be equal to each other.


```python
x = rnorm(10)
y = rnorm(10)
t.test(x, y)

"""
 Welch Two Sample t-test
 
 data:  x and y
 t = -1.6264, df = 16.666, p-value = 0.1226
 alternative hypothesis: true difference in means is not equal to 0
 95 percent confidence interval:
  -1.4494854  0.1886137
 sample estimates:
   mean of x   mean of y 
 0.007872345 0.638308171
"""
```


# F-distribution

*or F-ratio also known as Snedecor's F distribution or the Fisher–Snedecor distribution*

> is a continuous probability distribution that arises frequently as the null distribution of a test statistic, most notably in the ANOVA and other F-tests.

The F-distribution with \\(d_1\\) and \\(d_2\\) degrees of freedom is the distribution of:

$$X = \frac{S_1/d_1}{S_2/d_2}$$

where \\(S_1\\) and \\(S_2\\) are independent random variables with chi-square distributions respective degrees of freedom \\(d_1\\) and \\(d_2\\)

# F-test

> is any statistical test in which the test statistic has an F-distribution under the null hypothesis.

It is most often used when comparing statistical models that have been fitted to a data set, in order to identify the model that best fits the population from which the data were sampled. Exact "F-tests"
mainly arise when the models have been fitted to the data using least squares.

The test statistic can be obtained by computing the ration of the two variances \\( S_A^2 \\) and \\( S_B^2 \\)

$$F = \frac{S_A^2}{S_B^2}$$

The degrees of freedom are \\( n_A - a \\) (for the numerator) and \\( n_B -1 \\) (for the denominator)


# Chi-square distribution

*also chi-square or \\( \chi^2 \\)-distribution*

> with k degrees of freedom is the distribution of a sum of the squares of k independent standard normal random variables. 

if \\(Z_1, ..., Z_k \\) are independent, standard normal random variables, then sum of their squares:

$$Q=\sum^k_{i=1} Z_i^2$$

is distributed according to the chi-squared distribution with k degrees of freedom. This is usually denoted as:

$$Q \sim \chi^2 (k) \text{ or } Q \sim \chi^2_k $$

The chi-squared distribution has one parameter: a positive integer k that specifies the number of degrees of freedom (the number of random variables being summed, Zi s)



# Multiple Comparisons Problem

*or multiple comparisons, multiplicity or multiple testing problem*

> occurs when one considers a set of statistical inferences simultaneously or inders a subset of parameters selected based on the observed values.


## Tukey's Range Test

*or Tukey's test, Tukey method ...*

> is a single-step multiple comparsion procedure and statistical test. It can be used to find means that are significantly different from each other.

Tukey's test is based on a formula very similar to that of the t-test. In fact, Tukey's test is essentially a t-test, except that it corrects for family-wise error rate.

The formula for Tukey's test is:

$$q_s = \frac{Y_A - Y_B}{SE}$$

where Y_A is the larger of the two means being compared, Y_B is the smaller, and SE is the standard error of the sum of the means.


## Scheffé's method

> is a method for adjusting significance levels in a linear regression analysis to account for multiple comparsions.

It is particularly useful in ANOVA and in constructing simultaneous confidence bands for regressions involving basis functions.

# Bartlett's test

> is used to test homoscedasticity, that is, if multiple samples are from populations with equal variances.

Some statistical tests, such as the ANOVA assume that variances are equal across groups or samples, which can be verified with Bartlett's test.
If the corresponding p-value of the test statistic is less than some significance level (like α = .05) then we can reject the null hypothesis and conclude that not all groups have the same variance.

Sample output in R:  
```
	Bartlett test of homogeneity of variances

data:  clotting by diet
Bartlett's K-squared = 1.668, df = 3, p-value = 0.6441
```

If we assume significance level 0.05, we can reject null hypothesis (that clotting depends on diet).


# Levene's test

> is an inferential statistic used to asses the equality of variances for a variable calculated for two or more groups.


Levene's test is alternative to Bartlett but is often less sensitive. Rejecting hypothesis same as Bartlett's.

```
Levene's Test for Homogeneity of Variance (center = median)
      Df F value Pr(>F)
group  3  1.0109 0.4086
      20       
```


# ANOVA

We must met three assumptions: normality, equal variances, independence.

If p-value is smaller than significance level we reject the null hypothesis that the variances are equal across all groups.

## Normality

ANOVA assumes that each sample was drawn from a normally distributed population.

- Check the assumption visually using histograms or Q-Q plots.
- Check the assumption using formal statistical tests like Shapiro-Wilk, Kolmogorov-Smironov, Jarque-Barre, or D’Agostino-Pearson.


## Equal Variance

ANOVA assumes that the variances of the populations that the samples come from are equal.

- Check the assumption visually using boxplots.
- Check the assumption using a formal statistical tests like Bartlett’s or Levene's Test.

## Independence

The observations in each group are independent of the observations in every other group. The observations within each group were obtained by a random sample.



# Sign Test

> is a statistical method to test for consistent differences between pairs of observations

# Wilcoxon signed-rank test

*Jednovýběrový Wilcoxonův párový test*

> is a non-parametric statistical hypothesis test used either to test the location of a set of samples or to compare the locations of two populations using a set of matched samples.


# Mann–Whitney U test

*Dvouvýběrový Wilcoxonův párový test or Wilcoxon rank-sum test*

> is a non-parametric test of the null hypothesis that, for randomly selected values X and Y from two populations, the probability of X being greater than Y is equal to the probability of Y being greater
> than X.


# Van der Waerden test

is a statistical test that k population distribution functions are equal. Van der Waerden test converts the ranks from a standard Kruskal-Wallis one-way analysis of variance to quantiles of the standard
normal distribution.


# Kruskal–Wallis test

*or Kruskal–Wallis one-way analysis of variance or one-way ANOVA on ranks*

> is a non-parametric method for testing whether samples originate from the same distribution.
> 
> The parametric equivalent of the Kruskal–Wallis test is the ANOVA

It used for comparing two or more independent samples of equal or different sample sizes. It exteds the *Mann-Whitney U test*, which is used for comparing only two groups.



# Normality tests

normality tests are used to determine if a data set is well-modeled by a normal distribution and to compute how likely it is for a random variable underlying the data set to be normally distributed. 

## Kolmogorov–Smirnov test

*or KS test*

> is a nonparametric test of the equality of continuous, one dimensional probability distributions

It can be used to compare a sample with a reference probability distribution (one-sample KS) or to comapre two-samples (two-sample KS).

```R
ks.test(X, "pnorm", mean=..., sd=...)
```

## Pearson's chi-squared test
Test dobré shody

*\\(\chi^2\\)* test

> is a statistical test applied to sets of categorical data to evaluate how likely it is that any observed difference between the sets arose by chance. It is the most widely used of many chi-squared
> tests (Yates, likelihood ratio, portmanteau test in time series, etc.)

```R
chisq.test(X, p=...)
```


## Lilliefors test

> is a normality test based on the Kolmogorov–Smirnov test. It is used to test the null hypothesis that data come from a normally distributed population, when the null hypothesis does not specify which
> normal distribution; i.e., it does not specify the expected value and variance of the distribution.

```R
lillie.test(X)
```

## Other Normality Tests in R

```R
# Anderson–Darling test
ad.test(X)

# Cramér–von Mises test
cvm.test(X)

# Shapiro–Wilk test
shapirotest(X)

# D'Agostino's K-squared test
agostino.test(X)

# Jarque–Bera test
jarque.test(X)

# Q-Q plot
qqnorm(X)
# or
qqline(X)
```







# title: MA120-2

---
date: 2021-10-02
url: fi/ma012/2
title: "ma012 2"
---

# Test (ne)korelovanosti

Pearsonuv vyberovy korelacni koeficient \\( \rho_{XY} \\) je odhadem teoreticke korelace \\( rho_{XY} \\) mezi nahodnymi velicinami X a Y.

Test (ne)korelovanosti je vlastne testem vyznamnosti korelace \rho_(XY)

$$
H_0: \rho_{XY} \eq 0 
H_1: \rho_{XY} \neq 0 
$$

H_0 nezamitneme \\( r_{XY} \approx 0 \\): nekorelovanost = lineární nezávistlost X, Y. Pozor nekorelovanost neimplikuje stochastickou nezávistlost.
H_0 zamitneme \\( r_{XY} \approx 1 \\): souhlasná lineární závislost X, Y
H_0 zamitneme \\( r_{XY} \approx -1 \\):nesouhlasná lineární závislost X, Y



# Spearmanuv korelační koeficient

Neparametrická analogie Personova. 


# Test pořadové nekorelovanosti

test významnosti r_s, lze provádět pomocí některé z testovacích statistik jako Spearmanuv korel koef..


# Kendallův korelační koeficient - Kendallovao \tau

\tau kvantifikuje ordinální asociaci mezi velicinami X, Y. Na rozdíl or r-s totiz \tau neuvazuje vzdálenost pořadí.

## Konkordantní páry

pokud jsou jejich pořadí souhlasná, tzn. \\( X_i \leq X_j & Y_i \leq Y_j \\) anebo \\( X_i \geq X_j & Y_i \geq Y_j \\) 

## Diskordantní páry

pokud jsou jejich pořadí nesouhlasná, tzn. \\( X_i \leq X_j & Y_i \geq Y_j \\) anebo \\( X_i \geq X_j & Y_i \leq Y_j \\) 









# title: MA120-ex

---
url: fi/ma012/ex
title: Examples
---

# Ex 1

On significance level 0.05, test null hypothesis that mean values for X are same for all groups Y.

Steps:
```
Bartlett and Levene -> ANOVA -> Tukey and Scheffe
```

# Ex 2

Let's have two random vectors X = (2, 4, 6, 8) a Y = (1, 3, 5, 7).

Compute Kendall \\( \tau \\) and number of concordant pairs:
```
res<-cor.test(X, Y, method="kendall")
res
```

The result will be:
```
	Kendall's rank correlation tau

data:  Y and X
T = 6, p-value = 0.08333
alternative hypothesis: true tau is not equal to 0
sample estimates:
tau 
  1
```

From output we can see there are 6 concordant pairs an kendall \\(tau\\) is 1.




