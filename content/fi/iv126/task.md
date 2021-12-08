---
url: fi/iv126/task
---

fyzicke stroje p \in P
virtualni stroje v \in C

R(v, r) udava, kolik zdroje r vyuziva virtualni stroj v
C(p, r) udava jakou kapacitu zdroje r je mozne na fyzickem stroji p naaalokavat
SC(p, r) bezpecna kapacita zdroje r na fyzickem stroji p

plati: `SC(p, r) < C(p, r)`

MC(v) cena za migraci virtualniho stroje v
PMC(p, p') cena za migraci libovolneho virtualniho stroje z fyzickeho stroje p na fyzicky stroj p'.
PMC(p, p) = 0

Reseni je konzistentni, pokud neni pro fyzicky stroj p na zadnem zdroji r prekrocena jeho kapacita C(p, r)

3 optimalizacni kriteria, cilem je minimalizovat jejich vazeny soucet.
Vahove konstanty zarucuji vhodnou normalizaci.

Minimalizujeme:
- cenu za zatizeni - mnozstvi prekrocene bezpecne kapacity SC(p, r)
- cenu za migraci - MC(v) vsech migrovany virt. stroju a PMC(p, p') pro kazdy virt stroj z p do p'.
- cenu za energii - ktera je urcena poctem aktivnich fyzickych stroju



kodovani - zapis
operatory - zapis/vyznam


# Notes

accepting threshod is typically negative exp


The algorithm will then assign a weight
to each heuristic which reflects its success. In the absence of other possibilities,
we assume the past success as the best indicator for future success. During the
runtime, these weights are adjusted periodically


destroy + repair operators


Distance-oriented Removal
Worst Removal
Cluster Removal
random removal and put back using heuristic (first fit)

swap 2 is still local search.

take 1 evaluate best pm for it and put it there. 

Penalties for time-intensive Heuristics


In order to avoid precision
problems with floating point numbers close to zero, we set the initial weights to
1000. The choice of the length of the update period has already been discussed
in Section 5.2. It is set to 100 in all experiments.


## Encoding

1)

a)

S = [1, 2, 2, 3, 1, 2]

vektor S reprezentuje na index i vir. stroj prirazen k phy stroj S_i.

b)

binarni matice S s velikosti a x b, kde a je pocet pm a b je pocet vm,
Pozice S_xy reprezentuje jestli je V_x prirazeno P_y

  v v v
[ 1 0 0
  0 1 0
  1 0 0]



$$\displaylines{R(v, r) \\\ C(p, r) \\\ SC(p, r) \\\ MC(v) \\\ PMC(p, p')}$$

2)

chci co nejmensi pocet bezicich pm,
chci co nejmensi overflow SCs
chci minimalizovat pocet presouvani (jak moc je nove reseni odlisne od pocatecniho)
+
normalizace



---

$$CL = \sum_{i=0}^{rn} R_{i} - P_{R_i}$$

, kde rn je pocet zdroji


$$
FS = \sum 
$$

\sum_i^Pn

for vm, pm in S:
  P[pm] 

for pm in P:
 sum()




3)












# Charakteristika

TSP - jednou charakteristikou bude jedna hrana, cena hrany je cena charakteristiky

pokud je hrana v reseni I vraci 1 jinak 0

tzn. pokud to aktualni reseni ma tu charakteristiku (hranu), pak vracim 1 ...

cilem je prohledavat cast grafu ktere maji nizsi cenu charakteristik.


# ucelova fce - zapis

u TSP napr. f(s) = \sum^n_{i=1} d_{i, t(i)} , kde d je vzdalenost mezi aktualnim a dalsim mestem.

# inkrementalne ucelova fce

klasika u TSP, prohazujeme 2 mesta, ale nechceme prepocitavat uplne celou trasu a tak prepocita pouze delta mezi dvema mestama co jsme prohodili.


# vahy









