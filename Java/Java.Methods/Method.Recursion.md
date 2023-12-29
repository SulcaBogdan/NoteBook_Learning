# Recursivitatea metodelor

`Recursiunea` este tehnica de a efectua un apel de funcție în sine. Această tehnică oferă o modalitate de a împărți problemele complicate în probleme simple, care sunt mai ușor de rezolvat.

`Recursiunea` poate fi puțin greu de înțeles. Cel mai bun mod de a-ți da seama cum funcționează este să experimentezi cu el.

### Exemplu

Adunarea a două numere este ușor de făcut, dar adăugarea unui interval de numere este mai complicată. În exemplul următor, recursiunea este folosită pentru a adăuga o serie de numere împreună, împărțind-o în sarcina simplă de a adăuga două numere:

```java
public class Main {
  public static void main(String[] args) {
    int result = sum(10);
    System.out.println(result);
  }
  public static int sum(int k) {
    if (k > 0) {
      return k + sum(k - 1);
    } else {
      return 0;
    }
  }
}

output:
55
```

### Explicatie:

Când funcția `sum()` este apelată, adaugă parametrul `k` la suma tuturor numerelor mai mici decât `k` și returnează rezultatul. Când `k` devine `0`, funcția returnează doar `0`. Când rulează, programul urmează acești pași:

`0 + sum(9)`

`10 + ( 9 + sum(8) )`

`10 + ( 9 + ( 8 + sum(7) ) )`

`...`

`10 + 9 + 8 + 7 + 6 + 5 + 4 + 3 + 2 + 1 + sum(0)`

`10 + 9 + 8 + 7 + 6 + 5 + 4 + 3 + 2 + 1 + 0`

Deoarece funcția nu se autoapelează când `k` este `0`, programul se oprește acolo și returnează rezultatul.

## Conditie de oprire

La fel cum buclele se pot confrunta cu problema buclei infinite, funcțiile recursive se pot confrunta cu problema recursiunii infinite. Recursiunea infinită este atunci când funcția nu încetează să se autoapeleze. Fiecare funcție recursivă ar trebui să aibă o condiție de oprire, care este condiția în care funcția încetează să se mai apeleze. În exemplul anterior, condiția de oprire este atunci când parametrul `k` devine `0`.

Este util să vedeți o varietate de exemple diferite pentru a înțelege mai bine conceptul. În acest exemplu, funcția adaugă un interval de numere între un început și un sfârșit. Condiția de oprire pentru această funcție recursivă este atunci când sfârșitul nu este mai mare decât începutul:

```java
public class Main {
  public static void main(String[] args) {
    int result = sum(5, 10);
    System.out.println(result);
  }
  public static int sum(int start, int end) {
    if (end > start) {
      return end + sum(start, end - 1);
    } else {
      return end;
    }
  }
}

output:
45
```

Dezvoltatorul ar trebui să fie foarte atent cu recursiunea, deoarece poate fi destul de ușor să introduci în scrierea unei funcții care nu se termină niciodată, sau una care utilizează cantități în exces de memorie sau puterea procesorului. 

Cu toate acestea, atunci când este scrisă corect recursiunea poate fi o abordare foarte eficientă și elegantă din punct de vedere matematic pentru programare.


