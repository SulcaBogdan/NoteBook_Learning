# Python functions

O funcție este un bloc de cod care rulează numai atunci când este apelată.

Puteți trece date, cunoscute ca parametri, într-o funcție.

O funcție poate returna date ca rezultat.

### În Python, o funcție este definită folosind cuvântul cheie 'def':

De exemplu:

```python
def functia_mea():
    print("Mesajul functiei")
```

## Apelarea unei functii

Pentru a apela o funcție, utilizați numele funcției urmat de paranteze:

De exemplu:

```python
def functia_mea():
    print("Mesajul functiei")

functia_mea()

output:
Mesajul functiei
```

## Argumentele

Informațiile pot fi transmise în funcții ca argumente.

Argumentele sunt specificate după numele funcției, în interiorul parantezei. Puteți adăuga câte argumente doriți, doar separați-le cu o virgulă.

Următorul exemplu are o funcție cu un singur argument (fname). Când funcția este apelată, transmitem un prenume, care este folosit în interiorul funcției pentru a tipări numele complet:

```python
def functia_mea(nume):
  print(name + " Georgia")

functia_mea("Emil")
functia_mea("Adrian")
functia_mea("Marius")

output:
Emil Georgia
Adrian Georgia
Marius Gerogia
```

**Argumentele sunt adesea scurtate la args în documentațiile Python.**

## Parametri sau argumente?
Termenii parametru și argument pot fi folosiți pentru același lucru: informații care sunt transmise într-o funcție.

**Din perspectiva unei funcții:**

**Un parametru este variabila listată între paranteze în definiția funcției.**

**Un argument este valoarea care este trimisă funcției atunci când este apelată**.

## Numarul argumentelor

În mod implicit, o funcție trebuie apelată cu numărul corect de argumente. Înseamnă că, dacă funcția ta așteaptă 2 argumente, trebuie să apelezi funcția cu 2 argumente, nu mai multe și nu mai puțin.

```python
def functia_mea(nume, prenume):
  print(nume + " " + prenume)

functia_mea("Dodan", "Bogdan")

output:
Dodan Bogdan
```

Această funcție așteaptă 2 argumente, dar primește doar 1:

```python
def functia_mea(nume, prenume):
  print(nume + " " + prenume)

functia_mea("Dodan")

output:
Traceback (most recent call last):
  File "[your file]", line 4, in <module>
    functia_mea("Dodan")
TypeError: functia_mea() missing 1 required positional argument: 'prenume'
```

## Argumente arbitrare, *args

Dacă nu știți câte argumente vor fi trecute în funcția dvs., adăugați un * înaintea numelui parametrului în definiția funcției.

În acest fel, funcția va primi un tuplu de argumente și poate accesa elementele în consecință:

```python
def functia_mea(*copii):
  print("Cel mai mic copil este " + copii[2])

functia_mea("Emil", "Tobias", "Adrian")

output:
Cel mai mic copil este Adrian
```

## Argumentele cuvintelor cheie

De asemenea, puteți trimite argumente cu sintaxa cheie = valoare.

În acest fel ordinea argumentelor nu contează.

```python
def functia_mea(copil3, copil2, copil1):
  print("The youngest child is " + child3)

functia_mea(copil1 = "Emil", copil2 = "Tobias", copil3 = "Adrian")

output:
Cel mai mic copil este Adrian
```

## Argumente de cuvinte cheie arbitrare, **kwargs

Dacă nu știți câte argumente cheie vor fi trecute în funcția dvs., adăugați două asteriscuri: ** înaintea numelui parametrului în definiția funcției.

În acest fel, funcția va primi un dicționar de argumente și poate accesa elementele în consecință:

```python
def functia_mea(**kid):
  print("Prenumele lui este " + kid["prenume"])

functia_mea(nume = "Dodan", prenume = "Bogdan")

output:
Prenumele lui este Bogdan
```

## Valoarea implicită a parametrului

Următorul exemplu arată cum se utilizează o valoare implicită a parametrului.

Dacă apelăm funcția fără argument, aceasta folosește valoarea implicită:

```python
def functia_mea(country = "Romania"):
  print("Locuiesc in " + country)

functia_mea("Suedia")
functia_mea("India")
functia_mea()
functia_mea("Brazilia")

output:
Locuiesc in Suedia
Locuiesc in India
Locuiesc in Romania
Locuiesc in Brazilia
```

## Trecerea unei liste ca argument

Puteți trimite orice tip de date de argument unei funcții (șir, număr, listă, dicționar etc.) și va fi tratat ca același tip de date în interiorul funcției.

De exemplu. dacă trimiteți o Listă ca argument, aceasta va fi totuși o Listă când ajunge la funcția:

```python
def functia_mea(mancare):
  for x in mancare:
    print(x)

fructe = ["mar", "banana", "cirese"]

functia_mea(fructe)

output:
mar
banana
cirese
```

## Valori returnabile

Pentru a permite unei funcții să returneze o valoare, utilizați instrucțiunea return:

```python
def my_function(x):
  return 5 * x

print(my_function(3))
print(my_function(5))
print(my_function(9))

output:
15
25
45
```

## pass statement

Definițiile funcției nu pot fi goale, dar dacă dintr-un motiv oarecare aveți o definiție a funcției fără conținut, introduceți 'pass' pentru a evita o eroare.

```python
def myfunction():
  pass

# având o definiție de funcție goală ca aceasta, ar genera o eroare fără instrucțiunea pass
```

## Recursivitate

Recursiunea este un concept matematic și de programare comun. Înseamnă că o funcție se apeleaza singură. Acest lucru are avantajul de a însemna că puteți parcurge datele pentru a ajunge la un rezultat.

Dezvoltatorul ar trebui să fie foarte atent cu recursiunea, deoarece poate fi destul de ușor să introduci în scrierea unei funcții care nu se termină niciodată, sau una care utilizează cantități în exces de memorie sau puterea procesorului. Cu toate acestea, atunci când este scrisă corect recursiunea poate fi o abordare foarte eficientă și elegantă din punct de vedere matematic pentru programare.

În acest exemplu, tri_recursion() este o funcție pe care am definit-o să se numească singură ("recurse"). Folosim variabila k ca date, care scade (-1) de fiecare dată când recurgem. Recursiunea se termină atunci când condiția nu este mai mare de 0 (adică când este 0).

Pentru un nou dezvoltator, poate dura ceva timp pentru a afla cum funcționează exact acest lucru, cel mai bun mod de a afla este testarea și modificarea acestuia.

```python
def tri_recursion(k):
  if(k > 0):
    result = k + tri_recursion(k - 1)
    print(result)
  else:
    result = 0
  return result

print("\n\nRecursion Example Results")
tri_recursion(6)

output:
Recursion Example Results
1
3
6
10
15
21
```