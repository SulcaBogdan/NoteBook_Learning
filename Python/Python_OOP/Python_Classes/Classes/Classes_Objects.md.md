# Python Programarea Orientata Pe Obiecte(OOP)

Python este un limbaj de programare orientat pe obiecte.

Aproape totul în Python este un obiect, cu proprietățile și metodele sale.

### O clasă este ca un constructor de obiecte sau un „plan” pentru crearea obiectelor.

#### Cum se creaza o clasa?

Exemplu:

```python
class ClasaMea:
    x = 5
```
Am creat o clasa cu notatia CamelCase adica fiecare cuvant sa inceapa cu litera mare ex-> DouaMasini , ClasaNoua, AltaClasa  etc...

#### Am creat o clasa, dar acum ce putem crea sau ce putem face cu aceasta clasa?

Putem crea un obiect de clasa pentru a putea folosii functii / metode pe acesta.

De exemplu:

```python
class ClasaMea:
    x = 5

#Am stocat un obiect de ClasaMea() in variabila obiectul_meu    
obiectul_meu = ClasaMea()

#Acum avem acces la toate componentele clasei 'ClasaMea' de ex 
#variabila de instanta x cu valoarea 5
print(obiectul_meu.x)

output:
5
```

## Functia __init__()

Exemplele de mai sus sunt clase și obiecte în forma lor cea mai simplă și nu sunt cu adevărat utile în aplicațiile din viața reală.

Pentru a înțelege semnificația claselor, trebuie să înțelegem funcția încorporată __init__().

Toate clasele au o funcție numită __init__(), care este întotdeauna executată atunci când clasa este inițiată.

Utilizați funcția __init__() pentru a atribui valori proprietăților obiectului sau alte operațiuni care sunt necesare pentru a le face atunci când obiectul este creat:

De exemplu:

```python
class ClasaMea:
    #Utilizarea functie __init__ (constructorul clasei)
    def __init__(self, atribut1, atribut2):
        self.nume = nume
        self.varsta = varsta

obicetul_meu = ClasaMea("Clasa", 1)

print(obiectul_meu.atribut1)
print(obiectul_meu.atribut2)

output:
Clasa
1
```

In exemplul de mai sus am creat un constructor cu folosind functia __init__() si am pus ca parametrii 2 atribute (abstracte in ex acesta, dar puteti pune orice doriti de exemplu nume, varsta, salariu etc..). 

**Notă: Funcția __init__() este apelată automat de fiecare dată când clasa este utilizată pentru a crea un obiect nou.**



## Functia __str__()

Funcția __str__() controlează ce ar trebui returnat atunci când obiectul de clasă este reprezentat ca string.

Dacă funcția __str__() nu este setată, este returnată reprezentarea string a obiectului:


#### Reprezentarea în șir a unui obiect FĂRĂ funcția __str__():
```python
class Persoana:
  def __init__(self, name, age):
    self.name = name
    self.age = age

p1 = Persoana("Ionut", 36)

print(p1)

output:
<__main__.Persoana object at 0x15039e602100>
```

#### Reprezentarea în șir a unui obiect CU funcția __str__():
```python
class Persoana:
  def __init__(self, nume, varsta):
    self.name = name
    self.age = age

  #Functia __str__() returneaza string
  def __str__(self):
    return f"{self.name}({self.age})"

p1 = Persoana("Ionut", 36)

print(p1)
Ionut(36)
```

## Metodele obiectelor

Obiectele pot conține și metode. Metodele din obiecte sunt funcții care aparțin obiectului.

Să creăm o metodă în clasa Person:

```python
class Persoana:
  def __init__(self, nume, varsta):
    self.nume = nume
    self.varsta = varsta

  def myfunc(self):
    print("Buna numele meu este " + self.nume)

p1 = Persoana("Dodan", 26)
p1.myfunc()

output:
Buna numele meu este Dodan
```

#### Notă: Parametrul self este o referință la instanța curentă a clasei și este folosit pentru a accesa variabilele care aparțin clasei.

## Parametrul self

Parametrul self este o referință la instanța curentă a clasei și este folosit pentru a accesa variabilele care aparțin clasei.

Nu trebuie să fie numit self , îl puteți numi cum doriți, dar trebuie să fie primul parametru al oricărei funcție din clasă:


De exemplu:

```python
class Persoana:
  def __init__(cumdoresc, nume, varsta):
    cumdoresc.nume = nume
    cumdoresc.varsta = varsta

  def myfunc(abc):
    print("Buna numele meu este " + cumdoresc.nume)

p1 = Persoana("Dodan", 26)
p1.myfunc()

output:
Buna numele meu este Dodan
```

### Best practice este sa folosim self .

## Modificarea proprietatilor obiectului

Proprietatile obiectului pot fi modificate astfel

```python
class Persoana:
  def __init__(self, nume, varsta):
    self.nume = nume
    self.varsta = varsta

  def myfunc(self):
    print("Buna numele meu este " + self.nume)

p1 = Persoana("Dodan", 26)
p1.nume = "Marian"
p1.myfunc()

output:
Buna numele meu este Marian
```

## Stergerea proprietatilor unui obiect

Prin folosirea cuvantului cheie 'del':

```python
class Persoana:
  def __init__(self, nume, varsta):
    self.nume = nume
    self.varsta = varsta

  def myfunc(self):
    print("Buna numele meu este " + self.nume)

p1 = Persoana("Dodan", 26)
del p1.nume 
print(p1.nume)

output:
Traceback (most recent call last):
  File "[your file]", line 13, in <module>
    print(p1.nume)
AttributeError: 'Persoana' object has no attribute 'nume'
```

La fel si pentru a sterge obiecte

```python
class Persoana:
  def __init__(self, nume, varsta):
    self.nume = nume
    self.varsta = varsta

  def myfunc(self):
    print("Buna numele meu este " + self.nume)

p1 = Persoana("Dodan", 26)
del p1 
print(p1.nume)

output:
Traceback (most recent call last):
  File "[your file]", line 13, in <module>
    print(p1)
NameError: 'p1' is not defined
```


## pass statement

Definițiile de clasă nu pot fi goale, dar dacă dintr-un motiv oarecare aveți o definiție de clasă fără conținut, introduceți instrucțiunea de trecere pentru a evita o eroare.

```python
class Persoana:
    pass
```