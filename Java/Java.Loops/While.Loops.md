# While loops in Java

## Bucle (Loops)

Buclele pot executa un bloc de cod atât timp cât o anumită condiție este îndeplinită.

Buclele sunt utile pentru că economisesc timp, reduc erorile și fac codul mai ușor de citit.

### Instrucțiunea `while`

Instrucțiunea `while` parcurge un bloc de cod atâta timp cât o anumită condiție este adevărată:


```java
while (condition) {
  // code block to be executed
}
```

### Exemplu `while`

În exemplul de mai jos, codul din buclă va rula în continuare atâta timp cât o variabilă (i) este mai mică decât 5:

```java
int i = 0;
while (i < 5) {
  System.out.println(i);
  i++;
}

output:
0
1
2
3
4
```

**Notă**: Nu uita să crești variabila folosită în condiție, altfel bucla nu se va termina niciodată!


### Bucla `do/while`

Bucla `do/while` este o variantă a buclei `while`. Această buclă va executa blocul de cod o dată, înainte de a verifica dacă condiția este adevărată, apoi va repeta bucla atâta timp cât condiția este adevărată.

```java
do {
  // code block to be executed
}
while (condition);
```

### Exemplu buclă `do/while`

Exemplul de mai jos folosește o buclă `do/while`. Bucla va fi întotdeauna executată cel puțin o dată, chiar dacă condiția este falsă, deoarece blocul de cod este executat înainte ca condiția să fie testată:

```java
int i = 0;
do {
  System.out.println(i);
  i++;
}
while (i < 5);

output:
0
1
2
3
4
```



