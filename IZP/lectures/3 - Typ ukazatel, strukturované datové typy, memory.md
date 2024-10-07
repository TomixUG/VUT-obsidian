Links: [[IZP]]
Prezentace: [[5s_ukazatel-pole-funkce.pdf]]

## Ukazatel
- **"ukazatel na něco"**
	- ukazatel na int
	- ukazatel na ukazatel na ukazatel na char
	- ukazatel na double
	- ukazatel na pole
- je to datový typ
- hodnoty ukazatele
	- celočíselné
	- ukazuje na **adresu v paměti**
		- začínají na 0x00000, končí 0xffffff...
			- dle počet bitů OS
	- Tato adresa v paměti má být proměnná nějakého typu
	
##### důležité definice
Pole je datový typ
Struktura je datový typ
int je datový typ
double je datový typ

#### Ukazatel na int (ukazatel na bázový typ)
```c
int *pi;
```
- vytvoř proměnnou typu ukazatel na proměnnou typu int.
- v tomto příkladu má nedefinovanou hodnotu
```c
int *pi;
int a = 112;

pi = &a; // datový typ je T* ukazatel na T
```

Můžu získat pointer i na element v array
```c
int p [] = {1,2,3,4,5};
int *px;

px = &p[2]; // uloží pointer na třetí element
```

**Ampersand** nám dá adresu v paměti dané proměnné. (**= referenční operátor**)

**Dereferenční operátor** (\*) nám vrátí zpět value proměnné
```c
int p [] = {1,2,3,4,5};
int *px;

px = &p[2]; // uloží pointer na třetí element

int element = *px;
```

#### Adresa NULL
- speciální adresa
- Určíme, že ukazatel ještě **nikam neukazuje**
- Znamená to: "Nesmíš použít dereferenční operátor \*"
```c
int *pointer = NULL;
```

#### Obecný ukazatel (void \*)
- Normální (typový ukazatel) umožňuje typovou kontrolu
- Obecný ukazatel **NEumožňuje typovou** kontrolu
	- můžeme přetipovat proměnné (typecasting)
		- Například: char -> int, int -> char
#### Vícenásobný nepřímý odkaz
pointer na pointer na pointer

## Alokace paměti
- Nejnižší adresy jsou dole, nejvyšší jsou nahoře
![[Pasted image 20241002162709.png|250]]
![[Pasted image 20241002163917.png]]
- String z kódu se prostě hodí do paměti

- **dostaneme 2 pointery!!!!**
	- kde končí stack (stack pointer - SP)
	- kde je první instrukce, kterou máš spustit
##### Stack (zásobník)
- vyhrazena pro naše data
- naše lokální proměnné
- můžeme přistupovat POUZE do stacku, zbytek je chráněn OS a nemůžeme zapisovat
##### Heap (hromada)
- teoreticky můžeme žádat extrémně hodně, více než máme v paměti
- můžeme přistupovat POUZE do stacku, zbytek je chráněn OS a nemůžeme zapisovat
- když *potřebujeme více*
	- žádáme OS, aby nám dal více místa
	- OS nám přidělí a **můžeme tam zapisovat** v heapu
		- až dokončíme měli bychom vrátit zpět (free)
##### Datová oblast
- když například definujeme string "hello", tak se uloží sem.
- Když poté chceme printf, tak načte memory adresu tohoto stringu.

##### kódová oblast
- instrukce


### Statická data (globální proměnné)
- jsou v datové oblasti
- hardcoded hodnoty v source code (?)
### Dynamická data 
- žádají se až při běhu programu
- mohou být v:
	1. ve stacku
		- lokální proměnná, která je **předem definovaná**
	2. v heapu
		- pokud **dynamicky žádáme** o paměť (`malloc`)
#### Malloc
- žádáme o alokaci paměti v heapu
- `void *malloc(size_t size)`
	- <u>parametr</u>: pouze velikost
	- <u>vrátí</u>: první adresu našeho adresního prostoru
		- Když už NENÍ MÍSTO returnuje `NULL`
			- **Pokaždé když malloc, tak musíme zkontrolovat, zda se alokace provedla**
- `void free(void *ptr)`
	- <u>parametr:</u> to co chceme uvolnit
- Story: alokuj zdroj, použijeme ho, vrať paměť
```c
#include <stdio.h>
#include <stdlib.h>

int main() {
  int *ptr = malloc(sizeof(int));
  *ptr = 6969;

  printf("%d\n", *ptr); // 6969

  free(ptr);

  printf("%d\n", *ptr); // bullshit

  return 0;
}

```