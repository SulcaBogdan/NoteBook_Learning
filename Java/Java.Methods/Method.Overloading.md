# Method Overloading in Java

Cu method overloading, mai multe metode pot avea același nume, cu parametri diferiți:

```java
int myMethod(int x)
float myMethod(float x)
double myMethod(double x, double y)
```

Ia în considerare următorul exemplu, care are două metode care adaugă numere de tip diferit:

```java
static int plusMethodInt(int x, int y) {
  return x + y;
}

static double plusMethodDouble(double x, double y) {
  return x + y;
}

public static void main(String[] args) {
  int myNum1 = plusMethodInt(8, 5);
  double myNum2 = plusMethodDouble(4.3, 6.26);
  System.out.println("int: " + myNum1);
  System.out.println("double: " + myNum2);
}

output:
int: 13
double: 10.559999999999999
```

În loc să definim două metode care ar trebui să facă același lucru, este mai bine să suprascriem una.

În exemplul de mai jos, suprascriem metoda `plusMethod` să funcționeze atât pentru `int`, cât și pentru `double`:


```java
static int plusMethod(int x, int y) {
  return x + y;
}

static double plusMethod(double x, double y) {
  return x + y;
}

public static void main(String[] args) {
  int myNum1 = plusMethod(8, 5);
  double myNum2 = plusMethod(4.3, 6.26);
  System.out.println("int: " + myNum1);
  System.out.println("double: " + myNum2);
}

output:
int: 13
double: 10.559999999999999
```

**Notă**: Mai multe metode pot avea același nume atâta timp cât numărul și/sau tipul parametrilor sunt diferiți.



