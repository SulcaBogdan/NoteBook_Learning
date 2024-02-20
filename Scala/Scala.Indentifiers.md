# Indentificatorii in Scala

Toate componentele Scala necesită nume. Numele folosite pentru obiecte, clase, variabile și metode sunt numite identificatori. Un cuvânt cheie nu poate fi utilizat ca identificator, iar identificatorii sunt sensibile la majuscule. Scala acceptă patru tipuri de identificatori.


## Identificatori alfanumeric
Un identificator alfanumeric începe cu o literă sau o liniuță de subliniere, care poate fi urmată de alte litere, cifre sau liniuțe de subliniere. Caracterul `„$”` este un cuvânt cheie rezervat în Scala și nu trebuie utilizat în identificatori.

Următoarele sunt `identificatorii alfanumerici legali` −

```
age, salary, _value,  __1_value
```
Următoarele sunt `identificatori ilegali` −

```
$salary, 123abc, -salary
```

## Identificatori de operator
Un identificator de operator este format din unul sau mai multe caractere operator. Caracterele operator sunt caractere `ASCII` imprimabile, cum ar fi `+`, `:`, `?`, `~` sau`#`.

Următoarele sunt `identificatorii de operator legal` −

```
+ ++ ::: <?> :>
```
Compilatorul Scala va „deforma” în interior identificatorii operatorilor pentru a le transforma în identificatori Java legali cu caractere $ încorporate. De exemplu, identificatorul :-> ar fi reprezentat intern ca $colon$minus$mai mare.

## Identificatori mixti
Un identificator mixt constă dintr-un identificator alfanumeric, care este urmat de un caracter de subliniere și un identificator de operator.

Următoarele sunt `identificatorii mixți legali` −

```
unary_+,  myvar_=
```

Aici, `unary_+` folosit ca nume de metodă definește un operator `unary +` și `myvar_=` folosit ca nume de metodă definește un operator de atribuire (operator overloading).

## Identificatori literali
Un identificator literal este un șir arbitrar cuprins în bifături din spate (` . . . `).

Următoarele sunt `identificatorii literali legali` −

```
`x` `<clinit>` `yield`
```


