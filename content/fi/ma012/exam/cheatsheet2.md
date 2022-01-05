---
title: cheatsheet1
url: exam2
---

# Model vícenásobné lineárníj regrese

Slouží k modelování jednorozměrné náhodné veličiny Y skupinou p náhodných veličin X1,...,Xp. Vycházíme ze znalosti (p+1)-dimenzionálního náhodného výběru rozsahu n. Model mnohonásobné 
lineární regrese zapíšeme ve tvaru Y=X*Beta. Y je vektor (Y1,..Yn), Beta je vektor (B0,B1, ...,Bn), kde B1,..,Bn jsou lineární koeficienty náhodných veličin X1,...,Xp. X je matice, která má první sloupec 
jednotkový, a další sloupce tvoří náhodné výběry rozsahu n jednotlivých náhodných veličin. Model řešíme odhadem parametrů metodou nejmenších čtverců. Odhadneme Y nebo Beta.


# Koeficient mnohonásobné korelace 

Vyjadřuje míru závislosti náhodné veličiny Y a náhodnými veličinami X1,...,Xp. Je to korelační koeficient mezi Y a nejlepší lineární aproximací Y^ pomocí veličin X. Jedná se tedy o největší ze všech
absolutních hodnot korelačních koeficientů Y a libovolnou lineární kombinací veličin X.

# Koeficient parciální korelace

Vyjadřuje míru čisté závislosti mezi veličinami Y a Z při eliminaci vlivu veličin X. Je to korelační koeficient mezi reziduí Y-Y^ a Z-Z^ při nejlepších lineárních aproximacích Y^ a Z^ pomocí veličin X.


# Autokorelace

V některých případech (nejčastěji v časových řadách) hodnota náhodné chyby ei závisí na hodnotě předchozích chyb ei-k. Efekt náhodné chyby není jen okamžitý, ale se projevuje i v budoucnosti. Tento  jev
voláme autokorelace.

autokorelace prvniho radu, chyba je zavisla na te predchozi.

Častým typem autokorelace je autokorelace 1. řádu, označovaná jako AR(1), pro kterou platí že `ei=theta ei-1 + ui. kde |theta| < 1` a Eui=0, Dui=oui2 a korelace s ostatními uj je nulová.

# Aitkenuv odhad

V rozsirenem regresnim modelu se symetrickou a pozitivne definitni matici \o^2W je odhad vektoru regresnich koeficientu B zobecnenou metodou nejmensich ctvercu roven:

\beta = (X'W-1X)-1 X'WY


# Dubrin Watson

Dubrinova-Watsonova statistika D se počítá pomocí reziduí v lineárním modelu. 

Durbin-Watsonův test. Statistika vyjde vždy z rozsahu `0<=D<=4`, přičemž je-li D=2 tak chyby nekorelují, pokud D=0 tak je mezi nimi kladná korelace a pokud D=4 tak je mezi nimi záporná korelace.

Kritické hodnoty testu závisí na počtu parametrů, počtu měření a alfa hodnot a jsou tabelované.


# Multikolinearita

Multikolinearita je jev když je lineární závislost mezi vysvětlujícími proměnnými v lineárním modelu. 
Přesná multikolinearita je definována jako lineární závilost sloupců xj v matici plánu X bez sloupce s 
absolutními hodnotami.

V praxi bychom se neměli setkávat s přesnou multikolinearitou, protože bychom měli využívat lineární kombinaci vysvětlujících proměnných a měli bychom se snažit o jejich redukci. V praxi se setkáváme s
částečnou multikolinearitou když je X'X skoro singulární a má skoro nulový determinant. Nastává když použijeme nadbytečné množství vysvětlujících proměnných, přičemž nadbytečné  můžeme identifikovat a
vyřadit.

Při přesné multikolinearitě nedokážeme udělat klasickým postupem metodou nejmenších čtverců odhad
B^. Při částečné multikolinearitě můžeme invertovat X'X, ale výpočty budou nízké kvality.  Multikolinearita snižuje kvalitu výpočtů.

# Metoda postupne regrese

is a method of fitting regression models in which the choice of predictive variables is carried out by an automatic procedure.


# PCA 

PCA (Analýza hlavních komponent) je statistická metoda pro snížení počtu proměnných, které bývají často korelovány.

PCA využívá ortogonalizaci bázi vektorového prostoru původních náhodných veličin. Nové bázové náhodné veličiny, zvané hlavní komponenty, jsou nekorelovány. Volba nové báze je optimální v tom, že
pro vysvětlení podílu celkové variability dat stačí uvažovat nižší počet hlavních komponent, než byl počet původních náhodných veličin. Jednotlivé hlavní komponenty jsou postupně hledány tak, aby 
vysvětlily co největší část celkové variability dat pomocí co nejnižšího počtu nových náhodných veličin.

Nevýhodou může být nemožnost interpretace hlavních komponent. z důvodu nekompatibility použitých jednotek.


- Standardizace dat
- Vypočtení kovarianční nebo korelační matice pro data
- Vypočtení vlastních vektorů a čísel
- Výběr hlavních komponent


