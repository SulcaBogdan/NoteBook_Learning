# Data types in Scala

`Scala` are aceleași tipuri de date ca și `Java`, cu aceeași amprentă de memorie și precizie. Mai jos este tabelul care oferă detalii despre toate tipurile de date disponibile în Scala −

| Tip     | Descriere                                                   |
|---------|-------------------------------------------------------------|
| `Byte`    | Valoare semnată de 8 biți. Interval de la -128 la 127       |
| `Short`   | Valoare semnată de 16 biți. Interval de la -32768 la 32767  |
| `Int`     | Valoare semnată de 32 biți. Interval de la -2147483648 la 2147483647 |
| `Long`    | Valoare semnată de 64 biți. De la -9223372036854775808 la 9223372036854775807 |
| `Float`   | Float de precizie simplă de 32 biți conform IEEE 754        |
| `Double`  | Float de precizie dublă de 64 biți conform IEEE 754         |
| `Char`    | Caracter Unicode fără semn de 16 biți. Interval de la U+0000 la U+FFFF |
| `String`  | O secvență de caractere Char                                |
| `Boolean` | Fie literalul true, fie literalul false                     |
| `Unit`    | Corespunde lipsei de valoare                                |
| `Null`    | Referință null sau goală                                    |
| `Nothing` | Subtipul oricărui alt tip; nu include valori                |
| `Any`     | Supertipul oricărui tip; orice obiect este de tip Any       |
| `AnyRef`  | Supertipul oricărui tip de referință                        |


**Toate tipurile de date enumerate mai sus sunt obiecte. Nu există tipuri primitive ca în Java. Aceasta înseamnă că puteți apela metode pe un Int, Long etc.**

## Scala Basic Literals
Regulile pe care Scala le folosește pentru `literale` sunt simple și intuitive. Această secțiune explică toate Literalele Scala de bază.

## Literale integrale
Literale întregi sunt de obicei de tip Int sau de tip Long când sunt urmate de un sufix L sau l. Iată câteva literale întregi −

```
0
035
21 
0xFFFFFFFF 
0777L
```

## Floating Point Literal
Literale cu virgulă mobilă sunt de tip Float atunci când sunt urmate de un sufix de tip virgulă mobilă F sau f și sunt de tip Double în caz contrar. Iată câteva literale în virgulă mobilă −

```
0.0 
1e30f 
3.14159f 
1.0e100
.1
```

## Boolean Literals
Literale booleen `true` și `false` sunt membri de tip boolean.

## Symbol Literals
Un simbol literal 'x este o prescurtare pentru expresia `scala.Symbol`("x"). Simbolul este o clasă de caz, care este definită după cum urmează.

```scala
package scala
final case class Symbol private (name: String) {
   override def toString: String = "'" + name
}
```


## Character Literals
Un caracter literal este un singur caracter cuprins între ghilimele. Caracterul este fie un caracter Unicode imprimabil, fie este descris printr-o secvență de escape. Iată câteva caractere literale −

```
'a' 
'\u0041'
'\n'
'\t'
```

## String Literals

Un string literal este o secvență de caractere între ghilimele duble. Caracterele sunt fie caractere Unicode imprimabile, fie sunt descrise prin secvențe de escape. Iată câteva literale string −

```scala
"Hello,\nWorld!"
"This string contains a \" character."
```

## Multi-Line Strings

Un multi-Line String este o secvență de caractere cuprinsă între ghilimele triple `„"" ... """.` Secvența de caractere este arbitrară, cu excepția faptului că poate conține trei sau mai multe ghilimele consecutive numai la sfârșit.

Caracterele nu trebuie neapărat să fie imprimabile; liniile noi sau alte caractere de control sunt de asemenea permise. Iată un literal șir cu mai multe linii -

```scala
"""the present string
spans three
lines."""
```

## Null Values

Valoarea nulă este de tip scala.`Null` și este astfel compatibilă cu fiecare tip de referință. Acesta denotă o valoare de referință care se referă la un obiect special „nul”.

Următoarele secvențe de escape sunt recunoscute în `caractere și caractere literale`.

| Escape Sequences | Unicode | Description         |
|------------------|---------|---------------------|
| `\b`               | \u0008  | backspace BS        |
| `\t`               | \u0009  | horizontal tab HT   |
| `\n`               | \u000c  | formfeed FF         |
| `\f`               | \u000c  | formfeed FF         |
| `\r`               | \u000d  | carriage return CR  |
| `\"`               | \u0022  | double quote "      |
| `\'`               | \u0027  | single quote '      |
| `\\`               | \u005c  | backslash \         |


Un caracter cu Unicode între 0 și 255 poate fi reprezentat și printr-un escape octal, adică o bară oblică inversă `„\”` urmată de o secvență de până la trei caractere octale. Următorul este exemplul pentru a afișa câteva caractere de secvență de evadare -

```scala
object Test {
   def main(args: Array[String]) {
      println("Hello\tWorld\n\n" );
   }
} 

output:
Hello  World
```