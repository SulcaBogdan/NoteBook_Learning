# Terraform general

Ce zici de asta:


**Ce este Terraform?**

*`Terraform`* este o unealtă de infrastructură ca cod care vă permite să construiți, să modificați și să versionați resurse în cloud și local în mod sigur și eficient.

*`HashiCorp Terraform`* este o unealtă de infrastructură ca cod care vă permite să definiți resurse atât în `cloud`, cât și `local`, în fișiere de configurare ușor de citit, pe care le puteți versiona, reutiliza și partaja. Apoi, puteți utiliza un flux de lucru consistent pentru a proviziona și gestiona întreaga infrastructură pe parcursul ciclului său de viață. `Terraform` poate gestiona componente de nivel înalt, precum intrările DNS și caracteristici SaaS, precum și componente de nivel scăzut, cum ar fi resursele de calcul, stocare și rețea.


## Cum funcționează Terraform?

*Terraform* creează și gestionează resurse pe platformele cloud și alte servicii prin intermediul interfețelor lor de programare a aplicațiilor (API-uri). Provider-ii permit lui Terraform să lucreze cu aproape orice platformă sau serviciu care are o API accesibilă.

![terraform](https://developer.hashicorp.com/_next/image?url=https%3A%2F%2Fcontent.hashicorp.com%2Fapi%2Fassets%3Fproduct%3Dterraform%26version%3Drefs%252Fheads%252Fv1.6%26asset%3Dwebsite%252Fimg%252Fdocs%252Fintro-terraform-apis.png%26width%3D2048%26height%3D644&w=2048&q=75)

**`HashiCorp`** și comunitatea *`Terraform`* au scris deja mii de provider-i pentru a gestiona multe tipuri diferite de resurse și servicii. Puteți găsi toți provider-ii disponibili public pe *`Terraform Registry`*, inclusiv Amazon Web Services (AWS), Azure, Google Cloud Platform (GCP), Kubernetes, Helm, GitHub, Splunk, DataDog și multe altele.

Fluxul principal de lucru al *Terraform* constă în trei etape:

1. *`Write`*: Definiți resursele, care pot fi în mai multe cloud-uri și servicii. De exemplu, puteți crea o configurare pentru a implementa o aplicație pe mașini virtuale într-o rețea *Virtual Private Cloud (VPC)* cu grupuri de securitate și un echilibrator de sarcină.

2. *`Plan`*: *Terraform* creează un plan de execuție care descrie infrastructura pe care o va crea, actualiza sau distruge în funcție de infrastructura existentă și configurarea dvs.

3. *`Apply`*: După aprobare, *Terraform* efectuează operațiile propuse în ordinea corectă, respectând orice dependențe între resurse. De exemplu, dacă actualizați proprietățile unei VPC și schimbați numărul de mașini virtuale în acea VPC, *Terraform* va recrea VPC-ul înainte de a scala mașinile virtuale.


![terraform](https://developer.hashicorp.com/_next/image?url=https%3A%2F%2Fcontent.hashicorp.com%2Fapi%2Fassets%3Fproduct%3Dterraform%26version%3Drefs%252Fheads%252Fv1.6%26asset%3Dwebsite%252Fimg%252Fdocs%252Fintro-terraform-workflow.png%26width%3D2038%26height%3D1773&w=2048&q=75)

## **De ce Terraform?**
Armon Dadgar, co-fondator și CTO HashiCorp, explică cum Terraform rezolvă provocările infrastructurale. 

1. **Gestionați orice infrastructură**: Găsiți provideri pentru multe dintre platformele și serviciile pe care le utilizați deja în *Terraform Registry*. Puteți scrie și proprii provideri. Terraform adoptă o abordare imutabilă față de infrastructură, reducând complexitatea actualizării sau modificării serviciilor și infrastructurii dvs.

2. **Urmăriți-vă infrastructura**: Terraform generează un plan și vă solicită aprobarea înainte de a modifica infrastructura. De asemenea, ține evidența infrastructurii reale într-un fișier de stare, care acționează ca sursă de adevăr pentru mediul dvs. Terraform folosește fișierul de stare pentru a determina schimbările de făcut în infrastructura dvs., astfel încât să se potrivească cu configurația dvs.

3. **Automatizați schimbările**: Fișierele de configurare Terraform sunt declarative, ceea ce înseamnă că descriu starea finală a infrastructurii dvs. Nu trebuie să scrieți instrucțiuni pas cu pas pentru a crea resurse, deoarece Terraform gestionează logica de bază. Terraform construiește un grafic al resurselor pentru a determina dependențele resurselor și creează sau modifică resursele non-dependente în paralel. Acest lucru permite lui Terraform să provisioneze resurse eficient.

4. **Standardizarea Configurărilor**
Terraform susține componente de configurare reutilizabile numite module, care definesc colecții configurabile de infrastructură, economisind timp și încurajând bunele practici. Puteți utiliza modulele disponibile public în Terraform Registry sau să scrieți propriile module.

5. **Colaborare**
Deoarece configurația dvs. este scrisă într-un fișier, o puteți comite într-un Sistem de Control al Versiunilor (VCS) și utiliza Terraform Cloud pentru a gestiona eficient fluxurile de lucru Terraform în echipă. Terraform Cloud rulează Terraform într-un mediu consecvent, fiabil și oferă acces securizat la starea partajată și datele secrete, controale de acces bazate pe roluri, un registru privat pentru partajarea atât a modulelor, cât și a providerilor, și multe altele.
