# Break/Continue in Java

## Instrucțiunea `break` în Java

Ai văzut deja instrucțiunea "break" folosită într-un capitol anterior al acestui tutorial. A fost folosită pentru a "ieși" dintr-o instrucțiune switch.

Instrucțiunea "break" poate fi de asemenea folosită pentru a ieși dintr-o buclă.

Acest exemplu oprește bucla când `i` este egal cu 4:
```java
for (int i = 0; i < 10; i++) {
  if (i == 4) {
    break;
  }
  System.out.println(i);
}

output:
0
1
2
3
```

## Instrucțiunea `continue` în Java

Instrucțiunea "continue" întrerupe o iterație (în buclă), dacă apare o condiție specificată, și continuă cu următoarea iterație în buclă.

Acest exemplu sare peste valoarea 4:
```java
for (int i = 0; i < 10; i++) {
  if (i == 4) {
    continue;
  }
  System.out.println(i);
}

output:
0
1
2
3
5
6
7
8
9
```

## Instrucțiunile `break` și `continue` în bucla `while` în Java

Puteți folosi, de asemenea, instrucțiunile "break" și "continue" în buclele "while":

```java
int i = 0;
while (i < 10) {
  System.out.println(i);
  i++;
  if (i == 4) {
    break;
  }
}

output:
0
1
2
3
```
Si acelasi exemplu si cu `continue`.

```java
int i = 0;
while (i < 10) {
  if (i == 4) {
    i++;
    continue;
  }
  System.out.println(i);
  i++;
}

output:
0
1
2
3
5
6
7
8
9
```



