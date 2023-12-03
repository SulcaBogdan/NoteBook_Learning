# Modificarea unei tuple

### Dupa cum am mai mentionat structura de date Tuple este imutabila. Adica odata ce aceasta a fost create ea nu mai poate fi modificata.

Pentru a modifica o tuple trebuie sa folosim anumite tehnici.

1. Convertirea unei tuple intr-o lista pentru a putea modifica informatiile:


```python
my_tuple = (1,2,3,4)
my_list = list(my_tuple)

#Putem adauga cu .append()
my_list.append(5)
#Putem modifica o valoare deja existenta
my_list[1] = 3

my_tuple = tuple(my_list)

print(my_tuple)

output:
(1,3,3,4,5)
```

2. Prin adaugarea unei alte tuple la tuple noastra principala:

```python
my_tuple = ("mar", "portocala", "banana")
#Am creat o tuple cu un singur element si l-am adaugat la tuple noastra principala
element = ("kiwi",)
my_tuple += element

print(my_tuple)

output:
("mar", "portocala", "banana", "kiwi")
```

### Nu poti sterge elemente dintr-o tupla dupa ce aceasta a fost initializati, dar exista cateva ocolisuri pentru a putea face acest lucru posibil.

1. Convertirea unei tuple intr-o lista pentru a putea sterge informatiile

```python
my_tuple = ("mar", "portocala", "banana", "kiwi")
my_list = list(my_tuple)

#Putem adauga cu .append()
my_list.remove("mar")

my_tuple = tuple(my_list)


print(my_tuple)

output:
("portocala", "banana", "kiwi")
```

2. Folosirea cuvantului cheie "del", dar acesta va sterge intreaga tuple:

```python
my_tuple = ("mar", "portocala", "banana", "kiwi")

del my_tuple

print(my_tuple)

output:
#Se va ridica o eroare doarece tuple-ul nostru nu mai exista.
```