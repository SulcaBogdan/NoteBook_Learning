# Try Except

Blocul `try `vă permite să testați un bloc de cod pentru erori.

Blocul `except` vă permite să gestionați eroarea.

Blocul `else` vă permite să executați cod atunci când nu există nicio eroare.

Blocul `final` vă permite să executați cod, indiferent de rezultatul blocurilor try- and except.

## Tratarea exceptiilor

Când apare o eroare sau o excepție, așa cum o numim, Python se va opri în mod normal și va genera un mesaj de eroare.

Aceste excepții pot fi gestionate folosind instrucțiunea `try`:

**Blocul try va genera o excepție, deoarece x nu este definit:**
```python
try:
  print(x)
except:
  print("S-a intamplat o eroare")
  
output:
S-a intamplat o eroare
```

Deoarece blocul `try` generează o eroare, blocul `except` va fi executat.

Fără blocul `try`, programul se va bloca și va genera o eroare:

```python
print(x)

output:
Traceback (most recent call last):
  File "[your file name]", line 3, in <module>
    print(x)
NameError: name 'x' is not defined
```

## Mai multe exceptii

Puteți defini câte blocuri de excepție doriți, de ex. dacă doriți să executați un bloc special de cod pentru un tip special de eroare:

```python
try:
  print(x)
except NameError:
  print("Variabila x nu este definita")
except:
  print("Ceva nu a mers bine")

output:
Variabila x nu este definita
```

## Else

Puteți folosi cuvântul cheie `else` pentru a defini un bloc de cod care să fie executat dacă nu au apărut erori:

In acest exemplu blocul `try` nu genereaza nici o eroare.

```python
try:
  print("Hello")
except:
  print("Ceva nu a mers bine")
else:
  print("Totul este in regula")

output:
Hello
Totul este in regula
```

## Finally

Blocul `final`, dacă este specificat, va fi executat indiferent dacă blocul `try` ridică o eroare sau nu.


```python
try:
  print(x)
except:
  print("Ceva nu a mers bine")
finally:
  print("try except' s-a finalizat")

output:
Ceva nu a mers bine
try except' s-a finalizat
```
**Acest lucru poate fi util pentru a închide obiecte și pentru a curăța resurse:**

```python
try:
  f = open("demofile.txt")
  try:
    f.write("Lorum Ipsum")
  except:
    print("Ceva nu a mers in procesul de scriere a documentului")
  finally:
    f.close()
except:
  print("Ceva nu a mers la deschiderea documentului")
  
Programul poate continua, fără a lăsa obiectul fișier deschis.

output:
Ceva nu a mers in procesul de scriere a documentului
```


## Ridicarea exceptiilor

În calitate de dezvoltator Python, puteți alege să aruncați o excepție dacă apare o condiție.

Pentru a arunca (sau a ridica) o excepție, utilizați cuvântul cheie de ridicare.

Generați o eroare și opriți programul dacă x este mai mic decât 0:
```python
x = -1

if x < 0:
  raise Exception("Sorry, no numbers below zero")

output:
Traceback (most recent call last):
  File "[your file]", line 4, in <module>
    raise Exception("Fara numere mai mici ca 0")
Exception: Fara numere mai mici ca 0
```


Cuvântul cheie `raise` este folosit pentru a ridica o excepție.

Puteți defini ce fel de eroare să semnalați și textul de imprimat utilizatorului.

```python
x = "hello"

if not type(x) is int:
  raise TypeError("Only integers are allowed")

output:
Traceback (most recent call last):
  File "[your file]", line 4, in <module>
    raise TypeError("Doar numerele sunt permise")
TypeError: Doar numerele sunt permise
```
