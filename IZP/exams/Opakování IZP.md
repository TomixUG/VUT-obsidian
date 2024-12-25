Links: [[IZP]]

**Jednosměrně vázaný seznam**
- každá dodá informace, kdo je její následník
	- tudíž nepotřebuji to označení, že se jedná o kolekci
	- vidím pouze *hlavní proměnnou*
- máme pouze first (head), pomocí ní se dostaneme dál

každá položka má datový typ toho structu:

| DATA | Next    |
| ---- | ------- |
| int  | pointer |

```c
typedef struct item titem;

struct item{
  int data;
  titem *next;
};

// když chceme alokovat první prvek
head = malloc(sizeof(titem));
if(head == NULL){
	return 0;
}

head->next = NULL;
head->next = tmp;
```

```c
// zkontroluje, zda je seznam rostoucí
bool rostouci(titem *head){
	if(head == NULL)
		return true;
	titem *tmp = head;

	while(tmp->next != NULL){
		if(tmp->data > tmp->next->data)
			return false;
	
		tmp = tmp->next;
	}

	return true;
	
}
```

# Variantní datový typ
- uchovává hodnotu předem neurčeného datového typu
- datový typ se vybírá z pevně stanovené množiny datových typů v době přiřazení
- ![[Pasted image 20241202153028.png]]

- Pomocí **UNION**
	- na stejné místě v paměti může být více datových typů, ale pouze jeden najednou můžeme použít
	- ![[Pasted image 20241202153337.png]]


# Espace frekvence
= znaky, které mají v řetězcích jiný význam než doslovnou reprezentaci znaků
- Příklady 
	- "Hello, world\n" (C)
	- "The file is \"output.txt\"." (C)
	- "The word ""output"""(CSV)

# Stavový automat
- Finite State Machine (FSM)
	- model výpočetního/řídícího systému, který  se skládá z konečné množiny stavů a přechodů mezi nimi
- Jedna ze základních formálních definic: $M=(Q, \Sigma, \phi)$
- v různých rozšířených obdobách
- složen z
	- množiny stavů
	- množiny možných vstupů (symbolů)
	- počáteční stav
	- přechodové relace
	- množiny akcí
- Automat má právě jeden stav aktivní. "Automat se nachází ve stavu XY"
- Automat postupně přijímá vstupy a přechází mezi stavy na základě daných přechodů
	- posloupnost symboů na vstupu může být nekonečná
	- symbol může reprezentovat událost (např.: window_closed, serviceFailed)
	- symbol může být parametrický, tj. může nést dodatečnou hodnotu (userAuthed("john"))
	- ve zvláštních případech symbolů může být popsán predikátem (pravdivostním výrazem). Ten je nazýván stráž/guard (vehicle_speed > 90)
- Výhoda
	- můžeme je **graficky reprezentovat**
	- ![[Pasted image 20241204162114.png|250]]
		- uzly reprezentují stavy
		- orientované hrany reprezentují přechody
		- hrany jsou označené (popsané) vstupním symbolem, případně i akcí prováděnou při aplikaci přechodu mězi stavy
		- popis
			- Šipka - počáteční stav
- Typy automatů
	- dle jednoznačnosti vstupu
		- **Deterministické**
			- z každého stavu existuje maximálně jeden proveditelný přechod. Jednoduché pro implementaci
		- **Nedeterministické**
			- jednodušší na tvorbu. Je nutno provést determinizaci
##### Využití
- Validace
	- kontrolují platnost nějakého řetězcového vstupu (např.: kontrola formátu emailové adresy)
	- *vstup*: zřetězená data
	- *výstup*: pravdivostní (řetězec přijat = koncový stav, nepřijat)
- Transformace
	- transformují jeden vstup na jiný (např.: kodér Morseovy abecedy)
	- *vstup*: zřetězená data
	- *výstup*: zřetězená data jiného formátu
- Řízení
	- slouží pro ovládání konečně stavového stroje (např.: řídící jednotka výtahu, semaforu)
	- *výstup*: aktivace aktualizace pomocných proměnných, řídící signály pro pomocné jednotky (světla, aktuátory, ...)
	- *výstup*: 
