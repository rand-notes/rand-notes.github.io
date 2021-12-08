---
title: overview 2
---

# 2 cviko

Na hladine vyznamnosti testujte nulovou hypotezu, ze stredni hodnoty trzeb vsechno proddavacu
se rovnaji.
Spocitejte ze hmotnost brambor nesouvisi s odrudou.

reseni: 
**Levene a Bartletts** test pro overeni ze variance(rozptyl) je podobna mezi skupinami 
**Shapiruv-Wilkeuv a Kolmogorovuv-Smirnovuv** test pro overeni normality
**ANOVA** pro testovani stredni hodnoty
**Tukey a Scheffe** pro porovnani ktere dvojice se nejvic lisi

R:

leveneTest(tabulka$hmotnost ~ tabulka$odruda) # odruda musi byt factor
bartlett.test(tabulka$hmotnost ~ tabulka$odruda)

Shapiro–Wilk:
```R
# nejdriv si rozdelime do nekolika tabulek podle odrud
skupiny <- lapply(levels(tabulka$odruda), function(L) {
  return(subset(tabulka, odruda == L))
})

# a pak aplikujeme Shapiro nebo Kolmogorov–Smirnov
skupiny <- lapply(levels(tabulka$odruda), function(L) {
  return(subset(tabulka, odruda == L))
})

lapply(skupiny, function(x) {
  X <- x$hmotnost
  ks.test(X, "pnorm", mean = mean(X), sd = sd(X))
})

alternativne to muzem projet po jednom

shapiro.test(tabulka[tabulka$odruda == 1, ]$hmotnost)
shapiro.test(tabulka[tabulka$odruda == 2, ]$hmotnost)
```

ANOVA:

```R
aov.model <- aov(tabulka$hmotnost ~ tabulka$odruda)
aov.model
```

Tukey a Scheffe:

```R
ScheffeTest <- scheffe.test(aov.model, "tabulka$odruda")
ScheffeTest
ScheffeTest$groups


TukeyTest <- TukeyHSD(aov.model)
TukeyTest
plot(TukeyTest, las = 1) # graficky 
```


Linearni regresni model:

```R
model3 <- lm(Y ~ 1 + x + I(x^2) + I(x^3), data = tabulka)
model2 <- lm(Y ~ 1 + x + I(x^2), data = tabulka)
model1 <- lm(Y ~ 1 + x, data = tabulka)
summary(model3)
summary(model2)
summary(model1)
```



# 3 cviko

Zkoumame vynosy sena v zavislosti na typu pudy a hnojeni. Kazda kombinace byla realizovana
ctyrikrat, nezavisle na sobe. Provdte analyzu rozptylu pomoci dvojneho trideni bez interakci,
dvojneho trideni s interakcemi i pomoci jednoducheho trideni.

Reseni:

Opet Bartlett a Levene pro varianci a Shapiro a KS pro normalitu.

```R
# dvojne trideni bez interakci

aov.model <- aov (vynos ~ puda + hnojeni, data = tabulka)
summary (aov.model)
aov.model$coefficients

# Mnohonasobne porovnavani

TukeyTest <- TukeyHSD (aov.model)
TukeyTest

ScheffeTest.puda <- scheffe.test (aov.model, "puda")
ScheffeTest.puda$groups
ScheffeTest.hnojeni <- scheffe.test (aov.model, "hnojeni")
ScheffeTest.hnojeni$groups


# Dvojne trideni s interakcemi
aov.model <- aov (vynos ~ puda * hnojeni, data = tabulka)
aov.model
```


# 4 cviko

Testuje hypotezu, ze polovina testovanych osob doby jedne minuty podhodnotila a polovina
nadhodnotila.

```R
# znamenkovy test
SIGN.test(X, md = 60) # p-hodnota > 0.05 => nezamitame nulovou hypotezu 

# Wilcoxonuv signed-rank test / jednovyberovy wilcoxon
wilcox.test(X, mu = 60)

# dvouvyberovy wilcoxonuv test
wilcox.test (X, Y)
```

Brambory - pomoci Kruskal-Wallis a median testu pro jednoduche trideni testujte H, ze stredni
hodnota hmotnosti trsu brambor nezavisi na odrude. Naleznete odlisne dvojice.

```R
# Jednoduche trideni: Kruskaluv-Wallisuv test
# p-hodnota < 0.05 => zamitame nulovou hypotezu o rovnosti vsech medianu 
KWtest <- kruskal(tabulka$hmotnost, tabulka$odruda)


# Jednoduche trideni: Medianovy test
Mtest <- Median.test(tabulka$hmotnost, tabulka$odruda)
```

# 5 cviko

Byl vybran pocet chlapcu v rodinach. Testujte ze pocet chlapcu v rodinach ma binomicke
rozdeleni Bi(5; 0.5);

```R
tabulka <- read.csv2(file = "data/rodiny.csv")

pc = tabulka$pocet_chlapcu #diskretni kategorie
k <- length (pc)

pr <- tabulka$pocet_rodin #Z nahodneho vyberu mame empiricke cetnosti
n <- sum (pr)

bin <- dbinom (pc, size = 5, prob = 0.5)

Matice <- rbind (pr, n * bin) # umistime empiricke i teoreticke cetnosti do jedne matice jako dva radky
Matice


#	Yarnoldovo kriterium 
q <- sum (n * bin < 5) / k
n * bin >= 5 * q # output: TRUE TRUE TRUE TRUE TRUE TRUE
# Yarnoldovo kriterium  je splneno


#	Testovaci statistika
K <- sum (pr^2 / (n * bin)) - n
K >= qchisq (0.95, df = k - 1) #output: FALSE
#	Hypotezu o shode dat s rozdelenim Bi (5; 0.5) nezamitame


#	Podminka dobre aproximace 
n * bin >= 5 
#	Prvni a posledni kategorie maji nizke teoreticke cestnosti, Sloucime tedy prvni 2 a posledni 2 kategorie

#Slouceni kategorii
pc2 <- c ("0-1", pc[3:4], "4-5")
k2 <- length (pc)
pr2 <- c (sum (pr[1:2]), pr[3], pr[4], sum (pr[5:6]))
bin2 <- c (sum (bin[1:2]), bin[3], bin[4], sum (bin[5:6]))

# to stejny - ale ted uz je podmnika splnena

Matice <- rbind (pr2, n * bin2)
Matice

n * bin2 >= 5

K <- sum (pr2^2 / (n * bin2)) - n
K >= qchisq (0.95, df = k2 - 1) #output: FALSE
#	Hypotezu o shode dat s rozdelenim Bi (5; 0.5) nezamitame
```


Sledovana doba cekani na obsluhu. Testujte zda ma exponencialni rozdeleni pst. a to testem
dobre shody a testem pro exponencialni rozdeleni.

```R
tabulka <- read.csv2(file = "data/fronta.csv")
str(tabulka)
summary(tabulka)

tabulka

# kategorie
dcc <- as.character (tabulka$doba_cekani) # doba cekani char
k <- length (dcc)
dc <- seq (0, 24, by = 3) # doba cekani


#	Z nahodneho vyberu mame empiricke cetnosti
pz <- tabulka$pocet_zakazniku
n <- sum (pz)

# Odhad parametru lambda v exponencialnim rozdeleni 
prumer <- seq (1.5, 22.5, by = 3) # stredy v intervalech
lambda <- 1 / (sum (prumer * pz) / n)

# Dopocitame teoreticke pravdepodobnosti z predpokladu exponencialniho rozdeleni s lambda 
dck <- pexp (dc, lambda) # distribucni funkce v krajnich bodech
pst <- diff (dck) # pravdepodobnost = rozdil hodnot distribucni funkce

# Soucet pravdepodobnosti ale neni 1, nebot chybi kategorie "> 24"
dcc <- c (dcc, "> 24")
k <- length (dcc)
pz <- c (pz, 0)
pst <- c (pst, 1 - pexp (24, lambda))
#	kontrola: soucet psti = 1
sum (pst)	

#	Sloupcove grafy empirickych a teoretickych cetnosti
Matice <- rbind (pz, n * pst)	#	umistime empiricke i teoreticke cetnosti do jedne matice jako dva radky
barplot (Matice, names.arg = dcc, beside = TRUE, main = "doba cekani", ylab = "pocet zakazniku", col = c("orange", "cyan"), las = 2)

#	Podminka dobre aproximace 
n * pst >= 5 
# Yarnoldovo kriterium
q <- sum (n * pst < 5) / k
q
n * pst >= 5 * q

# Podle podminky dobre aproximace bychom spojili posledni dve dvojice kategorii.
# Podle Yarnoldova kriteria bude stacit spojit posledni 2 kategorie do nove "> 21".
# Nam postaci splneni Yarnoldova kriteria. 
dcc2 <- dcc[1:(k-1)]
k2 <- length (dcc2)
dcc2[k2] <- "> 21"
pz2 <- c (pz[1:(k2-1)], pz[k2] + pz[k])
pst2 <- c (pst[1:(k2-1)], pst[k2] + pst[k])
sum (pz2)
sum (pst2)

Matice <- rbind (pz2, n * pst2)	#	umistime empiricke i teoreticke cetnosti do jedne matice jako dva radky
barplot (Matice, names.arg = dcc2, beside = TRUE, main = "doba cekani", ylab = "pocet zakazniku", col = c("orange", "cyan"), las = 2)

# Yarnoldovo kriterium
q <- sum (n * pst2 < 5) / k2
q
n * pst2 >= 5 * q
#	Yarnoldovo kriterium je nyni jiz splneno

#	Testovaci statistika
K <- sum (pz2^2 / (n * pst2)) - n
#	Kvantil a porovnani 
K
# Stupne volnosti snizujeme navic o 1 za odhadnuty parametr lambda 
qchisq (0.95, df = k2 - 1 - 1)
K >= qchisq (0.95, df = k2 - 1 - 1)
#	Hypotezu o shode dat s exponencialnim rozdelenim testem dobre shody nezamitame


# Specificky test
pz <- tabulka$pocet_zakazniku
X <- rep (prumer, pz)
Q <- (n-1) * var (X) / (mean (X))^2 
Q
q1 = qchisq (0.025, n-1)
q2 = qchisq (0.975, n-1)
c (q1, q2)
Q <= q1 | Q >= q2
#	Hypotezu o shode dat s exponencialnim rozdelenim Specifickym testem zamitame
```


# 6 cviko

Byli sledovan pocet clenu (C), prijmy (P) a vydaje (V) za potraviny a napoje. Dale spocitejte koeficient mnohonasobne korelace mezi vydaji a zbylymi 2 velicinami.

Korelace meri silu zavislosti, kovariance meri smer.

Spearmanův korelační koeficient udává statistickou závislost (korelaci) mezi dvěma veličinami.
Kendallovo tau - measure the ordinal association between two measured quantities

```R
library("Hmisc")			#	rcorr
library("corrplot")		#	corrplot
library("ppcor")			#	pcor, pcor.test
library("rgl")		# 3D grafika 


#	Nacteni dat
tabulka <- read.csv2("data/domacnosti.csv", header = TRUE, skip = 5)

C <- tabulka$C
P <- tabulka$P
V <- tabulka$V
X <- as.matrix(tabulka) # C, P, V jako sloupce

#	Ciselne charakterisitky 
apply(X, 2, mean)
cov(X)
cor(X)

#	Scatter-plot
pairs(X)

#	MNOHONASOBNA LINEARNI REGRESE

#	Linearni regresni model
model <- lm(V ~ P + C, data = tabulka)
#	Koeficienty mnohonasobne linearni regrese
summary(model)

#	Predikce vynosu (V) v zavislosti na poctu clenu domacnosti (C) a prijmech (P)
c <- seq(1, 5, by = 0.1) # 1 a 5 je min a max v C
p <- seq(0, 150, by = 0.1) # 0 a 150 je min a max v P
grid.2d <- expand.grid(C = c, P = p)
prediction <- predict(model, grid.2d, interval = "prediction")
V.predicted <- matrix(prediction[,1], length (c), length (p))

#	KORELACNI ANALYZA

#	Korelacni matice a testy vyznamnosti
R <- rcorr(X)
R$r
R$P

#	Matice parcialnich korelaci a testy vyznamnosti
parc <- pcor(X)
parc$estimate
parc$p.value

#	MNOHONASOBNA KORELACE
#	V . C P

# 1. jako korelace s nejlepsim linearnim odhadem
m <- lm(V ~ C + P, data = tabulka)
v <- summary(m)
cor(V, m$fitted.values)

# 2. jako r.squared v linearnim regresnim modelu
sqrt(v$r.squared)
```

# 7 cviko

Durbin-Watson - test statistic used to detect the presence of autocorrelation at lag 1 in the residuals (prediction errors).
Cochran-Orcutt - obdobné procedury pro korekci autokorelace


Pomoci lienarni modelu s AR(1) modelujte zavislost druhe odmocniny poctu ptactva na case (v rocich). Overte, zda se v datech vyskytuje autoregrese 1. radu a prip ji odstrante.

```R
tabulka <- read.csv (file = "data/Hawaii.csv")
str(tabulka)
tabulka$Y <- sqrt(tabulka$Birds)
Year.min <- min(tabulka$Year)
tabulka$t <- tabulka$Year - Year.min 

# plot(tabulka$Year, tabulka$Y, type = "p", pch = 21, col = "black", bg = "yellow", xlab = "Year (= t + 1956)", ylab = "sqrt (Birds)", main = "OLS")

model <- lm(Y ~ t, data = tabulka) # Y pocet ptactva, t je pocet roku od zacatku mereni (roky)
summary(model, correlation = TRUE)
confint(model) # Computes confidence intervals for one or more parameters in a fitted model.
tt <- seq(min (tabulka$t), max (tabulka$t), by = 0.1)
Yhat <- predict(model, data.frame (t = tt))

# rezidua
r <- model$residuals
n <- length(r)

# korelace mezi rezidui s o 1 posunutymi indexy
r1 <- r[-n]
r2 <- r[-1]


# odhad theta
theta <- cor(r1, r2)
theta
#
theta1 <- as.numeric( (t(r1) %*% r2) / (t(r1) %*% r1))
theta1
# asymptoticky test
alpha <- 0.05
U <- abs(sqrt(n) * theta1)
c(U = U, kvantil = qnorm (1 - alpha/2)) 
U > qnorm (1 - alpha/2)  
# Zamitame hypotezu H: theta = 0

# Durbinova-Watsonova statistika
DW <- dwtest(Y ~ t, data = tabulka)
D <- DW$statistic
D
# Dtest
DW$p.value 
# Take zamitame hypotezu H: theta = 0
# odhad theta z D-W statistiky
theta2 <- 1 - unname(D) / 2
theta2
```


# 9 cviko

```R
# definice GLM modelu
m1 <- glm(formula = cbind(killed, population - killed) ~ dose, family = binomial(link = "logit"), data = tab) # killed, population, dose - vsechno array - casova osa
m2 <- glm(formula = cbind(killed, population - killed) ~ dose, family = binomial(link = "probit"), data = tab)
summary(m1)

# linearni prediktor
eta1 <- predict(m1, data.frame(dose = t), type = "link")

# linearni preditkor s 95% pasem spolehlivosti
fit1 <- predict(m1, data.frame(dose = t), type = "link", se.fit = TRUE)

```









