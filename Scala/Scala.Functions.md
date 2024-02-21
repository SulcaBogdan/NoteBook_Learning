# Functiile in Scala

O funcție este un grup de instrucțiuni care îndeplinesc o sarcină. Puteți împărți codul în funcții separate. Modul în care împărțiți codul între diferite funcții depinde de dvs., dar logic, împărțirea este de obicei astfel încât fiecare funcție să îndeplinească o anumită sarcină.

Scala are atât `funcții`, cât și `metode` și folosim termenii metodă și funcție interschimbabil, cu o diferență minoră. O metodă Scala este o parte a unei clase care are un nume, o semnătură, opțional niște `adnotări` și niște `bytecode`, unde ca funcție în Scala este un obiect complet care poate fi atribuit unei variabile. Cu alte cuvinte, o funcție, care este definită ca membru al unui obiect, se numește metodă.

O definiție de funcție poate apărea oriunde într-un fișier sursă și Scala permite definiții de funcții imbricate, adică definiții de funcție în interiorul altor definiții de funcție. Cel mai important punct de reținut este că numele funcției Scala poate avea caractere precum +, ++, ~, &,-, --, \, /, : etc.

## Declararea unei functi

Sintaxa

```scala
def functionName ([list of parameters]) : [return type]
```

**Metodele sunt implicit declarate abstracte dacă nu folosiți semnul egal și corpul metodei.**

## Definirea unuei functi

```scala
def functionName ([list of parameters]) : [return type] = {
   function body
   return [expr]
}
```

Aici, tipul de returnare ar putea fi orice tip de date Scala valid, iar lista de parametri va fi o listă de variabile separate prin virgulă, iar lista de parametri și tipul de returnare sunt opționale. Foarte similar cu Java, o instrucțiune return poate fi folosită împreună cu o expresie în cazul în care funcția returnează o valoare. Urmează funcția care va adăuga două numere întregi și va returna suma lor −

Sintaxa:

```scala
object add {
   def addInt( a:Int, b:Int ) : Int = {
      var sum:Int = 0
      sum = a + b
      return sum
   }
}
```

O funcție care nu returnează nimic poate returna o unitate care este echivalentă cu void în Java și indică faptul că funcția nu returnează nimic. Funcțiile care nu returnează nimic în Scala, se numesc `proceduri`(procedures).


Sintaxa

```scala
object Hello{
   def printMe( ) : Unit = {
      println("Hello, Scala!")
   }
}
```

## Apelarea functiilor

Scala oferă o serie de variații sintactice pentru invocarea metodelor. Urmează modul standard de a apela o metodă −

```scala
functionName( list of parameters )
```

Dacă o funcție este apelată folosind o instanță a obiectului, atunci am folosi notația punct similară cu Java, după cum urmează -

```scala
[instance.]functionName( list of parameters )
```

Exemplu:

```scala
object Demo {
   def main(args: Array[String]) {
      println( "Returned Value : " + addInt(5,7) );
   }
   
   def addInt( a:Int, b:Int ) : Int = {
      var sum:Int = 0
      sum = a + b

      return sum
   }
}

output:
Returned Value : 12
```

Funcțiile Scala sunt inima programării Scala și de aceea Scala este considerat un limbaj de programare funcțional. Următoarele sunt câteva concepte importante legate de funcțiile Scala, care ar trebui să fie înțelese de un programator Scala.