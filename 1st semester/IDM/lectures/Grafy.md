LInks: [[IDM]]

Stupně grafu: počet spojení v bodě
Izomorfní graf = stejnost
- postup:
	- Sedí počty vrcholů?
	- sedí posloupnost stupňů?
	- zkusit mirrornout

Je graf souvislý
- jestli je pospojovaný? Jestli má pouze jednu komponentu?

Kružnice
- je to spojené ve tvaru kruhu
- **nejmenší kružnice je trojúhelník**, dále více úhelníky

Strom
- graf **bez** kružnic
- nemá žádné cykly
- souvislý
Les
- jednoduchý graf bez kružnic (nemusí být souvislý)

Minimální kostra
- = je strom
	- musí být souvislý (z každého vrcholu se musíme dostat do každého)
- budeme vyhazovat hrany
- některé cykly jsou redundantní
- Váha (délka) kostry
	- sčítám všechny ohodnocení kostry
- Jarníkův algoritmus
	1. vyberu si random bod
	2. najdu nejbližšího souseda (marknu bod a souseda jako zpracované)
	3. ze všech **zpracovaných bodů** hledám nejbližší (pozor ať neudělám kružnici)
	4. takto pokračuju dále
	- https://mst-calculator.vercel.app/

Rovinný graf
- když nemá žádné překřížení
- Pokud je graf rovinný **nesmí obsahovat podgrafy**
- ![[Pasted image 20241223022224.png]]
	- rozpoznání rovinných grafů
		- když má trojúhelník
			- ![[Pasted image 20241223022906.png]]
			- v - počet vrcholů
			- to na začátku - počet hran
		- Když nemá trojúhelník
			- ![[Pasted image 20241223022857.png]]
		- Příklad
			- ![[Pasted image 20241223023017.png]]

Stěna
- oblast ohraničená hranami

Lze sestrojit graf?
![[Pasted image 20241223140213.png]]
- vezmeme si ty body 
	- 1,1,1,2,3,4
	- seřadíme od nejmenšího po největší
	- podíváme se na nejvyšší element a od tolikati členů jako je hodnota toho elementu odečteme jedničku. A ten element zahodíme
	- pokračujeme dále
	- ![[Pasted image 20241223140242.png]]

## Řešení disktrijktova algoritmu
první příklad
![[Pasted image 20241222162158.png]]
druhý příklad
![[Pasted image 20241222162133.png]]

třetí
![[Pasted image 20241222183215.png]]

čtvrtý
![[Pasted image 20241222182820.png]]

pátý příklad
![[Pasted image 20241223021944.png]]