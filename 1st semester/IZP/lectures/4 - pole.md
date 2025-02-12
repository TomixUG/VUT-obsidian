Links: [[IZP]]
[[5s_ukazatel-pole-funkce.pdf]]
#### Inicializace pole
```c
char pole[10]; // by default tam hodí nuly or something
```

```c
char pole[] = {1, 2, 3, 4, 5};
```
- vytvoří se pole, poté se nakopírují data

```c
char *p = "Hello";
```
- vytvoří se ukazatel na char, ukazuje pouze na `H`.


### Čtení
`char *y[10];`
- y je pole o 10 prvcích, typu ukazatel na char
`char p[5][20]`
- p je pole o 20 prvcích, typu char pole o 5 prvcích


PROMĚNNÁ = pojmenovaný prostor v paměti
```c
const int MAX_POCET_STUDENTU = 9999;
```
- konstatní pojmenovaný prostor v paměti

### 2D pole
![[Pasted image 20241007142931.png|500]]

![[Pasted image 20241007143522.png|450]]
#### Alokace dynamického pole
- musíme dynamicky alokovat do heapu
##### Možnost 1
```c
*pic = malloc(sizeof(int) * numberofRows * numberofColumns); // ukazuje na první element v array

// pristupovani:
pic[row * columns + column];
```

##### Možnost 2 - vícenásobný ukazatel
![[Pasted image 20241007144739.png]]
- neefektivní, protože ukládáme strašně hodně informací o místě
- BAD způsob

![[Pasted image 20241007145316.png|450]]
- první vytvoříme první pointery, POČET RÁDKŮ
- poté každému zvlášť alokujeme POČET SLOUPCŮ


### enum
- zapamatuj si tyto identifikátory a přiřaď int hodnoty
```c
enum errcodes {ERR_NOER, ERR_PROFF, ERR_PAPER};
```

- můžu používat POUZE, 0 a 1
- Když ostatní **POUŽÍVEJ konstanty**!!!!! (enums)
![[Pasted image 20241007151350.png|450]]
- pak se to používá normálně jako int



### Předávání parametrů
#important 
- 2 druhy
	- *Předávání hodnotu*
		- **Kopie argumentu do parametru**
			- vytvoří se nová proměnna v pamětním prostoru
		- změna hodnoty ve funkci se vně neprojeví
	- *Předávání ukazatele na hodnotu*
		- nekopíruje se
		- změna hodnoty ve funkci se vně projeví
		
*Předávání hodnoty*:
```c
float mxf(float a, float b){
	if(a > b){
		return a;
	} else {
		return b;
	}
}

int main{
	float x;
	
	x = maxf(40, 1);
}
```
- první naalokuje `a` a `b`, poté provede if (například vyhodnotí se první podmínka): `b` se vymaže v paměti, `a` jde ven  a uloží se do `x`

*Předávání ukazatele na hodnotu*:
```c
void swap(float *a, float *b) {
  float tmp = *a;

  *a = *b;
  *b = tmp;
}

int main() {
  float x, y;
  x = 4;
  y = 8;

  swap(&x, &y);
}

```
- funkce má tzv. VEDLEJŠÍ DŮSLEDKY
	- a* a b* si vytvoří vlastní adresní prostor vzadu, aby to mohl změnit

Otázky ve zkoušce: co to udělá v paměti, jaké hodnoty budou mít variables

#### Předávání pole jako parametru
- Předá se pouze pointer na první prvek pole
- Tyto dvě jsou **totožné**
	- `void foo(int pole[], int n)`
	- `void foo(int *pole, int n)`
- V každém případě můžeme používat hranaté závorky `pole[5]`

### Dynamicky akoluj pole
![[Pasted image 20241007154516.png|550]]

- POZOR: jako argument funkce musí být pointer na pointer toho pole
	- Kvůli tomu \*\*pole
	- k