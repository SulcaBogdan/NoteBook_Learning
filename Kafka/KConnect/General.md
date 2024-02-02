# Informatii generale Kafka

### Ce este event streaming?
Event streaming reprezintă echivalentul digital al sistemului nervos central al corpului uman. Este fundamentul tehnologic pentru lumea "**always-on**", în care afacerile devin din ce în ce mai definite și automate prin software, iar utilizatorul de software devine tot mai mult un element software în sine.

Din punct de vedere tehnic, event streaming este practica capturării datelor în timp real din surse de events precum:
- baze de date
- senzori
- dispozitive mobile 
- servicii cloud 
- aplicații software sub forma unor fluxuri de events
- stocarea durabilă a acestor fluxuri de events pentru a le recupera ulterior; 
- manipularea,  procesarea si reacționarea la fluxurile de events în timp real și retrospectiv
- dirijarea fluxurilor de events către diferite tehnologii destinație, după cum este necesar. 
  
Event streaming-ul asigură astfel un flux și o interpretare continua a datelor, astfel încât informația corectă să fie la locul potrivit, în momentul potrivit. 


### Pentru ce pot folosi event streaming?
Event streaming este aplicată într-o varietate largă de cazuri de utilizare în numeroase industrii și organizații. Multe exemple includ:

1. Procesarea plăților și a tranzacțiilor financiare în timp real, cum ar fi în bursele de valori, bănci și asigurări.
2. Urmărirea și monitorizarea în timp real a mașinilor, camioanelor, flotelor și expedierilor, cum ar fi în logistică și industria auto.
3. Capturarea și analiza continuă a datelor de la senzori provenind de la dispozitive IoT sau alte echipamente, cum ar fi în fabrici și parcuri eoliene.
4. Colectarea și reacționarea imediată la interacțiunile și comenzile clienților, cum ar fi în retail, industria hotelieră și de călătorii, și în aplicațiile mobile.
5. Monitorizarea pacienților în îngrijirea medicală și prezicerea modificărilor de stare pentru a asigura tratamentul la timp în situații de urgență.
6. Conectarea, stocarea și punerea la dispoziție a datelor produse de diferite divizii ale unei companii.
7. Servirea ca fundație pentru platforme de date, arhitecturi bazate pe events și microservicii.


### Apache Kafka® este o platformă de transmitere a evenimentelor. Ce înseamnă asta?

`Kafka` îmbină trei capacități cheie, astfel încât să poți implementa cazurile tale de utilizare pentru transmiterea de events de la început până la sfârșit, cu o singură soluție testată în luptă:

1. Pentru a publica (a scrie) și a se abona (a citi) la fluxuri de events, inclusiv **importul**/**exportul** continuu al datelor tale din alte sisteme.
2. Pentru a stoca fluxuri de events **durabil** și **fiabil**, pentru cât timp dorești.
3. Pentru a procesa fluxuri de events pe măsură ce apar sau retrospectiv.

Și toate aceste funcționalități sunt furnizate într-un mod distribuit, extrem de scalabil, flexibil, tolerante la erori și securizat. Kafka poate fi implementat pe hardware `bare-metal`, `mașini virtuale` și `containere`, atât **on-premises**, cât și în **cloud**. Poți alege între gestionarea autonomă a mediilor Kafka sau utilizarea serviciilor complet gestionate oferite de diverse companii.

### Cum funcționează Kafka?
`Kafka` este un sistem `distribuit` format din `servers` și `clients` care comunică printr-un protocol de rețea `TCP` de înaltă performanță. 

#### `Servers`
 Kafka rulează ca un `cluster` format din una sau mai multe servere, care pot acoperi mai multe centre de date sau regiuni cloud. Unele dintre aceste servere formează stratul de stocare, numit `brokeri`. Alte servere rulează `Kafka Connect` pentru a importa și exporta continuu date sub formă de fluxuri de events, integrând Kafka cu sistemele existente, precum bazele de date relaționale sau alte clustere Kafka. Pentru a permite implementarea cazurilor de utilizare critice, un cluster Kafka este extrem de scalabil și tolerant la erori: dacă unul dintre servere întâmpină probleme, celelalte preiau munca pentru a asigura operarea continuă fără pierdere de date.

#### `Clients`
 Aceștia permit dezvoltarea de aplicații distribuite și microservicii care citesc, scriu și procesează fluxuri de events în paralel, la scară și într-un mod tolerant la erori, chiar și în caz de probleme de rețea sau eșecuri ale mașinilor. Kafka include câțiva astfel de clienți, care sunt completate de zeci de clienți oferiți de comunitatea Kafka: există clienți pentru Java și Scala, inclusiv biblioteca mai avansată Kafka Streams, pentru Go, Python, C/C++ și multe alte limbaje de programare, precum și API-uri REST.

### Principalele Concepte și Terminologie
Un `event` înregistrează faptul că "**ceva s-a întâmplat**" în lume sau în afacerea ta. În documentație, este numit și `record` sau `message`. Atunci când citești sau scrii date în Kafka, o faci sub forma de `events`. Conceptual, un `event` are un **key**, **value**, **timestamp** și opțional, **metadata headers**. Iată un exemplu de eveniment:

- Event key: "Alice"
- Event value: "A făcut o plată de 200 de dolari către Bob"
- Event timestamp: "25 iunie 2020, la ora 14:06"
- metadata headers (opționale)

`Producers` sunt aplicațiile client care publică (scriu) event-urile în Kafka, iar `consumers` sunt cei care se abonează (citesc și procesează) la aceste event-uri. În Kafka, `producers` și `consumers` sunt complet decuplați și agnostici unul față de celălalt, ceea ce este un element cheie de proiectare pentru a atinge scalabilitatea înaltă pentru care Kafka este cunoscut. De exemplu, `producers` nu trebuie să aștepte niciodată `consumers`. Kafka oferă diverse garanții, cum ar fi capacitatea de a procesa events cu exactitate o singură dată.

Event-urile sunt organizate și stocate durabil în `topics`. Într-o simplificare foarte mare, un **topic** este similar cu un dosar într-un sistem de fișiere, iar **events** sunt fișierele din acel dosar. Un exemplu de nume de topic ar putea fi "**plăți**". 

`Topics` în Kafka sunt întotdeauna` multi-producers` și `multi-consumers`: un **topic** poate avea zero, unul sau mai mulți **producers** care scriu **events** în ea, precum și zero, unul sau mai mulți **consumers** care se abonează la aceste **events**. Event-urile dintr-un topic pot fi citite de câte ori este nevoie - spre deosebire de sistemele tradiționale de mesagerie, event-urile nu sunt șterse după consum. În schimb, definesc cât timp Kafka ar trebui să păstreze event-urile tale printr-o configurație specifică pentru fiecare topic, după care event-urile vechi vor fi eliminate. Performanța lui Kafka este efectiv constantă în raport cu dimensiunea datelor, deci stocarea datelor pentru o perioadă îndelungată este perfect acceptabilă.

`Topics` sunt partajate, ceea ce înseamnă că un topic este răspândită într-un număr de "`buckets`" situate pe diferiți `brokeri` Kafka. Plasarea distribuită a datelor tale este foarte importantă pentru scalabilitate, deoarece permite aplicațiilor **client** să citească și să scrie datele de/pe mai mulți brokeri în același timp. Atunci când un event nou este publicat într-un topic, este efectiv adăugat la una dintre partțiile topic-ului. Event-urile cu aceeași `event key` (de exemplu, un ID de client sau vehicul) sunt scrise în aceeași partiție, iar Kafka garantează că orice `consumer` al unei anumite `topic-partition` va citi întotdeauna event-urile acelei partiții în exact aceeași ordine în care au fost scrise.

![imagine](https://kafka.apache.org/images/streams-and-tables-p1_p4.png)
Figura: Această topic de exemplu are patru partiții, P1–P4. Doi clienți producători diferiți publică, independent unul de celălalt, noi events în topic scriind evenimente peste rețea în partițiile temei. Event-urile cu acelasi key (indicate de culoarea lor în figură) sunt scrise în aceeași partiție. Observați că ambii producers pot scrie în aceeași partiție dacă este adecvat.

Pentru a face datele tale tolerante la erori și disponibile în mod constant, fiecare `topic` poate fi replicat, chiar și peste regiuni geografice sau centre de date, astfel încât să existe întotdeauna mai mulți `brokeri` care au o copie a datelor în cazul în care apar probleme, trebuie să efectuezi întreținere pe brokeri, etc. O configurare comună în producție este un `factor de replicare de 3`, adică întotdeauna vor exista `trei copii ale datelor tale`. Această replicare se realizează la nivelul partițiilor temei.

## Kafka APIs

În plus față de instrumentele de linie de comandă pentru sarcini de management și administrare, Kafka dispune de cinci API-uri de bază pentru Java și Scala:

1. **Admin API** pentru gestionarea și inspectarea topic-urilor, brokerilor și altor obiecte Kafka.
2. **Producer API** pentru a publica (scrie) un flux de events către una sau mai multe topic-uri Kafka.
3. **Consumer API** pentru a se citi la una sau mai multe topic-uri și pentru a procesa fluxul de evenimente produse către ele.
4. **Kafka Streams API** pentru a implementa aplicații și microservicii de procesare a fluxurilor. Oferă funcții de nivel superior pentru procesarea fluxurilor de evenimente, inclusiv transformări, operațiuni stătice precum agregările și îmbinările, windowing, procesare bazată pe timestamp-ul evenimentelor și altele. Datele de intrare sunt citite din una sau mai multe topic-uri pentru a genera date de ieșire către una sau mai multe topic-uri, transformând efectiv fluxurile de intrare în fluxuri de ieșire.
5. **Kafka Connect API** pentru a construi și rula conectori reutilizabili pentru import/export de date care consumă (citesc) sau produc (scriu) fluxuri de evenimente de și către sisteme și aplicații externe, astfel încât să se integreze cu Kafka. De exemplu, un conector către o bază de date relațională precum **PostgreSQL** ar putea captura fiecare schimbare într-un set de tabele. Cu toate acestea, în practică, de obicei nu este necesar să implementezi proprii conectori deoarece comunitatea Kafka furnizează deja sute de conectori gata de utilizare.

### Cazuri de Utilizare

Iată o descriere a câtorva cazuri populare de utilizare pentru Apache Kafka®.

#### **Mesagerie**
Kafka funcționează bine ca înlocuitor pentru un broker de mesaje mai tradițional. Brokerii de mesaje sunt utilizați din diverse motive (pentru a separa procesarea de producătorii de date, pentru a tampona mesajele neprocesate, etc). În comparație cu majoritatea sistemelor de mesagerie, Kafka oferă un debit mai bun, partajare încorporată, replicare și toleranță la erori, ceea ce îl face o soluție bună pentru aplicații de procesare a mesajelor la scară mare.
În experiența noastră, utilizările de mesagerie au adesea un debit comparativ redus, dar pot necesita o latenta redusă de la un capăt la altul și depind adesea de garanțiile de durabilitate puternice oferite de Kafka.

În acest domeniu, Kafka este comparabil cu sisteme de mesagerie tradiționale precum ActiveMQ sau RabbitMQ.

#### **Urmărirea Activității pe Website**
Cazul inițial de utilizare pentru Kafka a fost reconstruirea unui sistem de urmărire a activității utilizatorilor sub forma unui set de fluxuri de publicare-abonare în timp real. Acest lucru înseamnă că activitatea pe site (vizualizări de pagini, căutări sau alte acțiuni pe care utilizatorii le pot întreprinde) este publicată în topicuri centrale, cu un topic pentru fiecare tip de activitate. Aceste fluxuri sunt disponibile pentru abonare pentru o serie de cazuri de utilizare, inclusiv procesare în timp real, monitorizare în timp real și încărcare în Hadoop sau sisteme de stocare offline pentru procesare și raportare offline.
Urmărirea activității este adesea de volum mare, deoarece multe mesaje de activitate sunt generate pentru fiecare vizualizare de pagină a utilizatorului.

#### **Metrici**
Kafka este adesea folosit pentru datele operaționale de monitorizare. Acest lucru implică agregarea statisticilor din aplicații distribuite pentru a produce fluxuri centralizate de date operaționale.

#### **Log Aggregation**
Mulți oameni folosesc Kafka ca înlocuitor pentru o soluție de agregare a log-urilor. Agregarea log-urilor colectează în mod tipic fișierele de log-uri fizice de pe servere și le plasează într-un loc central (un server de fișiere sau, eventual, HDFS) pentru procesare. Kafka ascunde detaliile fișierelor și oferă o abstractizare mai curată a datelor de jurnal sau evenimentelor ca un flux de mesaje. Acest lucru permite procesarea cu latență mai mică și suport mai facil pentru surse multiple de date și consum de date distribuit. În comparație cu sistemele axate pe log-uri precum Scribe sau Flume, Kafka oferă performanțe la fel de bune, garanții de durabilitate mai puternice datorită replicării și o latență mult mai mică de la un capăt la altul.

#### **Stream processing**
Mulți utilizatori de Kafka procesează date în pipeline-uri de procesare alcătuite din mai multe etape, unde datele brute de intrare sunt consumate din topicuri Kafka și apoi agregate, îmbogățite sau altfel transformate în noi topicuri pentru consum sau procesare ulterioară. De exemplu, un pipeline de procesare pentru recomandarea de articole de știri ar putea analiza conținutul articolelor din fluxuri RSS și îl publica într-un topic "articole"; o procesare ulterioară ar putea normaliza sau deduplica acest conținut și publica conținutul articolelor curățat într-un nou topic; o etapă finală de procesare ar putea încerca să recomande acest conținut utilizatorilor. Astfel de pipeline-uri de procesare creează grafuri de fluxuri de date în timp real bazate pe topicurile individuale. Începând cu versiunea 0.10.0.0, este disponibilă în Apache Kafka o bibliotecă de procesare ușoară, dar puternică, numită Kafka Streams, pentru a efectua astfel de procesări de date așa cum sunt descrise mai sus. În afara Kafka Streams, alternativele pentru instrumente de procesare a fluxurilor de sursă deschisă includ Apache Storm și Apache Samza.

#### **Event Sourcing**
Event Sourcing este un stil de proiectare a aplicației în care schimbările de stare sunt înregistrate sub forma unei secvențe ordonate în timp a înregistrărilor. Suportul lui Kafka pentru date de jurnal foarte mari îl face un backend excelent pentru o aplicație construită în acest stil.

#### **Commit Log**
Kafka poate servi ca un fel de Commit Log extern pentru un sistem distribuit. Jurnalul ajută la replicarea datelor între noduri și acționează ca un mecanism de resincronizare pentru nodurile care au eșuat pentru a-și restabili datele. Funcția de compactare a log-urilor în Kafka ajută la susținerea acestui scop. În această utilizare, Kafka este similar cu proiectul Apache BookKeeper.