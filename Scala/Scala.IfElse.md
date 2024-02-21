# If Else statement in Scala

## if Statement
Instrucțiunea if constă dintr-o expresie booleană urmată de una sau mai multe instrucțiuni.

```scala
if(Boolean_expression) {
   // Statements will execute if the Boolean expression is true
}
```
Dacă expresia booleană se evaluează la true, atunci blocul de cod din interiorul expresiei `if` va fi executat. Dacă nu, va fi executat primul set de cod după sfârșitul expresiei `if` (după acolada de închidere).

Încercați următorul exemplu de program pentru a înțelege expresiile condiționate (dacă sunt expresii) în limbajul de programare Scala.

```scala
object Demo {
   def main(args: Array[String]) {
      var x = 10;

      if( x < 20 ){
         println("This is if statement");
      }
   }
}

output:
This is if statement
```

## If-else statement
O instrucțiune `„if”` poate fi urmată de o instrucțiune opțională `else`, care se execută atunci când expresia booleană este falsă.

Sintaxa

```scala
if(Boolean_expression){
   //Executes when the Boolean expression is true
} else{
   //Executes when the Boolean expression is false
}
```

```scala
object Demo {
   def main(args: Array[String]) {
      var x = 30;

      if( x < 20 ){
         println("This is if statement");
      } else {
         println("This is else statement");
      }
   }
}

output:
This is else statement
```

## If-else-if-else Statement
O instrucțiune `„if”` poate fi urmată de o instrucțiune opțională „`else if...else`”, care este foarte utilă pentru a testa diferite condiții folosind o singură instrucțiune ``if...else if`.

Când folosiți declarațiile if , else if , else, există câteva puncte de reținut.

- Un `if` poate avea zero sau unul altcineva și trebuie să vină după orice alt dacă.

- Un `if` poate avea de la zero la multe altele și trebuie să vină înaintea celorlalte.

- Odată ce un else if reușește, niciunul dintre el rămase alt if sau else nu va fi testat.

Următoarea este sintaxa unui if...else if...else” este după cum urmează −

Sintaxa

```scala
if(Boolean_expression 1){
   //Executes when the Boolean expression 1 is true
} else if(Boolean_expression 2){
   //Executes when the Boolean expression 2 is true
} else if(Boolean_expression 3){
   //Executes when the Boolean expression 3 is true
} else {
   //Executes when the none of the above condition is true.
}
```

```scala
object Demo {
   def main(args: Array[String]) {
      var x = 30;

      if( x == 10 ){
         println("Value of X is 10");
      } else if( x == 20 ){
         println("Value of X is 20");
      } else if( x == 30 ){
         println("Value of X is 30");
      } else{
         println("This is else statement");
      }
   }
}

output:
Value of X is 30
```

## Nested if-else Statement

Este întotdeauna legal să imbricați instrucțiuni `if-else`, ceea ce înseamnă că puteți utiliza o declarație `if` sau `else-if` în interiorul altei instrucțiuni `if` sau `else-if`.

Sintaxa:
```scala
if(Boolean_expression 1){
   //Executes when the Boolean expression 1 is true
   
   if(Boolean_expression 2){
      //Executes when the Boolean expression 2 is true
   }
}
```

```scala
object Demo {
   def main(args: Array[String]) {
      var x = 30;
      var y = 10;
      
      if( x == 30 ){
         if( y == 10 ){
            println("X = 30 and Y = 10");
         }
      }
   }
}

Output:
X = 30 and Y = 10
```