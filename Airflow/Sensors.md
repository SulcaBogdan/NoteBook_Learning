# Sensors in Airflow

## Senzori

Senzorii sunt un tip special de Operatori proiectați să facă exact o singură lucrare - să aștepte ca ceva să se întâmple. Poate fi bazat pe timp, să aștepte un fișier sau un eveniment extern, dar tot ceea ce fac este să aștepte până când ceva se întâmplă, și apoi să reușească astfel încât task-urile lor `downstream` să poată rula.

Deoarece sunt în principal inactivi, Senzorii au două moduri diferite de execuție pentru a fi mai eficienți în utilizarea lor:

- **poke (implicit):** Senzorul ocupă un slot de worker pentru întreaga sa durată de execuție.

- **reschedule:** Senzorul ocupă un slot de worker doar atunci când verifică și doarme pentru o durată setată între verificări.

Modurile `poke` și `reschedule` pot fi configurate direct atunci când instanțiezi senzorul; în general, compromisul dintre ele este latenta. Ceva ce verifică în fiecare secundă ar trebui să fie în modul `poke`, în timp ce ceva care verifică în fiecare minut ar trebui să fie în modul `reschedule`.

La fel ca Operatorii, Airflow dispune de un set mare de Senzori pre-construiți pe care îi poți utiliza, atât în modul de bază Airflow, cât și prin intermediul sistemului nostru de furnizori.
