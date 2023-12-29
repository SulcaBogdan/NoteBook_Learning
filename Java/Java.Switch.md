# Java switch

## Instrucțiunile `switch`

În loc să scrii multe instrucțiuni if..else, poți folosi instrucțiunea `switch`.

Instrucțiunea `switch` selectează unul dintre multe blocuri de cod care să fie 
executate:

```java
switch(expression) {
  case x:
    // code block
    break;
  case y:
    // code block
    break;
  default:
    // code block
}
```

## Cum funcționează `switch`:

1. Expresia `switch` este evaluată o singură dată.
2. Valoarea expresiei este comparată cu valorile fiecărui `case`.
3. Dacă există o potrivire, blocul de cod asociat este executat.
4. Cuvintele cheie `break` și `default` sunt opționale și vor fi descrise mai târziu în acest capitol.

Exemplul de mai jos folosește numărul zilei săptămânii pentru a calcula numele zilei:

```java
int day = 4;
switch (day) {
  case 1:
    System.out.println("Luni");
    break;
  case 2:
    System.out.println("Marti");
    break;
  case 3:
    System.out.println("Miercuri");
    break;
  case 4:
    System.out.println("Joi");
    break;
  case 5:
    System.out.println("Vineri");
    break;
  case 6:
    System.out.println("Sambata");
    break;
  case 7:
    System.out.println("Duminica");
    break;
}


output:
Joi
```

## Cuvântul cheie `break`

Când Java întâlnește un cuvânt cheie `break`, iese din blocul switch.

Acesta oprește execuția altui cod și testarea cazurilor în interiorul blocului.

Când se găsește o potrivire și lucrarea este terminată, este momentul pentru o pauză. Nu este necesară o testare suplimentară.

Un break poate salva mult timp de execuție, deoarece "ignoră" execuția întregului rest al codului din blocul switch.


## Cuvântul cheie `default`

Cuvântul cheie `default` specifică un cod care să fie executat dacă nu există o potrivire de caz:

```java
int day = 4;
switch (day) {
  case 6:
    System.out.println("Astazi este Sambata");
    break;
  case 7:
    System.out.println("Astazi este Duminica");
    break;
  default:
    System.out.println("Abia astept sa vina weekend-ul");
}

output:
Abia astept sa vina weekend-ul
```

Reține că, dacă instrucțiunea `default` este folosită ca ultima instrucțiune într-un bloc switch, nu este necesar un `break`.




