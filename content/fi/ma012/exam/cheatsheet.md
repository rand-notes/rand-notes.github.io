---
title: cheatsheet1
url: exam1
---

# Anova


## Predpoklady
 - faktor A (popr. B) musi mit 3 a vic urovni
 - Normalita hodnot jednotlivých náhodných výběrů
 - Stejný rozptyl hodnot ve všech srovnávaných skupinách
 - Nezávislost pozorovaných hodnot (casto se bere automaticky)

## Hypotezy

HA0: vsechny stredni hodnoty v radcich jsou stejne tj. faktor A nema vliv
HA1: nektere dvojice strednich hodnot v radcich se lisi tj. faktor A ma vliv
HB0: vsechny stredni hodnoty v sloupcich jsou stejne tj. faktor B nema vliv
HB1: nektere dvojice strednich hodnot v sloupcich se lisi tj. faktor B ma vliv


# Neparametricke testy

testy nezavisi na tom ze data maji urcite rozdeleni


## Znamenkovy test

slouzi na testovani medianu rozdeleni pravdepodobnosti spojiteho typu nahodneho vyberu.
Používa sa najmä v prípade keď je rozdelenie pravdepodobnosti 
náhodného výberu výrazne zošikmené. Ak sú rozdiely Xi-x0 nulové, 
tak sa dané zložky vynechajú a počíta sa so znížením n.

### Hypoteza

overujeme rovnosti medianu x vuci x0

H0: x ~= x0

### Vypocet
- vypocitame rozdil X_i - x0.
- spocitame pocet kladnych rozdilu jako S+.
- pokud `S+ <= k_alpha` nebo `S+ >= n - k_alpha` zamitame H0.

pokud n >= 20, muzeme pozuit asymptotickou variantu, \( U = (2 * S+ - n)/\sqrt{n} /). Pokud |U| >= u1 - alpha / 2 tak zamitame H0.


## Jednovyberovy Wilcoxon

Slúži na testovanie mediánu u náhodného výberu s veličinami, ktoré majú aspoň ordinálny charakter, z rozdelenia  pravdepodobnosti spojitého typu s hustotou symetrickou okolo  mediánu

### Vypocet

- vypocet rozdilu X_i - x0 - oznacime jako Y_i
- vytvoreni usporadaneho vyberu absolutnich hodnot Y - oznacime si jako R_i+
- spocitame poradi R_i+ pro kladne a zaporne Y_i - oznacime jako S+ a S-
- `min{S+, S-} <= w_alpha` tak zamitame H0

s n >= 30 muzeme pouzit asymptotickou variantu test statistiku U


## Dvojvyberovy Wilcoxon test

Mejme 2 stochasticky nezavisle nahodne vyberu X a Y z rozdeleni pst s distrib fcemi F(x) a G(y)

### Hypoteza 

Overujeme ze H0: F=G

### Vypocet
- nahodne vybery sloucime do sdruzeneho nahodneho vyberu Z a prevedeme na usporadany nahodny vyber.
- spocitame soucet poradi pro prvni a druhy nahodny vyber - T1 a T2
- Pomoci nich vypocitame test statistiky U1 a U2
- pokud `min{U1, U2} <= w_alpha(m, n)` zamitame H0

pokud mame aspon 10 z obou vyberu muzeme pouzit asymptotickou stat UMW.

## Kruskal Wallis

neparametricka obdoba ANOVY.
Muze se pouzit jako zobecneny dvouvyberovy wilcoxon pro 3 a vice vyberu.

### Hypoteza

H0: testujeme ze faktor A nema vliv na rozdeleni pravdepodobnosti sledovane veliciny Y, tedy testujeme rovnost distribucnich fci.

### Vypocet

vytvorime sdruzeny nahodny vybera z nej vytvorime usporadany nahodndy vyber v kterem prumerne poradi nahovne veliciny Y_ij oznacime jako R_ij.
Pro kazdkou uroven scitame poradi velicin na dane urovni.
Spocitame testovou statistiku Q a H0 zamitneme pokud je Q >= h_alpha(a-1), kde a-1 je rovno stredni hodnote testove statistiky Q.

#### optional

Ak platí H0 tak má statistika Q asymptoticky X2-rozdelenie  pravdepodobnosti. halfa(a-1) je tabelovaná kritická hodnota testu. Pre veľké n ju aproximujeme kvantili X2(a-1) rozdelenia pravdepodobnosti.


# Test dobre shody

Test dobrej zhody overuje hypotézu o rovnosti empirického a teoretického rozdelenia pravdepodobnosti. testovaci statistika K

\( K = \sum N_j / (n * p_j) - n \)

K ma za platnosti hypotezy rozdeleni chí kvadrát pravdepodobnosti (X2). Pokud jsme museli odhadnout nektere parametry tak je pocet stupnu volnosti snizen o pocet odhadnutych paramteru.

Plati ze pokud `K >= X2 1 - \alpha(k - 1)` tak hypoteza o rovnosti rozdeleni neplati.

Jelikoz je test asymptoticky tak ho muzeme pouzit jen pri dostatecne velkem poctu dat.

Musí platiť podmienka dobrej aproximácie nebo podle Yarnoldova kriteria. Ak neplatí tak musíme upraviť kategórie – zlúčiť a opakovať.

## Test dobrej zhody pre diskrétnu náhodnú veličinu

- Stanovime kategorie A tak aby odpovidali vsem moznym vysledkum t1, ..., tk testovane diskretni nah veliciny.
- Pro jednotlive katergorie si spocitame empiricke cetnosti Nj=|{Xi=tj}| a teoretické početnosti podľa pravdepodobnostnej alebo distribučnej funkcie teoretického rozdelenia pravdepodobnosti pj=P(x=tj) alebo pj=F(x=tj)-lim t->tj-F(x=t).
- Overíme podmienku dobrej aproximácie. Ak nevyjde tak musíme upraviť – zlúčiť kategórie a znovu overiť podmienku. Spočítame hodnotu testovej štatistiky. Ak K >= X2 1-alfa(k-1), tak zamietame hypotézu o rovnosti teoretického a empirického rozdelenia pravdepodobnosti.


## Test dobrej zhody pre spojitú náhodnú veličinu

Stanovime kategorie A jako intervaly Aj=(tj-1,tj), tak aby pokrývali celú množinu výsledkov teoretického rozdelenia pravdepodobnosti.

Pri malom rozsahu môžeme za k zvoliť odmocnina n, pri n > 80 sa doporučuje k = 15 * 5 odmocnina z (n/100)^2.

Spočítame empirické početnosti pre jednotlivé kategórie `Nj = |{tj-1<X<=tj}|` a pomocou distribučnej funkcie teoretického 
rozdelenia pravdepodobnosti spočítame teoretické početnosti `nj=F(tj)-F(tj-1)=P(tj-1<X<=tj)`. Overíme podmienku dobrej aproximácie, ak nevyjde tak upravíme kategórie a opakujeme 
overenie podmienky. Spočítame testovú štatistiku a ak K >=X^2alfa (k-1) tak zamietame hypotézu o rovnosti teoretického  a emprického rozdelenia pravdepodobnosti.

## Empirická distribučná funkcia

Je schodovitá a sprava spojitá funkcia. Pre náhodný výber X1,..,Xn 
je `F^(x)=1/n |{i:Xi<=x}|`.


## Kolmogorovov-Smirnovov test









# Kontinenční tabulka


Kontingenční tabulka typu 2 × 2 se nazývá čtyřpolní tabulka a slouží ke srovnání dvou dichotomických znaků.

|		|pravaci|levaci |
| muzi  | 1 | 2 |
| zeny  | 1 | 2 |


popr radek a sloupec s celkem

# předpoklady

nezavislost a homogenita. Obě hypotézy znamenají z hlediska pravděpodobnosti zcela totéž, takže se pro jejich ověření používá stejný test. 


Nezávislost v kontingenční tabulce znamená, že se oba znaky navzájem neovlivňují v tom, jakých konkrétních hodnot. tj. pohlaví nemá žádný vliv na pravorukost/levorukost
Klasický test nezávislosti je založen na testu dobré shody - rekne akorat jestli ovlivnuje nebo ne.

Pro zjištění síly vztahu používáme upravené koeficienty, případně testování založené na podílu šancí.
- koeficient kontingence podle Pearsona – funguje podobně jako korelační koeficient a je zalozen na chi kvadrat.
- pomer sanci = OR = (a * b) / (b * c)
- Cramérův  koeficient



# Podminka dobre aproximace

Rozložení statistiky K lze aproximovat rozložením chi kvadratem (r-1, s-1). Není-li splněna podmínka dobré aproximace, doporučuje se slučování některých variant.



# Logisticka regrese

Událost, zda zkoumaný jev nastal, se modeluje pomocí náhodné veličiny, která nabývá hodnoty 0, pokud jev nenastal, nebo 1, pokud jev nastal
V logistickej regresii sa používa logitová linkovacia funkcia g(p) = ln p/1-p.

Pravdepodobnosť úspechu, resp. neúspechu, je potom rovná p=exp(x’B)/1+exp(x’B) a šanca vychádza ako exponenciála lineárneho prediktoru, odds =e^n

B - beta - je vektorem neznámých parametrů. Odhadem vektoru beta se tedy odhaduje i hledaná pravděpodobnost výskytu zkoumaného jevu. x je vstup.

# Senzitivita

je podíl počtu správně zařazených vzorků do kategorie oproti všem vzorkům, které do kategorie opravdu patři.

# Specificita

udává kolik prvků nezařazených do kategorie do ní opravdu nepatři

# AUC ROC
je metrika, která dokáže zachytit výkonost modelu s různými klasifikačními prahy. AUC (Area Under the Curve) znamená plochu pod křivkou a je nejčastěji používána pravě s křivkou ROC (Receiver Operating
Characteristic), která se skládá z metriky FPR na ose x a TPR na ose y. Pro vygenerování funkce pod kterou se bude plocha počítat je vygenerováno 𝑥 bodů v ROC prostoru, pokaždé s jiným klasifikačním
práhem.









