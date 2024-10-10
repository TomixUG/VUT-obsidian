Links: [[IZP]]
[[8s_strukturovane-datove-typy.pdf]]

### Specifikátor typedef
- vytváření custom datového typu
- Vytvářet pouze, když to dává smysl
```c
# custom typ, NEPOUŽÍVAT
typedef int ROCNIK;
ROCNIK a, b, c;

# tohle je realne pouziti
typedef int POLE[10];
POLE x, y, z;

```


```c
# 
typedef double (*FUN) (double, int);
FUN f1, f2;
```
- fun je ukazatel na funkci o dvou parametrech double a int, která vrací double
##### Ukazatel na funkci
- ukazuje na adresu první instrukce dané funkce

#### Typedef na struktury
- Struktury
	- Obsahuje jiné prvky, každý prvek může být **jiného** datového typu
	- Arraye se přistupuje pomocí hranatých závorek, tohle pomocí tečky
	- **Nemá to indexy**, má to tzv. **selektory**
		- Indexy se počítají v runtime
		- Selektory se "počítají" v compile time
	- Anonymní struktura
		- nemá název, nemůžeme ji uchopit, proto když ji dáme identifikátor, tak zůstavá v paměti. Proto musíme používat typedef
			- `struct {char alpha; int num; };`

```c
typedef struct tri{
	char *a;
	int b;
	int x;
} st;

int main(){
	tri myData;

	myData.b = 123;
		
}
```

##### Anonymní
```c
struct tri{
	int a;
	int b;
	int c;
}

int main(){
	struct tri myData;
	myData.a = 123;
}
```

### Enum (výčtový typ)
- čísla rostou o jedničku
- pokaždé když použiju identifikátor, C ho nahradí jeho číslem
- magická konstanta
	- stupid lol, vytvoříme int, který 1 - žlutá, 2 - modrá, 3 - oranžová
	- JUST USE ENUMS
- Dáváme na začátek zdrojového souboru
	
```c
enum {CERVENA, ZELENA, ZLUTA} mojeBarva;
mojeBarva = ZLUTA;
```

```c
enum typ_doprava {AUTO, VLAK, LETADLO, AUTOBUS};

void vypisVozidlo (int vozidlo){
	if((vozidlo < AUTO) || (vozidlo > AUTOBUS)) return;

	const char *trans [] = {"auto", "vlak", "letadlo", "autobus"};
	printf("%s", trans[vozidlo]); // one liner instead of many ifs
}
```

Můžeme si udělat poslední, která určuje kolik je tam prvků
```c
enum {A, V, L, BUS, N_TRANS};

// nyni muzeme provest if nehlede na pocet prvku

if(v >= 0 && v<N_TRANS){}
```

