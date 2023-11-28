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

## Python este un limbaj de programare **intrerpretat**

**Python** este un limbaj de programare interpetat, ceea ce inseamna ca nu necesita o etapa separata de compilare inainte de a executa codul. In schimb, interpretorul Python citeste si executa direct codul sursa line by line.

_Procesul complet este:_

**1. Scrierea codului sursa(de catre programator):**

Etapa unde noi(programatorii) scriem  instructiunile si logicile programului(linii de cod).

```python
#Initializarea a doua varibile num1 si num2
num1 = 6
num2 = 7
#Initializarea variabilei suma cu adunarea variabilelor num1 si num2
suma = num1 + num2

#Printarea rezultatului intr-un fstring
print(f"Suma numerelor {num1} si {num2} este : {suma}")
```
   
**2. Analiza lexicala si sintatica(de catre interpetorul Python):**

Interpretorul Python parcurge codul sursa si il descompune in "token-uri", unitati semantice, si apoi construieste un "arbore sintatic abstract"(AST) care reprezinta structura logica a codului sursa.

<div style="text-align:center;">
<a href="https://postimg.cc/tsP1cXL8" target="_blank">
  <img src="https://i.postimg.cc/x1pKc8gj/AST.png" alt="Procedural Programming" width="350" height="250">
</a>
</div>

**Analiza Lexicală și Sintactică Simplificată**

#### "Token"-uri

- `numar1`
- `=`
- `5`
- `numar2`
- `=`
- `7`
- `suma`
- `=`
- `numar1` + `numar2`
- `print`
- `(` 
- `f"Suma numerelor {numar1} și {numar2} este: {suma}"`
- `)`

#### Arbore Sintactic Abstract Simplificat

- `atribuire`
  - `identificator: numar1`
  - `valoare: 5`

- `atribuire`
  - `identificator: numar2`
  - `valoare: 7`

- `atribuire`
  - `identificator: suma`
  - `adunare`
    - `identificator: numar1`
    - `identificator: numar2`

- `afisare`
  - `format_string: "Suma numerelor {numar1} și {numar2} este: {suma}"`


**3. Generarea bytecode-ului:**

AST este tradus in bytecode, care este un set de instructiuni intermediare specifice Python.

_Bytecode python:_

  **1    LOAD_CONST          0 (5)**

       STORE_NAME          0 (numar1)

  **2    LOAD_CONST          1 (7)**

       STORE_NAME          1 (numar2)

 **3    LOAD_NAME           0 (numar1)**

       LOAD_NAME           1 (numar2)

       BINARY_ADD

       STORE_NAME          2 (suma)


  **4    LOAD_NAME           3 (print)**

       LOAD_CONST          2 ('Suma numerelor {numar1} și {numar2} este: {suma}')

       LOAD_NAME           0 (numar1)

       LOAD_NAME           1 (numar2)

       LOAD_NAME           2 (suma)

       BUILD_STRING        4

       CALL_FUNCTION       1

       POP_TOP

       LOAD_CONST          3 (None)

       RETURN_VALUE




**4. Executia bytecode-ului:**

Bytecode-ul este executat de catre "Python Virtual Machine"(Python VM). In timplu executiei bytecode-ului, Python VM utilizeaza o structura de date numita stack(stiva) pentru a gestiona temporar valorile, rezultatele operatiilor si adresele de revenire. Vom discuta mai in detaliu despre stack in alt fisier.

**5. Rularea programului:**

La finalul executiei programului, VM poate furniza rezultatele asteptate(cum ar fi afisarea pe consola, returnarea unei valori, etc.).

## La ce poate fi utilizat Python?

1. Python poate fi utilizat pe un server pentru a crea aplicații web.
   
2. Python poate fi folosit alături de software pentru a crea fluxuri de lucru.
3. Python poate să se conecteze la sisteme de baze de date. De asemenea, poate citi și modifica fișiere.
4. Python poate fi folosit pentru manipularea **big data** și realizarea de calcule matematice complexe.
5. Python poate fi utilizat pentru prototipare rapidă sau pentru dezvoltarea de software gata pentru producție.

## De ce Python?

1. Python functioneaza pe diferite platforme (Windows, Mac, Linux, Raspberry Pi, etc.)
   
2. Python are o sintaxa simpla, similara limbii engleze, ceea ce permite programatorilor sa scrie cod cu mai putine linii de cod si automat mult mai rapid comparativ cu alte limbaje de programare.
3. Python ruleaza pe un sistem de interpretare, ceea ce inseamna ca codul poate fi executat imediat ce este scris. Acest lucru inseamna ca prototipizasrea poate fi foarte rapida.
4. Python poate fi tratat intr-un mod procedular, un mod OOP sau un mod functional.

## Sintaxa python comparata cu alt limbaj de programare

_Hello World:_

python:
```python
print("Hello World!")
```
java:
```java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello, World!");
    }
}
```
<div style="text-align:center;">
<a href="https://postimg.cc/xcj46hHG" target="_blank">
  <img src="https://media.tenor.com/DxeK02KwNbEAAAAd/java-python.gif" alt="Procedural Programming" width="500" height="">
</a>
</div>