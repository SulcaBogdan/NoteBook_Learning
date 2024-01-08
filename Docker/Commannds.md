# Comnenzine Docker

### Docker Build Comenzi:

| Comandă Docker                               | Explicație                                       | Exemplu                                               |
|-----------------------------------------------|--------------------------------------------------|-------------------------------------------------------|
| `docker build -t <nume_imagine> .`            | Construiește o imagine Docker dintr-un Dockerfile din directorul curent și o etichetează cu un nume. | `docker build -t myapp .`                             |
| `docker build --no-cache -t <nume_imagine> .` | Construiește o imagine Docker fără a utiliza memoria cache. | `docker build --no-cache -t myapp .`                 |
| `docker build -f <nume_dockerfile> -t <nume_imagine> .` | Construiește o imagine Docker folosind un Dockerfile specificat. | `docker build -f Dockerfile.prod -t myapp .`         |

### Docker Clean Up Comenzi:

| Comandă Docker                   | Explicație                                       | Exemplu                                    |
|-----------------------------------|--------------------------------------------------|--------------------------------------------|
| `docker system prune`             | Elimină toate resursele Docker neutilizate, inclusiv containere, imagini, rețele și volume. | `docker system prune`                      |
| `docker container prune`          | Elimină toate containerele oprite.              | `docker container prune`                   |
| `docker image prune`              | Elimină imaginile neutilizate.                 | `docker image prune`                       |
| `docker volume prune`             | Elimină volumele neutilizate.                  | `docker volume prune`                      |
| `docker network prune`            | Elimină rețelele neutilizate.                 | `docker network prune`                     |

### Comenzi de Interacțiune cu Containere:

| Comandă Docker                 | Explicație                                       | Exemplu                                    |
|---------------------------------|--------------------------------------------------|--------------------------------------------|
| `docker run <nume_imagine>`     | Rulează o imagine Docker ca un container.       | `docker run myapp`                         |
| `docker start <id_container>`   | Porneste un container oprit.                    | `docker start my_container`                |
| `docker stop <id_container>`    | Oprește un container în execuție.              | `docker stop my_container`                 |
| `docker restart <id_container>` | Restartează un container în execuție.           | `docker restart my_container`              |
| `docker exec -it <id_container> <comandă>` | Execută o comandă într-un container în execuție în mod interactiv. | `docker exec -it my_container bash`       |

### Comenzi de Inspectare a Containerelor:

| Comandă Docker                    | Explicație                                       | Exemplu                                    |
|------------------------------------|--------------------------------------------------|--------------------------------------------|
| `docker ps`                       | Listează containerele în execuție.             | `docker ps`                               |
| `docker ps -a`                    | Listează toate containerele, inclusiv cele oprite. | `docker ps -a`                            |
| `docker logs <id_container>`      | Adună jurnalele unui container specific.        | `docker logs my_container`                 |
| `docker inspect <id_container>`   | Inspectează informații detaliate despre un container. | `docker inspect my_container`              |

### Comenzi Imagini:

| Comandă Docker                    | Explicație                                       | Exemplu                                    |
|------------------------------------|--------------------------------------------------|--------------------------------------------|
| `docker images`                   | Listează imaginile Docker disponibile.         | `docker images`                           |
| `docker pull <nume_imagine>`      | Descarcă o imagine Docker dintr-un registru Docker. | `docker pull ubuntu`                       |
| `docker push <nume_imagine>`      | Încarcă o imagine Docker într-un registru Docker. | `docker push myapp`                        |
| `docker rmi <id_imagine>`         | Elimină o imagine Docker.                       | `docker rmi myapp`                         |

### Comenzi Docker Run:

| Comandă Docker                    | Explicație                                       | Exemplu                                    |
|------------------------------------|--------------------------------------------------|--------------------------------------------|
| `docker run -d <nume_imagine>`    | Rulează o imagine Docker ca un container în mod detaliat. | `docker run -d myapp`                      |
| `docker run -p <port_gazdă>:<port_container> <nume_imagine>` | Publică porturile containerului pe gazdă. | `docker run -p 8080:80 myapp`             |
| `docker run -v <cale_gazdă>:<cale_container> <nume_imagine>` | Montează un director sau volum gazdă într-un container. | `docker run -v /home/user:/app myapp`    |
| `docker run --name <nume_container> <nume_imagine>` | Asignează un nume personalizat containerului. | `docker run --name my_container myapp`   |

### Comenzi Docker Registry:

| Comandă Docker                    | Explicație                                       | Exemplu                                    |
|------------------------------------|--------------------------------------------------|--------------------------------------------|
| `docker login`                    | Autentificare într-un registru Docker.          | `docker login registry.example.com`        |
| `docker logout`                   | Deautentificare dintr-un registru Docker.       | `docker logout registry.example.com`       |
| `docker search <termen>`          | Caută imagini Docker într-un registru Docker.  | `docker search myapp`                      |
| `docker pull <registru>/<nume_imagine>` | Descarcă o imagine Docker dintr-un registru specific. | `docker pull registry.example.com/myapp` |

### Comenzi Docker Service:

| Comandă Docker                    | Explicație                                       | Exemplu                                    |
|------------------------------------|--------------------------------------------------|--------------------------------------------|
| `docker service create --name <nume_serviciu> <nume_imagine>` | Creează un serviciu Docker dintr-o imagine. | `docker service create --name my_service myapp` |
| `docker service ls`                | Listează serviciile Docker în execuție.        | `docker service ls`                        |
| `docker service scale <nume_serviciu>=<replici>` | Scalează replicile unui serviciu Docker. | `docker service scale my_service=3`        |
| `docker service logs <nume_serviciu>` | Afișează jurnalele (logs) ale unui serviciu Docker. | `docker service logs my_service`         |

### Comenzi Docker Network:

| Comandă Docker

                    | Explicație                                       | Exemplu                                    |
|------------------------------------|--------------------------------------------------|--------------------------------------------|
| `docker network create <nume_rețea>` | Creează o rețea Docker.                         | `docker network create my_network`        |
| `docker network ls`                | Listează rețelele Docker disponibile.          | `docker network ls`                        |
| `docker network inspect <nume_rețea>` | Inspectează informații detaliate despre o rețea Docker. | `docker network inspect my_network`      |
| `docker network connect <nume_rețea> <nume_container>` | Conectează un container la o rețea Docker. | `docker network connect my_network my_container` |

### Comenzi Docker Volume:

| Comandă Docker                    | Explicație                                       | Exemplu                                    |
|------------------------------------|--------------------------------------------------|--------------------------------------------|
| `docker volume create <nume_volum>` | Creează un volum Docker.                        | `docker volume create my_volume`          |
| `docker volume ls`                | Listează volumele Docker disponibile.          | `docker volume ls`                        |
| `docker volume inspect <nume_volum>` | Inspectează informații detaliate despre un volum Docker. | `docker volume inspect my_volume`        |
| `docker volume rm <nume_volum>`   | Elimină un volum Docker.                        | `docker volume rm my_volume`              |

### Comenzi Docker Swarm:

| Comandă Docker                    | Explicație                                       | Exemplu                                    |
|------------------------------------|--------------------------------------------------|--------------------------------------------|
| `docker swarm init`               | Inițializează un swarm Docker pe nodul curent.  | `docker swarm init`                        |
| `docker swarm join`               | Se alătură unui swarm Docker ca nod de lucru.   | `docker swarm join --token <token> <ip_nod_swarm>` |
| `docker node ls`                  | Listează nodurile dintr-un swarm Docker.        | `docker node ls`                          |
| `docker service create`           | Creează un serviciu într-un swarm Docker.       | `docker service create --name my_service myapp` |
| `docker service scale`            | Scalează replicile unui serviciu într-un swarm Docker. | `docker service scale my_service=3`       |

### Comenzi Docker Filesystem:

| Comandă Docker                    | Explicație                                       | Exemplu                                    |
|------------------------------------|--------------------------------------------------|--------------------------------------------|
| `docker cp <id_container>:<cale_container> <cale_gazdă>` | Copiază fișiere dintr-un container pe gazdă. | `docker cp my_container:/app /home/user`  |
| `docker cp <cale_gazdă> <id_container>:<cale_container>` | Copiază fișiere de pe gazdă într-un container. | `docker cp /home/user my_container:/app` |

### Variabile de Mediu Docker:

| Opțiune Docker                    | Explicație                                       | Exemplu                                    |
|------------------------------------|--------------------------------------------------|--------------------------------------------|
| `-e` sau `--env`                  | Setează variabile de mediu la rularea unui container. | `docker run -e VAR1=value1 -e VAR2=value2 myapp` |

### Verificări de Sănătate Docker:

| Opțiune Docker                    | Explicație                                       | Exemplu                                    |
|------------------------------------|--------------------------------------------------|--------------------------------------------|
| `HEALTHCHECK`                      | Instrucțiune pentru definirea unei comenzi pentru verificarea sănătății unui container. | Vezi în Dockerfile.                       |
| `docker container inspect --format='{{json .State.Health}}' <nume_container>` | Verifică starea de sănătate a unui container Docker. | `docker container inspect --format='{{json .State.Health}}' my_container` |

### Comenzi Docker Compose:

| Comandă Docker                    | Explicație                                       | Exemplu                                    |
|------------------------------------|--------------------------------------------------|--------------------------------------------|
| `docker-compose up`               | Creează și pornește containerele definite într-un fișier Docker Compose. | `docker-compose up`                       |
| `docker-compose down`             | Oprește și elimină containerele definite într-un fișier Docker Compose. | `docker-compose down`                     |
| `docker-compose ps`               | Listează containerele definite într-un fișier Docker Compose. | `docker-compose ps`                       |
| `docker-compose logs`             | Afișează jurnalele (logs) ale serviciilor definite într-un fișier Docker Compose. | `docker-compose logs`                     |

### Statistici Docker:

| Comandă Docker                    | Explicație                                       | Exemplu                                    |
|------------------------------------|--------------------------------------------------|--------------------------------------------|
| `docker stats`                    | Afișează un flux live al utilizării resurselor de către containere. | `docker stats`                            |
| `docker stats <nume_container>`   | Afișează utilizarea resurselor pentru un container specific. | `docker stats my_container`               |

