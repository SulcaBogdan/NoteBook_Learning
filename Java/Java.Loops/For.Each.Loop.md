# For Each loop

### Buclă "for-each"

Există și o buclă "for-each", care este folosită exclusiv pentru a parcurge elementele dintr-un array:

```java
for (type variableName : arrayName) {
  // bloc de cod
}
```

Următorul exemplu afișează toate elementele din array-ul "`cars`", folosind o buclă "`for-each`":

```java
String[] cars = {"Volvo", "BMW", "Ford", "Mazda"};
for (String i : cars) {
  System.out.println(i);
}

output:
Volvo
BMW
Ford
Mazda
```



