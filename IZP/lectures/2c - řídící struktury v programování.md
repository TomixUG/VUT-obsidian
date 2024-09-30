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