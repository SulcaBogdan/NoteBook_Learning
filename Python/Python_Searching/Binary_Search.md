# Binary Search sau cautarea binara

Pe scurt, acest algoritm de căutare profită de o colecție de elemente care este deja sortată ignorând jumătate dintre elemente după o singură comparație.

## Vizualizare Binary Search

![Binary search](https://ds1-iiith.vlabs.ac.in/exp/unsorted-arrays/binary-search/images/binary_search_stepwise.png)

Acest algoritm de cautare este cel mai eficient pentru colectiile de date ordonate.

El poate fi scris in mai multe feluri iterativ sau recursiv.

## Implementarea iterativa

```python
def binarySearch(arr, x):
    low = 0
    high = len(arr) - 1
    
    while low <= high:
        mid = (high+low) // 2

        if arr[mid] < x:
            low = mid + 1

        elif arr[mid] > x:
            high  = mid - 1

        else:
            return mid
    return -1
```

Am definit metoda `binarySearch` care primeste ca argumente un array `arr` si o valoare pe care o cautam `x`.

Initializam variabila `low` cu valoarea `0` care reprezinta primul index al elementului din array.

Initializam variabila `high` cu `len(arr) - 1` care reprezinta indexul ultimului element din array.

Parcurgem array-ul cu un `while loop` cu conditia de rulare ca `low <= high` adica valoarea lui `low` sa fie mai mica sau egala cu `high`. Daca aceasta conditie nu se indeplineste (`True`) atunci loop ul se va opri si se va returna `mid`.

In blocul `while loop` Initializam variabila `mid` cu `(high + low) // 2` care reprezinta indexul elementului aflat la jumatatea array-ului.

Verificam cu `if statement` daca `arr[mid] < x` adica daca elementul din mijloc este mai mica ca elementul pe care noi vrem sa il gasim. Daca conditia este `True` atunci inseamna ca elementul nostru se afla in jumatatea din dreapta si spunem ca noul nostru `low` va fi egal cu `mid + 1` adica elementul urmator dupa mijloc. Asadar modificam intervalul de cautare. Daca conditia este `False` verificam alta conditie cu `elif statement`.

Verificam daca `arr[mid] > x` adica daca elementul din mijloc este mai mare ca elementul pe care noi il cautam. Daca elementul de mijloc este mai mare ca elementul pe care noi il cautam atunci inseamna ca `x` se afla in jumatatea de stanga. Deci noul `high` va fi egal cu `mid - 1` adica de la mijloc inapoi cu un element. Daca nici aceasta conditie nu este `True` atunci inseamna ca elementul nostru se afla fix in mijloc. 

Daca nu s-a gasit nici un element atunci returnam `-1`.

Exemplu de utilizare:

Avem un array sortat `[1,2,3,4,5,6,7,8,9,10]` si vrem sa cautam elementul `8` folosind algoritmul Binary Search.

Pentru inceput stabilim valorile lui `low` si `high`. Deci `low` `=` `0` primul index al array-ului si `high` `=` `len(arr) -1` adica ultimul index al array-ului.

Parcurgem lista folosind un `while loop` cu conditia de rulare ca `low <= high` adica indexul primului element sa fie mai mic sau egal cu indexul ultimului element din array. Se verifica conditia:

`0 <= 9` `True`.

In interiorul loop-ului initializam variabila `mid` cu `(high + low) // 2` adica indexul elementului situat la mijlocul array-ului.

Prin `if statement` verificam daca elementul de mijloc al array-ului `arr[mid]` este mai mic ca elementul nostru `x` adica `arr[4] < 8` => `5 < 8` `True`. Asta inseamna ca elementul nostru se poate afla in partea dreapta a array-ului si pentru a efectua cautarea in intervalul drept de la mijloc pana la `high` va trebuii sa setam o noua valoare lui `low`. `low` `=` `mid + 1`. Spunem `mid + 1 ` pentru a trece si peste elementul anterior din mijloc care nu este egal cu `x`.

Ne intoarcem la `while loop` si verificam iar conditia:

`low <= high` adica `5 <= 9` `True`:

Se initializeaza iar variabila `mid` cu `(high+low) // 2` adica `(9+6) //2` `=` `7`. Deci indexul `8` este noul nostru element de mijloc.

Se verifica primul `if statement` `arr[7] < 8` adica `8 < 8` `False`. Vom verifica alta conditie.

Cu `elif` se verifica daca elementul de mijloc este mai mare ca elementul `x`. Deci `arr[7] > 8` adica `8 > 8` `False`. 

Daca nici una din aceste conditi nu este `True` atunci inseamna ca elementul de mijloc este egal cu elementul pe care il cautam si returnam indexul `return mid`.

In acest exemplu elementul a fost gasit pe indexul `7` al array-ului.


## Exemplul recursiv

```python
def binarySearch(arr, low, high, x):

	if high >= low:

		mid = (high + low) // 2

		if arr[mid] == x:
			return mid
		elif arr[mid] > x:
			return binarySearch(arr, low, mid - 1, x)
		else:
			return binarySearch(arr, mid + 1, high, x)
	else:
		return -1
```

Definim metoda `binarySearch` care accepta ca argumente `arr` care reprezinta array-ul nostru, `low` care este primul element din array, `high` care este ultimul element din array si `x` care este elementul pe care vrem sa-l gasim din array.

Verificam pentru inceput cu un `if statement` daca `high >= low` adica daca indexul ultimului element este mai mare sau egal cu indexul primului element din array. Daca aceasta conditie este `True` initializam variabila `mid` cu `(high + low) // 2` pentru a selecta elementul din mijlocul array-ului.

In orice metoda recursiva incepem mereu cu un **caz de baza**. Cazul nostru de baza este ca elementul pe care il cautam sa fie exact in mijlocul array-ului, adica `arr[mid] == x` si returnam indexul unde elementul a fost gasit. Daca `x` nu este egal cu elementul din mijloc vom verifica alta conditie.

`arr[mid] > x` daca elementul din mijloc este mai mare ca `x` elementul pe care il cautam atunci returnam recursiv metoda astfel `binarySearch(arr, low, mid-1, x)` adica punem ca parametrii `arr` , `low`  pentru primul element din array, `mid-1` in loc de `high` pentru ca elementul pe care il cautam este mai mic ca elementul din centrul array-ului si `x` elementul nostru. Voi explica procesul intr-un exemplu.

Daca conditia este `False` atunci returnam direct `binarySearch(arr, mid+1, high, x)` pentru daca elementul nostru este mai mare ca elementul din mijloc inseamna ca acesta se afla in partea dreapta a array-ului si trebuie sa modificam `low` `=` `mid+1`.

Daca elementul nu este gasit returnam direct `-1`.


Exemplu de utilizare:

Avem array-ul [1,2,3,4,5,6,7,8,9,10] si vrem sa gasim elementul `8` de pe indexul `7` folosing Binary Search recursiv.

Pentru inceput verificam cu un `if statement` daca ultimul index al array-ului este mai mare sau egal ca primul index al array-ului `high >= low` => `9 >= 0` `True`, mergem mai departe.

Initializam variabila `mid` cu `(high + low) // 2` adica `(9 + 0) // 2` -> `9 // 2` -> `4`. Deci `mid = 4`

Verificam daca elementul pe care il cautam este egal cu elementul de miloc `mid`. `arr[mid] == x` adica `arr[4] == 8` -> `5 == 8`? `False`, mergem mai departe.

Verificam apoi daca elementul de mijloc `mid` este mai mare ca elementul `x`. `arr[mid] > x` adica `arr[4] > 8` -> `5 > 8`? `False`, ceea ce inseamna ca `x` este mai mare ca elementul de mijloc si va trebuii sa cautam in partea de dreapta a array-ului.

Pentru a face asta returnam recursiv direct `binarySearch(arr, mid+1, high, x)` adica `binarySearch(arr, 4+1, len(arr)-1, 8)` -> `binarySearch(arr, 5, 9, 8)` si in acest moment se va apela o alta metoda care va intra in stack.

Luam tot de la inceput cu noile valori si verificam aceleasi lucruri.

`high >= low` -> `9 >= 5` `True`

`mid = (9 + 5) // 2` -> `16 // 2` -> `8`

Verificam daca elementul pe care il cautam este egal cu elementul de miloc `mid`. `arr[mid] == x` adica `arr[8] == 8` -> `9 == 8`? `False`, mergem mai departe.

Verificam apoi daca elementul de mijloc `mid` este mai mare ca elementul `x`. `arr[mid] > x` adica `arr[8] > 8` -> `9 > 8`? `True`, ceea ce inseamna ca `x` este mai mic ca elementul de mijloc si va trebuii sa cautam in partea de stanga a array-ului. 

Asadar apelam iar metoda cu noile valori `binarySearch(arr, low, mid-1, x)` adica `binarySearch(arr, 5, 8-1, 8)` -> `binarySearch(arr, 5, 7, 8)`

Intra in stack inca o metoda `binarySearch()` si vom face aceleasi verificari.

`high >= low` -> `7 >= 5` `True`

`mid = (7 + 5) // 2` -> `12 // 2` -> `6`

Verificam daca elementul pe care il cautam este egal cu elementul de miloc `mid`. `arr[mid] == x` adica `arr[6] == 8` -> `7 == 8`? `False`, mergem mai departe.

Verificam apoi daca elementul de mijloc `mid` este mai mare ca elementul `x`. `arr[mid] > x` adica `arr[6] > 8` -> `7 > 8`? `False`, ceea ce inseamna ca `x` este mai mare ca elementul de mijloc si va trebuii sa cautam in partea de dreapta a array-ului. 

Asadar apelam iar metoda cu noile valori `binarySearch(arr, mid+1, high, x)` adica `binarySearch(arr, 6+1, 7, 8)` -> `binarySearch(arr, 7, 7, 8)`

Intra in stack inca o metoda `binarySearch()` si vom face aceleasi verificari.

`high >= low` -> `7 >= 7` `True`

`mid = (7 + 7) // 2` -> `14 // 2` -> `7`
 
Verificam daca elementul pe care il cautam este egal cu elementul de miloc `mid`. `arr[mid] == x` adica `arr[7] == 8` -> `8 == 8`? `True` si returnam `mid` care opreste metoda si returneaza indexul gasit. In acest proces se vor oprii si restul metodelor adunate recursiv din stack.

Rezultatul va fi `7`