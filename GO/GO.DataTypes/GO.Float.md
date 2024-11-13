# Tipuri de Date Float în Go

Tipurile de date float sunt utilizate pentru a stoca numere pozitive și negative cu un punct zecimal, cum ar fi `35.3`, `-2.34`, sau `3597.34987`.

Tipurile de date float au două cuvinte cheie:

| Tip       | Dimensiune | Interval                            |
|-----------|------------|-------------------------------------|
| `float32` | 32 biți    | -3.4e+38 la 3.4e+38                |
| `float64` | 64 biți    | -1.7e+308 la +1.7e+308             |

> **Sfat:** Tipul implicit pentru float este `float64`. Dacă nu specifici un tip, acesta va fi `float64`.

---

### Cuvântul cheie `float32`

Acest exemplu arată cum se declară variabile de tipul `float32`:

```go
package main
import ("fmt")

func main() {
    var x float32 = 123.78
    var y float32 = 3.4e+38
    fmt.Printf("Tip: %T, valoare: %v\n", x, x)
    fmt.Printf("Tip: %T, valoare: %v\n", y, y)
}
```

---

### Cuvântul cheie `float64`

Tipul de date `float64` poate stoca un set mai mare de numere decât `float32`.

##### Exemplu

Acest exemplu arată cum se declară o variabilă de tip `float64`:

```go
package main
import ("fmt")

func main() {
    var x float64 = 1.7e+308
    fmt.Printf("Tip: %T, valoare: %v\n", x, x)
}
```

---

#### Ce Tip de Float să Folosim?

Tipul de float care trebuie ales depinde de valoarea pe care variabila trebuie să o stocheze.

#### Exemplu

Acest exemplu va rezulta într-o eroare deoarece `3.4e+39` este în afara intervalului pentru `float32`:

```go
package main
import ("fmt")

func main() {
    var x float32 = 3.4e+39
    fmt.Println(x)
}
```

**Rezultat:**
```
./prog.go:5:7: constant 3.4e+39 overflows float32
```