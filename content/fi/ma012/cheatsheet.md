---
url: fi/ma012/cs
title: cheatsheet
date: 2021-11-01
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


# Test dobre shody

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


Post hoc testy vyrovnavaji rust chyby: Tukey's a Scheffe's - jsou schopny najit rozdily mezi jednotlivymi kategoriemi

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

Je pro katergorie. ze kterych ale muzeme udelat spojitou fci. takze je univerzalni na vse.

# ECDF

empiricka distrib fce. prochazime x osu a ptame se kolik sledovanych dat je pod nimi.

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

Testuje rovnost korelacniho koeficientu p_{X,Y} nahodnych velicin X, Y konkretni zvolene hodnote p_o \in [0, 1].

H_0 : p_XY \eq p_0
H_1 : p_XY \neq p_0

# Spearmanuv poradovy korelacni koeficient

pocita korelaci na poradovych datech

# Kendallův test

kvantifikuje ordinalni asociaci, nekouka se ani na poradi ani na hodnoty, jen porovnava dvojice

Konkordantni jsou, kdyz elementy rostou stejne
diskordantni kdyz rostou naopak

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







