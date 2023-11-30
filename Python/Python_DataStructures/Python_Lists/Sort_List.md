# Sortarea listelor

### Obiectele de lista au o metoda build-in de sortare in ordine alfabetica sau crescatoare by default. Aceasta este metoda .sort()

Exemplu:

```python
lista_text = ["Dodan", "Arina", "Andra","Marian", "Bogdan"]
lista_numere = [4,2,1,5,7,5,3,8]

lista_text.sort()
lista_numere.sort()

print(lista_text)
print(lista_numere)

output:
["Andra", "Arina", "Bogdan","Dodan", "Marian"]
[1,2,3,4,5,5,7,8]
```

### Avand in vedere ca metoda sort() ordoneaza crescator si in ordine alfabetica by default, ca sa o putem inversa procesul putem folosii parametrii metodei. "reverse= True"

Exemplu:

```python
lista_text = ["Dodan", "Arina", "Andra","Marian", "Bogdan"]
lista_numere = [4,2,1,5,7,5,3,8]

lista_text.sort(reverse = True)
lista_numere.sort(reverse = True)

print(lista_text)
print(lista_numere)

output:
["Marian", "Dodan", "Bogdan","Arina", "Andra"]
[8,7,5,5,4,3,2,1]
```

### Putem modifica metoda sort() dupa bunul plac folosind parametrul "key = functie"

Exemplu

```python
def functia_mea(numar):
    return abs(numar-50)

lista = [100,50,65,82,23]
lista.sort(key = functia_mea)

print(lista)

output:
[50, 65, 23, 82, 100]
```

### By default metoda sort() este case sensitive, asa ca primele valori textuale care vor fi ordonate sunt cele care incep cu litera mare urmate de cele cu litera mica.

```python
lista = ["dodan", "Dodan", "Andra", "alina", "Marius"]
lista.sort()

print(lista)

output:
["Andra", "Dodan", "Marius", "alina", "dodan"]
```

### Pentru a evita acest lucru putiem folosii cuvantul cheie "key" ca parametru pentru sort si  functia build-in a tipului de date srt -> .lower() ca sa facem toate cuvintele din lista lower case.

Exemplu:

```python
lista = ["dodan", "Dodan", "Andra", "alina", "Marius"]
lista.sort(key = str.lower)

print(lista)

output:
["alina", "andra", "dodan", "dodan", "marius"]
```

### Daca vrem sa inversam ordinea fara a ne interesa ordinea din alfabet putem folosii direct functia .reverse().

Exemplu:

```python
lista = ["dodan", "Dodan", "Andra", "alina", "Marius"]
lista.reverse()

print(lista)

output:
["Marius", "alina", "Andra", "Dodan", "dodan"]
```
