# Variables in Scala

Variabilele nu sunt altceva decât locații de memorie rezervate pentru a stoca valori. Aceasta înseamnă că atunci când creați o variabilă, vă rezervați ceva spațiu în memorie.

Pe baza tipului de date al unei variabile, compilatorul alocă memorie și decide ce poate fi stocat în memoria rezervată. Prin urmare, atribuind diferite tipuri de date variabilelor, puteți stoca numere întregi, zecimale sau caractere în aceste variabile.

## Declarație variabilă
Scala are o sintaxă diferită pentru declararea variabilelor. Ele pot fi definite ca valoare, adică constantă sau variabilă. Aici, `myVar` este declarată folosind cuvântul cheie `var`. Este o variabilă care poate schimba valoarea și aceasta se numește `variabilă mutabilă`. Mai jos este sintaxa pentru a defini o variabilă folosind cuvântul cheie `var` −

```scala
var myVar : String = "Foo"
```

Aici, `myVal` este declarat folosind cuvântul cheie `val`. Aceasta înseamnă că este o variabilă care nu poate fi modificată și aceasta se numește `variabilă imuabilă`. Mai jos este sintaxa pentru a defini o variabilă folosind cuvântul cheie `val` −

```scala
val myVal : String = "Foo"
```

# Variable Data Types
Tipul unei variabile este specificat după numele variabilei și înainte de semnul `egal`. Puteți defini orice tip de variabilă Scala menționând tipul său de date după cum urmează -

```scala
val or val VariableName : DataType = [Initial Value]
```

Dacă nu atribuiți nicio valoare inițială unei variabile, atunci aceasta este valabilă după cum urmează −

```scala
var myVar :Int;
val myVal :String;
```

## Variable Type Inference
Când atribuiți o valoare inițială unei variabile, compilatorul Scala își poate da seama tipul variabilei pe baza valorii atribuite acesteia. Aceasta se numește inferență de tip variabil. Prin urmare, puteți scrie aceste declarații de variabile astfel −

```scala
var myVar = 10;
val myVal = "Hello, Scala!";
```

Aici, în mod implicit, `myVar` va fi de tip `Int` și `myVal` va deveni variabilă de tip `String`.

## Multiple assignments
Scala acceptă mai multe sarcini. Dacă un bloc de cod sau o metodă returnează un tuplu (Tuple - Deține o colecție de obiecte de diferite tipuri), tuplu-ul poate fi atribuit unei variabile `val`. [Notă − Vom studia tuplurile în capitolele următoare.]

```scala
val (myVar1: Int, myVar2: String) = Pair(40, "Foo")
```
Și inferența de tip face bine −

```scala
val (myVar1, myVar2) = Pair(40, "Foo")
```

## Exemplu de program
Următorul este un exemplu de program care explică procesul de declarare a variabilelor în Scala. Acest program declară patru variabile - două variabile sunt definite cu declarație de tip și celelalte două sunt fără declarație de tip

```scala
object Demo {
   def main(args: Array[String]) {
      var myVar :Int = 10;
      val myVal :String = "Hello Scala with datatype declaration.";
      var myVar1 = 20;
      val myVal1 = "Hello Scala new without datatype declaration.";
      
      println(myVar); println(myVal); println(myVar1); 
      println(myVal1);
   }
}

output:
10
Hello Scala with datatype declaration.
20
Hello Scala without datatype declaration.
```
## Variable Scope
Variabilele din Scala pot avea trei domenii diferite, în funcție de locul în care sunt utilizate. Ele pot exista ca câmpuri, ca parametri de metodă și ca variabile locale. Mai jos sunt detalii despre fiecare tip de domeniu.

## Fields
Câmpurile sunt variabile care aparțin unui obiect. Câmpurile sunt accesibile din interiorul fiecărei metode din obiect. Câmpurile pot fi accesibile și în afara obiectului, în funcție de modificatorii de acces cu care este declarat câmpul. Câmpurile obiect pot fi atât de tipuri mutabile, cât și imuabile și pot fi definite folosind fie `var`, fie `val`.

## Method Parameters
Parametrii metodei sunt variabile, care sunt folosite pentru a trece valoarea în interiorul unei metode, atunci când metoda este apelată. Parametrii metodei sunt accesibili numai din interiorul metodei, dar obiectele trecute pot fi accesibile din exterior, dacă aveți o referință la obiect din afara metodei. Parametrii metodei sunt întotdeauna imutabili, care sunt definiți prin cuvântul cheie `val`.

## Local Variables
Variabilele locale sunt variabile declarate în interiorul unei metode. Variabilele locale sunt accesibile numai din interiorul metodei, dar obiectele pe care le creați pot scăpa de metodă dacă le returnați din metodă. Variabilele locale pot fi atât tipuri mutabile, cât și imuabile și pot fi definite folosind fie `var`, fie `val`.

