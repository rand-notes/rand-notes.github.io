---
title: asd
url: pa163/exam2
---

CSP je silně k-konzistentní právě tehdy, když je j-konzistentní pro každé j≤k

Cesta (V0, V1, ... , Vm) je konzistentní právě tehdy, když pro každou
dvojici hodnot x∈D0 a y∈Dm splňující binární podmínky na hraně
V0, Vm existuje ohodnocení proměnných V1, ... Vm−1 takové, že
všechny binární podmínky mezi sousedy Vj, Vj+1 jsou splněny.

CSP je konzistentní po cestě, právě když jsou všechny cesty konzistentní.

- šířka grafu je minimum z šířek všech jeho uspořádaných grafů.
- Šířka uspořádaného grafu je maximum z šířek jeho vrcholů.
- Šířka vrcholu v uspořádaném grafu je počet hran vedoucích z tohoto vrcholu do předchozích vrcholů.
- Uspořádaný graf je graf s lineárním uspořádáním vrcholů.
- Šířka grafu nám říká, jak silnou úroveň směrové i-konzistence potřebujeme, abychom nalezli řešení problému bez navracení


# Omezená konzistence po cestě (RPC)

PC hrany se testuje pouze tehdy, pokud vyřazení dvojice může vést k
vyřazení některého z prvků z domény příslušné proměnné

# Prohledavani s inicialni konzistenci

Algoritmus je casto aplikovan az po zajisteni inicialni konzistence

# Vyber hodnoty

Obecný princip: první uspěch (succeed first)
 - volime tak jak si myslime ze dojdeme nejdriv k cili

muzeme bud brat staticky napr. prvni konzistetni hodnotu nebo dynamicky, tedy vezmeme si vsechny
hodnoty a koukneme co nam delaji treba s domena a podle heuristiky nejakou hodnotu vybereme.

## Vyber hodnoty - dynamicky
Minimalni konflikt
- vyber hodnoty, ktera smaze nejmensi pocet hodnot z domen budoucich promennych
Maximalni velikost domeny
- vyber hodnoty, ktera zpusobi vytvoreni nejvetsi minimalni velikost domeny mezi vsemi budoucimi
	promennymi
- intuice: promenne, ktere maji male domeny, zpusobi pravdepodobneji nekonzistenci

# Vyber promenne

vetsinou jsme brali  staticky, tedy vezmeme promennou s nejmensim indexem. Existuje ale i
dynamicky vyber.

Staticky:
 - Statické uspořádání proměnných: výběr proměnných dán předem
 - Maximální kardinalita (první proměnnou (uzel grafu) vybereme náhodně)
 - Minimální šířka (proměnné uspořádány tak, aby byla minimalizována šířka grafu)
Dynamicky:
 - Dynamické uspořádání proměnných: výběr proměnných počítán až v průběhu prohledávání
 - First-Fail


# First-Fail
- výběr proměnné, která nejvíce omezí zbytek stavového prostoru
- výbereme proměnnou s nejmenší doménou
- později už by mohlo být těžší pro tuto proměnnou nalézt správnou hodnotu
- kombinace first-fail a maximální kardinality
 

# Prohledavani

- Thrashing: opakované objevování stejných nekonzistencí a částečných úspěchů při prohledávání
- Backjumping se vrací k původci chyby
- Dynamický backtracking: změna uspořádání minulých proměnných


# Pohledy dopředu
- Kontrola dopředu (forward checking ) FC
- Opravdový úplný pohled dopředu (real full look-ahead ) RFLA = LA
- Úplný pohled dopředu (full look-ahead ) FLA
- Částečný pohled dopředu (partial look-ahead ) PLA


# Konflikty řízený skok zpět - CBJ

- CBJ udrzuje mnozinu kroku zpet(narozdíl od backtrackingu) pro každou proměnnou pomocí nesplněných omezení
- mezi nesplněnými omezeními vybereme to nejvzdálenější
- skočíme zpět na nejbližší proměnnou v tomto omezení

# Algoritmy učení

- Množiny skoků zpět jsou chybná přiřazení vypočítaná během prohledávání
- Tato chybná přiřazení se mohou vyskytovat i později v jiných cestách stromu prohledávání a jsou znovu počítána
- Přidáme chybná přiřazení jako nová omezení při detekci slepé větve
- Prořezávání stavového prostoru
- Zvětšování množiny omezení


## Učení skoku zpět (jumpback learning)
- pokud narazime na slepou vetev, pridame ji do omezeni
- Využijeme chybná přiřazení, která jsme se naučili v CBJ
- Algoritmus učení skoku zpět ≡ CBJ + přidávání nových omezení
- Po dosažení listu slepé větve ~ai−1 přidáme omezení zakazující ~ai−1[Ji]

# Dynamicky backtracking

Skok zpět + pamatování si důvodu konfliktu + přenos důvodu konfliktu + změna pořadí proměnných


# Bounded-backtrack search (BBS)
- je omezen pocet navratu
- pokud se vratim a nemam kam jiz jit, tak navrat nezapocitavam
- pro uplnost: pri neuspechu zvetsime pocet navratu o jedna

# Depth-bounded search (DBS)
- do dane hloubky stromu se zkousi vsechny alternativy
- ve zbytku stromu se muze pouzit jina neuplna metoda
- uplnosti: pri neuspechu zvetsime hloubku prohledavani o jedna
- priklad: DBS(1, BBS(0)) - do hloubky 1 prohledavame vsechny nodes, pak prohledavame pomoci BBS
	s max poctem navratu 0.


# Credit Search
- delime kredity, ktere slouzi pro navrat

# Iterative Broadening IB
- v kazdem bode rozvetvime pouze x vetvi
- napr. IB(2) - rozsirime 2 vetve v nich zase jen 2 vetve atd.


# Limited Discrepancy Search LDS
- omezeny maximalni pocet diskrepancni na ceste (v podstromu)


# Improved Limited Discrepancy Search ILDS
- dany pocet diskrepancí na ceste - cesty s diskrepancemi na konci prozkoumany drive (ikdyz to
	neni zrovna idealni)

# Depth-Bound Discrepancy Search - DDS
- diskrepance povoleny pouze do dane hloubky
- v teto hloubce je vzdy diskrepance tj. zabrání se procházení větví z předchozí iterace
- hloubka zároveň omezuje maximální počet diskrepancí
- cesty s diskrepancemi na začátku prozkoumány dříve


# Omezeni na polokruhy
c-polokruh `<A, +, X, 0, 1>`, kde:
- A je mnozina polokruhu
- 0 \in A (uplne nesplneni), 1 \in A (úplné splnění)
- + komutativní, idempotentní, asociativní operace s jednotkovým prvkem 0, s absorbujím prvkem 1
- × komutativní, asociativní operace, distributivní nad +, s jednotkovým prvkem 1, s absorbujím prvkem 0

# NC*

- projekce ceny hodnot pro každou proměnnou j do dolní hranice LB ceny řešení
- Smazání hodnot (j, a) převyšující (nebo rovné) horní hranici UB.


# AC*
- Projekce ceny hrany (i, a)(j, b) do ceny hodnoty (i, a) pokud je tato cena zahrnuta ve všech hranách (i, a)(j, ∗)

















