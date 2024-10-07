Links: [[IZP]]

### Práce s pamětí
- Buď čtení z adresy nebo zapisování do adresy

Nic nikdy neexistuje
- Kdyžtak undefined value

##### Každá proměnná má 3 věcí:
- jméno (s tím pracují programmers)
- datový typ
- adresa v paměti (to dělá překladač)

```c
int c;
```
- Překladač vyhradí v paměti místo pro proměnnou `c`.
- Existuje tabulka, ve které si o každé proměnné uloží
	- její adresu
	- jak se jmenuje
	- datový typ
- Takže když chceme uložit data do proměnné `c = 42;`
	- Program najde adresu proměnné, uloží na tu adresu číslo 42.

Funkce:
- Něco to vezme, něco to udělá a dá nám výsledek


Pozmění stav programu (nebo systému):
`x > - (y=(a+b)*c*d))`
- funkce, podprogramy mají vedlejší efekt
	- Vedlejší efekty jsou nechtěné
		- např. zapisování na pointer

## Operátory
- Ternární operator (if then else operator zkratka ITE)
- if podmínka
	- datový typ musí být stejný u porovnávání
## Výraz
- Má vstup a výstup
- Ve funkcionálních jazyků jsou pouze **výrazy**
- V C dáváme sekvenci příkazů

Složený příkaz (compound)
```someLanguage
{
	something1;
	something2;
	something3;
}
```
- jde to po sobě
- instruction pointer (program counter)
	- Říká, kolikátý příkaz má zrovna vykonat

- Jak zakódujeme jestli plus nebo mínus?
	- Uděláme **výčtovou tabulku** (ukazuje, jaký kód patří k jakému operátoru)

#### no effect
- příkaz by začal dávat smysl, pokud by měl efekt

#### Příkaz volám podprogram (funkci) (call, poté return):
- `foo()`
- `printf()`
- Volám další skupinu příkazů

#### řídící instrukce:
- if
- Podmínka (condition, decision) rozhoduje se jestli má jít pozitivní nebo negativní větví
	- větev má více příkazů
	- Rozhoduje se podle boolean
	- V podmínce může být libovoný výraz, kterého return type je boolean
#### Cyklus
- sekvence uzlů, kde se dostaneme na začátek, odkud jsme vyšli
	- Když se splní podmínka provede znova příkaz, když se podmínka nesplní ukončí se 
- zase jeden vstup a jeden výstup

### 'while'

```c
while (foo(b))
{
	b = bar(b);
}
```
- dokud platí podmínka `foo(b)` měň proměnou `b` pomocí funkce `bar(b)`

### 'do while'
- první provede poté až zkouší
```c
do {

} while (condition);
```

### 'for'
- Stejná funkcionalita jako `while`, ale jednodušší
- Pro **známý počet opakování**
- inicializace, pokud podmínka platí pokračuj body, incrementuj, ...
```c
for (init, condition, increment)
{
	body
}
```
- *inicializace* část se provede pouze jednou na začátku
- *condition* (boolean), pokaždé se zkontroluje
- *increment* zvyšuje

### 'switch'
- jedna podmínka, více cases
- vypočítá výraz (v condition) datový typ musí být **ORDINÁLNÍ**
	- takový typ, jehož hodnoty mají předchůdce i následovníky (`int`, `char`)
	- bitově zkoumá jestli jsou si ty proměnné rovni
- Když je to ono proveď
- Když to není ono, zeptej se následovníka
- Dokud nedojdeme na `default`
- Pokud je tam `break`, tak ukončí celý switch
- je to basically **sada ifů**
```c
switch (condition){
	case 'first': 
		amogus;
}
```
- reálně to v C funguje takto:
	- basically sada ifů
	- brake je VELICE DŮLEŽITÉ
	- ![[Pasted image 20240930150804.png]]
### Keywords v cyklu
##### brake
- nehledě na whatever, prostě ukonči cyklus
- zkratka ven pryč z cyklu
##### continue
- rovnou odskoč na podmínku, jestli má cyklus pokračovat
- skipni current iteration

##### (goto)
- přeskoč někam úplně někam, hodně random lol
- NIKDY NEPOUŽÍVEJ xdd
### Algoritmus
- Strukturálně je to složenina různých řídících instrukcí v sobě vnořených
	- třeba if v tom loop v tom loop v tom if, ....
	