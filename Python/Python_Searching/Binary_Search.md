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






 
