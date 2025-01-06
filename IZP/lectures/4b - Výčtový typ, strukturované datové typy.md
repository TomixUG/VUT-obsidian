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


c
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

![[Pasted image 20241027222811.png]]

Heterogenní

K poli přistupujeme pomocí indexace
- Indexace počítá KDY **za běhu programu**
- index je dynamický
- počet prvků je **statická vlastnost**
	- pole je statická struktura z ohledem na počet prvků
K záznamu přistupujeme pomocí selektorem
- 

Seznam
- každý jeho prvek vystupuje sám za sebe

## Datové typy
- unsigned int
	- <0; 2^32>
- unsigned long int
	- <0; 2^64>
- unsigned long long int

sizeof(int) <= sizeof(long int) <= sizeof(long long int)

## Pointer na struct
- pointer na struct má stejnou velikost jako prostě normální ukazatel
```c
typedef struct TOsoba{
	int vyska;
	int vek;
	double vaha[4];
};
...

TOsoba o;
TOsoba *p = &o;

// UKOL: accessni posledni prvek vahy pomoci pointeru p
// nasledujici napisy jsou ekvivalentni
(*p).vaha[3];
p->vaha[3];
```
- přímá struktura používáme tečku `.`
- ukazatel na strukturu používáme šipku `->`

#### Jak funguje scanf
- dívá se na stdin, dívá se na ta data, proccesinguje to a hledá ty formatter strings
- `scanf("%d", &myVar);`
- vrací počet proměnných, které se mu povedlo transformovat

### Structs
- incicializace:
```c
typedef struct {
	int vyska;
	int vek;
	double vaha;
} TOsoba;

TOsoba c4 = {.vyska = 12, .vek = 4, .vaha = 4.4};
TOsoba c4 = {25, 182, 82.5}

```
#### dynamic
```c
TOsoba = *novyClovek = malloc(sizeof(TOsoba));
```

