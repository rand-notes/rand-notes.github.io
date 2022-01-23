---
title: exam PA163
url: pa163/exam
---

# funfacts
- Hranová konzistence je směrová - konzistence hrany (Vi, Vj) nezaručuje konzistenci hrany (Vj, Vi)
- Použitím AC odstraníme mnoho nekompatibilních hodnot, ale nedostame reseni problemu ani nevime jestli reseni existuje.
- PC ⇒ AC, ale AC !⇒ PC

# CSP na binarni pomoci dualniho problemu

vezmeme podminku C_i a prevedeme ji na V_i, ktera bude obsahovat n-tice hodnot, ktere splnuji podminku.

napr. C1 = C + E > 2, kde C ma domenu {1,2,3} a E ma domenu {0,1}. potom: V4 = {(2,1), (3,0), (3,1)}

V bloky  propojime podle toho jak se rovnaji promenne v podminkach

napr. c1 : A + D + F = 1, c2 : A − C + D = 1 ==> propojime s R11 & R23


# AC-1 a AC-3

U algoritmu AC-1 dochází k revizi všech hran pokaždé, kdy se doména některé z proměnných
změní. U algoritmu AC-3 se hrany k zrevidování berou z fronty. Do té se na začátku vloží hrany
všechny a pokaždém pruchodu se vloží pouze ty hrany, které mohou být zasaženy některou z případných změn domén


pr. `A∈{1, ..., 10}, B∈{1, ..., 10}, C∈{1, ..., 10}, B < A, A ≤C + 4`


# Podpora

Vytvarime tzv. podpory mezi promennymi, pokud vime ze pokud domena promenne V1 bude a, tak V2
musi byt. b nebo c, tak vytvorime podpory mezi ab a ac. Vyhoda je v tom, ze jakmile odstranime
hodnotu ve V1, tak ve V2 nemusime kontrolovat vsechny hodnoty, ale zkontrolujeme pouze podpory.
Pokud ma dana hodnota i jinou podporu mezi V1 a V2 pak se necha jinak se hodnota odstrani z
domeny.



# K konzistence

- AC: rozšiřujeme jednu hodnotu do druhé proměnné
- PC: rozšířujeme dvojici hodnot do třetí proměnné

CSP je k-konzistentní právě tehdy, když můžeme libovolné
konzistentní ohodnocení (k-1) různých proměnných rozšířit do libovolné k-té proměnné


# Obecné Hranové Konzistence (GAC)
někdy nazývána doménová konzistence

CSP je obecně hranově konzistentní `<=>` všechna jeho omezení jsou obecně hranově konzistentní

- Uspořádaný graf je graf s lineárním uspořádáním vrcholů.
- Šířka vrcholu v uspořádaném grafu je počet hran vedoucích z tohoto vrcholu do předchozích vrcholů.
- Šířka uspořádaného grafu je maximum z šířek jeho vrcholů.
- Šířka grafu je minimum z šířek všech jeho uspořádaných grafů.


pro zjisteni sirky grafu vezmeme vsechny jeho uzly a zjistime nejmensi pocet hran vedouci z
nejakeho uzlu


# Adaptivní konzistence (ADC)


# Backtracking

rozsirime aktualni uzel a pak vsechny jeho deti zkousime z podminek a vyradime ty ktere neprojdou.

# Forward-checking

na zacatku rozsirime vsechny uzly, pomoci prvni podminky omezime domenu dalsi promenne. Pokud nam
nezbyde zadna volna hodnota tak konec, jinak rozsirime jenom ty deti ktere prosli podminkou.

# Look-Ahead

Prvni krok stejny jako Forward-checking, ale po redukci domeny zaroven redukujeme i dalsi domeny
podle nasledujicich podminek (pomoci jiz redukovanych domen). Pokracujeme ve vetvi jen pokud
existuje ve vsech domenach aspon 1 hodnota.


- Thrashing: opakované objevování stejných nekonzistencí a částečných úspěchů při prohledávání
- Algoritmy pohledu dopředu kontrolují podmínky dopředu
	- backtracking odhalí nesplnění podmínky teprve když přiřadí hodnoty jejím proměnným
	- konzistenčními algoritmy lze předem upravit domény A a E
- Backjumping se vrací k původci chyby
	- backtracking vyzkouší všechny možnosti pro B,C,D než odhalí A!=1 hned po prvním neúspěšném přiřazení E se lze vrátit k přiřazování A
- Dynamický backtracking: změna uspořádání minulých proměnných
- Neúplná prohledávání: hledání pouze v některých částech stavového prostoru

# Pohledy dopredu

## Kontrola dopředu (forward checking) FC

FC zajišťuje konzistenci mezi aktuální proměnnou a budoucími proměnnými, které jsou s ní spojeny dosud nesplněnými podmínkami

## RFLA == LA


## Úplný pohled dopředu (full look-ahead) FLA

pouze jeden průchod repeat until cyklem algoritmu

## Částečný pohled dopředu (partial look-ahead) PLA

pouze jeden průchod repeat until cyklem algoritmu
nahrazuje `for ∀ k, k != j, i < k ≤ n` výrazem `for ∀ k, j < k ≤ n`
tj. budoucí proměnné porovnávány pouze s těmi, které je následují, tj. DAC

# Výběr hodnoty

Jakým způsobem vybírat ze zbývajích hodnot v doméně proměnné?

Triviální výběr hodnoty:
 - doména procházena ve vzrůstajícím pořadí
 - doména procházena v klesajícím pořadí

Obecný princip výběru hodnoty: první úspěch (succeed first)


## Minimální konflikt

- výběr hodnoty, která smaže nejmenší počet hodnot z domén budoucích proměnných
- experimentálně: tato heuristika vykazuje velmi dobré výsledky


## Maximální velikost domény

výběr hodnoty, která způsobí vytvoření největší minimální velikost domény mezi všemi budoucími proměnnými
intuice: proměnné, které mají malé domény, způsobí pravděpodobněji nekonzistenci


# Výběr proměnných: statický

## Statické uspořádání proměnných: výběr proměnných dán předem
 - triviálně: výběr nejlevější proměnné tj. proměnné s nejmenším indexem

## Maximální kardinalita
- první proměnnou (uzel grafu) vybereme náhodně
- každý uzel je spojen s maximálním počtem už uspořádaných (= dříve vybraných) vrcholů
- proměnné vybíráme v pořadí dle tohoto počtu vrcholů


## Minimální šířka
- proměnné uspořádány tak, aby byla minimalizována šířka grafu (minimalizován počet zpětných hran)
- odzadu vybíráme proměnné s nejmenším počtem hran v aktualizovaném grafu (algoritmus viz dříve)

# Výběr proměnných: dynamický

Dynamické uspořádání proměnných: výběr proměnných počítán až v průběhu prohledávání


## First-fail

- velmi často používaná metoda (vhodná jako default)
- výběr proměnné, která nejvíce omezí zbytek stavového prostoru
- **vybereme proměnnou s nejmenší doménou**
- později už by mohlo být těžší pro tuto proměnnou nalézt správnou hodnotu
- kombinace first-fail a maximální kardinality
- `A, B, C ∈ {1, 2, 3}, A < 3, A = B + C` nejlépe je začít s výběrem A


# Silnější pohled dopředu

Algoritmy pohledu dopředu zatím uvažovaly pouze hranovou konzistenci
Po každém přiřazení hodnoty proměnné lze vyžadovat dosažení vyššího stupně konzistence


# Přehled typů algoritmů pohledu zpět look-back

## Algoritmy skoku zpět (backjumping)

- při zpětném průchodu se nevracíme pouze jeden krok jako algoritmus backtrackingu
- snažíme se vracet co nejdále až ke zdroji chyby


## Algoritmy učení (constraint recording, no-good learning)

- no-good = chybné částečné přiřazení 
- přidáme nová omezení, která zakazují nalezená chybná přiřazení


## Dynamický backtracking

- při skoku zpět se snažíme nezapomínat na už udělanou práci
- měníme hodnoty pouze u minulých proměnných s konfliktem
- realizace: změníme uspořádání proměnných

## Backmarking

- pamatuje si, kde testy na konzistenci neuspěly
- eliminuje opakování dříve provedených konzistenčních testů


# Konfliktní množina

- Jestliže neexistuje hodnota b z domény x tak, aby (a, x) bylo konzistentní, říkáme, že a je konfliktní množina x a nebo, že a je v konfliktu s x.
- Pokud a neobsahuje j-tici `(j < k)`, která je v konfliktu s x, pak nazýváme a minimální konfliktní množina.


# Chybné přiřazení

- Částečné přiřazení a, které se nevyskytuje v žádném řešení CSP, se nazývá chybné přiřazení (no-good ).
- konfliktní množiny jsou chybná přiřazení.
- Minimální chybná přiřazení neobsahují chybná přiřazení méně proměnných


## Přiřazení je konfliktní množinou i chybným přiřazením

Takové přiřazení, které nám znemožní přiřadit další proměnné hodnotu a proto nedokážeme udělat
řešení konzistentní a samotné řešení tedy není validní

## Přiřazení není konfliktní množinou i chybným přiřazením

Takové přiřazení, které splňuje podmínky a je zárověň i řešením.


## Přiřazení je konfliktní množinou, ale není chybným přiřazením

Takové přiřazení neexistuje, protože každá konfliktní množina je chybné přiřazení vzhledem k
jedné proměnné.

## Přiřazení není konfliktní množinou, ale je chybným přiřazením

Přiřadíme hodnotu nějaké proměnné (popř. několik hodnot proměnným) tak, že hodnoty splňují
všechny podmínky, ale nemohou se zároveň vyskytovat v řešení.


# Konfliktní proměnná

Pokud víme, že x_j je chybné přiřazení pak víme že x_j je bezpečná. Protože pokud při backtracking skočíme zpátky na x_j pak si
 můžeme být jistí, že jsme nepřeskočili žadné řešení.


# Gaschnig’s backjumping (GBJ)

Když nedokážeme přiřadit hodnotu proměnné xi, vracíme se zpět (skáčeme zpět) ke konfliktní proměnné.

Určení konfliktní proměnné: 
 - pro každou hodnotu vi ∈ xi nalezneme proměnnou s nejmenším indexem, která je s xi /vi v konfliktu (přiřazení této proměnné musíme určitě změnit, aby šla hodnota vi použít)
 - konfliktní proměnná je ta z nich, která má největší index (když její hodnotu změníme, můžeme zrušit konflikt s odpovídající hodnotou)




# Konflikty řízený skok zpět (Conflict-directed backjumping CBJ)

Při skoku zpět na proměnnou xj z listu slepé větve nemusíme nalézt v doméně xj
žádné hodnoty pro přiřazení. aj−1 se pak nazývá vnitřní slepá větev.

CBJ skáče zpět v listu slepé větve i ve vnitřní slepé větvi:
 - udržujeme Ji množinu skoků zpět pro každou proměnnou pomocí nesplněných omezení
 - `xj (j < i)` je bližší k xi než `xk (k < i)`, jestliže `k < j`. Naopak xk je vzdálenější
 - omezení R je vzdálenější než omezení S, jestliže je nejbližší proměnná v rozsahu R vzdálenější než nejbližší proměnná v rozsahu S (pokud totožné proměnné, rozhodují další proměnné).
 - mezi nesplněnými omezeními vybereme to nejvzdálenější (ostatní omezení neumožní nejdelší možný skok zpět)
 - skočíme zpět na nejbližší proměnnou v tomto omezení (je bezpečné změnit proměnnou, která byla nejpozději přiřazená)


# Algoritmy učení

- Množiny skoků zpět jsou chybná přiřazení vypočítaná během prohledávání
- Tato chybná přiřazení se mohou vyskytovat i později v jiných cestách stromu prohledávání a jsou znovu počítána
- Přidáme chybná přiřazení jako nová omezení při detekci slepé větve
 - nemá cenu uchovávat celou slepou větev ~ai v proměnné xi+1 na toto přiřazení už později nenarazíme
 - uchováme chybná přiřazení na podmnožině proměnných {x1, ..., xi }
- Prořezávání stavového prostoru: čím menší chybná přiřazení se podaří uchovat, tím rychlejší bude prohledávání
- Zvětšování množiny omezení: cena za prořezávání stavového prostoru nesmí přerůst cenu za zvětšování množiny omezení


# Učení skoku zpět (jumpback learning)

- Využijeme chybná přiřazení, která jsme se naučili v CBJ
- Algoritmus učení skoku zpět ≡ CBJ + přidávání nových omezení
- Po dosažení listu slepé větve ~ai−1 přidáme omezení zakazující ~ai−1[Ji]


# Problémy skoku zpět

Při skoku zpět zapomínáme už udělanou práci

**dynamický backtracking** = Skok zpět + pamatování si důvodu konfliktu + přenos důvodu konfliktu + změna pořadí proměnných

Nevýhody dynamickeho backtrackingu: přeuspořádáváním proměnných rušíme efekt heuristik výběru proměnných


# Neúplné prohledávání do hloubky

- Neprohledáváme celý stavový prostor
- Nemáme záruku, že řešení neexistuje, i když ho algoritmus nenalezne
- V řadě případů najdeme řešení rychleji
- Neúplné algoritmy často odvozeny od algoritmu úplného (DFS)
  - přerušení běhu algoritmu (cutoff): po vyčerpání přiděleného prostředku (prostředek může být globální i lokalni)
  - opakovaní běhu algoritmu (restart) s jinym nastavenim


## Depth first search (DFS)
- odpovídá algoritmu backtrackingu
- Reálné problémy mají často tak velké prostory možných ohodnocení, že není možné je celé prohledat.
- možné prohledat jen omezený prostor -> Neúplná stromová prohledávání
- Neúplné prohledávání do hloubky


## Randomizovaný backtracking

- časově omezený backtracking (přerušení)
 - běh (úplného) algoritmu ukončíme po zadaném časovém intervalu
 - časový interval lze pro další běhy zvětšit
- náhodný výběr hodnot a proměnných (opakování)
 - pokud máme možnost volby při výběru hodnot nebo proměnných náhodně zvolíme některou z nich

## Randomizovaný backtracking s učením
- chybná přiřazení předchozích běhů uchováme a využíváme
- takto lze také dosáhnout úplnosti, protože chybných přiřazení je konečně mnoho


# Omezení počtu návratů - Bounded-backtrack search (BBS)

Omezený počet návratů (přerušení)
 - návrat do bodů volby, kde už nelze vybrat novou hodnotu nezapočítáváme

Pro úplnost: při neúspěchu zvětšíme počet návratů o jedna (opakování)


# Omezení hloubky - Depth-bounded search (DBS)

Omezíme hloubku prohledávaného stromu (přerušení)
- do dané hloubky stromu se zkouší všechny alternativy
- ve zbytku stromu se může použít jiná neúplná metoda

Pro úplnost: při neúspěchu zvětšíme hloubku prohledávání o jedna (opakování)

napr. DBS(1, BBS(0)) - prohledava pouze nejlevejsi vetve do hloubky 


# Prohledávání s kreditem - Credit search (CS)

Omezený kredit (počet návratů) pro prohledávání (přerušení)
 - kredit se rovnoměrně dělí mezi alternativní větve prohledávání
 - jednotkový kredit zakazuje možnost volby (hodnoty), tj. pokračujeme pouze bez návratů

Pro úplnost: při neúspěchu navýšíme kredit o jedna (opakování)

# Iterativní rozšiřování - Iterative broadening IB

Omezený maximální počet voleb (hodnot) - při každém výběru proměnné (přerušení)
 - v každém bodě volby větvení omezeno konstantou
 - při překročení max. počtu voleb pokračujeme předchozím bodem volby

Úplnost: při neúspěchu zvýšíme povolený počet voleb o jedna (opakování)

Implementace: po výběru proměnné umožníme pouze výběr určeného počtu jejích hodnot


# Stromová prohledávání a heuristiky

Při řešení reálných problémů často existuje nápověda odvozená ze zkušeností s „ručním” řešením problému

Heuristiky – radí, jak pokračovat v prohledávání
 - doporučují hodnotu pro přiřazení
 - často vedou přímo k řešení
 
Co dělat, když heuristika neuspěje?
 - DFS se stará hlavně o konec prohledávání (spodní část stromu)
 - DFS tedy spíše opravuje poslední použité heuristiky než první
 - DFS předpokládá, že dříve použité heuristiky ho navedly dobře

Pozorování
 - počet porušení heuristiky na úspěšné cestě je malý
 - heuristiky jsou méně spolehlivé na začátku prohledávání než na jeho konci (na konci máme více informací a méně možností)

# Zotavení se z chyb heuristiky

- Heuristika doporučuje hodnotu pro přiřazení
- **Diskrepance** = porušení heuristiky (použita jiná hodnota, než doporučila heuristika)
- Pozorování: málo chyb heuristiky na cestě k řešení (cesty s méně diskrepancemi jsou prozkoumány dříve)
- Pozorování: chyby heuristiky hlavně na začátku cesty (cesty s diskrepancemi na začátku jsou prozkoumány dříve)

# Omezené diskrepance

Limited discrepancy search (LDS)
Omezený maximální počet diskrepancí na cestě (přerušení)
 - cesty s diskrepancemi na začátku jsou prozkoumány dříve
Při neúspěchu navýšíme
 - počet povolených diskrepancí o jedna (opakování)
 - tj. nejprve jdeme tak, jak doporučuje heuristika; potom jdeme po cestách s maximálně jednou diskrepancí; pak maximálně se dvěma diskrepancemi, atd.

Diskrepance pro nebinární domény:
 - nedoporučené hodnoty se berou jako jedna diskrepance
 - výběr každé další hodnoty proměnné je jedna diskrepance


# Omezené diskrepance – zlepšení

LDS v každé další iteraci prochází i větve z předchozí iterace, tj. opakuje již provedený výpočet a navíc se v rámci iterace musí vracet do již prošlých částí

## Improved limited discrepancy search (ILDS)

daný počet diskrepancí na cestě (přerušení): cesty s diskrepancemi na konci prozkoumány dříve

Při neúspěchu navýšíme počet diskrepancí o jedna (opakování)


# Hloubkou omezené diskrepance
ILDS bere cesty s diskrepancemi na konci dříve  
Depth-bounded discrepancy search (DDS)  
Diskrepance povoleny pouze do dané hloubky (přerušení)
 - v této hloubce je vždy diskrepance, tj. zabrání se procházení větví z předchozí iterace
 - hloubka zároveň omezuje maximální počet diskrepancí
 - cesty s diskrepancemi na začátku prozkoumány dříve
Při neúspěchu navýšíme hloubku o jedna (opakování)


# Lokální prohledávání (LS)

pracuje s úplnými nekonzistentními přiřazeními proměnných
snaží se lokálními opravami snížit počet konfliktů

Heuristická metoda prohledávání:
 - neúplná metoda
 - nezaručuje nalezení (vyloučení existence) řešení i když existuje (neexistuje)
 - malé paměťové nároky


Ne-striktní lokální optimum: stav, v jehož okolí exisují stavy se stejnou evaluací; není globálním optimum


# Metoda největšího stoupání (hill climbing ) HC



# Metoda minimalizace konfliktů (MC)


# Náhodná procházka (Random Walk) RW

Jak uniknout z lokálního optima bez restartu? přidáním „šumu” do algoritmu

Pokud se dostaneme do lokálního optima:
 - náhodně zvolíme stav z okolí a pokračujeme jím
 - tato metoda samostatně k řešení nepovede
 - potřebuje další směrování v prohledávacím prostoru: lze kombinovat s HC i MC

RW kombinujeme s heuristikou pomocí pravděpodobnostního rozložení:
 - pravděpodobnost náhodného kroku je p
 - např. 0.02 ≤ p ≤ 0.1
 - pravděpodobnost použití směrové heuristiky je 1 − p
 - náhodná procházka tedy nahrazuje restart: unik z lokálního minima prostřednictvím náhodného výběru


# Tabu seznam

Tabu seznam = seznam tabu (zakázaných) stavů
Aspirační kritérium = odtabuizování stavu (např kdyz krok vede k celkově lepšímu stavu)


# Výběr souseda: přehled

Metoda stoupání (HC)
 - soused s nejlepší evaluací vybrán
Tabu prohledávání (TS+HC)
 - soused s nejlepší evaluací vybrán (metoda stoupání)
 - sousedé z tabu seznamu nemohou být vybráni
Minimální konflikt (MC)
 - soused je omezen na náhodně vybranou konfliktní proměnnou
 - výběr její hodnoty s nejlepší evaluací
Náhodná procházka (RW)
 - soused vybrán náhodně
Minimální konflikt (metoda stoupání) s náhodnou procházkou MC+RW (HC+RW)
 - s malou pravděpodobností: náhodný výběr souseda
 - jinak: minimální konflikt (metoda stoupání)


# Simulované žíhání (simulated annealing) SA

Myšlenka: simulace procesu ochlazování kovů
 - na začátku při vyšší teplotě atomy více kmitají a pravděpodobnost změny krystalické mřížky je vyšší
 - postupným ochlazováním se atomy usazují co „nejlepší polohy” s nejmenší energií a pravděpodobnost změny je menší
 - na začátku je tedy pravděpodobnost toho, že akceptujeme zhoršování řešení, vyšší

Akceptování nového stavu
 - vždy při zlepšení
 - při zhoršení pouze za dané pravděpodobnosti která klesá se snížením teploty

Cykly algoritmu
 - vnější: simulace procesu ochlazování snižováním teploty T
  - čím nižší bude teplota, tím nižší bude pravděpodobnost akceptování zhoršení
 - vnitřní: počítáme, kolikrát jsme neakceptovali zhoršení: dán limit MaxIter 


# Metropolisovo kritérium

Rozdíl mezi kvalitou nového řešení δ a existujícího řešení θ

\\( \delta E = E(δ) - E(θ) \\)

E (chybovost) musí být minimalizována

Metropolisovo kritérium
 - lepší (někdy případně i stejně kvalitní) řešení akceptováno: \\( \delta E \leq 0 \\)
 - horší řešení (∆E > 0) akceptováno pokud: \\( U \leq e^{-\delta E/T} \\)


U náhodné číslo z intervalu (0, 1)

# Algoritmus GSAT (Greedy SAT )
 - postupné překlápění proměnných
 - evaluace udává, jaký je (vážený) počet nesplněných klauzulí

## Heuristiky pro GSAT

GSAT lze kombinovat s různými heuristikami, které zvyšují jeho efektivitu
 - obzvláště při řešení strukturovaných problémů

Použití náhodné procházky spolu s minimalizací konfliktů

Vážení klauzulí:
 - některé klauzule zůstávají po řadu iterací nesplněné, klauzule tedy mají různou důležitost
 - splnění „těžké” klauzule lze preferovat přidáním váhy
 - váhu může systém odvodit
  - na začátku mají všechny klauzule stejnou váhu
  - po každém pokusu zvyšujeme váhu u nesplněných klauzulí

Průměrování řešení
 - standardně každý pokus začíná z náhodného řešení
 - společné části předchozích řešení lze zachovat
  - restartovací stav se vypočte ze dvou posledních výsledků bitovým srovnáním, stejné bity zachovány, ostatní nastaveny náhodně


## Hybridní prohledávání

Příklady kombinace lokálního prohledávání a stromoveho prohledavani

- Lokální prohledávání před nebo po stromovém prohledávání
- Stromové prohledávání je doplněno lokálním prohledávání
- Lokální prohledávání je doplněno stromovým prohledáváním

# Iterativní dopředné prohledávání - Iterative Forward Search (IFS)

Hybridní prohledávání: konstruktivní nesystematický algoritmus
 - pracuje nad modelem s pevnými a měkkými omezujícími podmínkami
 - pevné podmínky: musí být splněny
 - měkké podmínky: reprezentují účelové funkce, jejichž vážený součet je minimalizován

Pracuje s konzistentními přiřazeními

Základní myšlenky (blízký dynamickému backtrackingu)
 - začíná s prázdným přiřazením
 - vybere novou proměnnou k přiřazení
 - pokud nalezne konflikt, zruší přiřazení všech proměnných v konfliktu s vybranou proměnnou
 - výběr hodnot pomocí konfliktní statistiky
 - výběr proměnných není pro algoritmus kritický, protože lze proměnné přiřadit opakovaně


# Náhodné problémy

Algoritmy porovnávány na umělých, náhodně vygenerovaných problémech
 - lze generovat problémy různé obtížnosti (fáze přechodu)
 - libovolný počet datových instancí
 - lze testovat, co se stane


Náhodné binární CSP (random binary CSP) - parametry (n, m, p1, p2)

## Fáze přechodu

Náhodný k-SAT problém:
 - formule pevné délky jsou generovány výběrem m klauzulí
 - každá klauzule délky k je uniformně náhodně generována z množiny všech klauzulí



# Optimalizační problém s podmínkami (COP)

Problém splňování podmínek (X, D, C)
 - proměnné X
 - domény D
 - omezení C

Základní definice:
 - Optimalizační problém s podmínkami (constraint optimization problem)


## COP: operační výzkum

- Pevné (hard, required) omezení C_h
- Měkké (soft) omezení C_s

Optimalizační problém s podmínkami (COP): (X, D, Ch, Cs)

## Použití měkkých omezení

- Problémy optimalizační, příliš podmíněné, špatně definované problémy
- Fuzzy preference, pravděpodobnosti, ceny, váhy, úrovně požadavků
- Příliš podmíněné problémy: řešení CSP neexistuje
- Problémy s nejistotou
- Špatně definované problémy: není zřejmé, která omezení definují CSP

## Přístupy pro měkká omezení

Vybrané přístupy:
 - základní: MAX-CSP, omezení s váhami, fuzzy omezení
 - zobecňující: omezení nad polookruhy (semiring-based )

Rozlišení systémů na základě:
 - omezení – rozšíření klasického omezení
 - problém – rozšíření CSP
 - úroveň splnění – jak přiřazení hodnot splňuje problém
 - řešení – které přiřazení je (optimálním) řešením
 - úroveň konzistence problému – jak je možné nejlépe splnit problém tj. jak (optimální) řešení splňuje problém


## Omezení s váhami
 - váha/cena spojená s každým omezením
 - omezení – dvojice (c, w (c))
 - problém – trojice (V , D, C_w)
 - úroveň splnění – funkce na množině přiřazení => součet vah nesplněných omezení
 - řešení – přiřazení θ s minimální
 - úroveň konzistence – úroveň splnění řešení

# MAX-CSP (maximální CSP)
 - váha je rovna jedné ⇒ maximalizace počtu splněných omezení



# Fuzzy CSP

Fuzzy množiny: příslušnost prvku k množině zadána číslem z intervalu [0, 1]

Fuzzy omezení: fuzzy relace μc(d1, ..., dk)∈〈0,1〉udává úroveň preference

Fuzzy CSP (X, D, Cf)
 - Cf je množina fuzzy omezení
 - X uspořádaná množina proměnných


# Kombinace a projekce omezení

Kombinace (+ v kolecku): bere se min z podminek
 - c, cX, cY omezení nad Z, X, Y

Projekce(sipka dolu): bere se max
 - c, cX, cY omezení nad X, X, Y

Reseni fuzzy je max z vsech moznych kombinaci podminek

# Omezení nad polookruhy

// TODO


# Optimalizace & soft omezení: algoritmy

## Soft propagace

Klasická propagace: eliminace nekonzistentních hodnot z domén proměnných

Soft propagace:
 - propagace preferencí (cen) nad k-ticemi hodnot proměnných
 - snaha o získání realističtějších preferencí
 - výpočet realističtějších příspěvků pro cenovou funkci

## SAC A COP
//TODO



# Metoda větví a mezí (branch&bound) BB

Prohledávání stromu do hloubky:
 - přiřazené=minulé proměnné P, nepřiřazené=budoucí proměnné F
 - omezení pouze na minulých proměnných C_P,
 - omezení na minulých i budoucích proměnných C_PF
 - omezení pouze na budoucích proměnných C_F

Výpočet mezí:
 - horní mez UB: cena nejlepšího dosud nalezeného řešení
 - dolní mez LB: dolní odhad minimální ceny pro současné částečné přiřazení

Ořezávání: LB ≥ UB
 - víme, že rozšíření současného částečného řešení už bude mít horší (vyšší) cenu LB než dosud nalezené řešení UB
 - lze proto ořezat tuto část prohledávacího prostoru
 - příklad: pokud nalezneme řešení s cenou 10 odřízneme všechny větve, které mají cenu vyšší než 9


## Metoda větví a mezí: výběr hodnoty
 - generický algoritmus rozšiřitelný jako implementace backtrackingu
 - možná rozšíření zejména o: pohled dopředu, výpočet dolní meze

LB(~d ) vrací dolní odhad ceny pro každé částečné přiřazení ~d

- Optimistický výběr hodnoty


## Dolní mez
Kvalita dolní meze: velmi důležitá pro efektivitu BB

Dolní mez lze ovlivnit pomocí:
 - ceny minulých proměnných: vzdálenost (součet vah omezení na minulých proměnných)
 - lokální ceny budoucích proměnných vzhledem k minulým proměnným: NC*
 - lokální ceny budoucích proměnných: AC* 

# NC∗ algoritmus

- Projekce ceny hodnot (j, ∗) pro každou proměnnou j do dolní hranice LB ceny řešení
- Smazání hodnot (j, a) převyšující (nebo rovné) horní hranici UB



























