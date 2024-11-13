# Tipuri de Date Întregi în Go

### Tipuri de Date Întregi

- Tipurile de date întregi sunt folosite pentru a stoca numere întregi fără zecimale, cum ar fi `35`, `-50` sau `1345000`.
- Tipurile de date întregi în Go sunt împărțite în două categorii:
  - **Întregi semnați (Signed Integers)**: Pot stoca atât valori pozitive, cât și negative.
  - **Întregi fără semn (Unsigned Integers)**: Pot stoca doar valori nenegative.

> **Tip**: Tipul implicit pentru întregi este `int`. Dacă nu specifici un tip, Go va folosi `int`.

### Întregi Semnați

Întregii semnați sunt declarați folosind unul dintre cuvintele cheie `int`. Aceștia pot stoca atât valori pozitive, cât și negative.

Exemplu:

```go
package main
import ("fmt")

func main() {
    var x int = 500
    var y int = -4500
    fmt.Printf("Tip: %T, Valoare: %v\n", x, x)
    fmt.Printf("Tip: %T, Valoare: %v\n", y, y)
}
```

Go are cinci tipuri de întregi semnați:

| Tip     | Dimensiune          | Interval                                         |
| ------- | -------------------- | ------------------------------------------------ |
| `int`   | Depinde de platformă: 32 biți în sistemele pe 32 biți și 64 biți în sistemele pe 64 biți | -2147483648 până la 2147483647 în sistemele pe 32 biți și -9223372036854775808 până la 9223372036854775807 în sistemele pe 64 biți |
| `int8`  | 8 biți / 1 byte      | -128 până la 127                                 |
| `int16` | 16 biți / 2 bytes    | -32768 până la 32767                             |
| `int32` | 32 biți / 4 bytes    | -2147483648 până la 2147483647                   |
| `int64` | 64 biți / 8 bytes    | -9223372036854775808 până la 9223372036854775807 |

### Întregi fără Semn

Întregii fără semn sunt declarați folosind unul dintre cuvintele cheie `uint`. Aceștia pot stoca doar valori pozitive.

Exemplu:

```go
package main
import ("fmt")

func main() {
    var x uint = 500
    fmt.Printf("Tip: %T, Valoare: %v\n", x, x)
}
```

Go are cinci tipuri de întregi fără semn:

| Tip      | Dimensiune          | Interval                                         |
| -------- | -------------------- | ------------------------------------------------ |
| `uint`   | Depinde de platformă: 32 biți în sistemele pe 32 biți și 64 biți în sistemele pe 64 biți | 0 până la 4294967295 în sistemele pe 32 biți și 0 până la 18446744073709551615 în sistemele pe 64 biți |
| `uint8`  | 8 biți / 1 byte      | 0 până la 255                                    |
| `uint16` | 16 biți / 2 bytes    | 0 până la 65535                                  |
| `uint32` | 32 biți / 4 bytes    | 0 până la 4294967295                             |
| `uint64` | 64 biți / 8 bytes    | 0 până la 18446744073709551615                   |

### Ce Tip de Întreg Să Folosești?

Tipul de întreg ales depinde de valoarea pe care variabila trebuie să o stocheze. Dacă valoarea depășește intervalul de valori al tipului specificat, va apărea o eroare.

Exemplu:

```go
package main
import ("fmt")

func main() {
    var x int8 = 1000 // Aceasta va produce o eroare deoarece int8 nu poate stoca 1000
    fmt.Printf("Tip: %T, Valoare: %v\n", x, x)
}
```

---

# Tipuri de Date Float și Complexe în Go

### Tipuri de Date cu Virgulă Mobilă (Float Data Types)

Tipurile de date `float32` și `float64` sunt utilizate pentru a stoca numere zecimale.

Exemple:

- `float32`: poate stoca valori de la aproximativ `1.18e-38` până la `3.4e38`.
- `float64`: poate stoca valori de la aproximativ `2.23e-308` până la `1.8e308`.

> În general, se folosește `float64` pentru o precizie mai mare.

Exemplu de utilizare:

```go
package main
import ("fmt")

func main() {
    var x float32 = 3.1415
    fmt.Printf("Tip: %T, Valoare: %v\n", x, x)
}
```

### Tipuri de Date Complexe

Go include tipuri de date pentru numere complexe, precum `complex64` și `complex128`. Aceste tipuri stochează numere complexe, care includ o parte reală și una imaginară.

Exemple:

- `complex64`: folosește `float32` pentru părțile reală și imaginară.
- `complex128`: folosește `float64` pentru părțile reală și imaginară.

Exemplu de utilizare:

```go
package main
import ("fmt")

func main() {
    var x complex64 = 1 + 2i
    fmt.Printf("Tip: %T, Valoare: %v\n", x, x)
}
```

