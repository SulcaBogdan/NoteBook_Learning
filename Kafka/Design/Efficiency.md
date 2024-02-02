# Eficiența

Am depus eforturi semnificative pentru eficiență. Unul dintre principalele noastre cazuri de utilizare este manipularea datelor de activitate web, care este foarte voluminoasă: fiecare vizualizare de pagină poate genera zeci de scrieri. În plus, presupunem că fiecare mesaj publicat este citit de cel puțin un consumator (adesea mulți), prin urmare, ne străduim să facem consumul cât mai ieftin posibil.

Am constatat, de asemenea, din experiența construirii și operării a unui număr de sisteme similare, că eficiența este cheia pentru operațiuni eficiente multi-tenant. Dacă serviciul de infrastructură din downstream poate deveni ușor un bottleneck din cauza unei mici creșteri a utilizării de către aplicație, astfel de modificări mici vor crea adesea probleme. Prin faptul că suntem foarte rapizi, contribuim la asigurarea faptului că aplicația va cădea sub sarcină înaintea infrastructurii. Acest lucru este deosebit de important atunci când încercăm să rulăm un serviciu centralizat care susține zeci sau sute de aplicații pe un cluster centralizat, deoarece schimbările în modelele de utilizare sunt o apariție aproape zilnică.

Am discutat despre eficiența discului în secțiunea anterioară. Odată ce modelele proaste de acces la disc au fost eliminate, există două cauze comune de ineficiență în acest tip de sistem: prea multe operațiuni I/O mici și copiere excesivă de octeți.

Problema I/O mică apare atât între client și server, cât și în operațiunile persistente ale serverului.

Pentru a evita acest lucru, protocolul nostru este construit în jurul unei abstracții "set de mesaje" care grupază natural mesajele împreună. Acest lucru permite cererilor de rețea să grupeze mesajele și să amortizeze costul întoarcerii rețelei în loc să trimită un singur mesaj o dată. Serverul, la rândul său, adaugă bucăți de mesaje în jurnalul său o dată, iar consumatorul preia bucăți mari și lineare o dată.

Această optimizare simplă produce o accelerare de ordinul mărimii. Lotarea duce la pachete de rețea mai mari, operațiuni de disc mai mari secvențiale, blocuri de memorie continue, etc., toate acestea permit lui Kafka să transforme un flux exploziv de scrieri aleatoare de mesaje în scrieri lineare care curg către consumatori.

Cealaltă ineficiență este în copierea de octeți. La rate scăzute de mesaje, aceasta nu este o problemă, dar sub sarcină impactul este semnificativ. Pentru a evita acest lucru, folosim un format standardizat de mesaje binare care este partajat de producător, broker și consumator (astfel încât blocurile de date pot fi transferate fără modificare între ele).

Jurnalul de mesaje menținut de broker este în sine doar un director de fișiere, fiecare populat de o secvență de seturi de mesaje care au fost scrise pe disc în același format utilizat de producător și consumator. Menținerea acestui format comun permite optimizarea celei mai importante operațiuni: transferul de rețea al bucăților de jurnal persistente. Sistemele de operare Unix moderne oferă o cale de cod foarte optimizată pentru transferul datelor din pagecache către un socket; în Linux, acest lucru se face cu apelul de sistem sendfile.

Pentru a înțelege impactul sendfile, este important să înțelegem calea comună a datelor pentru transferul de date de la fișier la socket:

1. Sistemul de operare citește datele de pe disc în pagecache în spațiul kernel
2. Aplicația citește datele din spațiul kernel într-un buffer de spațiu utilizator
3. Aplicația scrie datele înapoi în spațiul kernel într-un buffer de socket
4. Sistemul de operare copiază datele din bufferul de socket în bufferul NIC de unde sunt trimise prin rețea

Acest lucru este clar ineficient, există patru copii și două apeluri de sistem. Utilizând sendfile, această re-copiere este evitată, permițând sistemului de operare să trimită datele direct de la pagecache la rețea. Prin urmare, în această cale optimizată, este nevoie doar de copierea finală în bufferul NIC.

Ne așteptăm ca un caz de utilizare obișnuit să fie mai mulți consumatori pe un subiect. Utilizând optimizarea de copiere fără copie de mai sus, datele sunt copiate în pagecache exact o dată și sunt reutilizate la fiecare consum, în loc să fie stocate în memorie și copiate în spațiul utilizator de fiecare dată când sunt citite. Acest lucru permite mesajelor să fie consumate la o rată care se apropie de limita conexiunii de rețea.

Această combinație de pagecache și sendfile înseamnă că pe un cluster Kafka unde consumatorii sunt în mare parte la zi, nu veți vedea nicio activitate de citire pe discuri deloc, deoarece vor servi datele în întregime din cache.

Bibliotecile TLS/SSL operează în spațiul utilizator (în prezent, SSL_sendfile nu este acceptat de Kafka). Datorită acestei restricții, sendfile nu este utilizat atunci când este activat SSL. Pentru configurarea SSL, consultați security.protocol și security.inter.broker.protocol.

Pentru mai multe informații de fond despre suportul sendfile și zero-copy în Java, consultați acest articol.

### Compresie batch end-to-end
În unele cazuri, bottleneck-ul este de fapt lățimea de bandă a rețelei, nu CPU sau disc. Acest lucru este valabil în special pentru o conductă de date care trebuie să trimită mesaje între centrele de date pe o rețea întinsă. Desigur, utilizatorul poate comprima întotdeauna mesajele sale unul câte unul fără nicio asistență necesară de la Kafka, dar acest lucru poate duce la rate foarte slabe de compresie, deoarece mult din redundanță se datorează repetării între mesaje de același tip (de exemplu, nume de câmp în JSON sau agenți de utilizator în jurnalele web sau valori comune de șir). Compresia eficientă necesită comprimarea a mai multor mesaje împreună în loc să comprime fiecare mesaj individual.

Kafka suportă acest lucru cu un format eficient de lot. Un lot de mesaje poate fi grupat, comprimat și trimis la server în această formă. Acest lot de mesaje va fi scris în formă comprimată și va rămâne comprimat în jurnal și va fi decomprimat doar de consumator.

Kafka suportă protocoalele de compresie GZIP, Snappy, LZ4 și ZStandard. Mai multe detalii despre compresie pot fi găsite aici.
