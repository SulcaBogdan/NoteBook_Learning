# Polimorfismul(Polymorphism)

#### Cuvântul „polimorfism” înseamnă „multe forme”, iar în programare se referă la metode/funcții/operatori cu același nume care pot fi executate pe mai multe obiecte sau clase.

Un exemplu de funcție Python care poate fi utilizată pe diferite obiecte este funcția len().

De exemplu functia len() poate fi folosita pe :

### String

Pentru string-uri de caractere len() returnează numărul de caractere:

```python
x = "Hello World!"

print(len(x))

output:
12
```

### Tuple

Pentru tuplu, len() returnează numărul de elemente din tuplu:
```python
mytuple = ("mar", "banana", "cirese")

print(len(mytuple))

output:
3
```

### Dictionare

Pentru dicționare, len() returnează numărul de perechi cheie/valoare din dicționar:

```python
thisdict = {
  "brand": "Ford",
  "model": "Mustang",
  "an": 1964
}

print(len(thisdict))

output:
3
```

## Polimorfismul in clase

Polimorfismul este adesea folosit clase, unde putem avea mai multe clase cu metode denumite exact la fel dar cu functionalitati diferite.

De exemplu, să presupunem că avem trei clase: Mașină, Barcă și Avion și toate au o metodă numită move():

```python
class Mașina:
  def __init__(self, brand, model):
    self.brand = brand
    self.model = model

  def move(self):
    print("Drive!")

class Barca:
  def __init__(self, brand, model):
    self.brand = brand
    self.model = model

  def move(self):
    print("Sail!")

class Avion:
  def __init__(self, brand, model):
    self.brand = brand
    self.model = model

  def move(self):
    print("Fly!")

masina1 = Car("Ford", "Mustang")       #Creaza un obiect de Masina
barca1 = Boat("Ibiza", "Touring 20") #Creaza un obiect de Barca
avion1 = Plane("Boeing", "747")     #Creaza un obiect de Avion

for x in (masina1, barca1, avion1):
  x.move()

output:
Drive!
Sail!
Fly!
```

Datorita polimorfismului putem apela o metoda cu aceiasi denumire pentru fiecare clasa in parte, executant instructiuni diferite.

## Putem folosii polimorfismul impreuna cu mostenirea?

Da putem, de exemplu avem o clasa Animal si aceasta este mostenita de catre alte doua clase Caine si Pisica. Clasa Animal are o metoda make_sound() care este mostenita de calsele derivate Caine si Pisica. De exemplu:

```python
class Animal:
    def __init__(self, rasa, greutate, ani):
        self.rasa = rasa
        self.greutate = greutate
        self.ani = ani
    
    def make_sound(self):
        pass
    # nu initializam metoda ci o lasam cat mai abstracta.


class Pisica(Animal):
    def __init__(self, rasa, greutate, ani):
        super().__init__(rasa, greutate, ani)
    
    def make_sound(self):
        print("Miaw")


class Caine(Animal):
    def __init__(self, rasa, greutate, ani):
        super().__init__(rasa, greutate, ani)
    
    def make_sound(self):
        print("Ham Ham")


pisica1 = Pisica("Mainecoon", 10, 4)
caine1 = Pisica("Pikinez", 4, 10)

pisica1.make_sound()
caine1.make_sound()

output:
Miaw
Ham Ham
```


### Metodele preluate de catre clasele derivate din clasa parinte si modificate se numesc metode **suprascrise** sau **overriden**.

Datorita polimorfismului putem folosii aceiasi metoda pentru toate clasele mostenitoare.


