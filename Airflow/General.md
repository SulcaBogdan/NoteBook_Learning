# Informatii generale Airflow

**Ce este Airflow™?**
Apache Airflow™ este o platformă open-source pentru dezvoltarea, planificarea și monitorizarea fluxurilor de lucru orientate pe loturi. Cadru extensibil în Python permite construirea de fluxuri de lucru care se conectează practic la orice tehnologie. O interfață web ajută la gestionarea stării fluxurilor de lucru. Airflow poate fi implementat în multe moduri, variind de la un singur proces pe laptopul tău la o configurare distribuită pentru a susține chiar și cele mai mari fluxuri de lucru.

**Fluxuri de lucru ca și cod**
Principalul aspect al fluxurilor de lucru Airflow este că toate acestea sunt definite în cod Python. "Fluxurile de lucru ca și cod" îndeplinesc mai multe scopuri:

- **Dinamice:** Pipelines-ul Airflow este configurat ca cod Python, permițând generarea dinamică a pipeline-urilor.
  
- **Extensibile:** Cadru Airflow™ conține operatori pentru conectarea la numeroase tehnologii. Toate componentele Airflow sunt extensibile pentru a se adapta cu ușurință la mediul tău.

- **Flexibile:** Parametrizarea fluxului de lucru este inclusă, folosind motorul de șabloane Jinja.

Aruncă o privire la fragmentul de cod următor:
```python
from datetime import datetime

from airflow import DAG
from airflow.decorators import task
from airflow.operators.bash import BashOperator

# A DAG represents a workflow, a collection of tasks
with DAG(dag_id="demo", start_date=datetime(2022, 1, 1), schedule="0 0 * * *") as dag:
    # Tasks are represented as operators
    hello = BashOperator(task_id="hello", bash_command="echo hello")

    @task()
    def airflow():
        print("airflow")

    # Set dependencies between tasks
    hello >> airflow()
```

Acest fragment de cod reprezintă un simplu `DAG` (**Directed Acyclic Graph**) în Apache Airflow, în care se definesc operatori și relații între aceștia. `DAG`-ul poate fi apoi planificat, monitorizat și executat folosind platforma Apache Airflow.

Iată ce poți observa:

- Un `DAG` numit "demo", care începe pe 1 ianuarie 2022 și rulează o dată pe zi. Un `DAG` este reprezentarea în Airflow a unui flux de lucru.

- Două sarcini, un `BashOperator` care rulează un script `Bash` și o funcție Python definită folosind decoratorul `@task`.

- Operatorul "`>>`" între sarcini definește o dependență și controlează în ce ordine vor fi executate sarcinile.

Airflow evaluează acest script și execută sarcinile la intervalul setat și în ordinea definită. Starea DAG-ului "demo" este vizibilă în interfața web:

![airflow](https://airflow.apache.org/docs/apache-airflow/stable/_images/demo_graph_view.png)

Acest exemplu demonstrează un simplu script Bash și Python, dar aceste sarcini pot rula orice cod arbitrar. Poți să te gândești să rulezi o operațiune Spark, să transferi date între două bucket-uri sau să trimiți un email. Aceeași structură poate fi observată în derulare în timp:

![airflow](https://airflow.apache.org/docs/apache-airflow/stable/_images/demo_grid_view.png)

### Fiecare coloană reprezintă o rulare a DAG-ului.
Acestea sunt două dintre cele mai utilizate viziuni în Airflow, dar există și alte viziuni care îți permit să te aprofundezi în starea fluxurilor tale de lucru.

## De ce Airflow™?
Airflow™ este o platformă de orchestrare a fluxurilor de lucru în lot. Cadru Airflow conține `operatori` pentru a se conecta la multe tehnologii și este ușor extensibil pentru a se conecta la o tehnologie nouă. Dacă fluxurile tale de lucru au un început și un sfârșit clar, și rulează la intervale regulate, pot fi programate ca un `DAG Airflow`.

Dacă preferi să codezi în loc să dai clicuri, Airflow este instrumentul pentru tine. Fluxurile de lucru sunt definite ca și `cod Python`, ceea ce înseamnă:

- Fluxurile de lucru pot fi stocate în controlul versiunilor, astfel încât să poți reveni la versiunile anterioare.
- Fluxurile de lucru pot fi dezvoltate de mai multe persoane simultan.
- Pot fi scrise teste pentru a valida funcționalitatea.
- Componentele sunt extensibile, iar tu poți construi pe o colecție vastă de componente existente.
- Semantica bogată de programare și execuție îți permit să definești cu ușurință pipe-uri complexe, care rulează la intervale regulate. Backfilling îți permite să rulezi (re)pipe-uri pe date istorice după ce ai făcut modificări în logica ta. Și capacitatea de a relua pipe-uri parțiale după rezolvarea unei erori ajută la maximizarea eficienței.

### Interfața utilizator Airflow oferă:

- Vizualizări detaliate ale a două aspecte:
  - Pipe-uri (Pipelines)
  - Sarcini (Tasks)
- Prezentarea generală a fluxurilor tale de lucru în timp.

Prin intermediul interfeței, poți inspecta jurnale și gestiona sarcini, de exemplu, reîncercând o sarcină în caz de eșec.

Natura open-source a Airflow asigură faptul că lucrezi cu componente dezvoltate, testate și utilizate de multe alte companii din întreaga lume. În comunitatea activă poți găsi o mulțime de resurse utile sub formă de bloguri, articole, conferințe, cărți și altele. Poți conecta cu alți colegi prin mai multe canale, cum ar fi Slack și liste de discuții.

Airflow ca o platformă este extrem de personalizabilă. Prin utilizarea Interfeței Publice a Airflow, poți extinde și personaliza aproape fiecare aspect al Airflow.

## De ce nu Airflow™?
Airflow™ a fost construit pentru **fluxuri de lucru finite** în lot. În timp ce `CLI` și `REST API` permit declanșarea fluxurilor de lucru, Airflow nu a fost construit pentru fluxuri de lucru bazate pe evenimente care rulează la nesfârșit. `Airflow nu este o soluție de streaming`. Cu toate acestea, un sistem de streaming cum ar fi `Apache Kafka` este adesea văzut lucrand împreună cu Apache Airflow. `Kafka` poate fi folosit pentru ingestie și procesare în timp real, datele evenimentelor sunt scrise într-o locație de stocare, iar Airflow pornește periodic un flux de lucru care procesează un lot de date.

Dacă preferi să dai clicuri în loc să codezi, Airflow probabil nu este soluția potrivită. Interfața web își propune să facă gestionarea fluxurilor de lucru cât mai ușoară posibil, iar cadru Airflow este îmbunătățit în mod continuu pentru a face experiența dezvoltatorului cât mai fluidă posibil. Cu toate acestea, filozofia Airflow este de a defini fluxurile de lucru ca și cod, așa că codarea va fi întotdeauna necesară.
