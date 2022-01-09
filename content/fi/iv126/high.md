---
title: adadas
url: ai/exam2
---


basic/pokrocile prohledavani == grafy

ejection chain; cyclic exchange

hill climbing
simulovane zihani - akceptuje i horsi 
threshold accepting - akceptuje s max zhorsenim o prah
potopa - zmenusujeme hladinu
tabu seznam - muzeme overridnout pomoci aspiracniho kriteria


Multistart local search, Iterativní lokální prohledávání


VNS - variable neighborhood search
VND - variable neighborhood descent
 - deterministicka verze VNS
 - rozsirujeme okoli, po uspechu jedeme od zacatky

GLS - guided local search
 - cena + penalizace + charakteristika (bool jestli je v reseni)
 - upravena ucelova fce: f'(s) = f(s) + \lambda \sum p_i I_i(s) 

---

Výběr ruletovým kolem
Pravděpodobnostní univerzální vzorkování (ruletove kolo se 4 ukazateli)

Turnajový výběr, Výběr rankováním (rank-based selection) -- vybrani ti nejlepsi z k jedincu

Mutace
 - binarni reprezentace - flip
 - diskretni - zmena hodnoty za jinou v abecede
 - permutace - vložení, výměna, inverze hodnot(y)

Krizeni - jednobodove, n-bodove, uniformni, Křížení dané pořadím (Order crossover, OX, vyuziva 2 body krizeni)

ACO (prochazeni pomoci mapy, vyparovani, zesileni)

----

Klasicke planovani - stavove promenne, pocatecni a cilovy stav + akce (operatory)

STRIPS
 - prakticky binary klasicke planovani
 - Všechny proměnné mají doménu {T, F}
 - V podmínce akce a v cílovém stavu pouze v → T

Konceptualni model SIGMA modeluje stavy a prechody
 - mnozina stavu S
 - mnozina akci A
 - mnozina udalosti E
 - prechodova funkce

flexibilni/nemenne atomy
operator je trojice - jmeno, preconds, effects
Akce jsou plně instanciované operátory (za proměnné jsou dosazeny konstanty)

---

Klasická reprezentace: plánovací problém

Plánovací problém P je trojice SIGMA, s0, g
 - SIGMA je planovaci domena (trojice S, A, gamma)
 - s0 je poc stav
 - g je mnozina cilovych stavu

Plan je posloupnot akci
Plán π je řešením P, právě když γ(s0,π) splňuje g

---

dopredne planovani - zaciname v s0 jedem do cile "pomoci" bfs/dfs nebo a*
zpetne planovani - Začínáme s cílem (pozor to není stav, ale reprezentace množiny stavů!) a jdeme přes podcíle k počátečnímu stavu
zpetne liftovana verze
 - pouziva obecny operatory
 - MGU (největší společný unifikátor, tj. nejobecnější substituce atomů), 
 - použití volných proměnných zmenšuje větvení, ale komplikuje detekci cyklů


STRIPS
 - redukuje prohledávaný prostor zpětného plánování
 - z podcílů řeší vždy jen část odpovídající předpokladům poslední přidané akce

Domenove znalosti
 - kostka nesmí najednou stát na dvou jiných kostkách atd.

----

Plánování v prostoru plánů
 - začínáme z „prázdného plánu”
 - přidáváme další akce, které plní dosud nesplněné (otevřené) cíle
 - případně přidáváme vazby mezi již přítomnými akcemi
 - Na plánování se můžeme dívat jako na opravování kazů v částečném plánu
 - přecházíme od jednoho částečného plánu k dalšímu dokud nenajdeme úplný plán

Možné úpravy plánu
 - přidání akce
 - svázání proměnných
 - přidání podmínky uspořádání
 - přidání kauzální (příčinné) vazby


Počáteční stav i cíl zakódujeme jako speciální akce, které jsou v prvotním částečném plánu
 - akce a0 reprezentuje počáteční stav tak, že nemá žádné předpoklady a počáteční stav je zakódován jako efekt
 - akce a∞ reprezentuje cíl, který je zakódován jako předpoklad, efekt akce je prázdný; tato akce je za všemi ostatními akcemi

Uzly prohledávaného prostoru jsou tvořeny částečnými plány

Částečný plán Π je čtveřice (A,<,B,L), kde
 - A je množina částečně instanciovaných plánovacích operátorů
 - < je částečné uspořádání na A (ai < aj)
 - B je množina vazeb tvaru
 - L je množina kauzálních vztahů tvaru (ai p→ aj)


Otevřený cíl (open goal) je kazem plánu

Jedná se o předpoklad p nějakého operátoru b, o kterém zatím nebylo rozhodnuto, jak ho splnit (neexistuje kauzální vazba ai p→ b)

Odstranění otevřeného cíle p akce b:
 - najdi operátor a který lze použít na splnění p
 - svaž proměnné
 - vytvoř kauzální vazbu

Příklad:
 - předpoklad p: at(r1,l1)
 - operátor a: move(r,l,m)
 - svázání proměnných: r/r1, l1/m
 - kauzální vazba: move(r1,l,l1) < load(k1,c1,r1,l1)


Hrozba

Hrozba (threat) je dalším kazem plánu. Jedná se o akci, která může porušit kauzální vazbu

Odstranění hrozby lze udělat třemi způsoby:
 - uspořádání b před ai
 - uspořádáním b za aj
 - navázáním proměnných v b tak, že neruší platnost p

---

Algoritmus plánování v prostoru plánů (PSP)

zjemneni = odstraneni kazu

- volba kazu je deterministická - musí se odstranit všechny kazy
- volba zjemnění je nedeterministická - v případě neúspěchu se zkouší další alternativa

PoP

je konkretni instance algoritmu PSP

- agenda je množina dvojic (a,p), kde p je otevřený předpoklad akce a
- nejprve hledá akci ai pro pokrytí nějakého p z agendy
- ve druhé fázi řeší všechny hrozby, které vznikly přidáním akce ai , resp. kauzální vazby s ai

|  | Plánování se stavy | Plánování s plány |
|---|---|---|
| prohled. prostor | konečný | nekonečný |
| uzly | jednoduche (stavy světa) | komplikovanější (částečné plány) |
| stavy světa | explicitní | nejsou |
| částečný plán | uspořádání a volba akcí se dělá najednou | volba akcí a jejich pořadí oddělené |
| struktura plánu | lineární bez vazeb | kauzální vazby |

Díky doménově specifickým heuristikám je dnes plánování se stavy výrazně rychlejší

----

Pravděpodobnosti elementárních jevů můžeme popsat tabulkou, tzv. úplnou sdruženou distribucí

Chceme-li znát pravděpodobnost nějakého tvrzení, sečteme pravděpodobnosti všech „světů”, kde tvrzení platí (marginalizace)

Bayesovské sítě

efektivní způsob reprezentace podmíněných pravděpodobností a nezávislostí
Zachycuje závislosti mezi náhodnými proměnnými

Orientovaný acyklický graf (DAG)  - uzel odpovídá náhodné proměnné 

Bayesovská síť kompaktním způsobem reprezentuje úplnou sdruženou distribuci (popisuje pravděpodobnost všech elementárních jevů)

pro konstrukci site vyuzivame: Bayes vetu, retezcove a soucinove pravidlo

Evaluace se provádí shora dolů násobením hodnot po každé cestě a sečítáním hodnot v „+” uzlech

Eliminace proměnných

Enumerační metoda zbytečně opakuje některé výpočty. Stačí si výsledek zapamatovat a následně použít
Vyhodnocení provedeme zprava doleva
 - násobení činitelů je násobení po prvcích
 - vysčítáním činitelů eliminujeme příslušnou proměnnou
 - na závěr provedeme normalizaci

Vzorkovací metody

Exaktní odvozování je výpočetně náročné, můžeme ale použít aproximační techniky založené na metodě Monte Carlo

- příme vzorkování
- vzorkování se zamítáním
- vzorkování s vážením věrohodností - generujeme pouze vzorky vyhovujici pozorovani

----


Přechodový model popisuje, jak je stav ovlivněn předchozími stavy 
Senzorický model popisuje, na čem závisí pozorované náhodné proměnné Et

Resene ulohy:
 - Odhad stavu (filtrace): cílem je zjištění pravděpodobnosti aktuálního stavu na základě dosavadních pozorování
 - Predikce: cílem je zjištění pravděpodobnosti budoucího stavu na základě dosavadních pozorování
 - Vyhlazování: cílem je zjištění pravděpodobnosti minulého stavu na základě dosavadních pozorování
 - Nejpravděpodobnější průchod: na základě posloupnosti pozorování chceme zjistit nejpravděpodobnější posloupnost stavů, která tato pozorování generuje


----

Markovský rozhodovací proces (MDP)

sekvenční rozhodovací problém v plně pozorovatelném stochastickém prostředí

Ve stochastickém prostředí nemůžeme pracovat s pevným pořadím akcí (plánem)

Řešením MDP je strategie (policy) π(S), což je funkce určující pro každý stav doporučenou akci (hledáme strategii s největším očekávaným užitkem = optimální strategie)

Iterace Hodnot - vyuziva bellmana

iterace strategie, ktera je založena na opakovani 1. evaluace strategie 2. zlepseni strategie

---

pasivni/aktivni senzory

Efektory umožňují robotovi pohyb a změnu tvaru těla
Aktuátor/akční člen (actuator) zahajuje pohyb efektoru
Stupeň volnosti umožňuje pochopit návrh efektoru

----


Dynamická Bayesovská síť (DBN) reprezentuje temporální pravděpodobnostní model


skládá se z opakujících se vrstev proměnných:
 - stačí tedy popsat první vrstvu
 - apriorní distribuci P(X0)
 - přechodový model P(X1|X0)
 - senzorický model P(E1|X1)

Dynamická Bayesovská síť reprezentuje přechodový model (model pohybu) a senzorický model v částečně pozorovaném prostředí

---

Pracovni prostor - klasika tak jak ho vidime, problem je ze ne vsechny souradnice jsou dostupne
robotem

Konfiguracni prostor
 - reprezentace pomoci robotovych kloubu
 - plánování cesty: spojíme aktuální pozici a cíl rovnou čarou a robot se po ní pohybuje konstatní rychlostí, dokud nedorazí do cíle
 - muze vznikam redudance, dve stejne konfigurace

Konfiguracni prostor s prekazkami muzeme ziskat pomoci minkowskeho sumy

----
Spojitá reprezentace konfiguračního prostoru -> diskretizace -> prohledavani grafu

Bunkova dekompozice: rozdelime prostor na nekolik bunek, ktere jsou prazdne, obsazene, castecne
obsazene

Castecne obsazene bunky bud neprochazime, prochazime, zvetsime rozliseni nebo adaptivni diskretizace

-----

Cestovní mapa jako graf viditelnosti (visibility graph)

- Spojíme všechny páry vrcholů plus iniciální a cílové konfigurace
- Eliminujeme hrany, které protínají překážky
- Graf viditelnosti vždy zahrnuje nejkratší cestu konfiguračním prostorem

Cestovni mapa: Voroneho diagram

- dělí prostor R2 na oblasti podle zadaných objektů, např. bodů x ∈M
- proste takovy ty dilky, kazda jinou velikot i tvar, v kazde je jeden bod
Cestovní mapa jako VD, který maximalizuje vzdálenost od překážek

- Robot změní konfiguraci na bod ve VD
- Robot se pohybuje ve VD, dokud nedosáhne bod, ktery je nejbližší cílové konfiguraci
- Robot opustí VD a přesune se do cíle

Graf viditelnosti vs. Voroného diagram

Graf viditelnosti
- nejkratší cesta, ale blízko k překážkám nutno uvažovat bezpečnost cesty
- komplikované ve vyšší dimenzi

Voroného diagram
- maximalizuje vzdálenost od překážek, což poskytuje konzervativní cesty
- malé změny překážek mohou vést k velkým změnám VD
- komplikované ve vyšší dimenzi


Vertikální dekompozice(Exaktní buňková dekompozice): bunkova dekompozice ale bunky maji full vysku. rozkrajeny vertikalne

Oktalová dekompozice: Metoda přibližné buňkové dekompozice


---

Potenční funkce

Prvotní použití: cesta by neměla vést těsně vedle překážky  
Řešení: zavedeme dodatečnou cenovou funkci, tzv. potenční funkce
 
Náhodné vzorkováni pro blizke prekazky, uzke pasaze atd.


Pravděpodobnostní cestovní mapa – probabilistic roadmap

Diskrétní reprezentace spojitého konfiguračního prostoru generována náhodným vzorkováním konfigurací v Cfree, které spojíme do grafu

Více dotazů na pravděpodobnostní cestovní mapu
 - generování jedné cestovní mapy, která je používána pro plánovací dotazy vícekrát
Jeden dotaz na pravděpodobnostní cestovní mapu
 - pro každý plánovací problém konstruována nová cestovní mapa charakteristická pro podprostor konfiguračního prostoru
 - RRT

Strategie pro více dotazů
 - ucici se faze : vzorkovani 
 - dotazovaci faze: Spojení počáteční a cílové konfigurace s PRM


----

Rapidly exploring random tree (RRT)

 - Algoritmus pro jeden dotaz
 - Motivací je hledání cesty založené na řízení
 - Inkrementální konstrukce grafu (stromu) směrem k cílové oblasti


vlastnosti:

- Rychle prozkoumává prostor
- RRT nalezne proveditelnou cestu bez garance kvality

postup:






