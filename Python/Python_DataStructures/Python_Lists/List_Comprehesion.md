# List Comprehesion

### Acest concept ofera o sintaxa mult mai scurta cand vrem sa creeam o lista noua pe baza unei liste existente

Exemplu:

Pe baza unei liste de brand-uri de masini, vrei o lista noua, care sa contina doar fructele cu litera "a" in nume.

Pentru inceput o sa arat cum se poate face acest lucru traditionar cu un for loop

```python
#Am initializat o lista cu firme de masini
masini = ["Mercedes", "BMW", "Dacia", "Renault", "Audi"]
#Am declarat o lista noua goala
lista_noua = []

#for loop care verifica fiecare element din masini si cauta cuvintele care contin "a"
for x in masini:
    if "a" in masini:
        lista_noua.append(x)

print(lista_noua)

output:
["Dacia", "Renault"]
```

### **De tinut minte ca if statement-ul mentioneaza litera "a", iar daca "A" o sa fie gasit acesta nu o sa fie luat in calcul chiar daca sunt aceiasi litera in esenta. "Case sensitive"**

Acum vom face acelasi lucru ca mai sus doar ca vom folosii list comprehesion:

```python
masini = ["Mercedes", "BMW", "Dacia", "Renault", "Audi"]

#dupa ce se verifica conditia if , daca a este in cuvant se adauga acel element in lista noua.
lista_noua = [cuvant for cuvant in masini if "a" in cuvant]

print(lista_noua)

output:
["Dacia", "Renault"]
```

Aceste metode de scriere se numesc **One liners**.

### Sintaxa _**[x for x in colectie if conditie == True]**_

Acum stiind sintaxa ne putem juca cu conditiile pentru a avea rezultate diferite.

De exemplu:

```python
masini = ["Mercedes", "BMW", "Dacia", "Renault", "Audi"]

lista_noua = [cuvant for cuvant in masini if "a" != cuvant]

print(lista_noua)

output:
["Mercedes", "BMW", "Audi"]
```

**In loc de != care inseamna "_nu este_" sau "_diferit_" in Python putem folosii "_not_"**
```python
masini = ["Mercedes", "BMW", "Dacia", "Renault", "Audi"]

lista_noua = [cuvant for cuvant in masini if "a" not in cuvant]

print(lista_noua)

output:
["Mercedes", "BMW", "Audi"]
```

### Nu este obligatoriu sa folosim if statement. Putem face list comprehesion si fara conditionare

De exemplu:

```python
masini = ["Mercedes", "BMW", "Dacia", "Renault", "Audi"]

lista_noua = [cuvant for cuvant in masini]

print(lista_noua)

output:
["Mercedes", "BMW", "Dacia", "Renault", "Audi"]
```
Prin renuntarea la conditie am copiat lista principala. Aceasta metoda este buna pentru a executa operatii matematice pe listele numerice pentru fiecare element in parte.

De exemplu

```python
cifre = [1,2,3,4,5,6,7]
#Am inmultit fiecare cifra din lista cu 2
lista_noua = [cifra * 2 for cifra in cifre]

print(lista_noua)

output:
[2,4,6,8,10,12,14]
```

### Cu list comprehesion putem creea o lista de la 0

De exemplu:

```python
#Intelegem ca x pentru x de 10 ori. Adica x = 0, x = 0 + 1 , x = 1 + 1...... x = 8 + 1 sfarsit. Se opreste la 9 deoarece adunarea indexarea incepe de la 0.
cifre = [x for x in range(10)]

print(cifre)

output:
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
```

In acelasi context putem folosii si conditionarea

De exemplu:

```python
#Conditia ca numerele sa fie pare
cifre = [x for x in range(10) if x % 2 == 0]

print(cifre)

output:
[0, 2, 4, 6, 8]
```

### Expresia poate avea si ea o conditie inainte de iteratie.

De exemplu"

```python
#Am conditionat expresia ca elementele 3,4,5 sa fie egale cu 0 daca acestea exita in lista.
cifre = [x if x not in [3,4,5] else 0 for x in range(10)]

print(cifre)

output:
[0, 1, 2, 0, 0, 0, 6, 7, 8, 9]
```
