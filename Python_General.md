# Informatii generale legate de limbajul de programare Python.

-**Python** este un limbaj de programare dinamic care ofera suport pentru mai multe stiluri de programare. Acestea sunt:

**1. Programarea procedulara**
    
Aceasta este un stil de progamare in care programul este structurat intr-o secventa de instructiuni care sunt executate una dupa alta.

<div style="text-align:center;">
<a href="https://postimg.cc/KK50xYrK" target="_blank">
  <img src="https://i.postimg.cc/YS5ZNGvx/Procedular-prog.png" alt="Procedural Programming" width="200" height="250">
</a>
</div>


_Exemplu de cod:_

```python
#Definirea unei functii pentru adunare
def sum(a,b):
    rezultat = a + b
    return rezultat

#Declararea a doua variabile cu input float
num1 = float(input("Introdu primul numar:"))
num2 = float(input("Introdu al doilea numar:"))

#Apelarea functiei sum care aduna cele doua variabile
rezultat_adunare = sum(num1, num2)

#Afisarea rezultatului
print(rezultat_adunare)
```

**2. Programare orientata pe obiecte** 

In **Python** programarea orientata pe obiecte(OOP) este un stil de programare in care codul este organizat in jurul obiectelor. Voi extinde acest subiect intr-un fisier separat.

<div style="text-align:center;">
<a href="https://postimg.cc/F1V5KjNR" target="_blank">
  <img src="https://i.postimg.cc/MZhWdDLy/c3086a153b545f8273de5b57cfa16dca.png" alt="Procedural Programming" width="200" height="250">
</a>
</div>

_Exemplu de cod:_

```python
#Crearea clasei Animal
class Animal:
    #Crearea constructorului clasei Animal
    def __init__(self, nume, rasa, greutate):
        #Definirea atributelor / self = Obiectul de Animal.
        self.nume = nume
        self.rasa = rasa
        self.greutate = greutate
    
    #Definirea unei functii/metode a clasei Animal unde vom afisa informatiile despre fiecare obiect creat.
    def afiseaza_info(self):
        print(f"Numele animalului este {self.nume}, face parte din rasa {self.rasa} si are o greutate de {self.greutate}")
```

**3. Programarea functionala**

**Programarea functionala** este un stil de programare unde problema este abordata si rezolvata perin crearea si combinarea unui set de functii. Pentru ca aceasta abordare sa fie eficienta, functiile sunt concepute sa fie _"pure"_ (**primesc doar intrari si produc iesiri.**).

<div style="text-align:center;">
<a href="https://postimg.cc/xcj46hHG" target="_blank">
  <img src="https://i.postimg.cc/QxcZdrdz/Function.png" alt="Procedural Programming" width="400" height="250">
</a>
</div>

_Exemplu de cod:_

```python
#Definirea unei functii pure
def sum(a, b):
    return a + b

#Definirea unei functii care utilizeaza imutabilitatea
def double_val(lista):
    return [x * 2 for x in lista]

#Exemplu de utilizare a functiilor
rez_sum = aduna(3,4)
print(f"Rezultatul sum : {rez_sum} ")

#Initializarea unei liste cu 5 elemente
lista_initiala = [1,2,3,4,5]
#Intializarea listei cu valorilo dublate prin functia de mai sus
lista_dublata = double_val(lista_initiala)

#Printarea rezultatelor
print(f"Lista initiala: {lista_initiala}")
print(f"Lista dublata: {lista_dublata}")

```