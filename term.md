Links: [[IZP]]

# Kód

### arrays
```c
int a[11] = {7, 6, 4, [7] = 10, 9, 8, 5};
```
- data budou vypadat následovně
- 7 6 4 0 0 0 0 10 9 8 5
- 0 1 2 3 4 5 6 7 8 9 10

#### Argumenty
```c
int main(int argc, char *argv[]) {}
```

#### printf

| identifier | datatype                                |
| ---------- | --------------------------------------- |
| %d %i      | **i**nteger                             |
| %f         | **f**loat, double (floating point)      |
| %c         | char (**c**haracter)                    |
| %s         | char array (**s**tring)                 |
| %x         | he**x**adecimal (pointer address value) |
##### formatters
`printf("%.3f")`
tiskne na tři desetinná místa

#### scanf
čte z stdin
```c
int b;
char text[];
scanf("%d %s", &b, text);
```
- u int musí být apersand, protože funkce to plní pomocí pointerů
- u char array nikoliv, protože arraye jsou vlastně pointery na první prvek v array

#### sscanf
čte ze stringu
```c
   const char *input = "42 Alice";
   int number;
   char name[20];

   int result = sscanf(input, "%d %s", &number, name);
```

#### fscanf
čte ze souboru
```c
FILE *ptr = fopen("file.txt", "r");

int num;
fscanf(ptr, "%d", &num);
```

#### getchar()
získá jeden character z stdin
returns EOF after end of file
```c
char c = getchar();
```

#### getc(FILE)
returns EOF after end of file
```c
FILE *ptr = fopen("file.txt", "r");
char c = getc(ptr);
```
EOF je -1
#### fgetc(FILE)
```c
FILE *ptr = fopen("file.txt", "r");
char c = fgetc(ptr);
```
**TO STEJNÉ**, ALE JE TO MACRO


### Char arrays (strings)

| 5     | h   | e   | l   | l   | o   | <br>\0              |
| ----- | --- | --- | --- | --- | --- | ------------------- |
| délka |     |     |     |     |     | <br>ukončující znak |

### ternární operátor (jednařádková podmínka if)
```c
int b = (a == 10 ? 1 : 0);
//     pokud   tohle   jinak tohle

```


### Variable scope
```c
  int cislo = 10;
  printf("%d\n", cislo); // 10

  for (int i = 0; i < 1; i++) {
    int cislo = 20;
    printf("%d\n", cislo); // 20
  }

  printf("%d\n", cislo); // 10
```
lokální x globální proměnné



## Základní stavební bloky
```c
// V PODMINKACH MUSI BYT NENULOVE CISLO
// if
if(a == 0){
}

// while
while(a == 0){
}

// do while
// probehne vzdy alespon jednou
do{
	// code here
} while(a == 0);

//for 
// podminka je 'i < 10', to musi byt nenulove cislo, zbytek je whatever
for(int i = 0; i < 10; i++){
}
//for (init, condition, increment)
//{}
// *inicializace* část se provede pouze jednou na začátku
// *condition* (boolean), pokaždé se zkontroluje
// *increment* zvyšuje

// switch
switch (a) {
  case 10:
    printf("10");
    break;
  case 20:
    printf("hello");
    break;
  default:
    printf("not found");
    break;
  }
```
#### co musím dát do if, aby se provedl
```c
  if (-10) {
    printf("hello\n");
  }

```
- **JAKÉKOLIV NENULOVÉ ČÍSLO**

#### cykly
- continue;
	- přeskočí to co zbývá v cyklu a jde na novovu iteraci
- break;
	- ukončí cyklus kompletně

### Pointers
**Ampersand** nám dá adresu v paměti dané proměnné. (**= referenční operátor**)
**Dereferenční operátor** (\*) nám vrátí zpět value proměnné
```c
int *pi = NULL; // deklerace pointeru
int a = 112;

pi = &a; // reference proměnné a (získání adresu na proměnnou a)
printf("%d", *pi); // dereference promenne pi
```

#### void pointer
pointer, který nemá specifikovaný datový typ
```c
// a muze byt jakykoliv datovy typ
//int a;
//char a;
//float a;
double a;

void* p = &a;
```


## Dynamická alokace
do heapu, pomocí malloc
KNIHOVNA `#include <stdlib.h>`
```c
  int *a = malloc(sizeof(int));
  if (a == NULL) {
    printf("rip");
    return 1;
  }

  *a = 100;

  free(a);
```
- Po malloc musíme dát kontrolu, zda je null `if(a == NULL)`

#### Inicializace pole
```c
char pole[10]; // by default tam hodí nuly or something
```

```c
char pole[] = {1, 2, 3, 4, 5};
char pole[] = "hello";
```
- vytvoří se pole, poté se nakopírují data

```c
char *p = "hello";
```
- vytvoří se ukazatel na char, ukazuje pouze na `H`.
#### Pole v poli (2D a více array)
`char *y[10];`
- y je pole o 10 prvcích, typu ukazatel na char
`char p[5][20]`
- 5 dvaceti prvkových arrajů
```c
int matrix[2][6] = {
	{1, 2, 3, 4, 5, 6},
	{7, 8, 9, 10, 11, 12}
};
```

#### **Alokace dynamického pole**
- musíme dynamicky alokovat do heapu
```c
*pic = malloc(sizeof(int) * numberofRows * numberofColumns); // ukazuje na první element v array

// pristupovani:
pic[row * numberofColumns + column];
```

## enum
- zapamatuj si tyto identifikátory a přiřaď int hodnoty
```c
enum errcodes {ERR_NOER, ERR_PROFF, ERR_PAPER};
//                0        1          2
```

#### Deklerace
```c
  // udelame instanci enumu
  enum { ERR_NOER, ERR_PROFF, ERR_PAPER } err;
  err = ERR_PAPER;

  // udelame obecnou enum ERR_ENUM ze ktereho pak muzeme udelat instanci
  // (promenna ktera ma datovy typ toho enumu)
  enum ERR_ENUM { APPLE, BUS, CAR };
  enum ERR_ENUM things;
  things = APPLE;

  // anonymni enum
  enum { PHONE, LAPTOP, TV };
```

### Předávání parametrů
- 2 druhy
	- *Předávání hodnotu*
		- **Kopie argumentu do parametru**
			- vytvoří se ***nová*** proměnna v pamětním prostoru
		- změna hodnoty ve funkci se venku neprojeví
	- *Předávání ukazatele na hodnotu*
		- nekopíruje se
		- změna hodnoty ve funkci se venku projeví

### Structs
struktura, ukládá více proměnných v jedné proměnné
##### Deklarace bez typedef
- musíme použit slovo struct pro vytvoření instance
```c
// klasicka definice
struct Data {
	int a;
	int b;
	char str[100];
};

// vytvoreni instance
struct Data d = {.a = 1, .b = 2, .str = "hello"}; // POUZIVA se slovo struct
// pristup
d.a = 10;
d.b = 10;

```

##### Deklarace s typedef
- nemusíme použít slovo struct pro vytvoření instance
```c
// pomoci typedef
typedef struct {
	int a;
	int b;
	char str[100];
} Data;

// vytvoreni instance
Data d = {.a = 1, .b = 2, .str = "hello"}; // NEPOUZIVA se slovo struct
d.a = 10;
d.b = 10;

```

#### Struct a pointers
- když je struct pointer přistupujeme k jednotlivým prvkům pomocí šipky
	- `->`
	- ta automaticky provede dereferenci
		- (ekvivalentní zápis jako `*(ptr).element` narozdíl od `ptr->element` )
```c
typedef struct {
	int a;
	int b;
	char str[100];
} Data;

Data d = {.a = 1, .b = 2, .str = "hello"};

// vytvoreni pointeru
Data *ptr = &d;

ptr->a = 10;
ptr->b = 20;
```

#### Dávání struct jako parametr funkce
- Celý datový obsah toho structu se **překopíruje**
	- takže pokud chceme struct ve funkci měnit musíme ho předat jako pointer:

```c
// ukázka předání structu jako pointer

typedef struct {
  int a;
  int b;
  char str[100];
} Data;

void doSomething(Data *data) {
  // TOTO ZMNĚNÍ PŮVODNÍ STRUCT
  data->a = 691;
}

int main() {
  Data d = {.a = 1, .b = 2, .str = "hello"};

  printf("%d", d.a); // 1

  // předání
  doSomething(&d);

  printf("%d", d.a); // 691

  return 0;
}

```

#### Dynamická alokace structu
- normálně do mallocu stačí hodit `sizeof(struct)`. A naalokuje nám celý struct
```c
Data *d = malloc(sizeof(Data));
```

## Práce s textem
Jednoduché uvozovky
- **JEDEN ZNAK**
Dvě uvozovky
- **string** (slovo)
#### Knihovna <string.h>
**strcmp** 
- Porovnání stringů
- pokud se rovnají funkce vrátí jedničku
```c
if(strcmp(argv[1]) == "open"){
	printf("strings match");
}
```

## Práce se soubory
```c
// open the file
FILE *ptr = fopen("FILEOPEN.txt", "r");
```
- Čtení ze souboru
```c
int a;
fscanf(ptr, "%d", &a);
```
- Psaní do souboru
```c
fprintf(ptr, "hello %d", &a);
```

## Vrácení hodnoty v return
- můžeme returnout true nebo false takto
```c
return a == 1 && b == 2;
```


## Dělení
- POZOR DĚLENÍ INTEGERU INTEGEREM VZNIKÁ **INTEGER**
```c
  int a = 10;
  int b = 3;
  printf("hello: %d\n", (a / b)); // 3

```
- v tomto příkladu výjde 3 
- Pokud chceme dělit, tak alespoň jedno z čísel **musí být double nebo float**
# Teorie

## Bugy
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

## Syntaxe:
- Soubor pravidel udávající přípustnou kontrukci programu. Popisuje formální strukturu programu. Definuje klíčová slova, identifikátory, čísla.
- lze podle toho zjistit, zda je text korektní zápis programu v daném jazyce
- *jak se if píše*
## Sémantika
- určuje logický význam jednotlivých výrazů jazyka. 
- ze sémantiky plyne, jaký má daná konstrukce význam
- *jak pracuje if*

## Datové typy
Jméno datového typu
Jak jsou bity zakódované, co znamenají ty 1 a 0

## Argumenty vs parametry
![[Pasted image 20240925172356.png]]

## memory
![[Pasted image 20241002162709.png|250]]
- Zásobník (stack)
	-  nadefinujeme **před kompilací**, můžeme je měnit
	- **dynamické proměnné, které se mění**
- Hromada (heap)
	- dynamicky alokujeme přes malloc
	- musíme dát free
	- **dynamické proměnné, které se mění**
- datová oblast
	- například, když před kompilací vytvoříme string hello, tak se uloží tam
	- **statické proměnné, které se nemění**
- kódová oblast
	- obsahuje instrukce programu


## Postup ladění
1. Reprodukce (hledání vstupních dat, bug report)
2. Diagnóza
3. Oprava (bug fix)
4. Intergrace (fix test, commit)

#### Techniky ladění
- Statická analýza
	- čtu kód očima
- Dynamická analýza
	- **záznam sekvence** 
		- printy
	- **interaktivní** 
		- debugger

### Jednotkové testy
![[Pasted image 20250107182626.png]]


## Druhy hledání
#### 1) Sekvenční
- hledáme položku po položce od začátu po konec
#### 2) Nesekvenční
- binary search
	- **MUSÍ BÝT SEŘAZENÉ**
	- pouze na hledání porovnatelných klíčů (čísla)
	- Jdu přesně do půlky, porovnám sousedy, podle toho jaký je vyšší. Jdu do té půlky, tam vyberu prostřední prvek a opakuji
		- ![[Pasted image 20250107184909.png]]

## Řazení (sorting)
#### 1) sekvenční řazení
- např.: linked list nemůžeme přímo přístupovat
- musíme projet vždy celý list položka po položce
- Definice:
	- je vlastnost, která vyjadřuje, že řadící algoritmus pracuje se vstupními údaji i s datovými meziprodukty v tom pořadí v jakém jsou lineárně uspořádány v datové struktuře
#### 2) nesekvenční
- např. pole
- **přímý přístup** k jednotlivým položkám
- prostě když je jít na index 69, tak bez problému můžeme

### Vlastnosti metod řazení
- **přírozenost**
	- čas T(seřazená) < T(náhodně uspořádaná) < T(opačně uspořádaná)
- **stabilita**
	- když máme více identických klíčů, algoritmus zachová jejich pořadí (a nepřehazuje je)
- **in situ**
	- pracujeme rovnou tam, kde se ta data nachází. *Nekopírujeme je*
	- metoda pracuje přímo v místě uložení řazených dat
- **složitost**
	- je prostorová a časová
		- kolik místa potřebujeme, jak dlouho to bude trvat
### Bubble sort
![[Pasted image 20250107190512.png]]
### Selection sort
![[Pasted image 20250107192217.png]]
## Rekurze
- Způsob specifikace entity odkazem na sebe sama
##### Faktoriál:
```c
unsigned int fact(unsigned int n)
{
	if (n == 0)
		return 1;
	else
		return n*fact(n-1);
}
```
##### Fibonacci sequence
```c
int fibo (int n)
{
	if ((n == 0) || (n == 1)) return n;
	else return fibo(n-1) + fibo(n-2);
}
```
### How it works
Příklad jak to funguje
```c
void tisk(int n)
{
	if (n > 1) tisk(n-1);
	printf("%d ", n);
	return;
}
// 1 2 3 . . . . n
```
- tato funkce tiskne od konce
- **u volání tisk(n-1) se zopakuje a prinf se provede až když if není true**
Stejný příklad, ale tiskne naopak
```c
void tisk(int n)
{
	printf("%d ", n);
	if (n > 1) tisk(n-1);
	return;
}
// n . . . 4 3 2 1
```
- printf se provede pokaždé a až pak se znovu volá funkce tisk(n-1)
