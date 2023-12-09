# Mostenirea (inheritance)

Moștenirea ne permite să definim o clasă care moștenește toate metodele și proprietățile de la o altă clasă.

**Clasa părinte** este clasa de la care se moștenește, numită și **clasă de bază**.

**Clasa copil** este clasa care moștenește de la o altă clasă, numită și clasă derivată.

## Crearea unei clase parinte

Orice clasă poate fi o clasă părinte, deci sintaxa este aceeași cu crearea oricărei alte clase:

```python
class Persoana:
  def __init__(self, nume, varsta):
    self.nume = nume
    self.varsta = varsta

  def functia_mea(self):
    print("Buna numele meu este " + self.nume)

p1 = Persoana("Dodan", 26)
p1.functia_mea()

output:
Buna numele meu este Dodan
```

## Crearea unei clase copil/derivate:

Pentru a crea o clasă care moștenește funcționalitatea dintr-o altă clasă, trimiteți clasa părinte ca parametru atunci când creați clasa copil:

Exemplu:

```python
class Student(Persoana):
    pass
```

Acum clasa Student mosteneste toate proprietatile si metodele clasei Persoana.

```python
class Persoana:
  def __init__(self, nume, varsta):
    self.nume = nume
    self.varsta = varsta

  def functia_mea(self):
    print(f"Buna numele meu este {self.nume} si am {self.varsta} de ani")

class Student(Persoana):
    pass

p1 = Persoana("Dodan", 26)
p2 = Student("Marius", 33)

p1.functia_mea()
p2.functia_mea()

output:
Buna numele meu este Dodan si am 26 de ani
Buna numele meu este Marius si am 33 de ani
```

## Adaugarea functiei __init__()

Până acum am creat o clasă copil care moștenește proprietățile și metodele de la părintele ei.

Dorim să adăugăm funcția __init__() la clasa copil (în loc de cuvântul cheie pass).

#### Notă: Funcția __init__() este apelată automat de fiecare dată când clasa este utilizată pentru a crea un obiect nou.


```python
class Persoana:
  def __init__(self, nume, varsta):
    self.nume = nume
    self.varsta = varsta

  def functia_mea(self):
    print(f"Buna numele meu este {self.nume} si am {self.varsta} de ani")

class Student(Persoana):
    def __init__(self, nume, varsta):
        self.nume = nume
        self.varsta = varsta

p1 = Persoana("Dodan", 26)
p2 = Student("Marius", 33)

p1.functia_mea()
p2.functia_mea()

output:
Buna numele meu este Dodan si am 26 de ani
Buna numele meu este Marius si am 33 de ani
```

Când adăugați funcția __init__(), clasa copil nu va mai moșteni funcția __init__() a părintelui. 

Funcția __init__() a copilului suprascrie moștenirea funcției __init__() a părintelui.

Pentru a păstra moștenirea funcției __init__() a părintelui, adăugați un apel la funcția __init__() a părintelui.

Exemplu:

```python
class Persoana:
  def __init__(self, nume, varsta):
    self.nume = nume
    self.varsta = varsta

  def functia_mea(self):
    print(f"Buna numele meu este {self.nume} si am {self.varsta} de ani")

class Student(Persoana):
    def __init__(self, nume, varsta):
        Persoana.__init__(self, nume, varsta)

p1 = Persoana("Dodan", 26)
p2 = Student("Marius", 33)

p1.functia_mea()
p2.functia_mea()

output:
Buna numele meu este Dodan si am 26 de ani
Buna numele meu este Marius si am 33 de ani
```

Acum am adăugat cu succes funcția __init__() și am păstrat moștenirea clasei părinte și suntem gata să adăugăm funcționalitate în funcția __init__().

## Utilizarea functiei super()

Python are, de asemenea, o funcție super() care va face ca clasa copil să moștenească toate metodele și proprietățile de la părintele său:
```python
class Persoana:
  def __init__(self, nume, varsta):
    self.nume = nume
    self.varsta = varsta

  def functia_mea(self):
    print(f"Buna numele meu este {self.nume} si am {self.varsta} de ani")

class Student(Persoana):
    def __init__(self, nume, varsta):
        super().__init__(self, nume, varsta)

p1 = Persoana("Dodan", 26)
p2 = Student("Marius", 33)

p1.functia_mea()
p2.functia_mea()

output:
Buna numele meu este Dodan si am 26 de ani
Buna numele meu este Marius si am 33 de ani
```

Folosind funcția **super()**, nu trebuie să utilizați numele elementului părinte, acesta va moșteni automat metodele și proprietățile de la părintele său.

## Adaugarea proprietatilor

```python
class Persoana:
  def __init__(self, nume, varsta):
    self.nume = nume
    self.varsta = varsta

  def functia_mea(self):
    print(f"Buna numele meu este {self.nume} si am {self.varsta} de ani")

class Student(Persoana):
    def __init__(self, nume, varsta):
        super().__init__(self, nume, varsta)
        self.inaltime = 170

p1 = Persoana("Dodan", 26)
p2 = Student("Marius", 33)

p1.functia_mea()
p2.functia_mea()
print(p2.inaltime)

output:
Buna numele meu este Dodan si am 26 de ani
Buna numele meu este Marius si am 33 de ani
170
```

In exemplul acesta am adaugat o noua proprietate definita dupa apelarea functiei super. Acum clasa Student are un atribut in plus fata de clasa parinte Persoana. Dar daca dorim sa cream mai multe obiecte Student cu inaltimi variate atunci putem itroduce si ca parametru noul atribut. 

De exemplu:

```python
class Persoana:
  def __init__(self, nume, varsta):
    self.nume = nume
    self.varsta = varsta

  def functia_mea(self):
    print(f"Buna numele meu este {self.nume} si am {self.varsta} de ani")

class Student(Persoana):
    def __init__(self, nume, varsta, inaltime):
        super().__init__(self, nume, varsta)
        self.inaltime = inaltime

p1 = Persoana("Dodan", 26)
p2 = Student("Marius", 33, 160)

p1.functia_mea()
p2.functia_mea()
print(p2.inaltime)

output:
Buna numele meu este Dodan si am 26 de ani
Buna numele meu este Marius si am 33 de ani
160
```

## Adauga metode

```python
class Persoana:
  def __init__(self, nume, varsta):
    self.nume = nume
    self.varsta = varsta

  def functia_mea(self):
    print(f"Buna numele meu este {self.nume} si am {self.varsta} de ani")

class Student(Persoana):
    def __init__(self, nume, varsta, inaltime):
        super().__init__(self, nume, varsta)
        self.inaltime = inaltime

    def welcome(self):
        print(f"Bine ai venit {self.nume} in clasa aceasta. Are varsta de {self.varsta} de ani si inaltimea de {self.inaltime} de cm")

p1 = Persoana("Dodan", 26)
p2 = Student("Marius", 33, 160)

p1.functia_mea()
p2.functia_mea()
p2.welcome

output:
Buna numele meu este Dodan si am 26 de ani
Buna numele meu este Marius si am 33 de ani
Bine ai venit Marius in clasa aceasta. Are varsta de 33 de ani si inaltimea de 160 de cm
```

Dacă adăugați o metodă în clasa copil cu același nume ca o funcție din clasa părinte, moștenirea metodei părinte va fi suprascrisă(overriden).