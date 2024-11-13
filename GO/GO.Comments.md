

# Comentarii în Go

Un comentariu este un text care este ignorat la execuție.

Comentariile pot fi utilizate pentru a explica codul și pentru a-l face mai ușor de citit.

Comentariile pot fi folosite și pentru a preveni execuția codului atunci când se testează un cod alternativ.

Go suportă comentarii pe o singură linie și comentarii pe mai multe linii.

## Comentarii pe o singură linie în Go

Comentariile pe o singură linie încep cu două bare oblice (`//`).

Orice text între `//` și sfârșitul liniei este ignorat de compilator (nu va fi executat).

### Exemplu

```go
// Acesta este un comentariu
package main

import ("fmt")

func main() {
    // Acesta este un comentariu
    fmt.Println("Hello World!")
}
```

Următorul exemplu folosește un comentariu pe o singură linie la sfârșitul unei linii de cod:

### Exemplu

```go
package main

import ("fmt")

func main() {
    fmt.Println("Hello World!") // Acesta este un comentariu
}
```

## Comentarii pe mai multe linii în Go

Comentariile pe mai multe linii încep cu `/*` și se termină cu `*/`.

Orice text între `/*` și `*/` va fi ignorat de compilator.

### Exemplu

```go
package main

import ("fmt")

func main() {
    /* Codul de mai jos va afișa Hello World
       pe ecran și este extraordinar */
    fmt.Println("Hello World!")
}
```

> **Sfat**: Alegerea tipului de comentariu depinde de preferințe. În mod obișnuit, `//` este folosit pentru comentarii scurte, iar `/* */` pentru comentarii mai lungi.

---

# Comentarii pentru prevenirea execuției codului

Puteți folosi comentarii și pentru a preveni execuția codului.

Codul comentat poate fi salvat pentru referințe ulterioare și depanare.

### Exemplu

```go
package main

import ("fmt")

func main() {
    fmt.Println("Hello World!")
    // fmt.Println("Această linie nu se execută")
}
```

