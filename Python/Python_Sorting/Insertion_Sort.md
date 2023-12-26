# Insertion Sort

Acest algoritm de sortare menține un subarray care este întotdeauna sortat. Valorile din partea nesortată a array-ului sunt plasate în poziția corectă în partea sortată. Este mai eficient în practică decât alți algoritmi, cum ar fi Selection Sort sau Bubble Sort. 

Insertion Sort are o complexitate în timp de O(n2) în cazul mediu și cel mai rău și O(n) în cel mai bun caz.

## Vizualizarea Insertion Sort

![Insertion Sort](https://www.swtestacademy.com/wp-content/uploads/2021/11/insertion-sort-Insertion-Sort.drawio-6.png)

## Implementarea Insertion Sort

```python
def insertionSort(arr):
    n = len(arr)
    for i in range(1, n):

        a = arr[i]
        j = i - 1

        while j >= 0 and a < arr[j]:
            arr[j+1] = arr[j]
            j -= 1
        arr[j + 1] = a

    return arr
```

Am initializat variabila `n` cu valoarea lungimii array-ului `arr`.

Parcurgem array-ul cu un `for loop` cu variabila `i` in `range(1,n)` adica de la `1` la lungimea lui `arr`.

Initializam variabila `a` cu `arr[i]` pentru a salva valoarea curenta a elementului din array pentru a se efectua comparari si mutari ulterioare.

Initializam variabila `j` cu `i - 1` care reprezinta ultimul element deja sortat in comparatie cu elementul curent `a`.

Realizam un `while loop` cu conditiile ca `j >= 0` si `a < arr[j]` adica atata timp cat una din aceste conditii este `False` loop-ul nu se va opri. In esență, bucla `while` rulează atâta timp cât indexul `j` este valid (mai mare sau egal cu zero) și valoarea curentă `a` este mai mică decât elementul din array-ul deja sortat la poziția `arr[j]`.

La final returnam array-ul sortat.

Exemplu de utilizare :

Avem array-ul `[5, 2, 9, 1, 5]` si vrem sa il sortam folosind algoritmul Insertion Sort.

Intram in `for loop` cu variabila `i` in `range(1, n)` adica de la `1` la `5`.

Initializam variabila `a` cu `arr[i]` adica cu `arr[1]` => `2`. Deci valoarea curenta este `2`.

Initializam variabila `j` cu `i-1` adica cu `1-1` => `0`.

Intram in `while loop` si verificam conditiile:

`j >= 0` -> `0 >= 0`? `True`.

`a < arr[j]` -> `2 < 5` `True`

Intram in loop si spunem ca `arr[j+1] = arr[j]` adica `arr[0+1] = arr[0]` => `2 = 5`.
Scadem `1` lui `j` deci `j = i - 1 - 1` => `j = 1 - 1 - 1` `=` `-1`. 

Se verifica iar conditiile `while loop` :

`j >= 0` -> `-1 >= 0`? `False`. Se opreste loop-ul.

Apoi spunem `arr[j + 1] = a` adica `arr[-1 + 1] = 5` => `arr[0] = 5`.


Deci array-ul arata asa acum `[2, 5, 9, 1, 5]`. Continuam `for loop`. `i` este `2` acum.

Initializam variabila `a` cu `arr[i]` adica cu `arr[2]` => `9`. Deci valoarea curenta este `9`.

Initializam variabila `j` cu `i-1` adica cu `2-1` => `1`.

Intram in `while loop` si verificam conditiile:

`j >= 0` -> `1 >= 0`? `True`.

`a < arr[j]` -> `9 < 5` `False`. Se opreste loop-ul.


Apoi spunem `arr[j + 1] = a` adica `arr[1 + 1] = 9` => `arr[2] = 9`. Se pastreaza aceiasi pozitie deoarce este ordonata.

Deci array-ul arata asa acum `[2, 5, 9, 1, 5]`. Continuam `for loop`. `i` este `3` acum.

Initializam variabila `a` cu `arr[i]` adica cu `arr[3]` => `1`. Deci valoarea curenta este `1`.

Initializam variabila `j` cu `i-1` adica cu `3-1` => `2`.

Intram in `while loop` si verificam conditiile:

`j >= 0` -> `2 >= 0`? `True`.

`a < arr[j]` -> `1 < 9` `True`

Intram in loop si spunem ca `arr[j+1] = arr[j]` adica `arr[2+1] = arr[2]` => `1 = 9`.
Scadem `1` lui `j` deci `j = i - 1 - 1` => `j = 3 - 1 - 1` `=` `1`. 

Se verifica iar conditiile `while loop` :

`j >= 0` -> `1 >= 0`? `True`.

`a < arr[j]` -> `1 < 5` `True`. 

Intram in loop si spunem ca `arr[j+1] = arr[j]` adica `arr[1+1] = arr[1]` => `9 = 5`.
Scadem `1` lui `j` deci `j = i - 1 - 1` => `j = 3 - 1 - 1 - 1` `=` `0`. 

Se verifica iar conditiile `while loop` :

`j >= 0` -> `0 >= 0`? `True`. 

`a < arr[j]` -> `1 < 2` `True`. 

Intram in loop si spunem ca `arr[j+1] = arr[j]` adica `arr[0+1] = arr[0]` => `5 = 2`.
Scadem `1` lui `j` deci `j = i - 1 - 1 - 1 - 1` => `j = 3 - 1 - 1 - 1 - 1` `=` `-1`. 

Se verifica iar conditiile `while loop` :

`j >= 0` -> `-1 >= 0`? `False`. Se opreste loop-ul.
 

Apoi spunem `arr[j + 1] = a` adica `arr[-1 + 1] = 1` => `arr[0] = 1` => `2 = 1` 

Array-ul nostru arata astfel `[1, 2, 5, 9, 5]`. Continuam `for loop`. `i` este `4` acum.


Initializam variabila `a` cu `arr[i]` adica cu `arr[4]` => `5`. Deci valoarea curenta este `5`.

Initializam variabila `j` cu `i-1` adica cu `4-1` => `3`.

Intram in `while loop` si verificam conditiile:

`j >= 0` -> `3 >= 0`? `True`.

`a < arr[j]` -> `5 < 9` `True`

Intram in loop si spunem ca `arr[j+1] = arr[j]` adica `arr[3+1] = arr[3]` => `5 = 9`.
Scadem `1` lui `j` deci `j = i - 1 - 1` => `j = 4 - 1 - 1` `=` `2`. 

Intram in `while loop` si verificam conditiile:

`j >= 0` -> `2 >= 0`? `True`.

`a < arr[j]` -> `5 < 5` `False` Se opreste loop-ul.

Apoi spunem `arr[j + 1] = a` adica `arr[2 + 1] = 5` => `arr[3] = 5` => `9 = 5` 

Array-ul arata asta `[1, 2, 5, 5, 9]` si este sortat.