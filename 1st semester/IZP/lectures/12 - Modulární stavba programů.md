Links: [[IZP]]

https://moodle.vut.cz/pluginfile.php/944585/mod_folder/content/0/17s_modularni_stavba_programu.pdf

# Hlavičkové soubory
- slouží, abychom řekli překladači, že bych rád abych něco mohl v následující části využívat
- nabídka všech možných funkcí, které můžu využít
- důvod:
	- společné místo pro deklarace
	- typicky si nevystačíme se základními datovými typy a operacemi 
- globální identifikátor 
	- všechny funkce, které můžeme odevšad volat
	- Např.: stdin, stdout, ERNO, scanf, malloc, printf
- abych mohl funkci zavolat, MUSÍME ZNÁT
	- parametry, návratový typ, název funkce
	- ABYCH TOTO NEMUSEL PSÁT POKAŽDÉ ZNOVA
- **znovupoužití**
	- jednou někdo něco udělal a teď to můžu používat v mém projektu
	- "přesunout deklarace do hlavičkového souboru"
- stdio.h hlavičkový soubor obsahuje deklarace
	- datové typy (struct tm, FILE)
	- funkce (printf, scanf)
	- globální proměnné (stdin, errno)
	- maker (assert)
	- identifikátory (v rámci enum)
- ![[Pasted image 20241209142602.png|450]]

### Problém s opětovou deklarací
\# include doslova nahrazuje obsah souboru
![[Pasted image 20241209143007.png]]
- může se stát, že bychom znovu deklarovali nějakou proměnnou
##### Jak se to řeší?
- použijeme `#ifndef` "if not defined"
- Tzv. **podmíněný překlad**
	- ![[Pasted image 20241209143329.png|450]]

# Moduly
= vyšší stupeň strukturálního programování
- snažíme se dekomponovat velké problémy na malé
	- "dekompozice velkých problémů na malé"
- modul tvoří samostatnou ucelenou jednotku, kterou lze samostatně kompilovat a opakovně využívat
- implementační detaily mohou být skryty (ve smyslu, že nezatěžují programátory)
- moduly se používají prostřednictvím jejich rozhraní
	- ![[Pasted image 20241209144200.png|250]]

### Modulární programování
= technika vývoje softwaru
- Výhody
	- srozumitelnost 
		- každý modul se zabývá pouze jedním problémem, navenek viditelné pouze jeho rozhraní
	- spolehlivost
		- jasně definovaná jednotka je lépe testovatelná
	- udržovatelnost
		- malé části se lépe udržují, upravují, mění
	- znovupoužití
		- efektivní využití zdrojů, absence chyb z kopírování kódu
- Nevýhody
	- problémy z integrace modulů
		- skrývá vnitřní stav modulů (problém při špatně navrženém nebo využívaném rozhraní)
	- konkretizace modulů
		- odvozené moduly se špatně udržují

### Moduly
- modul má své rozhraní = jak vystupuje navenek
- **export**
	- množina funkcí, datových typů, identifikátorů, atd, které modul poskytuje
- **import**
	- množina funkcí, datových typů, identifikátorů, které modul vyžaduje

Modul je binární

- `"bar.h"` hledej v current adresáři
- `"<stdlib.h>` globální knihovna


# Aplikační rozhraní
- systém, aplikace, komponenta
- aplikační rozhraní
	- popis, jaké procedury tam jsou, jakým způsobem se volají, co pro ně platí když je potřebujeme volat
- Příklady APIs
	- standardní knihovna jazyka C
	- REST (http requests)
	- Unity3D scripty
	- Arduino API (motorky se hýbají, LEDky blikají)
- Komponenta s aplikačním rozhraním se v C nazývá **knihovna**
	- C soubor bez int main

### Knihovny v C
- máme soubor `figmanip.c` `figsearch.c`
	- z těchto se vytvoří `figmanip.o` a `figsearch.o`
		- A z těchto se vytvoří jeden soubor `libfig.so` na Linuxu a `libfig.dll` na Windowsu
- Poté náš program používá tuto knihovnu 
- **Dynamická knihovna**
	- načítá se do paměti až za běhu
	- *Sdílená knihovna*
		- standardní knihovna jazyka C je nahraná v jedné části paměti POUZE JEDNOU. A programy ji používají tu jednu načtenou.
			- třeba GTK (gtk.h)
- **Statická knihovna**
	- ta velká knihovna se musí packagenout do té samotné binárky. Nevýhoda, protože je to velké. Když máme hodně programů, tak bychom měli duplicitní programy. 
- Knihovny by měli mít
	- Licenci
		- co s tím můžeme dělat
			- komerční x nekomerční
		- kdo je autor
		- svobodné licence
			- koukejte se do zdrojáku, udělejte ci so chcete, komerčně i. Ale musíme zachovat autorství 

# Zpětná volání
- ještě v compile time nevíme, jakou funkci chceme volat. To se dozvíme až podle dat, které se objeví v průběhu programu.

```c
typedef double (*Callback) (double x);
double find_local_min(Callback fce, double a, double b);

void foo()
{
	Callback bar = sqrt;
	find_local_min(bar, -1, +1);
	find_root(log, 0.5, bar(4.0));
}

```

# Zásuvné moduly
- programový modul, který rozšiřuje základní funkcionalitu programu
- program musí být připraven na rošíření formou zásuvných modulů
- Dělíme podle
	- podle životního cyklu
	- podle typu
		- *doplněk* (add-on) - rozšíření/doplnění základní funkcionality programu
		- *rozšíření* (extension) - rozšíření programu takové, že program lze použít i k jinému než původnímu účelu
		- *applet*, *servlet* - poskytnutý prostor pro funckionalitu definovanou externím modulem
		- *zásovný modul* (plug-in) - obecný pojem pro proramově rozšířitelnou funkcionalitu
		- *sdílená knihovna* (shared library)
			- pro rychlé operace se zásuvnými moduly
	- podle principu komunikace
- 

DLOPEN
- otevře shared library
```c
dlopen()
```