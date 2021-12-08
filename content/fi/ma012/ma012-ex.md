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




