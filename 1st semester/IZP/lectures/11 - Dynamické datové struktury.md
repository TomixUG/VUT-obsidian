Links: [[IZP]]
https://moodle.vut.cz/pluginfile.php/944585/mod_folder/content/0/14s_dynamicke-struktury.pdf

Přidání prvku na konkrétní místo způsobí časově náročný odsud všech následujících prvků, obdobně rušení prvku.
![[Pasted image 20241125142627.png]]


### Jednosměrně vázaný seznam
- máme položku, která má data a ukazatel na další položku
![[Pasted image 20241125142754.png]]

![[Pasted image 20241125142849.png]]
- `titem` je stejné jako struct item přes typedef

Ztratili jsme ukazatel na alokované místo v paměti
Přišli jsme o ukazatel na dané místo v paměti
fix:
- dealokuju
- předám někomu jinému

### Obousměrně vázaný seznam


#### Lineární datová struktura
- má právě jeden začátek a jeden konec

### Seznam
- seznam je prvek seznamu a ukazatel na zbytek seznamu
- nebo je seznam null
## FIFO (first in, first out)
- kdo dřív přijde, ten dřív mele