# If Else conditiile

Știi deja că Java suportă condițiile logice obișnuite din matematică:

- Mai mic decât: `a < b`
- Mai mic sau egal cu: `a <= b`
- Mai mare decât: `a > b`
- Mai mare sau egal cu: `a >= b`
- Egal cu: `a == b`
- Diferit de: `a != b`

Poți folosi aceste condiții pentru a realiza diferite acțiuni în funcție de decizii.

Java are următoarele instrucțiuni condiționale:

- Folosește `if` pentru a specifica un bloc de cod care să fie executat dacă o condiție specificată este adevărată.
- Folosește `else` pentru a specifica un bloc de cod care să fie executat dacă aceeași condiție este falsă.
- Folosește `else if` pentru a specifica o nouă condiție de testat, dacă prima condiție este falsă.
- Folosește `switch` pentru a specifica mai multe blocuri alternative de cod care să fie executate.


### Instrucțiunea `if`

Folosește instrucțiunea `if` pentru a specifica un bloc de cod Java care să fie executat dacă o condiție este adevărată.

```java
if (condition) {
  // blocul de cod va fi executat daca codintia este true
}
```

Reține că `if` este scris cu litere mici. Literele mari (`If` sau `IF`) vor genera o eroare.

În exemplul de mai jos, testăm două valori pentru a afla dacă 20 este mai mare decât 18. Dacă condiția este adevărată, se va afișa un text:

```java
if (20 > 18) {
  System.out.println("20 este mai mare ca 18");
}

output:
20 este mai mare ca 18
```

Putem testa si variabile:

```java
int x = 20;
int y = 18;
if (x > y) {
  System.out.println("x este mai mare ca y");
}

output:
x este mai mare ca y
```

### Explicația Exemplului

În exemplul de mai sus, folosim două variabile, `x` și `y`, pentru a testa dacă `x` este mai mare decât `y` (folosind operatorul `>`). Deoarece `x` este `20` și `y` este `18`, și știm că `20` este mai mare decât `18`, afișăm pe ecran că "`x` este mai mare decât `y`".

### Instrucțiunea `else`

Folosește instrucțiunea `else` pentru a specifica un bloc de cod care să fie executat dacă condiția este falsă.

```java
if (condition) {
  // blocul de cod o sa fie executat daca condition este true
} else {
  // blocul de cod o sa fie executat daca condition false
}
```

```java
int time = 20;
if (time < 18) {
  System.out.println("Good day.");
} else {
  System.out.println("Good evening.");
}

output:
Good evening
```

### Explicația Exemplului

În exemplul de mai sus, ora (20) este mai mare decât 18, deci condiția este falsă. Din acest motiv, trecem la condiția `else` și afișăm pe ecran "Bună seara". Dacă ora ar fi fost mai mică de 18, programul ar fi afișat "Bună ziua".

### Instrucțiunea `else if`

Folosește instrucțiunea `else if` pentru a specifica o nouă condiție de testat, dacă prima condiție este falsă.

```java
if (condition1) {
  // blocul de cod o sa fie executat daca condition1 este true
} else if (condition2) {
  // blocul de cod o sa fie executat daca condition1 este false si condition2 este true
} else {
  // blocul de cod o sa fie executat daca condition1 si condition2 sunt false
}
```

```java
int time = 22;
if (time < 10) {
  System.out.println("Good morning.");
} else if (time < 18) {
  System.out.println("Good day.");
} else {
  System.out.println("Good evening.");
}

output:
Goog evening
```

### Explicația Exemplului

În exemplul de mai sus, ora (22) este mai mare de 10, deci prima condiție este falsă. Următoarea condiție, din instrucțiunea `else if`, este, de asemenea, falsă, așa că trecem la instrucțiunea `else` deoarece ambele condiții (condition1 și condition2) sunt false și afișăm pe ecran "Bună seara".

