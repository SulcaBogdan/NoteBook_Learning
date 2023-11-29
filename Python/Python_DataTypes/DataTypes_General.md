# Tipurile de date in Python

## ❔Ce sunt tipurile de date?

Tipurile de date primitive in programare reprezinta un concept important.
Variabilele stocheaza informatii de tipuri diferite. Aceste tipuri sunt tipurile de date.

Python are urmatoarele tipuri de date by default:

Tipul textual: `str`

Tipul numeric: `int`, `float`, `complex`

Tipul logic: `bool`

Tipul binar: `bytes`, `bytearray`, `memoryview`

None Type: `NoneType`

Exemple de cod:

```python
# Tipul textual (str)
text = "Hello, World!"

# Tipul numeric (int, float, complex)
integer_number = 42
float_number = 3.14
complex_number = 1 + 2j

# Tipul logic (bool)
is_true = True
is_false = False

# Tipul binar (bytes, bytearray, memoryview)
my_bytes = b"binary"
my_bytearray = bytearray([65, 66, 67])
my_memoryview = memoryview(b"binary")

# None Type (NoneType)
my_none = None
```
## Cum facem conversia tipurilor de date in Python?

Prin conversie intelegem ca transformam un tip de date intr-unul nou. De exemplu:

```python
#Initializam variabila cu valoare textuala
text_var = "25"
#Conversia din text in numar
num_var = int(text_var)
```
Putem face conversia intre tipurile de date care au sens de exemplu nu are logica sa incercam sa transformam "Dodan" intr-o valoare numerica sau logica deoarece Dodan nu reprezinta cifre.
