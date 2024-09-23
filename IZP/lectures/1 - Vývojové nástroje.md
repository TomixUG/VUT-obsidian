Links: [[IZP]]
# Dělíme
Kde se soubor uloží, kde se spouští
1. na lokálním PC
2. na vzdáleném PC (přes síť)
3. část běží na serveru, část na klientovi (Node.js)
4. můžeme programovat na dálku přes terminál (vše se spouští remotely)

## Jak probíhá spouštění
- **Překladač (compiler)** 
	- nástroj pro překlad textových zdrojových souborů do binárního jazyka instrukcí
		- Instrukce = operace prováděná buď nativně (CPU instrukce) nebo jiným SW
	- Například:
		- Jazyk C 
			- _cc_ (C Compiler), gcc, clang
		- Go, Rust, C++, Java, Ocaml
- **Interpret**
	- nástroj, který "interpretuje" program - spouští textové zdrojové soubory **přímo**
	- čte řádek po řádku text. soubor a vykonává ho **řádek po řádku** (říká CPU, co dělat)
	- Například:
		- Python
			- CPython interpreter (soubor .pyc)
		- Javascript, PHP, Ruby

# Struktura projektu
Softwarový projekt = **sada soborů, dokumentace, požadavků** řešící softwarový problém
- nám vystačí projekt = soubory

### Struktura souborů
- ve složkách
- moduly 

- Příklad pro začátek
	- README.md - základní popis
	- src/ - adresář se soubory
	- tests/ - adresář s testy
Dělej testy :(

# Pracovní nástroje
- Editor zdrojových kódů
- Manuál, nápověda, web
- Překladač (compiler)
- Automatizace překladu a spouštění testů

Editory kódů (code editor)
- Vim, vscode, Atom
IDE
- Eclipse, Visual Studio, Xcode
- preconfigured, umí vše

# Verzování
- Je třeba uchovávat vývoj projektu:
	- Záloha - když se cokoliv pokazí můžeme obnovit
	- Porovnání změn - když se něco nového pokazí, lehce zjistit, proč 
	- Různé varianty - nově implementované vlastnosti
- Nejjednodušší je kopie souborů projektu
	- Příklad: projekt/*, projekt-2024-01-03/*
	- Nekopírovat jednotlivé soubory, ale vše
	- Výhody:
		- rychle provedeno, obnoveno
	- Nevýhody:
		- nepřehlednost, úprava ve starém projektu způsobí zmatek, nekolaborativní
#### Verzovací systémy
- Verzovací systém ví o různých verzí projektu
	- Lokální: v adresáři projektu jsou v podadresáři uloženy různé verze souborů
	- Příklad: RCS (obsolete)
	- ![[Pasted image 20240918161329.png]]
- Centralizovaná správa verzí
	- **Verze jsou ukládány vzdáleně na verzovacím serveru**
	- Sloučení souborů, konflikty
		- Těžko se řeší konflikty
			- Když někdo pushne dříve, ale někdo mezitím něco udělal mohou nastat problémy
	- Příklad: CSV, Subversion (SVN)
	- ![[Pasted image 20240918161524.png]]
- Distribuovaná správa verzí
	- Upravíme si **lokálně**, lokálně vytvoříme novou verzi
		- Před push o tom ostatní neví
	- Každý počítač má uložen klon celé verze, dělá si lokální
	- Všichni znají historii všech (větvení - branches)
	- Příklad: Git, Mercurial
	- ![[Pasted image 20240918162041.png]]
	- git pull - natáhnout aktuální budoucnost
		- při tom sloučí lokální s budoucností
##### Patch 
- Rozdílové soubory (patch file)
- Slouží k poslání a záznamu rozdílu dvou verzí
- Součást souboru patch
	- Přidané a smazané řádky
	- Sada rozdílu, které se mají udělat
- Patch = stará_verze - nová_verze
- Jeden patch soubor může zaznamenávat úpravu jednoho nebo více souborů
- Používá se k
	- Návrhu změn, oprav chyb
	- jde vidět, co se změnilo
- CLI
	- ![[Pasted image 20240918163032.png]]

#### Git
- ![[Pasted image 20240918163327.png]]
  ![[Pasted image 20240918163620.png]]
- commit vytvoří novou verzi, zaarchivuje, udělá hash, ...
	- pořád jenom lokální

### C
- cc vybere jakýkoliv C compiler


