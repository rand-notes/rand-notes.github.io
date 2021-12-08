
```
# PCA 
# cor=TRUE => pracuje s korelacni matici misto kovariancni, tj. standardizuje vsechny veliciny
# scores=TRUE => spocita i koeficienty pozorovani v hlavnich komponentach
pca <- princomp(X, cor = TRUE, scores = TRUE)
```

```
pca$scores
```



Variance inflation factor (VIF) is a measure of the amount of multicollinearity in a set of multiple regression variables

```
vif(model)             # VIF = variance inflation factors
```

```
model <- lm(vydaje ~ ., data = domacnosti) # klasicky LRM
```

```
# Stepwise regressiom

# backward
model.back <- step(model, direction = "backward", trace = 1)
summary(model.back)

# bidirectional
model.bidir <- step(model, direction = "both", trace = 1)
summary(model.bidir)

# forward
model0 <- update(model, . ~ 1) # minimalni (nulovy) model
model0
model.forw <- step(model0, scope = formula(model), direction = "forward", trace = 1)
summary(model.forw)
```


