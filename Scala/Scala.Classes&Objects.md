# Clasele si Obiectele in Scala

Acest capitol vă prezintă cum să utilizați clasele și obiectele în programarea Scala. O clasă este un plan pentru obiecte. Odată ce definiți o clasă, puteți crea obiecte din planul clasei cu cuvântul cheie `new`. Prin obiect puteți utiliza toate funcționalitățile clasei definite.

Următoarea diagramă demonstrează clasa și obiectul luând un exemplu de elev al clasei, care conține variabilele membre (`name` și `roll no`) și metodele membre (`setName()` și `setRollNo()`). În cele din urmă, toți sunt membri ai clasei. Clasa este o amprentă și obiectele sunt reale aici. În diagrama următoare, `Student` este o clasă, iar `Harini`, `John` și `Maria` sunt obiectele clasei Student, acestea având nume și număr de rol.

![imagine](https://www.tutorialspoint.com/scala/images/scala_classes_objects.jpg)

Urmează o sintaxă simplă pentru a defini o clasă de bază în Scala. Această clasă definește două variabile `x` și `y` și o metodă: `move`, care nu returnează o valoare. Variabilele de clasă sunt numite, câmpurile clasei și metodele sunt numite metode de clasă.

Numele clasei funcționează ca un constructor de clasă care poate prelua o serie de parametri. Codul de mai sus definește două argumente de constructor, `xc` și `yc`; ambele sunt vizibile în tot corpul clasei.

```scala
class Point(xc: Int, yc: Int) {
   var x: Int = xc
   var y: Int = yc

   def move(dx: Int, dy: Int) {
      x = x + dx
      y = y + dy
      println ("Point x location : " + x);
      println ("Point y location : " + y);
   }
}
```

După cum sa menționat mai devreme în acest capitol, puteți crea obiecte folosind un cuvânt cheie `new` și apoi puteți accesa câmpurile și metodele de clasă, așa cum se arată mai jos în exemplu -

```scala
import java.io._

class Point(val xc: Int, val yc: Int) {
   var x: Int = xc
   var y: Int = yc
   
   def move(dx: Int, dy: Int) {
      x = x + dx
      y = y + dy
      println ("Point x location : " + x);
      println ("Point y location : " + y);
   }
}

object Demo {
   def main(args: Array[String]) {
      val pt = new Point(10, 20);

      // Move to a new location
      pt.move(10, 10);
   }
}

output:
Point x location : 20
Point y location : 30
```

## Extending a Class
Puteți extinde o clasă Scala de bază și puteți proiecta o clasă moștenită în același mod în care o faceți în Java (utilizați cuvântul cheie extins), dar există două restricții: suprascrierea metodei necesită cuvântul cheie de suprascriere și numai constructorul primar poate trece parametri la constructorul de bază. Să extindem clasa noastră de mai sus și să adăugăm încă o metodă de clasă.

### Exemplu
Să luăm un exemplu de două clase Clasă punct (ca același exemplu ca mai sus) și Clasa locație este o clasă moștenită folosind cuvântul cheie extins. O astfel de clauză „extinde” are două efecte: face ca clasa Locație să moștenească toți membrii non-privati din clasa Point și face ca tipul Locație să fie un subtip al clasei de tip Point. Deci aici clasa Point se numește superclasă, iar clasa Locație se numește subclasă. Extinderea unei clase și moștenirea tuturor caracteristicilor unei clase părinte se numește moștenire, dar Scala permite moștenirea doar de la o singură clasă.

Notă − **Metodele move() din clasa Point și metoda move() din clasa Location nu suprascrie definițiile corespunzătoare pentru mutare, deoarece acestea sunt definiții diferite (de exemplu, prima ia două argumente, în timp ce a doua are trei argumente).**

Încercați următorul exemplu de program pentru a implementa moștenirea.

```scala
import java.io._

class Point(val xc: Int, val yc: Int) {
   var x: Int = xc
   var y: Int = yc
   
   def move(dx: Int, dy: Int) {
      x = x + dx
      y = y + dy
      println ("Point x location : " + x);
      println ("Point y location : " + y);
   }
}

class Location(override val xc: Int, override val yc: Int,
   val zc :Int) extends Point(xc, yc){
   var z: Int = zc

   def move(dx: Int, dy: Int, dz: Int) {
      x = x + dx
      y = y + dy
      z = z + dz
      println ("Point x location : " + x);
      println ("Point y location : " + y);
      println ("Point z location : " + z);
   }
}

object Demo {
   def main(args: Array[String]) {
      val loc = new Location(10, 20, 15);

      // Move to a new location
      loc.move(10, 10, 5);
   }
}

output:
Point x location : 20
Point y location : 30
Point z location : 20
```

## Implicit Classes
Clasele implicite permit conversații implicite cu constructorul principal al clasei atunci când clasa este în domeniu. Clasa implicită este o clasă marcată cu cuvântul cheie `„implicit”`. Această caracteristică este introdusă în Scala 2.10.

Sintaxă - Următoarea este sintaxa pentru clasele implicite. Aici clasa implicită se află întotdeauna în domeniul obiectului în care toate definițiile metodelor sunt permise, deoarece clasa implicită nu poate fi o clasă de nivel superior.

```scala
object <object name> {
   implicit class <class name>(<Variable>: Data type) {
      def <method>(): Unit =
   }
}
```

Să luăm un exemplu de clasă implicită numită `IntTimes` cu metoda `times()`. Înseamnă că ori `()` conține o tranzacție în buclă care va executa instrucțiunea dată în numărul de ori pe care îl oferim. Să presupunem că instrucțiunea dată este „de 4 ori println (“Bună ziua”)” înseamnă că instrucțiunea println (“„Bună ziua”) se va executa de 4 ori.

Următorul este programul pentru exemplul dat. În acest exemplu sunt folosite două clase de obiecte (Run și Demo), astfel încât trebuie să salvăm acele două clase în fișiere diferite cu numele lor, după cum urmează.

Run.scala − Salvați următorul program în Run.scala.

```scala
object Run {
   implicit class IntTimes(x: Int) {
      def times [A](f: =>A): Unit = {
         def loop(current: Int): Unit =
         
         if(current > 0){
            f
            loop(current - 1)
         }
         loop(x)
      }
   }
}
```

```scala
import Run._

object Demo {
   def main(args: Array[String]) {
      4 times println("hello")
   }
}
```

```
OUTPUT:
Hello
Hello
Hello
Hello
```

Notă −

- Clasele implicite trebuie definite în interiorul unei alte clase/obiect/trăsătură (nu la nivelul superior).

- Clasele implicite pot lua un singur argument non-implicit în constructorul lor.

- Clasele implicite nu pot fi orice metodă, membru sau obiect în domeniu cu același nume ca și clasa implicită.


## Obiecte Singleton
Scala este mai orientat pe obiecte decât Java, deoarece în Scala, nu putem avea membri statici. În schimb, Scala are obiecte `singleton`. Un `singleton` este o clasă care poate avea o singură instanță, adică `Object`. Creați `singleton` folosind cuvânt cheie `object` în loc de cuvântul cheie de `class`. Deoarece nu puteți instanția un obiect singleton, nu puteți transmite parametri constructorului primar. Ați văzut deja toate exemplele folosind obiecte singleton unde ați numit metoda principală a lui Scala.

Urmează același exemplu de program pentru implementarea singleton.

```scala
import java.io._

class Point(val xc: Int, val yc: Int) {
   var x: Int = xc
   var y: Int = yc
   
   def move(dx: Int, dy: Int) {
      x = x + dx
      y = y + dy
   }
}

object Demo {
   def main(args: Array[String]) {
      val point = new Point(10, 20)
      printPoint

      def printPoint{
         println ("Point x location : " + point.x);
         println ("Point y location : " + point.y);
      }
   }
}

output:
Point x location : 10
Point y location : 20
```