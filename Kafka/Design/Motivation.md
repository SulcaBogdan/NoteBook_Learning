# Descrierea Platformei Kafka

Am proiectat Kafka pentru a acționa ca o platformă unificată pentru gestionarea tuturor fluxurilor de date în timp real pe care o companie mare le-ar putea avea. Pentru a realiza acest lucru, a trebuit să luăm în considerare o gamă destul de largă de scenarii de utilizare.

- **Throughput Ridicat:** Trebuia să aibă un throughput ridicat pentru a susține fluxuri de evenimente cu un volum mare, cum ar fi agregarea în timp real a jurnalelor.

- **Tratarea a Backlog-urilor Mari:** Trebuia să facă față cu grație backlog-urilor mari de date pentru a susține încărcări periodice de date din sisteme offline.

- **Livrare cu low latency:** Acest lucru însemna că sistemul trebuia să gestioneze livrarea cu latență redusă pentru a gestiona cazurile de utilizare mai tradiționale ale mesageriei.

- **Suport pentru Procesarea În Timp Real Partiționată și Distribuită:** Dorim să susținem procesarea în timp real, distribuită și partajată a acestor fluxuri pentru a crea fluxuri noi, derivate. Acest lucru a motivat modelul nostru de partizionare și consumator.

- **Garantarea Toleranței la Defecțiuni:** În cazurile în care fluxul este alimentat în alte sisteme de date pentru servire, știam că sistemul trebuia să poată garanta toleranța la defecțiuni în prezența eșecurilor de mașină.

Susținerea acestor utilizări ne-a condus la un design cu mai multe elemente unice, mai asemănătoare cu un jurnal de bază al unei baze de date decât cu un sistem de mesagerie tradițional.

