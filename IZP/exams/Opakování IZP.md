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

## Variantní datový typ
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