# Listele in Python

**Listele** sunt una din cele 4 stucturi de date build-in in Python. Celelalte trei sunt **tuple** , **dictionarele** si **set-urile**.

## Cum sunt create listele?

Listele sunt create folosind paranteze patrare.

Exemplu:

```python
#Declararea unei liste fara elemente.
lista = []
```

Putem adauga elemente in lista noastra:

```python
#Initializam lista cu valori numerice
lista = [1,2,3,4,5,6]

print(lista)

output:
[1,2,3,4,5,6]
```

Elementele listei sunt ordonate, modificabile si permit valori dublicate.

Elementele din lista sunt indexate, primul element are index[0], al doilea index[1], etc..

In momentul in care adaugam un nou element in lista, acesta se va pune la sfarsitul listei. De exemplu

```python
lista = [1,2,3]
lista.append(1)

print(lista)

output:
[1,2,3,1]
```

Listele permit dublicatele. 

Exemplu:

```python
lista = [1,2,3]
lista.append(2)

print(lista)

output:
[1,2,3,2]
```

Putem afla lungimea listei (sau numarul elementelor din lista) folosind functia len().

```python
lista ["Marian", "Dodan", "Cosmin"]

print(len(lista))

output:
3
```

**De tinut minte ca len() numara elementele incepand de la 1 nu de la 0 cum am spus ca se indexeaza lista.**

Listele pot tine orice tip de date separat dar si simultan.

Exemplu:

```python
#Separat
lista1 = [1,2,3,4] # int
lista2 = ["Marian", "Dodan", "Cosmin"] # str
lista3 = [True, False, True] # bool

#Simulat
lista_combo = [1,2,"Dodan", True] # int, str, bool
etc
```

Alta modalitate de a crea o lista folosind constructorul list():

```python
lista = list(("Dodan", 2, True)) # elementele listei se pun intre () nu intre []

print(lista)

output:
["Dodan", 2, True]
```
