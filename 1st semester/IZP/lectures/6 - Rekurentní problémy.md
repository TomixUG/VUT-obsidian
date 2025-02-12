Links: [[IZP]]
https://moodle.vut.cz/pluginfile.php/944585/mod_folder/content/0/9s_rekurentni-problemy.pdf

### Pojmy
- rekurentní - opakující se 
- statická data - konstanty, nemění se (const)
- dynamická data - proměnné
	- dynamická data, které se mění
	
- proměnná - pojmenované místo v paměti identifikátorem
- 

Rekurzivní
- pomocí sebe sama

Rekurentní
- Opakování
- Základem je cyklus (for - s známým počtem opak, while - cyklus s podmínkou na začátku, do while)

první iterace (nultá)
iterace
Nekonečný cyklus
- nekonečné množství iterací
	- semafor nepřestane fungovat
	- OS se nevypne
	
Rekurentní problémy **implementujeme pomocí cyklů**
- Posloupnosti
	- Cíl je
- Řady
- Predikát
	- jestli jsem spokojen z Yi-k nebo ještě ne

![[Pasted image 20241021142700.png]]

Uvažujeme rekurentní vztah:
$$Y_{i+1} = F_{Yi}$$
# Algoritmické schéma
- algoritmus
- schéma - můžeme aplikovat na něco jiného
![[Pasted image 20241021143000.png|400]]

- Jediné, co se mění jsou Y, A je konst
$$y_{i+1} = \frac{1}{2}(\frac{A}{y_i} + y_i)$$
Predikát B, jak blízko chceš být u cíle

#### Postupná aproximace
![[Pasted image 20241021144200.png]]
- pro zjištění konce, reálný konec neznáme
![[Pasted image 20241021144323.png|400]]
- než se systém usabilní (nikdy, v nekonečnu), nám stačí jestli je dostatečně

### Jak ukončit program
- výpočet se opakuje, dokud $|y_i - y_{i+1}|$ není menší něž nějaká zadaná hodnota
- této hodnotě se říká přesnost výpočtu - značíme **eps**

- přesnost může být podle velikosti proměnné (float, double)

### Algoritmus
![[Pasted image 20241021144704.png|400]]
- Opakuj dokud nové a staré je v přesnosti definované eps

### Jak násobí počítače mocninou dvojky:
![[Pasted image 20241021145817.png]]
- přičitá počet nul dle mocniny
- Floating point není přesný


Posloupnost
- postupně počítáme než se dostaneme na dostatečnou přesnost


Vezmu všechny členy, sečtu je dohromady.
- Postupně jsem s prvním sčítáním spokojen? Ne, přitču další, jsem s druhým sčítáním spokojen? Ne, pričtu další, ......... Ano jsem spokojen, hotovo
- $|t_n < eps|$

- ![[Pasted image 20241021152539.png|450]]
![[Pasted image 20241021152651.png|450]]
Tailorova řada (taylor polynomial)
- například sinus, logaritmus, ..
![[Pasted image 20241021152855.png|400]]


S - součet všeho co jsme vypočítali
T = momentální člen
![[Pasted image 20241021153919.png|300]]

### Aproximace Eulerova čísla
![[Pasted image 20241021154212.png|450]]
- nekonečný

