# Containerele Docker

Un **container** este o instanță care poate fi rulată a unei imagini. Puteți crea, porni, opri, muta sau șterge un **container** folosind API-ul sau CLI-ul Docker. Puteți conecta un **container** la una sau mai multe rețele, atașa stocare la el sau chiar crea o imagine nouă pe baza stării sale curente.

În mod implicit, un **container** este relativ bine izolat față de alte containere și față de mașina gazdă. Puteți controla cât de izolată este rețeaua, stocarea sau alte subsisteme subiacente ale unui container față de alte containere sau față de mașina gazdă.

Un container este definit de imaginea sa, precum și de orice opțiuni de configurare pe care le furnizați atunci când îl creați sau îl porniți. Atunci când un container este șters, orice modificări la starea sa care nu sunt stocate în stocare persistentă dispar.

## Exemplu comandă docker run
Următoarea comandă rulează un container `ubuntu`, se atașează interactiv la sesiunea locală a liniei de comandă și rulează `/bin/bash`.

```bash
docker run -i -t ubuntu /bin/bash
```

Când rulați această comandă, următoarele se întâmplă (presupunând că utilizați configurația implicită a registrului):

1. Dacă nu aveți imaginea ubuntu local, **Docker** o descarcă din registru-ul configurat, la fel ca și cum ați fi rulat manual `docker pull ubuntu`.
2. Docker creează un container nou, la fel ca și cum ați fi rulat manual o comandă `docker container create`.
3. Docker alocă un sistem de fișiere cu scriere-citire containerului, ca ultim strat. Acest lucru permite unui container în execuție să creeze sau să modifice fișiere și directoare în sistemul său de fișiere local.
4. Docker creează o interfață de rețea pentru a conecta containerul la rețeaua implicită, deoarece nu ați specificat opțiuni de rețea. Acest lucru include asignarea unei adrese IP containerului. În mod implicit, containerele pot să se conecteze la rețele externe folosind conexiunea la rețeaua mașinii gazdă.
5. Docker pornește containerul și execută `/bin/bash`. Deoarece containerul rulează interactiv și este atașat la terminalul dvs. (datorită flag-urilor `-i` și `-t`), puteți furniza intrare folosind tastatura, în timp ce Docker înregistrează ieșirea în terminalul dvs.
6. Când rulați `exit` pentru a încheia comanda /bin/bash, containerul se oprește, dar nu este șters. Puteți să-l porniți din nou sau să-l ștergeți.