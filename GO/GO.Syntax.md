

# Sintaxa Go

Un fișier Go este compus din următoarele părți:

- Declararea pachetului
- Importul pachetelor
- Funcții
- Instrucțiuni și expresii

Examinați codul de mai jos pentru a înțelege mai bine:

### Exemplu

```go
package main

import ("fmt")

func main() {
    fmt.Println("Hello World!")
}
```

### Explicația exemplului

- **Linia 1**: În Go, fiecare program face parte dintr-un pachet. Definim acest lucru folosind cuvântul cheie `package`. În acest exemplu, programul aparține pachetului `main`.
- **Linia 2**: `import ("fmt")` ne permite să importăm fișiere incluse în pachetul `fmt`.
- **Linia 3**: O linie goală. Go ignoră spațiile albe. Adăugarea de spații albe face codul mai ușor de citit.
- **Linia 4**: `func main() {}` este o funcție. Orice cod din interiorul acoladelor `{}` va fi executat.
- **Linia 5**: `fmt.Println()` este o funcție disponibilă în pachetul `fmt`. Este folosită pentru a afișa text. În exemplul nostru, va afișa „Hello World!”.

> **Notă**: În Go, orice cod executabil aparține pachetului `main`.

---

# Instrucțiuni în Go

`fmt.Println("Hello World!")` este o instrucțiune.

În Go, instrucțiunile sunt separate fie prin încheierea unei linii (prin apăsarea tastei Enter), fie printr-un punct și virgulă `;`.

Apăsarea tastei Enter adaugă implicit un „;” la sfârșitul liniei (nu apare în codul sursă).

Acolada stângă `{` nu poate apărea la începutul unei linii.

Rulați următorul cod și observați ce se întâmplă:

### Exemplu

```go
package main

import ("fmt")

func main() {
    fmt.Println("Hello World!")
}
```

---

# Cod compact în Go

Puteți scrie cod mai compact, cum este ilustrat mai jos (nu este recomandat deoarece face codul mai greu de citit):

### Exemplu

```go
package main; import ("fmt"); func main() { fmt.Println("Hello World!");}
```

---

