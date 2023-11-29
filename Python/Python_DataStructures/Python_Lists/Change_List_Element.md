# Schimbarea elementelor dintr-o lista

### Putem modifica un element specific dintr-o lista prin index

De exemplu:

```python
lista = ["Dodan", "Marius", "Robert"]
#Am selectat elementul de pe indexul 1 si i-am atribuit alta valoare.
lista[1] = ["Marian"]

print(lista)

output:
["Dodan", "Marian", "Robert"]
```

### Putem modifica mai multe elemente prin accesarea unui interval

De exemplu:

```python
lista = ["Dodan", "Marius", "Robert", "Dumicat"]
#Am selectat intervalul intre 1 si 3 si am modificat elementele 1 si 2
lista[1:3] = ["Mihaela", "Cristian"]

print(lista)

output:
["Dodan", "Mihaela", "Cristian", "Dumicat"]
```

### In cazul incare adaugam mai multe elemente decat in interval acestea se vor adauga in intervalul mentionat si restul elementelor se vor muta in continuare.

De exemplu:

```python
lista = ["Dodan", "Marius", "Robert", "Dumicat"]
#Am selectat intervalul intre 1 si 3 si am modificat elementele 1 si 2
lista[1:3] = ["Mihaela", "Cristian", "Catalin"]

print(lista)

output:
["Dodan", "Mihaela", "Cristian", "Catalin", "Dumicat"]
```