# Arhitectura Docker

**Docker** folosește o arhitectură client-server. Clientul Docker comunică cu daemonul Docker, care se ocupă de construirea, rularea și distribuirea containerelor Docker. Clientul și daemonul Docker pot rula pe același sistem, sau puteți conecta un client Docker la un daemon Docker la distanță. Clientul și daemonul Docker comunică folosind o interfață API REST, peste soclu UNIX sau o interfață de rețea. Un alt client Docker este Docker Compose, care vă permite să lucrați cu aplicații alcătuite dintr-un set de containere.


[![docker-architecture.webp](https://i.postimg.cc/1zwK7BNv/docker-architecture.webp)](https://postimg.cc/v189cWhn)

## Demonul Docker
Demonul Docker (dockerd) ascultă cererile API Docker și administrează obiectele Docker precum imagini, containere, rețele și volume. Un demon poate, de asemenea, comunica cu alți demoni pentru a administra serviciile Docker.

## Clientul Docker
Clientul Docker (docker) este modalitatea principală prin care mulți utilizatori Docker interacționează cu Docker. Atunci când utilizați comenzi precum `docker run`, clientul trimite aceste comenzi către dockerd, care le execută. Comanda `docker` utilizează API-ul Docker. Clientul Docker poate comunica cu mai mulți demoni.

## Registre Docker
Un registru Docker stochează imagini Docker. Docker Hub este un registru public pe care oricine îl poate utiliza, iar Docker caută imagini pe Docker Hub în mod implicit. Puteți chiar să rulați propriul registru privat.

Atunci când utilizați comenzile `docker pull` sau `docker run`, Docker extrage imaginile necesare din registru-ul configurat. Atunci când utilizați comanda `docker push`, Docker împinge imaginea dvs. către registru-ul configurat.

## Obiecte Docker
Atunci când utilizați Docker, creați și utilizați **imagini**, **containere**, **rețele**, **volume**, **plugin**-uri și alte obiecte. Această secțiune oferă o prezentare succintă a unora dintre aceste obiecte.