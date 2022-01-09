---
title: algos
url: ai/exam
---

# k-opt

TODO

# k-distance

TODO

# Ejection Chain

- řetězec odstranění: posloupnost přesunů zákazníka z jednoho okruhu na následující
- úspěšná změna: žádný vrchol není v řešení více než jednou
- řetězec odstranění nemusí být cyklický (stačí umístit konzistentně posledního zákazníka do posledního okruhu)

## postup
- každý řetězec odstranění zahrnuje k úrovní začínajících na okruhu 1 a končících na okruhu k
- vrchol je odstraněn z okruhu 1 a přesunut na okruh 2, vrchol z okruhu 2 přesunut na okruh 3, atd. až vrchol z k-1 na k, poslední vrchol z okruhu k přesunut do okruhu 1

# Cyclic Exchange

prvky mají být rozděleny do skupin S = {S1,...,Sq}  
cyklická výměna 3 prvků (3-okolí): prvek a2 ∈S2 je přesunut do S3, a3 ∈S3 je přesunut do S4, a4 ∈S4 přesunut do počáteční skupiny S2

# Treshold accepting

akceptovana i horsi reseni s maximalnim zhoresenim o prahovou hodnotu Q 

# Great Deluge

algoritmus je uveden klasicky pro minimalizacni problemy tj. hladinu(level) musimem redukovat a snazime se zustat pod LEVEL;

## postup:
 - init reseni, rychlost deste (UP), vodni hladina
 - generuj soused, akceptuj pokud pod level, sniz hladinu o UP a znovu
 - // UP je kriticky, pokud je moc vysoky - budeme prilis moc omezeni a nebudeme akceptovat reseni, pokud moc nizky - budeme akceptovan kazdou blbost -> bude trvat dlouho


# Tabu Prohledavani
- udrzujeme seznam poslednich zmen - tabu seznam, iterujeme a akceptujeme kazdeho vygenerovaneho souseda ktery neni v tabu seznamu
- řešení horší/stejné kvality akceptováno, pokud neexistuje lepší
- často kombinováno i s dalšími algoritmy

## Aspiracni kriterium

podmínka, za které je možné realizovat i změny z tabu seznamu, např. povolení změn, které vedou k lepší hodnotě účelové funkce


# Iterativní lokální prohledávání
 - Multistart local search -  iniciální řešení je generováno při další iteraci náhodně
 - Iterativní lokální prohledávání - nalezené lokální optimum změněno a použito při dalším lokálním prohledávání


# Prohledávání s proměnlivým okolím, (variable neighborhood search, VNS)

myslenka je takova ze misto abych porad prohazoval 1 predmet, tak muzu prohodit 2, 3 nebo vice.

# Zlepšující prohledávání s proměnlivým okolím (variable neighborhood descent algorithm, VND)

VND je deterministická verze VNS  

## postup
 - zaciname na nejmensim moznem okoli a postupujeme k maximalnimu moznemu okoli
 - pokud najdeme lepsiho souseda jdeme zpatky na zacatek
 - pokud ne rozsirime okoli
 - pr. rozvrh - zkusime prohodit 2 predmety, pokud nepomuze zkusime prohodit 3, pokracujeme do MAX. pokud najdeme vhodneho souseda zacine od znovu a opet to stejny



# Řízené lokální prohledávání - guided local search, GLS

- Opakovaná lokální prohledávání s upravenou účelovou funkcí
- nova ucelova fce: f'(s) = f(s) + \lambda \sum p_i I_i(s)
- Každé řešení s ∈S má množinu m charakteristik i s cenou c_i
- I_i (s) = 1 pokud s ma charakteristiku i jinak 0
- snaha o prohledávání částí stav. prostoru s nižší cenou charakteristik
- př. problém obchodního cestujícího: zda je hrana (a,b) v řešení, cenu určuje délka hrany (vzdálenost měst)
- penalizace pi : význam charakteristiky (vysokou penalizaci nechceme)


## Charakteristika
 - Charakteristika i s nejvyšším hodnotou u_i(s) = I_i (s) = c_i / (1 + p_i)
 - chceme se příště vyhnout charakteristikám s vysokou cenou ci
 - charakteristiky použité v řešení penalizovány pro podporu diversifikace

## Intensifikace

GLS prohledává stavový prostor s nižšími cenami ci

## Diversifikace

GLS penalizuje charakteristiky použité ve vygenerovaném lokálním optimu, abychom se jim vyhnuli


Příklad: TSP a GLS

# Metaheuristiky s populacemi
 - algoritmy využívající evoluci
 - algoritmy s pameti (blackboard)

Společné koncepty: generování počáteční populace
 - Náhodné generování
 - Sekvenční diversifikace - 
 - Paralelní diversifikace - řešení generována nezávisle paralelně se snahou o celkovou maximální odlišnost řešení v populaci
 - Heuristická inicializace - jednotlivá řešení generována libovolnými heuristickými algoritmy


Společné koncepty: podmínky ukončení
 - Statická procedura - pevný počet iterací
 - Adaptivní procedura - pevný počet iterací bez zlepšení


Základní koncepty evolučních algoritmů:
 - Reprezentace
	- populace
	- chromozom/jedinec
	- gen
	- alely
 - Vhodnost (fitness) - používaný termín pro účelovou funkci 
 - Strategie vyberu - rodičů (řešení) pro vytváření další populace
 - Strategie reprodukce - křížení a mutace: operace vytvářející nové jedince (potomky)
 - Strategie nahrady - výběr jedinců do nové populace


# Evoluční algoritmy

- Genetické algoritmy
- Evoluční strategie
- Evoluční programování - spojitá optimalizace
- Genetické programování - jedinci jsou programy


# Genetické algoritmy
 - Typicky použití operátoru křížení nad dvěma řešeními
 - Mutace využívána pro zlepšení diversifikace
 - Pevna pravdepodobnsot mutace p_m krizeni p_c
 - Náhrada bývá generační: rodiče systematicky nahrazeni potomky


# Evoluční strategie (ES)
 - Většinou pro: spojité optimalizace, vektory reálných hodnot
 - Křížení využito zřídka ⇐ i pro problémy, kde nemáme vhodné křížení
 - Obvykle: náhrada nejlepšími jedinci (elitismu)
 - Populace rodičů velikosti μ, populace potomků velikosti λ ≥ μ

nahrady:
 - (1 + 1)-ES: jednoduchá verze, 1 rodič nahrazen 1 potomkem 
 - (μ + λ)-ES: opakuj λ-krát: (náhodný výběr rodiče, vygenerován potomek); seřazení μ rodičů a λ potomků dle vhodnosti, náhrada nejlepšími
 - (μ,λ)-ES: pro novou populaci se vybírá jen mezi λ potomky


# Výběr ruletovým kolem
 - nejpoužívanější strategie výběru
 - fi vhodnost jedince i v populaci
 - pravděpodobnost výběru jedince dána jako p_i = f_i / \sum f_i f_j
 - analogie: ruletové kolo s díly pro všechny jedince v populaci; velikost dílu ruletového kola pro jedince odpovídá pi
 - Problémy: příliš velká snaha vybírat kvalitní jedince ⇒ předčasná konvergence


# Pravděpodobnostní univerzální vzorkování

řeší problémy rulet.kola
 - u ruletového kola dáme μ rovnoměrně rozložených ukazatelů
 - jedno otočení ruletového kola vybírá μ jedinců

# Turnajový výběr, výběr rankováním
 - náhodný výběr k jedinců
 - turnaj: z těchto k jedinců je výbrán nejlepší jedinec
 - pro výběr μ jedinců aplikujeme turnaj μ-krát

# Výběr rankováním (rank-based selection)
 - pro každého jedince spočítán rank a dle něj jsou vybíráni jedinci
 - rank může např. škálovát linerárně se závislostí na snaze o výběr nejlepšího jedince
 - rank použit pro výpočet pravděpodobnosti a aplikován stejně jako u ruletového kola


# Mutace
- operátor mutace mění jedince v populaci a způsobí jeho malou změnu
- pravděpodobnost mutace genu pm ∈[0.001,0.01]
- př. inicializace pm na 1/k, kde k je počet genů (rozhodovacích proměnných), tj. v průměru zmutovaná 1 proměnná

**Mutace v binární reprezentaci** - prohození (flip) hodnoty binární proměnné
**Mutace v diskrétní reprezentaci** - změna hodnoty prvku za jinou hodnotu v abecedě
**Mutace v permutacích** - vložení, výměna, inverze hodnot(y)


# Křížení
 - binární (někdy n-ární) operátor
 - cil: zdědit vlastnosti rodičů potomkem
 - pravděpodobnost křížení rodičů pc ∈[0,1], běžně pc ∈[0.45,0.95]


## Linerární reprezentace (vyjma permutací)

**1-bodové křížení (1-point crossover)** - podle vybrané pozice k v potomcích prohozeny hodnoty dvou rodičů
**2-bodové (a n-bodové) křížení** - vybrány dvě (n) pozice a provedeno prohození hodnot
**uniformní křížení (uniform crossover)**
 - jedinci kombinováni bez ohledu na velikost segmentů;
 - každý gen potomka náhodně vybrán z rodiče;
 - každý rodič rovnoměrně přispívá ke generování potomků stejně


## Reprezentace permutacemi
křížení je složitější, jedince nelze takto jednoduše kombinovat, protože každá alela (hodnota) se musí výskytnout v jedinci právě jednou (používány různé formy mapování)

**Křížení dané pořadím (Order crossover, OX)**
 - vybrány náhodně dva body křížení
 - z rodiče 1 hodnoty mezi nimi zkopírovány na stejné pozice v potomkovi
 - z rodiče 2 začneme od druhého bodu křížení vybírat prvky, které již nebyly vybrány z rodiče 1, a dávame je do potomka od 2. bodu křížení


# Strategie náhrady

Vybíráme mezi rodiči a potomky další populaci

## Extrémní strategie náhrady (nepříliš používané)
 - úplná náhrada (generational replacement)
	- potomky bude nahrazena systematicky celá populace rodičů
	- ztrácíme i nejlepší jedince
 - náhrada jednotlivce (steady-state replacement)
	- bude vytvořen pouze jediný potomek, který nahradí např. nejhoršího jedince populace
	- tj. degradace genetických algoritmů, otázka smyslu práce s populací

## Používány strategie na pomezí mezi těmito krajními přístupy
 - náhrada pevného množství jedinců
	 - pro náhradu vybíráno λ jedinců populace při velikosti populace μ
	 - `1 < λ μ`
 - elitářský model
	- výběr nejlepších jedinců mezi rodiči a potomky
	- rychlá avšak předčasná konvergence
	
	
# Inteligence hejna (swarm intelligence)

Algoritmy inspirované skupinových chováním druhů jako jsou mravenci, včely, vosy, termiti, ryby nebo ptáci  
Původ v sociální chování těchto druhů při hledání potravy  
Základní charakteristika algoritmů:
 - jedinci jsou jednodušší nesofistikovaní agenti
 - jedinci kooperují nepřímo pomocí média


# Optimalizace mravenčí kolonie (Ant Colony Optimization, ACO)
 - Myšlenky inspirující algoritmus
  - mravenčí kolonie schopna najít nejkratší cestu mezi dvěma body
  - mravenci během cesty nechávají na zemi chemickou stopu (feromony)
  - feromony vedou mravence v cíli
  - feromony se postupně vypařují
 - Algoritmus
  - inicializace feromonů
  - iterace: konstrukce řešení mravencem, aktualizace feromonů

Feromonové informace:
 - τ typicky jako matice/vektor hodnot obsahující feromonovou stopu
 - př. matice jako reprezentace grafu obsahuje feromony na hranách
Vypařování feromonů:
 - τ_ij = (1 −ρ)τ_ij realizuje pro každé i,j vypařování feromonů
 - ρ ∈[0,1]
Zesilovani feromonu:
 - online aktualizace
  - τij aktualizováno v každém kroku
 - online pozdržená aktualizace
  - τ aktualizováno po nalezení úplného řešení jedním mravencem
  - př. čím lepší řešení, tím více feromony zesíleny
 - off-line aktualizace
  - τ aktualizováno po nalezení úplného řešení všemi mravenci
  - nejpopulárnější přístup
  - př. aktualizace feromonů dle kvality (feromony aktualizovány dle nejlepšího (nebo několika nejlepších) řešení)



# Plánování v kostce: klasické plánování
Vstup:
 - počáteční (současný) stav světa
 - popis akcí schopných měnit stav světa
 - požadovaný stav světa
Vystup: 
 - seznam akcí (plán)

klasické plánování: 
 - Stavové proměnné
 - Počáteční stav
 - Cílový stav
 - Akce a.k.a. operátory

STRIPS plánování: Všechny proměnné mají doménu {T,F}

# Plánování a rozvrhování

Plánování (planning)
 - rozhodování, jaké akce jsou potřeba pro dosazeni danych cilu
 - složitost: často horší než NP-úplné

Rozvrhování (scheduling)
 - rozhodování, jak zpracovat dané akce použitím omezených zdrojů a času
 - složitost: typicky NP-úplné


Plánování: rozhodnutelnost
 - PlanSAT: Existuje plán, který řeší zadaný plánovací problém?
 - BoundedPlanSAT: Existuje plán délky k nebo kratší, který řeší zadaný plánovací problém?

Oba problémy rozhodnutelné pro klasické plánování `<=` pocet stavu je konecny

Přidání funkčních symbolů do jazyka:
 - počet stavů je nekonečný
 - PlanSAT částečně rozhodnutelný
  - existuje algoritmus, který skončí pro řešitelné problémy
  - pro neřešitelné problémy nemusí skončit
 - BoundedPlanSAT zůstává rozhodnutelný



## Formalizace: konceptuální model

Plánování se zabývá volbou a organizací akcí, které mění stav systému

Systém Σ modelující stavy a přechody:
 - množina stavů S (rekurzivně spočetná)
 - množina akcí A (rekurzivně spočetná)
  - plánovač kontroluje akce!
  - no-op (prázdná akce)
 - množina událostí E (rekurzivě spočetná)
  - událost mimo kontrolu plánovače!
  - neutrální událost ε
 - přechodová funkce γ : S ×A ×E →P(S)
  - někdy se akce a události aplikují odděleně γ : S ×(A ∪E) → P(S) 

## Cíle plánování

Cílem plánování je zjistit, jaké akce a na které stavy se mají aplikovat, abychom za dané situace dosáhli požadovaných cílů

Co je cílem plánování?
 - cílový stav nebo množina cílových stavů
 - splnění dané podmínky nad posloupností stavů, přes které systém prochazi
  - např. stavy, kterým se vyhnout, nebo stavy, které se musí navštívit
 - optimalizace dané objektivní funkce nad posloupností stavů
  - např. maximum nebo součet ohodnocení stavů 

- Plánovač generuje plány
- Řadič se stará o jejich realizaci
-  - pro daný stav určí akci k provedení
-  - pozorování převádějí reálný stav na modelovaný stav
- Dynamické plánování - umožňuje přeplánování na základě aktuálního stavu provádění


# STRIPS plánování

Pracujeme s deterministickým, statickým, konečným a plně pozorovatelným stavovým modelem s omezenými cíli a implicitním časem Σ = (S,A,γ).

Plánovací problém P = (Σ,s0,g):
 - s0 je počáteční stav
 - g charakterizuje cílové stavy

Řešením plánovacího problému P je posloupnost akcí 〈a1,a2,...,ak>


# Klasické plánování: množinová reprezentace

Stav systému je popsán množinou výroků

Každá akce je syntaktický výraz specifikující:
 - jaké výroky musí patřit do stavu, aby na něj byla akce aplikovatelná
 - jaké výroky akce přidá a jaké výroky smaže, aby vytvořila nový stav


Klasická reprezentace zobecňuje množinovou reprezentaci směrem k predikátové logice:
 - stavy jsou množiny logických atomů (místo výroků u množ.rep.), které jsou v dané interpretaci buď pravda nebo nepravda
 - akce jsou reprezentovány plánovacími operátory, které mění pravdivostní hodnotu těchto atomů


Přesněji:
 - L (jazyk) je konečná množina predikátových symbolů a konstant (nemáme funkce!)
 - atom je predikátový symbol s argumenty napr. on(c3, c1)
 - můžeme používat proměnné napr. on(x, y)


Reprezentace stavů:
 - Stav je množina instanciovaných atomů (bez proměnných).
 - Pravdivostní hodnota některých atomů se mění
	 - flexibilní atomy (fluent) napr. at(r1, loc1)
 - Některé atomy nemění svoji pravdivostní hodnotu s různými stavy
	- neměnné atomy (rigid) napr. adjacent(loc1,loc2)


Předpoklad uzavřeného světa (closed world assuption): atom, který není ve stavu explicitně uveden, neplatí

Plánovací operátory
Operátor o je trojice: (name(o), precond(o), effects(o))
 - name(o): jméno operátoru ve tvaru n(x1,...,xk)
  - n je identifikator
  - x1 az xk jsou argumenty
 - precond(o): předpoklady - literály, které musí být splnitelné, aby šlo operátor použít
 - effects(o): důsledky - literály, které se stanou pravdivými aplikací operátoru

## Akce

Akce jsou plně instanciované operátory - za proměnné jsou dosazeny konstanty

Notace:
 - S+ = {pozitivní atomy v S}
 - S− = {atomy, jejichž negace je v S}

## Planovaci domena

Nechť L je jazyk a O je množina operátorů.  
Plánovací doména Σ nad jazykem L a s operátory O je trojice (S,A,γ):
 - stavy S ⊆ P({všechny instanciované atomy nad L})
 - akce A = {všechny instanciované operátory z O nad L}
 - přechodová funkce γ:
	 - γ(s,a) = (s −effects−(a)) ∪effects+(a), je-li a použitelná na s

## Plánovací problém

Plánovací problém P je trojice (Σ,s0,g):
 - Σ = (S,A,γ) je plánovací doména
 - s0 je počáteční stav, s0 ∈S
 - g ⊆L je množina instanciovaných literálů

Zápis plánovacího problému je trojice (O,s0,g)
Plán π je posloupnost akcí 〈a1,a2,...,ak
Plán π je řešením P, právě když γ(s0,π) splňuje g


4 lec
----

# Plánování se stavy

Prohledávaný prostor odpovídá stavovému prostoru plánovacího problému
 - uzly odpovídají stavům
 - hrany odpovídají stavovým přechodům pomocí akcí
 - cílem je najít cestu mezi počátečním stavem a některým koncovým stavem

Typy prohledavani:
 - dopředné (forward search)
 - zpětné (backward search) (liftovana verze, STRIPS)
 - problémově závislé (svět kostek)


# Dopředné plánování
Začínáme v počátečním stavu a jdeme k některému cílovému stavu

Je potřeba umět:
 - rozhodnout, zda je daný stav cílový nebo ne
 - najít množinu akcí aplikovatelných na daný stav
 - vypočítat stav, do kterého se dostaneme aplikací akce

## Postup
 - 1. prazdny plan P a pocatecni stav
 - 2.  pokud splnujeme g vratime plan P jinak iterujeme
 - do E si ulozime vsechny akce ktere splnuji preconds
 - z E deterministicky vybereme jednu akci A
 - aplikuje A a ulozime ji do planu P
 - opakujeme od 2

## Vlastnosti
 - Procedura dopředného plánování je korektní (pokud vrátí nějaký plán, potom je řešením)
 - Procedura dopředného plánování je úplná
  - pokud existuje plán potom ho alespoň jedna z nedeterministických větví najde
  - indukcí podle délky plánu
  - v každém kroku má algoritmus šanci zvolit správnou akci (pokud v přechozích krocích volil akce z plánu)

# Deterministické implementace

Algoritmus dopředného prohledávání můžeme implementovat deterministicky:
 - prohledávání do šířky (korektní, úplné, ale paměťově náročné)
 - prohledávání do hloubky (korektní, úplnost lze zajistit kontrolou cyklů)
 - A* algoritmus (nejčastěji používaný přístup)

## Větvení

Vysoký větvící faktor: počet možností k výběru - to vadí u determinismu, který může ztrácet čas zkoušením irelevantních akcí

Řešení:
 - heuristika doporučující výběr akce
 - ořezání prohledávacího prostoru


# Zpětné plánování

Začínáme s cílem (pozor to není stav, ale reprezentace množiny stavů!) a jdeme přes podcíle k počátečnímu stavu

Je potřeba umět:
 - zjistit, zda daný stav odpovídá cíli
 - pro daný cíl najít relevantní akce
 - vypočítat podcíl umožňující aplikovat danou akci

> myslenka je takova, ze relevantni akce obsahuji cil nebo jeho casti v efektech

akce je relevantni pro cil g prave kdyz:
 - akce přispívá do g: g ∩ effects(a) != ∅
 - efekty akce nejsou v konfliktu s g:
  - g− ∩ effects+ = ∅
  - g+ ∩ effects- = ∅


Regresní (zpětná) množina cíle g pro (relevantní) akci a: γ−1(g,a) = (g − effects(a)) ∪ precond(a)

## Postup
 - 1. prazdny plan P
 - 2. vrat plan pokud s0 splnuje g jinak iteruj
 - vyber akci a pro kterou je definovano γ−1(g,a)
 - nedeterministicky vyber akci a, aplikuj g = γ−1(g,a) a pridej a do planu P

## Vlastnosti
 - Procedura zpětného plánování je korektní a úplná
 - Můžeme ji implementovat deterministicky (pro úplnost potřebujeme detekci cyklů)

## Větvení
 - může být menší než u dopředného plánování (zacílení)
 - pořád ale zbytečně velké
  - Chceme-li, aby byl robot v pozici loc51, do které existují cesty z loc1, . . . , loc50, dostaneme 50 možných podcílů. Nám je ale pro splnění cíle jedno, odkud robot příjel!
  - Částečné instanciování akcí (místo úplného) dále zmenší velikost větvení, tzv liftování (lifting).

## Zpětné plánování - Liftovaná verze
 - o je kopie operátoru s přejmenovanými (=novými) proměnnými
  - napr. misto move(1,2), ..., move(1, n), udelame move(1, l)
 - MGU = největší společný unifikátor, tj. nejobecnější substituce atomů
 - použití volných proměnných zmenšuje větvení, ale komplikuje detekci cyklů

## Postup
 - 1. prazdny plan P
 - 2. pokud s0 splnuje g vrat P jinak iterace
 - A = {(o | θ) - substituce θ je MGU atomu v g a atomu v effects(o) a γ−1(θ(g),θ(o)) je definováno)
 - nedeterministicky vyber z A
 - P = spojení θ(o) a θ(P)
 - g = γ−1(θ(g),θ(o))


TODO ^


# STRIPS

Dosud probrané plánovací algoritmy sdílejí stejný problém – jak zlepšit efektivitu redukcí prohledávacího prostoru

STRIPS algoritmus redukuje prohledávaný prostor zpětného plánování, a to takto:
 - z podcílů řeší vždy jen část odpovídající předpokladům poslední přidané akce:
  - tj. místo γ−1(s,a) se jako nový cíl použije precond(a)
  - vede k neúplnosti algoritmu
 - pokud aktuální stav splňuje všechny předpoklady operátoru, daný operátor se použije a tento závazek nebude rušen při backtrackingu



# Sussmanova anomálie

Pravděpodobně nejznámější problém, který STRIPS neumí efektivně řešit (najde pouze redundantní plány)

mame kostky: s0: acb a g: cba -> odebereme b z vrchu -> v cili ma byt b na c, takze b ktere jsme odebrali dame zpet na c. tim ale nikdy
nedosahneme toho aby a bylo navrchu

reseni:
 - prolínání plánů
  - plánování v prostoru plánů
 - použití doménově závislé informace
  - Kdy má problém ve světě kostek řešení?
   - v cíli nesmí být kostky, které nejsou v počátečním stavu
   - kostka nesmí najednou stát na dvou jiných kostkách

# Plánování v prostoru plánů

## Overview pro planovani se stavovym prostorem

Prakticky celou dobu pracujeme s castecnym planem. (A, `<`, B, L),
 - A jsou operatory
 - `<` je usporadani, tzn. nemuzu polozit kostku kdyz jsem ji nevzal, takze usporadam akce take, put
 - B, mnozina vazeb, tzn auto a patri do domeny aut A, a \in A 
 - L je mnozina kauzalnich vztahu, tzv kdyz auto nekam prijede, tak musi rovnou nalozit, nedava smysl aby prijelo a hned odjelo, takze vazba mezi
	 move a load

Otevreny cil je predpoklad nejakeho operatoru ktery nevime jak splnit; potrebuju splnit vsechny otevrene cile.
Hrozba je akce ktera muze porusit kauzalni vazbu.
Resici Plan je castecny plan ktery je cil.



## planovani

Princip podobný zpětnému plánování ve stavovém prostoru
 - začínáme z „prázdného plánu” obsahujícího popis počátečního stavu a cíle
 - přidáváme další akce, které plní dosud nesplněné (otevřené) cíle
 - případně přidáváme vazby mezi již přítomnými akcemi

Na plánování se můžeme dívat jako na opravování kazů v částečném plánu:
 - přecházíme od jednoho částečného plánu k dalšímu, dokud nenajdeme úplný plán

Možné úpravy plánu:
 - přidání akce
 - svázání proměnných
 - přidání podmínky uspořádání
 - přidání kauzální (příčinné) vazby

Počáteční stav i cíl zakódujeme jako speciální akce, které jsou v prvotním částečném plánu:
 - akce a0 reprezentuje počáteční stav tak, že nemá žádné předpoklady a počáteční stav je zakódován jako efekt;
 - akce a∞ reprezentuje cíl, který je zakódován jako předpoklad, efekt akce je prázdný; tato akce je za všemi ostatními akcemi


Plánování bude založeno na odstraňování kazů (flaws) v částečném plánu:
 - budeme přecházet od jednoho částečného plánu k dalšímu dokud nenajdeme řešící plán


## Uzly jsou plány

Uzly prohledávaného prostoru jsou tvořeny částečnými plány

Částečný plán Π je čtveřice `(A,<,B,L)`, kde:
 - A je množina částečně instanciovaných plánovacích operátorů {a1,...,ak}
 - `<` je částečné uspořádání na A (ai `<` aj)
 - B je množina vazeb tvaru x = y,x != y nebo x ∈ Di
 - L je množina kauzálních vztahů tvaru (ai p→ aj)
  - ai ,aj jsou akce uspořádané ai `<` aj
  - p je výraz, který je efektem ai a předpokladem a
  - v B jsou vazby svazující příslušné proměnné v p

## Otevřený cíl
Otevřený cíl (open goal) je kazem plánu  

Jedná se o předpoklad p nějakého operátoru b, o kterém zatím nebylo rozhodnuto, jak ho splnit (neexistuje kauzální vazba ai p→ b)

Odstranění otevřeného cíle p akce b:
 - najdi operátor a (buď již přítomný v plánu nebo nový), který lze použít na splnění p (má p mezi efekty a může být před b)
 - svaž proměnné
 - vytvoř kauzální vazbu


## Hrozba
Hrozba (threat) je dalším kazem plánu

Jedná se o akci, která může porušit kauzální vazbu:
 - přesněji, je-li ai p→ aj kauzální vazba a akce b ma efekt unifikovatelný s negací p a může se nacházet mezi ai a aj, potom je b hrozbou

Odstranění hrozby lze udělat třemi způsoby:
 - uspořádání b před ai
 - uspořádáním b za aj
 - navázáním proměnných v b tak, že neruší platnost p


## Řešící plán

Částečný plán `Π = (A,<,B,L)` je řešícím plánem pro problém P = (Σ,s0,g), pokud:
 - částečné uspořádání `<` a vazby B jsou globálně konzistentní
 - libovolná lineárně uspořádaná posloupnost plně instanciovaných akcí A splňující `<` a vazby B vede z s0 do stavu splňujícího g

Definice nám bohužel přímo nedává výpočtovou proceduru, jak ověřit, zda je plán řešící!


# Algoritmus plánování v prostoru plánů (PSP)

postup:
 - vstupem je plan P
 - kazy = otevrene cile P + hrozby P
 - pokud nejsou zadne kazy pak vratime P
 - vybereme libovolny kaz z P
 - zjemnění Z je mnozina moznosti jak odstranit kaz
 - nedeterministicky vybereme p \in Z
 - P' = aplikujeme p
 - vratime PSP(P')

Determinismus:
 - volba kazu je deterministická - musí se odstranit všechny kazy
 - volba zjemnění je nedeterministická - v případě neúspěchu se zkouší další alternativa 

## Podrobnosti k algoritmu PSP

- Otevřené cíle lze efektivně zjistit udržováním agendy předpokladů akcí
 - přidání kauzální vazby pro p vyřadí p z agendy
- Všechny hrozby lze najít prozkoumáním všech trojic akcí nebo inkrementálně
 - po přidání akce se zjistí, komu je hrozbou
 - a po přidání kauzální vazby se ověří její hrozby

- Pro odstranění otevřených cílů a hrozeb se používají pouze konzistentní zjemnění plánu
 - konzistence uspořádání buď detekcí cyklů nebo lépe udržováním tranzitivního uzávěru 
 - konzistence vztahů B
  - pokud není negace, lze rychle například pomocí hranové konzistence
  - je-li přítomna negace, jedná se o NP-úplný problém

## Vlastnosti PSP
 - Algoritmus PSP je korekní a úplný
 - Pozor na deterministickou implementaci
 - prostor plánů není konečný
 - úplná deterministická procedura musí garantovat prohledání všech plánů dané délky


# Algoritmus PoP

- PoP je konkrétní (a populární) instance algoritmu PSP
- agenda je množina dvojic (a,p), kde p je otevřený předpoklad akce a
- nejprve hledá akci ai pro pokrytí nějakého p z agendy
- ve druhé fázi řeší všechny hrozby, které vznikly přidáním akce ai , resp. kauzální vazby s ai

## Postup

- PoP(P, agenda) , kde `P = (A, <, B, L)`
- pokud je agenda prazda vrat P, jinak vyber libovolny par (a_j, p) a smaz ho z agenda
- relevant = pokry_predpoklad(p, P)
- nedeterministicky vyber akci ai ∈ relevant;
- L = L ∪{〈ai p→ aj 〉};
- aktualizuj B se svázanými omezeními této kauzální vazby;
- pro kazdou hrozbu v〈ai p→ aj 〉nebo kvůli ai
 - zjemneni = množina možností odstraňující tuto hrozbu 
 - nedeterministicky vyber p ∈ zjemnění
 - přidej p do `<` nebo do B;
- return PoP(P, agenda)

# Srovnani planovani se stavy/plany

Díky doménově specifickým heuristikám je dnes plánování se stavy výrazně rychlejší.

Ale, plánování v prostoru plánů:
 - vytváří flexibilnější plány díky částečnému uspořádání
 - umožňuje další rozšíření, např. přidání času a zdrojů


|  | Plánování se stavy | Plánování s plány |
|---|---|---|
| prohled. prostor | konečný | nekonečný |
| uzly | jednoduche (stavy světa) | komplikovanější (částečné plány) |
| stavy světa | explicitní | nejsou |
| částečný plán | uspořádání a volba akcí se dělá najednou | volba akcí a jejich pořadí oddělené |
| struktura plánu | lineární bez vazeb | kauzální vazby |


# Neurčitost: Bayesovské sítě

Podmíněná pravděpodobnost: P(x|y) = P(x ^ y)/P(y)

Podmíněnou pravděpodobnost často zapisujeme v podobě součinového pravidla:
`P(x∧y) = P(x|y)×P(y)
P(X,Y ) = P(X|Y ) ×P(Y)`

(Úplná) nezávislost: náhodné proměnné jsou na sobě nezávislé:

P(X|Y) = P(X) nebo P(Y|X) = P(Y) nebo P(X,Y) = P(X)P(Y)

Pravděpodobnosti elementárních jevů můžeme popsat tabulkou tzv. úplnou sdruženou distribucí

Chceme-li znát pravděpodobnost nějakého tvrzení, sečteme pravděpodobnosti všech „světů”, kde tvrzení platí (marginalizace)

\\( P(Y) = \sum_{z \in Z} P(Y, z) \\)


## Diagnostická vs. kauzální vazba

Odhalení zdrojů dle symptomů, tj. diagnostická vazba
Z analýzy předchozích nemocí, spíš však máme k dispozici
 - pravděpodobnost nemoci P(nemoc)
 - pravděpodobnost symptomu P(symptom)
 - kauzální vztah nemocí a symptomu P(symptomy|nemoc)


# Bayesovská síť (BS)

- Zachycuje závislosti mezi náhodnými proměnnými
- Orientovaný acyklický graf (DAG)
 - uzel odpovídá náhodné proměnné
 - předchůdci uzlu v grafu se nazývají rodiče
 - každý uzel má přiřazenu tabulku podmíněné pravděpodobnostní distribuce P(X| Parents(X))

## Modelová situace  

- Máme v domě zabudovaný alarm, který se spustí při vloupání ale někdy také při zemětřesení
- Sousedi Mary a John slíbili, že vždy, když alarm uslyší, tak nám zavolají
- Zajímá nás pravděpodobnost vloupání, pokud John i Mary volají
- Náhodné boolovské proměnné reprezentují možné události
- Pravděpodobnostní tabulky reprezentují vztah podmíněné


Bayesovská síť kompaktním způsobem reprezentuje úplnou sdruženou distribuci
(popisuje pravděpodobnost všech elementárních jevů)

P(x1,...,xn) = ∏_i P(xi |parents(Xi))

Zpětně lze ukázat, že tabulky P(X|Parents(X)) jsou podmíněné
pravděpodobnosti podle výše uvedené sdružené distribuce

Protože úplnou sdruženou distribuci lze použít pro odpověď na libovolnou
otázku v dané doméně, lze stejnou dopověď získat z Bayesovské sítě
(marginalizací)


## Jak konstruovat Baysovské sítě?

Rozepíšeme P(x1,...,xn) pomocí tzv. řetězcového pravidla

## Uzly

- funguje libovolné uspořádání, ale pro různá uspořádání dostaneme různě kompaktní site
- doporučené uspořádání je takové, kdy příčiny předcházejí efekty

## Hrany

bereme proměnné Xi v daném pořadí od 1 do n

- v množině {X1,...,Xi−1} vybereme nejmenší množinu rodičů Xi tak, že platí P(Xi |Parents(Xi )) = P(Xi |Xi−1,...X1)
- z rodičů vedeme hranu do Xi
- vypočteme podmíněné pravděpodobnostní tabulky P(Xi |Parents(Xi ))

## Vlastnosti

- síť je z principu konstrukce acyklická
- síť neobsahuje redundantní informaci a tudíž je vždy konzistentní (splňuje axiomy pravděpodobnosti)

Bayesovská síť může být mnohem kompaktnější než úplná sdružená distribuce, pokud je síť řídká (je lokálně strukturovaná)
- náhodná proměnná často závisí jen na omezeném počtu jiných proměnných
- nechť je takových proměnných k a celkem máme n proměnných, pak potřebujeme prostor
 - n * 2^k pro Bayesovskou síť
 - 2^n pro uplnou sdruženou distribuci
- můžeme ignorovat „slabé vazby”, čímž budeme mít menší přesnost reprezentace, ale reprezentace bude kompaknější
- samozřejmě kompaktnost sítě hodně závisí na vhodném uspořádání proměnných

## Odvozování v Bayesovských sítí pomocí enumerace

- Připomeňme, k čemu mají Bayesovské sítě sloužit zjistit pravděpodobnostní distribuce náhodných proměnných X v dotazu za předpokladu znalosti hodnot e proměnných z pozorování
- Hodnotu P(X,e,y) zjistíme z Bayesovské sítě P(x1,...,xn) = ∏_i P(xi |parents(Xi ))

## Eliminace proměnných

- Enumerační metoda zbytečně opakuje některé výpočty
- Stačí si výsledek zapamatovat a následně použít
- f_i spočítáme jednou a uschováme pro budoucí použití dynamické programování
- Činitelé fi jsou matice (tabulky) pro dané proměnné
- Vyhodnocení provedeme zprava doleva (viz příklad dále)
 - násobení činitelů je násobení po prvcích (ne násobení matic)
 - vysčítáním činitelů eliminujeme příslušnou proměnnou
 - na závěr provedeme normalizaci
 - tj. bottom-up přístup pro předchozí graf u odvozování enumerací



## Složitost problému

Eliminace proměnných urychluje odvozování, ale jak moc?

- Pokud je Bayesovská síť poly-strom (mezi každými dvěma vrcholy vede maximálně jedna neorientovaná cesta), potom je časová a prostorová složitost odvozování lineární vzhledem k velikosti sítě (tj. velikosti tabulek).
- Pro více-propojené sítě je to horší

# Vzorkovací metody

- Exaktní odvozování je výpočetně náročné, můžeme ale použít aproximační techniky založené na metodě Monte Carlo
- Monte Carlo algoritmy slouží pro odhad hodnot, které je těžké spočítat exaktně
 - vygeneruje se množství vzorků(ohodnocení náhodných proměnných)
 - hledaná hodnota se zjistí statisticky
 - více vzorků = větší přesnost
- Pro Bayesovské sítě ukážeme přístupy
 - příme vzorkování
 - vzorkování se zamítáním
 - vzorkování s vážením věrohodností

# Přímé vzorkování

- Vzorkem pro nás bude ohodnocení náhodných proměnných
- Vzorek je potřeba generovat tak, aby „odpovídal” tabulkám v Bayesovské síti
 - uzly (proměnné) bereme v topologickém uspořádání
 - ohodnocení rodičů nám dá pravděpodobnostní distribuci hodnot aktuální náhodné proměnné
 - náhodně vybereme hodnotu podle této distribuce
 - Nechť N je počet vzorků a N(x1,...,xn) vyjadřuje počet výskytů jevu x1,...,xn, potom P(x1,...,xn) = lim_{N→∞}(N(x1,...,xn)/N)

# Vzorkování se zamítáním
- Nás ale zajímá P(X|e)
- Ze vzorků, které vygenerujeme, vezmeme jen ty, které jsou kompatibilní s e (ostatní zamítneme)
- Hlavní nevýhoda metody je zamítání příliš mnoha vzorků!

# Vážení věrohodností (Weighted Sampling, WS)
- Místo zamítání vzorků je efektivnější: generovat pouze vzorky vyhovující pozorování e
- Zafixujeme hodnoty z pozorování e a vzorkujeme pouze ostatní proměnné


# Čas a neurčitost

- Dynamiku světa budeme modelovat sérií časových řezů
- t je označení časového řezu
 - uvažujeme tedy diskrétní čas se stejnýmí časovými kroky 
- Každý řez/stav bude popsán (stejnou) množinou náhodných proměnných, které se dělí na
 - nepozorovatelné náhodné proměnné X_t
 - pozorované náhodné proměnné E_t
  - konkrétní pozorovanou množinu hodnot označíme e_t

X_{t1:t2} označujeme množinu proměnných od Xt1 po Xt2

## Modelová situace
 - Uvažujme agenta pracujícího na tajné podzemní základně, ze které nikdy nevychází 
 - Zajímá ho, zda venku prší - náhodná nepozorovatelná proměnná R_t
 - Jediné pozorování, které má k dispozici, říká, zda ráno ředitel přišel s deštníkem nebo bez deštníku -- náhodná pozorovaná proměnná Ut

## Přechodový model
 - Přechodový model popisuje, jak je stav ovlivněn předchozími stavy Přesněji popisuje pravděpodobnostní distribuci P(Xt|X0:t−1)

1. problem: s rostoucím t neomezeně roste množina X0:t−1
 - použijeme Markovský předpoklad: současný stav závisí pouze na pevně daném konečném počtu předchozích stavů – hovoříme potom o obecných Markovských řetězcích/procesech
 - např. současný stav závisí pouze na předchozím stavu Markovský proces prvního řádu P(Xt |X0:t−1) = P(Xt |Xt−1)

2. problém: pořád máme nekonečně mnoho různých přechodů
 - použijeme předpoklad stacionárního procesu, tj. stav se vždy mění podle stejných pevně daných pravidel
 - distribuce P(Xt |Xt−1) je stejná pro všechny časy t
 


# Senzorický model
 
- Senzorický model popisuje, na čem závisí pozorované náhodné proměnné E_t
- Ty mohou záviset i na proměnných z předchozích stavů, ale uděláme Markovský senzorický předpoklad – pozorované proměnné závisí pouze na nepozorovatelných proměnných Xt ze stejného stavu 
- P(Et|X0:t,E1:t−1) = P(Et|Xt)

# Bayesovské sítě pro přechodový a senzorický model

Přechodový a senzorický model můžeme popsat Bayesovskou sítí

# Zpřesnění modelu

Markovský proces prvního řádu předpokládá, že stavové proměnné obsahují veškerou informaci pro charakteristiku pravděpodobnostní distribuce dalšího stavu

Co když je tento předpoklad nepřesný?
 - můžeme zvýšit řád Markovského procesu
 - můžeme rozšířit množinu stavových proměnných


# Řešené úlohy

Odhad stavu (filtrace): cílem je zjištění pravděpodobnosti aktuálního stavu na základě dosavadních pozorování -- P(X_t|e_1:t)

Predikce: cílem je zjištění pravděpodobnosti budoucího stavu na základě dosavadních pozorování: P(Xt+k|e1:t) pro k > 0

Vyhlazování: cílem je zjištění pravděpodobnosti minulého stavu na základě dosavadních pozorování: P(X_k|e_1:t) pro `k, kde 0 ≤k < t`

Nejpravděpodobnější průchod: na základě posloupnosti pozorování chceme zjistit nejpravděpodobnější posloupnost stavů, která tato pozorování generuje: argma_x_x1:t P(x_1:t|e_1:t)

# Odhad stavu (filtrace)

Úkolem je zjistit pravděpodobnost aktuálního stavu na základě dosavadních pozorování: P(Xt|e1:t)
Dobrý filtrační algoritmus odhaduje aktuální stav z odhadu předchozího stavu a aktuálního pozorování (rekurzivní odhad)

TODO: rovnice

# Predikce 

Úkolem je zjistit pravděpodobnost budoucího stavu na základě dosavadních pozorování. Jedná se v podstatě o filtraci bez přidávání dalších pozorování (rozšíření jednokrokové predikce z odvození filtrace)

Po určité době (mixing time) konverguje předpovězená distribuce ke stacionární distribuci a nadále zůstane stejná

# Vyhlazování

Úkolem je zjistit pravděpodobnost minulého stavu na základě dosavadních pozorování. 
Opět použijeme rekurzivní předávání zpráv, tentokrát ve dvou směrech
Můžeme tedy použít techniku zpětné propagace zprávy


# Užitek a rozhodování

## Teorie uzitku

(Agentovy) preference lze zaznamenat funkcí užitku U(s), která mapuje stavy s na reálné číslo

Očekávaný užitek (expected utility) potom spočteme jako průměrný užitek přes všechny možné stavy vážené pravděpodobností výsledků

Racionální agent potom volí akci maximalizující očekávaný užitek MEU

MEU formalizuje racionalitu, ale jak budeme celý postup operačně realizovat?

- Cíl: hledáme funkci užitku popisující preference
- Agentovy preference se často vyjadřují relativním porovnáním
 - A > B: agent preferuje A před B 
 - `A < B`: agent preferuje B před A
 - A ∼ B: agent mezi A a B nemá žádnou preferenci (nerozlišuje A a B)
- Co je A nebo B?
 - mohou to být stavy světa, ale pro neurčité výstupy se používají loterie
 - loterie popisuje možné výstupy S1,...,Sn, které se vyskytují s danými pravděpodobnostmi p1,...,pn
- Příklad loterie (nabídka jídla v letadle): Chcete kuře nebo těstoviny?
 - [0.8, dobré kuře; 0.2 připečené kuře]
 - [0.7, dobré těstoviny; 0.3, rozvařené těstoviny]

## Funkce uzitku
 - Existuje funkce užitku vracející pro danou loterii reálné číslo tak, že
  - `U(A) < U(B) ⇔A < B` 
  - `U(A) = U(B) ⇔A ∼B`
 - Očekáváný užitek loterie lze spočítat:
  - U([p1,S1; ...,pn ,Sn ]) = ∑_i pi U(Si ) 
 - Racionální agent ani nemusí svoji funkci užitku znát, ale pozorováním jeho preferencí ji lze zrekonstruovat
 - Jak zjistit funkci užitku konkrétního agenta (preference elicitation)?
  - budeme hledat normalizovanou funkci užitku
  - uvažujme nejlepší možný stav Smax a dejme mu užitek 1: U(Smax) = 1
  - podobně pro nejhorší možný stav Smin a dejme užitek 0: U(Smin) = 0
  - nyní se pro libovolný stav S ptejme agenta na porovnání S a standardní loterie [p,Smax; 1 −p,Smin]
  - podle výsledku upravíme pravděpodobnost p a ptáme se znova, dokud agent vztah A a standardní loterie nepovažuje za nerozlišitelný
  - získané p je užitkem S: U(S) = p


- V praxi se často vyskytuje více atributů užitku, např. cena, nebezpečnost, užitečnost – víceatributová funkce užitku
- Budeme uvažovat, že každý atribut má definované preferované pořadí hodnot, vyšší hodnoty odpovídají lepšímu řešení
- Jak definovat preference pro více atributů dohromady?
 - přímo bez kombinace hodnot atributů – dominance
  - pokud je ve všech atributech řešení A horší než řešení B, potom B je lepší i celkově – striktní dominance
  - lze použít i pro nejisté hodnoty atributů
 - kombinací hodnot atributů do jedné hodnoty


# Rozhodovací sítě

Jak obecně popsat mechanismus rozhodování?
Rozhodovací síť (influenční diagram) popisuje vztahy mezi vstupy (současný stav), rozhodnutími (budoucí stav) a užitkem (budoucího stavu)

Náhodné uzly (ovál)
 - reprezentují náhodné proměnné stejně jako v Bayesovských sítích
Rozhodovací uzly (obdélníky)
 - popisují rozhodnutí (výběr akce), které může agent udělat (zatím uvažujeme jednoho agenta)
Uzly užitku (kosočtverce)
 - popisují funkci užitku


## Rozhodovací sítě: vyhodnocovací algoritmus
Akce jsou vybrány na základě vyzkoušení všech možných hodnot rozhodovacího uzlu

1. nastavíme hodnoty pozorovaných proměnných
2. pro každou možnou hodnotu rozhodovacího uzlu
3. 
 - nastavíme rozhodovací uzel na danou hodnotu
 - použitím pravděpodobnostní inference vypočteme pravděpodobnosti rodičů uzlu užitku
 - vypočteme užitek pomocí funkce užitku
4. vybereme akci s největším užitkem

Pro případy, kde je více uzlů užitku používáme při výběru akce techniky pro víceatributové funkce užitku

Přímé rozšíření algoritmu pro Bayesovské sítě:
 - při rozhodování agenta vybíráme akci s největším užitkem

Zajímavější problém až při vykonávání posloupnosti rozhodnutí

## Rozhodovací sítě: konstrukce a příklad

- Vytvoření kauzálního modelu
 - určení symptomů, nemocí, léčby a vztahů mezi nimi (dom.experti, literatura)
- Zjednodušení kvalitativního modelu
 - pokud nám jde o léčbu, můžeme odstranit uzly, které s nimi nesouvisí
 - některé uzly lze spojit (léčba Treatment a její načasování Timing)
- Přiřazení pravděpodobností – z kauzálních vazeb, diagnostické vazby z BS:
 - vyplnění pravděpodobnostních tabulek jako v Bayesovské síti 
- Navržení funkce užitku
 - můžeme enumerovat možné výstupy 
- Verifikace a doladění modelu
 - výsledky se porovnají se zlatým standardem, např. skupinou lékařů 
- Analýza citlivosti
 - kontrola, zda výsledky systému nejsou citlivé na drobné změny vstupu


# Shrnuti
- Teorie pravděpodobnosti nám umožní kvantifikovat, jak máme danému tvrzení věřit na základě pozorování
 - Bayesovské sítě a odvozování pomocí nich -- staticky v daném čase
 - Pravděpodobnostní uvažování o čase -- reprezentace přechodů s pravděpodobností: Markovský proces, zjištění pravděpodobnosti stavu vzhledem k probíhajícímu času
- Teorie užitku pro ohodnocení rozhodnutí
- Teorie rozhodování
 - pro jedno rozhodnutí (statický případ)
 - pro posloupnost rozhodnutí



# Sekvenční rozhodovací problémy
 - Cílem je tvorba racionálních agentů maximalizujících očekávanou míru užitku
 - Teorie pravděpodobnosti říká, čemu máme věřit na základě pozorování
 - Teorie užitku (utility theory) popisuje, co chceme a jak máme ohodnotit rozhodnutí
 - Teorie rozhodování (decision theory) spojuje obě teorie dohromady a popisuje, jak bychom měli vybrat akci s největším očekávaným užitkem

- Doposud jedno rozhodnutí → nyní posloupnost rozhodnutí
- užitek bude záviset na posloupnosti rozhodnutí
- Uvažujme agenta pohybujícího se v prostředí o rozměrech 3 × 4
- Prostředí je plně pozorovatelné (agent vždy ví, kde se nachází)
- Agent se chce dostat do stavu +1 a vyhnout se stavu -1
- Agent může provést akce Up, Down, Left, Right
 - množinu akcí pro stav s značíme A(s)
 - výsledek akce je ale nejistý
  - s pravděpodobností 0.8 půjde správným směrem
  - s pravděpodobností 0.1 půjde kolmo k požadovanému směru (resp. stojí na místě, pokud narazí na zeď)
 - pravděpodobnost [Up, Up, Right, Right, Right]: 0.8^5 


# Markovský rozhodovací proces (MDP)

- Pro popis přechodů (aplikace akce) použijeme pravděpodobnostní distribuci P(s′|s,a) – pravděpodobnost přechodu z s do s′ akcí a
 - opět uvažujeme Markovský předpoklad (pravděpodobnost přechodu nezávisí na předchozích navštívených stavech) 
- Užitek tentokrát závisí na prošlých stavech
 - každý stav má přiřazeno ocenění (reward) R(s)
 - funkce užitku bude (zatím) součet ocenění navštívených stavů
- Markovský rozhodovací proces (Markov Decision Process MDP)
 - sekvenční rozhodovací problém v plně pozorovatelném stochastickém prostředí s Markovským přechodovým modelem a aditivní funkcí užitku
  - tvořen množinou stavů s počátečním stavem s0
  - množinou akcí v každém stavu A(s)
  - přechodovým modelem P(s′|s,a)
  - oceněním R(s)

## Řešení MDP

- Ve stochastickém prostředí nemůžeme pracovat s pevným pořadím akcí (plánem)
 - agent se může vydat jinam, než bylo naplánováno
- Protože předem nevíme, kam akce agenta zavede potřebujeme v každém stavu vědět, co dělat (kam jít)
- Řešením MDP je strategie (policy) π(S), což je funkce určující pro každý stav doporučenou akci
 - hledáme strategii s největším očekávaným užitkem = optimální strategie 

## Optimální strategie

Optimální strategie maximalizuje očekávaný užitek

## Užitek v čase: horizont

Jak obecně definovat funkci užitku pro posloupnost stavů?
- je to podobné jako pro víceatributové funkce užitku U([s0,s1,...,sn]) (stavy jsou atributy), ale jaky mame horizont?


### Konečný horizont1

- máme daný pevný termín N a po něm už na ničem nezáleží
- optimální strategie záleží na termínu (není stacionární)



### Nekonečný horizont1

- to neznamená nutně nekonečné posloupnosti stavů, pouze zde není žádný deadline
- není důvod se ve stejném stavu chovat v různé časy různě
- optimální strategie je stacionární


## Užitek v čase: definice funkce

- Funkce užitku se chová jako víceatributová funkce užitku U([s0,s1,...,sn])
- Pro získání jednoduchého vztahu pro výpočet funkce užitku uvažujme stacionární preference
- V případě stacionárních preferencí jsou dva způsoby, jak rozumně definovat funkci užitku
 - aditivní funkce užitku: R(s0) + R(s1) + ...
 - kumulovaná (discounted) funkce užitku: R(s0) + γR(s1) + γR(s2) ...
 - faktor slevy γ ∈(0,1) -- preference mezi aktuálním a budoucím oceněním

## Užitek v čase: vlastnosti
- Budeme používat kumulovanou funkci užitku
- pro světy bez cílového stavu a nekonečný horizont by aditivní funkce užitku byla problémová
- užitek v kumulované funkci užitku je konečný (uvažujeme omezené ocenění s maximem Rmax)
- pokud má prostředí cílový stav, do kterého se agent garantovaně může dostat, nebudeme potřebovat pracovat s nekonečnými posloupnostmi
 - řádná (proper) strategie – garantuje dosažení cílového stavu
- u nekonečné posloupnosti lze porovnat průměrné ocenění
 - lepší je zůstat ve stavu s oceněním 0.1 než ve stavu s oceněním 0.01 


# Bellmanova rovnice

TODO: vzoroec
TODO: iterace hodnot


# Robotický hardware: senzory

- pasivní senzory slouží k pozorování prostředí, kdy zachycují signály generovanými dalšími zdroji v prostředí
- aktivní senzory vysílají energii do prostředí (např. sonar) založeny na tom, že je energie reflektována senzoru zpět
 - poskytují více informací než pasivní senzory
 - náročnější na energii než pasivní senzory
 - hrozí nebezpečí interfence při použití více aktivních senzorů zároveň

Senzory dělíme v závislosti na tom, zda určeny pro vnímání:
 - prostředí, tj. dálkoměry pro měření vzdálenosti od blízkých objektů
 - robotova umístění, tj. lokační senzory
  - časté řešení lokalizačního problému: Global Positioning System (GPS)
 - robotovy vnitřní konfigurace, např.
  - pro měření přesné konfigurace robotických kloubů, motorů
  - gyroskopy – pro udržení referenčního směru

Efektory umožňují robotovi pohyb a změnu tvaru těla
Aktuátor/akční člen (actuator) zahajuje pohyb efektoru
 - především elektrický akční člen
 - také hydraulický, penumatický akční člen
Stupeň volnosti (degree of freedom DOF)
 - umožňuje pochopit návrh efektoru
 - jeden DOF pro každý nezávislý směr, ve kterém se robot nebo jeden z jeho efektorů může pohybovat


Kinematický stav: určen DOFs
Dynamický stav: zahrnuje DOF kinematického stavu + dimenze pro rychlost změny kinematické dimenze
Počet DOFs nemusí být stejný jako počet ovládaných prvků (mobilní roboti)

## Software: problémy v robotice

Robot v izolovaném známém prostředí
 - agent jako Markovský rozhodovací proces MDP
Problémy v robotice
 - nedeterministické, částečně pozorovatelné, multiagentní
 - agent jako částečně pozorovatelný Markovův rozhodovací proces

Hierarchie problémů v robotice
 - plánování úloh (task planning): určení plánu nebo strategie
 - plánování pohybu (motion planning) nalezení cesty pro robota z jednoho budu do druhého pro splnění každého podcíle
 - řízení (control) k zajištění plánovaného pohybu akčnímí členy

učení preferencí: vyhodnocení cílů koncových uživatelů a predikce chování lidí v prostředí robota

# Dynamická Bayesovská síť (DBN)

Reprezentuje temporální pravděpodobnostní model. Skládá se z opakujících se vrstev proměnných. Dle Markovských předpokladů má každá proměnná rodiče buď ve stejné nebo  předchozí vrstvě

staci popsat:
 - prvni vrstvu
 - apriorni distribuci
 - prechodovy model
 - senzoricky model


# Plánování pohybu robota

Pohyb z bodu do bodu - přesun robota do cíle
Koordinovaný pohyb - robot se přesunuje v kontaktu s předmětem
Konfigurační prostor - používá se pro reprezentaci plánovacího problému, je to prostor stavů robota definovaný jeho umístěním, orientací a úhly kloubů, vhodnější reprezentace než původní 3D prostor.
Plánování cesty - problém nalezení cesty z jedné konfigurace do druhé v konfiguračním prostoru, na rozdíl od klasického hledání cesty v diskrétním prostoru se pohybuje ve spojitém prostoru.


# Reprezentace konfiguračního prostoru

Souřadnice určují reprezentaci pracovního prostoru – reálného prostoru, kdy jsou souřadnice robota zadány stejným souřadným systémem jako objekty, kterými manipulujeme. Reprezentace 
vhodná pro kontrolu kolizí zejména robota a objektů zadaných jednoduchými polygonálními modely. Problémy: všechny souřadnice pracovního prostoru nejsou dosažitelné, generování cest, 
které dodržují tato omezení je velmi náročné. 

# Reprezentace konfiguračního prostoru

Reprezentace pomocí robotových kloubů.

Plánování cesty: spojíme aktuální pozici a cíl rovnou čarou a robot se po ní pohybuje konstantní  rychlostí, dokud nedorazí do cíle
Problém: úloha robota je většinou zadána v pracovním, a ne v konfiguračním prostoru. 
Kinematika: transformace souřadnic z konfiguračního prostoru do pracovního prostoru je jednoduchá – lineární transformace pro otočné klouby
Inverzní kinematika: opačná transformace – obtížná, zřídka jedno řešení, např. pozice chapadla umožňují dvě konfigurace


# Plánování pohybu: postup řešení

1. Předzpracování / učící fáze / konstrukce grafu
 - vypočítání grafu – často označován jako cestovní mapa (roadmap)
  - graf viditelnosti
  - Voroného diagram
  - buňková dekompozice
  - potenční funkce

2. Zpracování dotazu
 - spojení počáteční a cílové konfigurace s grafem
 - identifikace počáteční a cílové buňky
 - prohledávání grafu

3. Inkrementální konstrukce grafu směrem k cíli
 - rychle prozkoumávající náhodný strom (RRT)

Základní problém plánování pohybu: nalezení spojité posloupnosti konfigurací, která převede robota z iniciální konfigurace qI do cílové
konfigurace qG tak, že se žádná konfigurace po cestě nepřekrývá s překážkou.

# graf viditelnosti (visibility graph)

- Spojíme všechny páry vrcholů plus iniciální a cílové konfigurace
- Eliminujeme hrany, které protínají překážky
- Graf viditelnosti vždy zahrnuje nejkratší cestu konfiguračním prostorem

Konstrukce grafu viditelnosti
 - popsaný (naivní) postup pro n vrcholů O(n^3)
 - s pomocí rotačního stromu pro množinu segmentů O(n^2)

# Voroného diagram
- dělí prostor R2 na oblasti podle zadaných objektů, např. bodů x ∈M
- každý bod x má přiřazenu Voroného oblast V (x)
- pro každý bod y ∈V (x) je x nejbližší bod z M

Cestovní mapa jako VD, který maximalizuje vzdálenost od překážek.

- Robot změní konfiguraci na bod ve VD - toto lze realizovat pohybem po rovné čáře v konfiguračním prostoru
- Robot se pohybuje ve VD, dokud nedosáhne bod, který je nejbližší cílové konfiguraci
- Robot opustí VD a přesune se do cíle - opět rovnou čarou v konfiguračním prostoru

# Graf viditelnosti vs. Voroného diagram

Graf viditelnosti
 - nejkratší cesta, ale blízko k překážkám nutno uvažovat bezpečnost cesty
 - komplikované ve vyšší dimenzi

Voroného diagram
 - maximalizuje vzdálenost od překážek, což poskytuje konzervativní cesty
 - malé změny překážek mohou vést k velkým změnám VD
 - komplikované ve vyšší dimenzi


# Buňková dekompozice

Dekompozice volného prostoru na konečný počet spojitých regionů nazývaných buňky. Plánování cesty redukováno na prohledávání v diskrétním grafovém prostoru. Základní grafová  dekompozice: pravidelná mřížka – úroveň šedi buňky určuje hodnotu buňky = cenu nejkratší cesty do cíle. Hodnoty spočítáme deterministickou verzí algoritmu iterací hodnot nebo A* algoritmem.


Zpracování částečně obsazených buněk:
 - neprocházet tyto buňky - neúplné: nemusí existovat cesta
 - procházet tyto buňky - nekorektní: může vrátit cestu, která neexistuje
 - zvětšít rozlišení mřížky - drahé: zejména ve vyšší dimenzi
 - adaptivní diskretizace - ztráta uniformní velikosti mřížky


# Vertikální dekompozice (vertical decomposition)

Exaktní buňková dekompozice (př. vertikální/lichoběžníková, triangulace):


# Potenciální pole

Dodatečná cenová fce. Hodnota potenciálu pole narůstá ze vzdáleností od nejbližší překážky. Potenciál pole je pak využit jako dodatečná cenová fce při výpočtu nejkratší vzdálenosti

# Pravděpodobnostní cestovní mapa – probabilistic roadmap

Diskrétní reprezentace spojitého konfiguračního prostoru generována náhodným vzorkováním konfigurací v Cfree, které spojíme do grafu

- vrcholy: přípustné konfigurace robota (milestones)
- hrany: reprezentují platnou cestu (trajektorii) mezi konfiguracemi

Nevyžaduje explicitní popis Cobs
Cesta (trajektorie) ze startu do cíle: grafové prohledávací algoritmy

## Jeden vs. více dotazů

Více dotazů na pravděpodobnostní cestovní mapu
 - generování jedné cestovní mapy, která je používána pro plánovací dotazy vícekrát

Jeden dotaz na pravděpodobnostní cestovní mapu
 - pro každý plánovací problém konstruována nová cestovní mapa charakteristická pro podprostor konfiguračního prostoru relevantní pro problém 
  - rychle prozkoumávající náhodný strom (RRT) 


## Strategie pro více dotazů

Vytvoření cestovní mapy (grafu), který reprezentuje prostředí
- Učící fáze
 - Vzorkování n bodů v C_free 
 - Spojení náhodných konfigurací s použitím lokálního plánovače (lokální plánovač hledá lokální cesty, např. přímé)
- Dotazovací fáze
 - Spojení počáteční a cílové konfigurace s PRM
 - Použití prohledávání grafu k nalezení cesty


## Vlastnosti PRM

Úplnost pro standardní PRM nediskutována
Většinou studována sPRM, která je
 - pravděpodobnostně úplná a asymptoticky optimální
 - složitost konstrukce grafu (učící fáze) O(n2)
 - složitost i prostorova slozitost dotazu O(n2)

# Rychle prozkoumávající náhodný strom – Rapidly exploring random tree (RRT)

- Algoritmus pro jeden dotaz
- Motivací je hledání cesty založené na řízení
- Inkrementální konstrukce grafu (stromu) směrem k cílové oblasti

## Postup tvorby stromu

- Začni s počáteční konfigurací qinit , která je kořenem konstruovaného stromu
- Generuj náhodnou konfiguraci qnew v Cfree
- Nalezni nejbližší uzel qnear ke qnew ve stromě
- Rozšiř qnear směrem ke qnew
- Pokud není strom v dostatečné vzdálenosti od cílové konfigurace, běž na krok 2.


## Vlastnosti RRT
 - Rychle prozkoumává prostor
 - Umožňuje uvažování kinodynamických/dynamických omezeni
 - Umí nalézt trajektorie nebo posloupnosti přímou kontrolou příkazů robotových ovladačů
 - Test na detekci kolize obvykle jako black-box
 - Podobně jako PRM má RRT problémy s úzkými pasážemi
 - RRT nalezne proveditelnou cestu bez garance kvality
  - cesta může být relativně daleko od optimální cesty dané např. délkou cesty
 - Navrženo mnoho variant RRT 


# Skeletonizace

Alternativní přístup pro převedení plánování cesty na prohledávání v diskrétním grafovém prostoru. Robotův volný prostor je redukován na jednodimenzionální reprezentaci nazvanou 
skeleton = Voroného diagram – množina všech bodů, které mají stejné vzdálenosti od dvou nebo více překážek. Plánování cesty redukováno na hledání nejkratší cesty ve Voroného diagramu.


# Dynamický stav

Přechodový model pro dynamický stav zahrnuje účinek sil na rychlost změny. Nutné modely vyjádřené diferenciálními rovnicemi, které provážou kvantitu s odpovídající změnou v čase. Pokud
bychom uměli generovat takové plány, roboti by měli skvělý výkon. Dynamický stav má však více dimenzí než kinematický, plánovací algoritmy by byly použitelné pouze pro nejjednodušší roboty. 
Robotické systémy v praxi se spoléhají na jednodušší kinematické plánovače cest. 


# Regulátor

Kompenzuje limitace kinematických plánů, aby byla zachována cesta.

Referenční regulátor – snaží se robota udržet na naplánované cestě.
Proporční derivační regulátor – nejjednodušší regulátor, který zachovává striktní stabilitu v naší doméně
Integrační proporční derivační regulátor - umožňuje odstranit chybové chování PD regulátoru v některých případech. Chybové hlášení jako důsledek systematické vnější síly, která není součástí modelu.
Dlouhotrvající odchylky mezi referenčním a aktuálním stavem  opraveny. Regulátor tak řeší systematické chyby na úkor zvýšeného nebezpečí oscilací.

# Další způsoby řízení pohybu


Řízení pomocí potenciálu pole – podobně jako při plánování pohybu
Reaktivní řízení – můžeme specifikovat regulátor bez explicitního modelu prostředí, 
nejprve si určíme vzor posunu končetin a pak už reaktivně reagujeme na daný stav
Zpětnovazební učení















