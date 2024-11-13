
# Constante în Go

Dacă o variabilă trebuie să aibă o valoare fixă, care nu poate fi schimbată, puteți folosi cuvântul cheie `const`.

Cuvântul cheie `const` declară variabila ca fiind „constantă”, ceea ce înseamnă că este nemodificabilă și doar pentru citire.

### Sintaxă

```go
const NUME_CONSTANTĂ tip = valoare
```

> **Notă**: Valoarea unei constante trebuie să fie atribuită în momentul declarării.

---

## Declararea unei constante

Iată un exemplu de declarare a unei constante în Go:

### Exemplu

```go
package main

import ("fmt")

const PI = 3.14

func main() {
    fmt.Println(PI)
}
```

---

## Reguli pentru constante

- Constantele urmează aceleași reguli de denumire ca și variabilele.
- Numele constantelor sunt de obicei scrise cu majuscule pentru a fi ușor de identificat și diferențiat de variabile.
- Constantele pot fi declarate atât în interiorul, cât și în afara unei funcții.

---

## Tipuri de constante

Există două tipuri de constante:

- Constante de tip definit (Typed constants)
- Constante de tip nedefinit (Untyped constants)

### Constante de tip definit

Constantele de tip definit sunt declarate cu un tip specificat:

### Exemplu

```go
package main

import ("fmt")

const A int = 1

func main() {
    fmt.Println(A)
}
```

---

### Constante de tip nedefinit

Constantele de tip nedefinit sunt declarate fără a specifica un tip:

### Exemplu

```go
package main

import ("fmt")

const A = 1

func main() {
    fmt.Println(A)
}
```

> **Notă**: În acest caz, tipul constantei este dedus din valoare (compilatorul decide tipul constantei pe baza valorii).

---

## Constante: Nemodificabile și doar pentru citire

Odată ce o constantă este declarată, nu este posibil să-i schimbați valoarea ulterior:

### Exemplu

```go
package main

import ("fmt")

func main() {
    const A = 1
    A = 2  // Eroare
    fmt.Println(A)
}
```

**Rezultat**:

```
./prog.go:8:7: cannot assign to A
```

---

## Declarația multiplă de constante

Mai multe constante pot fi grupate într-un bloc pentru o mai bună lizibilitate:

### Exemplu

```go
package main

import ("fmt")

const (
    A int = 1
    B = 3.14
    C = "Hi"
)

func main() {
    fmt.Println(A)
    fmt.Println(B)
    fmt.Println(C)
}
```

---

Aceasta este traducerea completă a secțiunii despre constante în Go. Dacă ai alte întrebări sau ai nevoie de mai mult ajutor, anunță-mă!