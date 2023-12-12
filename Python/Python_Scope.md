# Python Scope

O variabilă este disponibilă numai din interiorul regiunii în care este creată. Aceasta se numește Scope.

## Local Scope

O variabilă creată în interiorul unei funcții aparține domeniului local al acelei funcții și poate fi utilizată numai în interiorul acelei funcții.

```python
def functia_mea():
  x = 300
  print(x)

functia_mea()

output:
300
```

## Functie intr-o functie

După cum este explicat în exemplul de mai sus, variabila x nu este disponibilă în afara funcției, dar este disponibilă pentru orice funcție din interiorul funcției:

```python
def functia_mea():
  x = 300
  def functia_mea_inner():
    print(x)
  functia_mea_inner()

functia_mea()

output:
300
```

functia inner este apelata in interiorul functiei principale care trimite instructiuni de printare a variabilei x care este o variabila locala in functia principala. Apoi functia principala este apelata si outputul este 300.

## Global Scope

O variabilă creată în corpul principal al codului Python este o variabilă globală și aparține domeniului global.

Variabilele globale sunt disponibile din orice domeniu, global și local.

Exemplu:

```python
x = 300

def functia_mea():
  print(x)

functia_mea()

print(x)

output:
300
300
```

## Numirea variabilelor

Dacă operați cu același nume de variabilă în interiorul și în afara unei funcții, Python le va trata ca două variabile separate, una disponibilă în domeniul global (în afara funcției) și una disponibilă în domeniul local (în interiorul funcției):

```python
x = 300

def functia_mea():
  x = 200
  print(x)

functia_mea()

print(x)

output:
200
300
```

## Cuvantul cheie ''global''

Dacă trebuie să creați o variabilă globală, dar sunteți blocat în domeniul local, puteți utiliza cuvântul cheie global.

Cuvântul cheie global face variabila globală.

```python
def functia_mea():
  global x
  x = 300

functia_mea()

print(x)

output:
300
300
```
Dacă utilizați cuvântul cheie global, variabila aparține global scope.

De asemenea, utilizați cuvântul cheie global dacă doriți să modificați o variabilă globală în interiorul unei funcții.
```python
x = 300

def functia_mea():
  global x
  x = 200

functia_mea()

print(x)

output:
200
```
Pentru a modifica valoarea unei variabile globale în interiorul unei funcții, consultați variabila folosind cuvântul cheie global: