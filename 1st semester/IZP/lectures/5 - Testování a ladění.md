Links: [[IZP]]
https://moodle.vut.cz/pluginfile.php/944585/mod_folder/content/0/7-ladeni-programu.pdf

## Ladění (debugging)
- = proces hledání a redukování chyb
- na vstupu
- **Výstup**: lokace, kde v kódu jsou chyby
- **Vstup**: vstupní data programu, které mám spustit, aby se mi projevila chyba
- How: podíváme se na kód, (statická analýza), projdeme očima, provedeme vlastně

## Testování
- = systematický proces zlepšování kvality programu
- způsob, jak ten program spustit, že nám nefunguje
- výsledek každého testu je: v pořádku (*pass*), není v pořádku (**fail**)
- testovací sada
	- množina testů, které ukážou v jakých případech program funguje

# Bugy
- chyba/efekt/selhání
- dělíme dle obtížnosti odhalení
- typy
	- **Syntaktické chyby** - chyby v syntaxi
		- ez fix
		- měly by být odhalitelné překladačem
	- **Chyby sestavení**
	- **Základní semantické chyby** - chyba základní funkcionality, selhání
		- ez fix
	- Účelu specifické **sémantické chyby** - bez projevu až po selhání
		- hard fix
		- nejsou odhalitelné překladačem
			- jsou syntakticky správně, ale logicky špatně
# Koncept ladění (in midterm)
1. Reprodukce (hledání vstupních dat, bug report)
	1. zkusíme spustit
2. Diagnóza 
3. Oprava (bug fix)
4. Integrace (fix test, commit)

### 1. reprodukce
- KDO: reportér, tester, uživatel (ideálně jen v opensource), vývojář
- kontrola, zda chyba již nebyla opravena
- Postup
	- Hledání vstupních dat, které vedou k projevu chyby
	- Izolování chyby
		- minimalizace počtu kroků k reprodukci chyby
		- minimalizace počtu vnějších parametrů
		- odstranění nedeterminismu (pokud se chyba objevuje náhodně, najít a dostranit všechny náhodné vstupy)
	- automatizace chyby
		- vytvoříme automatický testing program (automatický)
		- regresní test 
### 2. diagnóza
- pochopení pcincipu chyby
- postup
	- (chyba v uživateli) Odpovídají vstupní podmínky správnému použití?
	- (chyba ve vnějším prostředí) Není chyba ve vnějším prostředí
		- Jsou soubory a data správná? knihovny očekávané verze? Arch počítače, OS ok
	- (chyba v kódu) Chyba je v programu
		- buď statická (očima) nebo dynamická analýza kódu (krokování - spusť jeden řádek, poté jeden řádek, po každém řádku se díváme na proměnné)
		- Minimalizace (krajování kódu)
		- Krokování nejmenšího kusu kódu, ve kterém se projevuje chyba
		- Hledání místa, kde chyba nastala
- checklist
	- nesplést si projev a reálnou příčinu chyby
	- podobné chyby nejsou v jiných částech kódu
	- jedná se o chybu programování, nikoliv návrhu

## Technicky ladění
1. *Statická analýza*
	- kontrolujeme před spuštěním programu
2. *Dynamická analýza*
	- kontrolujeme po spuštění programu (in runtime)
	- zkoumáme **průběh, stav** programu
		- pozastavíme spuštěný program, podíváme se na proměnné (=stav programu)
	- 2 druhy
		- **Záznam sekvence** událostí (log, logging, logování)
			- informování samotného programu pro programmer, co zrovna dělá (nezastavujeme, nezpomalujeme)
			- můžeme zapnout logging in prod, uživatel pošle
			- Kam?
				- do *stderr*
					- `fprintf(stderr, "skill issue %d\n", args);`
				- nebo ukládáme do log *souboru*
		- **Interaktivní** ladění
			- Debugger = interaktivní nástroj pro lokalizaci chyb
				- **sledují proměnné, aktuální průběh, možnost záchytných bodů (breakepoints)**
				- sleduje obsah lokálních proměnných
				- spustí binary
					- a informuj mě o všem, co se děje
				- Musíme tam přidat **Ladící informace**
					- je tam uložené, že tyto instrukce, vznikla kvůli danému řádku
1. *Code review*
	- požádáme o schválení kódu, někdo to musí schválit
		- (tudíž 2 a více vývojářů)
	- Ladění jako statická analýza
	- = programování + diskuze

# Preprocessor
- na začátku celého překladu nahrazuje v kódu až pak runnuje
- Makra
	- include, define, if, ifdef, error
```c
#define MACRO_NAME [nahrada]
#define MACRO_NAME

// priklad:
#define EOF (-1)
#define FILE struct _file

// dalsi priklady:
#define MACRO_NAME(p1,p2) [náhrada]

#define ABS(x) x<0 ? -x : x
#define MAX(a,b) a<b ? b : a
```

- ladění s preproccesorem
```c
#ifndef NDEBUG
#define pmesg (s, ...) fprintf(stderr, ...)
#else
#define pmesg(s, ...) (0)
#endif



// kdyz true prelozi se na:
fprintf(stderr, ....);

// kdyz false, prelozi se na
(0);
```
- když máme NDEBUG, tak printujeme, jinak ne

