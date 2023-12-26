# Selection Sort

Această tehnică de sortare găsește în mod repetat elementul minim și îl sortează în ordine. 

În timpul executării acestui algoritm, sunt menținute două subbarray:
1. Un subbarray care este deja sortat;
2. Un subbarray rămas care este nesortat. 
 
În timpul execuției Selection Sort pentru fiecare iterație, elementul minim al subgrupului nesortat este aranjat în subbary sortat. Selection Sort este un algoritm mai eficient decât  Bubble Sort. Sortarea are un time complexity de O(n2) în medie, în cele mai rele și în cele mai bune cazuri.

### Vizualizare Selection Sort

![Selection Sort](https://www.swtestacademy.com/wp-content/uploads/2021/11/selection-sort-Selection-Sort-1.drawio-1.png)

### Implementarea Selection Sort

```python
def selectionSort(arr):
    n = len(arr)

    # Parcurgem array-ul
    for i in range(n):
        # Inițializăm indexul minim la începutul fiecărui pas
        min_idx = i

        # Căutăm cel mai mic element în restul array-ului
        for j in range(i+1, n):
            if arr[j] < arr[min_idx]:
                min_idx = j

        # Facem schimbul între elementul curent și cel mai mic element găsit
        arr[i], arr[min_idx] = arr[min_idx], arr[i]

    # Returnăm array-ul sortat
    return arr
```

Primul pas este sa initializam o variabila `n` cu numarul elementelor din array `len(arr)`.

Apoi parcurgem array-ul folosind `for loop` cu variabila `i` in `range(n)` adica lui `i` ii vor fi atribuite valorile lungimii array-ului incepand de la `0` pana la sfarsitul lungimii.

Initializam o variabila `min_idx` cu `i` adica cu fiecare index din array.

Al doilea `for loop` cu variabila `j` in `range(i+1, n)` adica in `range(0+1, lungimea array-ului)` adica de la al doilea index din array pana la lungimea array-ului.

Urmeaza un `if statement` unde verificam daca `arr[j]` `<` `arr[min_idx]` adica daca elementul curent de pe pozitia `j` este mai mic decat elementul minim gasit pana acum `arr[min_idx]`. Daca este `True` se actualizeaza `min_idx` cu `j`.

Dupa ce s-a gasit cel mai mic element din restul array-ului, se face un `swap` intre elementul curent de la pozitia `i` si cel mai mic element gasit `min_idx`. -> `arr[i], arr[min_idx] = arr[min_idx], arr[i]`

La final se returneaza array-ul sortat.

Exemplu de utilizare:

Avem un array `[64, 25, 12, 22, 11]` si vrem sa il sortam folosind algoritmul Selection Sort.

Initializam variabila `n` cu `len(arr)` adica cu lungimea array-ului care este `5`.

Parcurgem array-ul cu un `for loop` cu variabila `i` in `range(n)` adica `i` va primi fiecare index ca valoare de la `0` la `5`. Valoarea lui `i` `=` `0`

Initializam variabila `mid_idx` `=` `i` care reprezinta indexul minim la inceputul fiecarui pas, adica `mid_idx` `=` `0`

Apoi va trebuii sa cautam cel mai mic element din array cu un alt `for loop` cu variabila `j` in `range(i+1, n)` adica `range(0+1, 5)` => de la `1` la `5`.

Verificam in acest loop daca `arr[j]` `<` `arr[min_idx]` adica `arr[1]` `<` `arr[0]` =>
`25` `<` `64` care este `True` si vom actualiza variabila `min_idx` cu `j` adica cu `1` si mergem mai departe.

`j` `=` `2` ,  `arr[2]` `<` `arr[1]` adica `12` `<` `25` `True` vom actualiza variabila `min_idx` cu `j` adica cu `2` si mergem mai departe.

`j` `=` `3`, `arr[3]` `<` `arr[2]` adica `22` < `12` `False` mergem mai departe.

`j` `=` `4`, `arr[4]` `<` `arr[2]` adica `11` `<` `12` `True` vom actualiza variabila `min_idx` cu `j` adica cu `4` si ne oprim.

Dupa ce s-a gasit cel mai mic element din restul array-ului, se face un `swap` intre elementul curent de la pozitia `i` si cel mai mic element gasit `min_idx`. -> `arr[i], arr[min_idx] = arr[min_idx], arr[i]` adica `arr[0], arr[4] = arr[4], arr[0]` => `64, 11 = 11, 64`.

Array-ul arata asa acum `[11, 25, 12, 22, 64]`

Revenim la primul `for loop` si valoarea lui `i` este acum `1`. Initializam variabila `mid_idx` `=` `i` care reprezinta indexul minim la inceputul fiecarui pas, adica `mid_idx` `=` `1` si repetam procesul de mai sus incepand de pe indexul `1`.

Verificam daca `arr[j]` `<` `arr[min_idx]` adica `arr[2]` `<` `arr[1]` => `12` `<` `25` `True` actualizam variabila `min_idx` cu `j` adica cu `2`.

`arr[3]` `<` `arr[2]` adica `22` `<` `12` `False` mergem mai departe.

`arr[4]` `<` `arr[2]` adica `64` `<` `12` `False` si oprim loop-ul.

Dupa ce s-a gasit cel mai mic element din restul array-ului, se face un `swap` intre elementul curent de la pozitia `i` si cel mai mic element gasit `min_idx`. 

-> `arr[i], arr[min_idx] = arr[min_idx], arr[i]` adica `arr[1], arr[2] = arr[2], arr[1]` => `25, 12 = 12, 25`.

Array-ul arata asa acum `[11, 12, 25, 22, 64]`.

Revenim iar la primul `for loop` si valoarea lui `i` este acum `2`. Initializam variabila `mid_idx` `=` `i` care reprezinta indexul minim la inceputul fiecarui pas, adica `mid_idx` `=` `2` si repetam procesul de mai sus incepand de pe indexul `2`.

Verificam daca `arr[j]` `<` `arr[min_idx]` adica `arr[3]` `<` `arr[2]` => `22` `<` `25` `True` actualizam variabila `min_idx` cu `j` adica cu `3`.

`arr[4]` `<` `arr[3]` adica `64` `<` `22` `False` se opreste loop-ul.


Dupa ce s-a gasit cel mai mic element din restul array-ului, se face un `swap` intre elementul curent de la pozitia `i` si cel mai mic element gasit `min_idx`. 


-> `arr[i], arr[min_idx] = arr[min_idx], arr[i]` adica `arr[2], arr[3] = arr[3], arr[2]` => `25, 22 = 22, 25`.

Array-ul arata asa acum `[11, 12, 22, 25, 64]` care este un array ordonat corect si va mai acest proces pana cand `i` va fi `4` si la final se va returna array-ul ordonat.

