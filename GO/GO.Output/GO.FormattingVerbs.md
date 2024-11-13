# Verbe de formatare pentru `Printf()`

Go oferă mai multe verbe de formatare care pot fi utilizate cu funcția `Printf()`.

## Verbe generale de formatare

Următoarele verbe pot fi folosite cu toate tipurile de date:

| Verb | Descriere                                         |
|------|---------------------------------------------------|
| `%v` | Afișează valoarea în formatul implicit            |
| `%#v`| Afișează valoarea în format Go-syntax             |
| `%T` | Afișează tipul valorii                            |
| `%%` | Afișează simbolul `%`                             |

### Exemplu

```go
package main

import ("fmt")

func main() {
    var i = 15.5
    var txt = "Hello World!"

    fmt.Printf("%v\n", i)
    fmt.Printf("%#v\n", i)
    fmt.Printf("%T\n", i)
    fmt.Printf("%%\n")

    fmt.Printf("%v\n", txt)
    fmt.Printf("%#v\n", txt)
    fmt.Printf("%T\n", txt)
}
```

**Rezultat**:
```
15.5
15.5
float64
%
Hello World!
"Hello World!"
string
```

---

## Verbe de formatare pentru întregi

Următoarele verbe pot fi folosite cu tipul de date întreg:

| Verb  | Descriere                             |
|-------|---------------------------------------|
| `%b`  | Baza 2                                |
| `%d`  | Baza 10                               |
| `%+d` | Baza 10 și afișează semnul întotdeauna|
| `%o`  | Baza 8                                |
| `%O`  | Baza 8, prefixată cu `0o`             |
| `%x`  | Baza 16, litere mici                  |
| `%X`  | Baza 16, litere mari                  |
| `%4d` | Aliniere la dreapta, cu spații (lățime 4) |
| `%-4d`| Aliniere la stânga, cu spații (lățime 4) |
| `%04d`| Lățime 4, completare cu zerouri       |

### Exemplu

```go
package main

import ("fmt")

func main() {
    var i = 15

    fmt.Printf("%b\n", i)
    fmt.Printf("%d\n", i)
    fmt.Printf("%+d\n", i)
    fmt.Printf("%o\n", i)
    fmt.Printf("%O\n", i)
    fmt.Printf("%x\n", i)
    fmt.Printf("%X\n", i)
    fmt.Printf("%4d\n", i)
    fmt.Printf("%-4d\n", i)
    fmt.Printf("%04d\n", i)
}
```

**Rezultat**:
```
1111
15
+15
17
0o17
f
F
  15
15  
0015
```

---

## Verbe de formatare pentru șiruri de caractere

Următoarele verbe pot fi folosite cu tipul de date șir de caractere (string):

| Verb   | Descriere                                                 |
|--------|-----------------------------------------------------------|
| `%s`   | Afișează valoarea ca șir simplu                           |
| `%q`   | Afișează valoarea ca șir cu ghilimele                     |
| `%8s`  | Afișează valoarea ca șir simplu (lățime 8, aliniat dreapta)|
| `%-8s` | Afișează valoarea ca șir simplu (lățime 8, aliniat stânga) |
| `%x`   | Afișează valoarea ca hex dump de valori byte              |
| `% X`  | Afișează valoarea ca hex dump cu spații                   |

### Exemplu

```go
package main

import ("fmt")

func main() {
    var txt = "Hello"

    fmt.Printf("%s\n", txt)
    fmt.Printf("%q\n", txt)
    fmt.Printf("%8s\n", txt)
    fmt.Printf("%-8s\n", txt)
    fmt.Printf("%x\n", txt)
    fmt.Printf("% X\n", txt)
}
```

**Rezultat**:
```
Hello
"Hello"
   Hello
Hello   
48656c6c6f
48 65 6c 6c 6f
```

---

## Verbe de formatare pentru tipul boolean

Următorul verb poate fi folosit cu tipul de date boolean:

| Verb | Descriere                                         |
|------|---------------------------------------------------|
| `%t` | Afișează valoarea operatorului boolean (`true` sau `false`) |

### Exemplu

```go
package main

import ("fmt")

func main() {
    var i = true
    var j = false

    fmt.Printf("%t\n", i)
    fmt.Printf("%t\n", j)
}
```

**Rezultat**:
```
true
false
```

---

## Verbe de formatare pentru tipul float

Următoarele verbe pot fi folosite cu tipul de date float:

| Verb   | Descriere                                           |
|--------|-----------------------------------------------------|
| `%e`   | Notație științifică cu `e` ca exponent              |
| `%f`   | Afișare cu punct zecimal, fără exponent             |
| `%.2f` | Lățime implicită, precizie 2                        |
| `%6.2f`| Lățime 6, precizie 2                                |
| `%g`   | Exponent doar dacă este necesar, doar cifrele necesare |

### Exemplu

```go
package main

import ("fmt")

func main() {
    var i = 3.141

    fmt.Printf("%e\n", i)
    fmt.Printf("%f\n", i)
    fmt.Printf("%.2f\n", i)
    fmt.Printf("%6.2f\n", i)
    fmt.Printf("%g\n", i)
}
```

**Rezultat**:
```
3.141000e+00
3.141000
3.14
  3.14
3.141
```

