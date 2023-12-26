# Algoritm-ul de sortare Bubble Sort

Bubble Sort este un algoritm simplu de sortare. Acest algoritm de sortare compară în mod repetat două elemente adiacente și le schimbă dacă sunt în ordinea greșită. 

### Time complexity:
1. O(n2) în scenariile medii și cele mai defavorabile
2. O(n) în scenariul cel mai bun. 
   
### Vizualizarea algortimului

![Bubble Sort](https://www.swtestacademy.com/wp-content/uploads/2021/11/bubble-sort-1.png)

Se verifica fiecare element din array pe perechi de a cate doua elemente, de unde vine si denumirea de "Bubble" adica elementele care se compara se afla intr-o bula. Daca primul element este mai mare decat al doilea atunci se va executa un "swap" intre acestea, dar daca primul element este mai mic atunci se se trece la urmatoarea pereche.

Indiferent de rezultatul verificarilor se va parcurge array-ul cu +1 la fiecare index. Adica indexul `0`(18) este mai mare ca indexul `1`(32)? `False` `+1` la fiecare index.
Indexul `1`(32) este mai mare ca indexul `2`(-11)? `True` executam `swap` si `+1` la fiecare index. Indexul `2`(32) este mai mare ca indexul `3`(6)? `True` executam `swap` si `+1` la fiecare index si tot asa pana cand ajungem la ultimul element din array.


Procesul se va repeta pana cand nu se va mai executa nici un `swap` intre elemente, adica array-ul este ordonat.

### Implementarea unui Bubble Sort

```python
def bubbleSort(arr):
    n = len(arr)

    for i in range(n):
        for j in range(0, n-i-1):

            if arr[j] > arr[j+1]:
                arr[j], arr[j+1] = arr[j+1], arr[j]

    return arr
```

Am initializat variabila `n` cu valoarea lungimii array-ului `arr` apoi am creat un dublu `for loop` pentru a itera prin array si pentru a compara elementele acestuia pe perechi.

Primul `for loop` va itera elementul `i` in `range(n)`, adica `i` va avea valorile incepand de la `0` pana la lungimea lui `arr`.

Al doilea `for loop` va itera elementul `j` in `range(0, n-i-1)`, adica `j` va avea valorile incepand de la `0` pana la rezultatul lungimii array-ului minus valoarea lui `i`(care reprezinta elementul din primul `for loop`) minus `1` pentru a selecta indexul array-ului.

Urmeaza un `if statement` cu conditia ca `arr[j] > arr[j+1]` adica primul element din array sa fie mai mare ca al doilea element din array. Daca conditia este `True` atunci intram in blocul de cod si executam `swap` intre elemente prin paralelism. Spunem `arr[j], arr[j+1]` `=` `arr[j+1], arr[j]` adica `primul element, al doilea element` `=` `al doilea element`, `primul element` => `primul element` `=` `al doilea element` si `al doilea element` = `primul element`.

Dupa ce se termina `primul for loop` adica dupa ce se ajunge la sfarsitul lungimii array-ului se va returna array-ul sortat.


Exemplu:

`[1,5,3,2,7]` Vrem sa ordonam acest array folosind Bubble Sort.

Initializam variabila `n` cu lungimea listei adica numarul de elemente din lista care este egal cu `5`. Deci `n` `=` `5`.

Primul `for loop` are variabila `i` in `range(n)` adica in `range(5)` adica de la `0` la `5`, deoarce functia `range()` porneste default de la `0`.

Al doilea `for loop` are variabila `j` in `range(n-i-1)` adica in `range(5-0-1)` deoarece prima valoare din prima iteratie a lui `i` este `0`. Deci dupa finalizarea calcularii rezulta `j` in `range(4)` adica de la `0` la `4`.

Intram in al doilea `for loop` si verificam daca `arr[j]` `>` `arr[j+1]` adica `arr[0]` `>` `arr[1]`, adica `1` `>` `5` ? `False` mergem mai departe.

`arr[1]` `>` `arr[1+1]` adica `arr[1]` `>` `arr[2]` => `5` `>` `3` `True` executam `swap` din blocul de cod a `if statement`. Spunem ca `arr[j], arr[j+1] = arr[j+1], arr[j]` adica `arr[1], arr[1+1] = arr[1+1], arr[1]` => `5, 3 = 3, 5` si mergem mai departe

`arr[2]` `>` `arr[2+1]` adica `arr[2]` `>` `arr[3]` => `5` `>` `2` `True` executam `swap` ca mai sus.

`arr[3]` `>` `arr[3+1]` adica `arr[3]` `>` `arr[4]` => `5` `>` `7` `False` si ne oprim.

Array-ul arata astfel `[1,3,2,5,7]` . Acesta nu este ordonat.

Revenim la primul `for loop` si continuam iteratia cu urmatorul element respectiv `1`.
Deci `i` `=` `1`.

Iar in al doilea `for loop` `j` in `range(5-1-1)` adica `j` in `range(3)`.

Intram in al doilea `for loop` si verificam daca `arr[j]` `>` `arr[j+1]` adica `arr[0]` `>` `arr[1]`, adica `1` `>` `3` ? `False` mergem mai departe.

`arr[1]` `>` `arr[1+1]` adica `arr[1]` `>` `arr[2]` => `3` `>` `2` `True` executam `swap` din blocul de cod a `if statement`. Spunem ca `arr[j], arr[j+1] = arr[j+1], arr[j]` adica `arr[1], arr[1+1] = arr[1+1], arr[1]` => `3, 2 = 2, 3` si mergem mai departe.

`arr[2]` `>` `arr[2+1]` adica `arr[2]` `>` `arr[3]` => `3` `>` `5` `False` si ne oprim.

Array-ul arata astfel `[1,2,3,5,7]`. Acum acesta este ordonat. Se vor executa urmatoarele iterari din primul `for loop` pana cand `i` `=` `4` si la final se va returna array-ul ordonat.
