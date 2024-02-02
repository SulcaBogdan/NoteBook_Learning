# Producătorul

## Load Balancing

Producătorul Kafka trimite date direct către broker-ul care este lider pentru partaj, fără a avea un nivel intermediar de rutare. Pentru a ajuta producătorul în acest proces, toate nodurile Kafka pot răspunde la cereri de metadate, furnizând informații despre serverele care sunt în prezent active și locația liderilor pentru partajele unui topic. Acest lucru permite producătorului să-și direcționeze eficient cererile.

Clientul are control asupra partajului către care publică mesajele. Acest lucru poate fi realizat aleatoriu, implementând o formă de balansare aleatoare a încărcăturii, sau poate fi realizat printr-o funcție de partajare semantică. Kafka expune interfața pentru partajarea semantică prin permiterea utilizatorilor să specifice o cheie pentru partajare și să utilizeze aceasta pentru a realiza o funcție de hash către un partaj (există și opțiunea de a înlocui funcția de partajare dacă este necesar). De exemplu, dacă cheia aleasă este un ID de utilizator, toate datele pentru un anumit utilizator vor fi trimise la același partaj. Această abordare permite consumatorilor să facă presupuneri despre localitatea consumului lor. Partajarea semantică este concepută în mod explicit pentru a facilita procesarea sensibilă la localitate în consumatori.

#### Trimitere Asincronă

Batching-ul este un factor semnificativ de eficiență în Kafka, iar pentru a permite batching-ul, producătorul Kafka încearcă să acumuleze date în memorie și să trimită loturi mai mari într-o singură cerere. Procesul de batching poate fi configurat să acumuleze nu mai mult de un număr fix de mesaje și să aștepte nu mai mult de o limită de latență specificată (de exemplu, 64k sau 10 ms). Această configurare permite acumularea a mai multe octeți pentru a fi trimiși în mai puține operațiuni I/O pe servere. Mecanismul de buffering este configurabil, oferind o modalitate de a echilibra o cantitate mică de latență suplimentară în schimbul unei throughput mai bune.

