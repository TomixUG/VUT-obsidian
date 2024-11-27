Links: [[IZP]]
https://moodle.vut.cz/pluginfile.php/944585/mod_folder/content/0/12s_rekurze.pdf

Výhoda:
- tady máš měšec spočítej, kolik je tady mincí, ale vrať mi ten měšec, takový který byl
	- na loopy bychom potřebovali 2 měšce
	- Zde stačí pouze jeden

### Definice
- Specifikace entity odkazem na sebe sama
- Rekurzivní funkce
	- funkce, která je definována pomocí volání sebe samé
##### Příklad faktoriál
- faktoriál (0) = 1
- faktoriál (n) = n x faktoriál (n-1), pro n > 0
![[Pasted image 20241118143213.png|350]]

#### DŮLEŽITÉ (zkouška possibly?)
- **Každou rekurzi, lze nahradit iterací (a naopak)**

##### Iterace
- pomocí **cyklů**
- sekvence příkazů, která je vykonávaná opakovaně na základě testu podmínky
- podmínka ukončení *je nezbytná*, jinak infinite cycle

#### iterace -> rekurze
![[Pasted image 20241118144401.png]]

#### Cyklus s podmínkou na konci -> rekurze
![[Pasted image 20241118144439.png]]

### Seznam
- je rekurzivní datová struktura

```c
struct seznam {
	student data;
	struct seznam *zbytek_s; // zbytek seznamu
}
```

Lineární jednosměrně vázaný seznam

### Rekurze a zásobníková paměť
- při volání funkce se na vrcholu zásobníku vymezí oblast potřebná pro
	- lokální proměnné
	- argumenty, se kterými byla funkce volána
	- výsledek funkce (když vrací hodnotu)
	- informace pro správný návrat z funkce
- toto se jmenuje **aktivační záznam funkce**

### Zásobník
- typická velikost několik MB
- Každá iterace rekurze zabírá paměť zásobníku, může se přeplnit

## Druhy rekurzí
#### Přímá reukze
- ve svém těle volá sama sebe
#### Nepřímá rekurze
- A volá B
- B volá C
- C volá A
- **NEPOUŽÍVAT NIKDY!!! Lol**

## zkouška
- máme funkci, jaká bude hodnota parametru proměnných
- NEBO vyřešte nějaký problém pomocí přímé rekurzivní funkce

## Fibonacci
![[Pasted image 20241127161048.png]]


Můžeme použít windows z arraye, pouze část arraye, Window.
implementace tohoto algoritmu bez rekurze je o dost efektivnější


# Buffer
- abychom maximalizovali rychlost
- aby někdo nečekal na někoho jiného
- první zpracovává a druhý může zároveň zpracovávat
- **minimalizovat čekání**
- 