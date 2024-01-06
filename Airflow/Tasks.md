# Tasks in AirFlow

## Tasks
Un `Task` este unitatea de bază a execuției în Airflow. Sarcinile sunt aranjate în DAG-uri, iar apoi au dependențe `downstream` și `upstream` setate între ele pentru a exprima ordinea în care ar trebui să ruleze.

Există trei tipuri de bază de `Tasks`:

- `Operators`
Șabloane predefinite de sarcini pe care le puteți lega rapid pentru a construi cea mai mare parte a DAG-urilor dvs.

-  `Sensors`
O subclasă specială a `Operatorilor` care se ocupă în întregime de așteptarea unui eveniment extern să se întâmple.

- Un `@task` decorat cu `TaskFlow`
O funcție personalizată Python împachetată ca o `Task`.

Intern, acestea sunt de fapt toate subclase ale `BaseOperator` din Airflow, iar conceptele de `Task` și `Operator` sunt într-o oarecare măsură interschimbabile, dar este util să le considerăm ca concepte separate - în esență, `Operators` și `Sensors` sunt șabloane, iar când apelezi unul într-un fișier DAG, creezi un `Task`.

## Relații
Partea cheie a utilizării `Tasks` constă în definirea modului în care sunt interconectate - dependențele lor sau, cum spunem în Airflow, sarcinile lor `upstream` și `downstream`. Tu declari mai întâi sarcinile și apoi declarile dependențele lor.

*Notă*

Numim sarcina `upstream` pe cea care precede direct celelalte sarcini. În trecut, o numeam `Task-ul parinte`. Fii conștient că acest concept nu descrie sarcinile care sunt mai sus în ierarhia sarcinilor (adică nu sunt părinții direcți ai sarcinii). Aceeași definiție se aplică și la sarcina în aval, care trebuie să fie un copil direct al celeilalte sarcini.

Există două moduri de a declara dependențe - folosind operatorii `>>` și `<<` (`bitshift`):

```python
first_task >> second_task >> [third_task, fourth_task]
```
Sau metodele mai explicite `set_upstream `și `set_downstream`:

```python
first_task.set_downstream(second_task)
third_task.set_upstream(second_task)
```

Ambele fac exact același lucru, dar în general vă recomandăm să utilizați `operatorii bitshift`, deoarece sunt mai ușor de citit în majoritatea cazurilor.

În mod implicit, un `task` va fi executat atunci când toate sarcinile sale `upstream` (părinte) au avut succes, dar există multe modalități de modificare a acestui comportament pentru a adăuga ramificări, pentru a aștepta doar unele sarcini `upstream` sau pentru a schimba comportamentul în funcție de locul în care rulează curentul în istorie.

Task-urile nu transmit informații între ele în mod implicit și rulează în mod complet `independent`. Dacă doriți să transmiteți informații de la o sarcină la alta, ar trebui să utilizați XComs.


## Task Instances

În același mod în care un DAG este instanțiat într-un DAG Run de fiecare dată când rulează, sarcinile dintr-un DAG sunt instanțiate în `Task Instances`.

O instanță a unui `Task` este o rulare specifică a acelei sarcini pentru un DAG dat (și, prin urmare, pentru un interval de date dat). Ele reprezintă, de asemenea, starea unei sarcini, indicând în ce etapă a ciclului de viață se află.

Stările posibile pentru o instanță de sarcină sunt:

- `none`: Sarcina nu a fost încă planificată pentru execuție (dependențele sale nu au fost îndeplinite încă)
- `scheduled`: Planificatorul a determinat că dependențele sarcinii sunt îndeplinite și că ar trebui să ruleze
- `queued`: Sarcina a fost asignată unui Executor și așteaptă un worker
- `running`: Sarcina rulează pe un worker (sau pe un executor local/sincron)
- `success`: Sarcina s-a terminat fără erori
- `restarting`: Sarcina a fost solicitată extern să fie restartată în timpul ruleazării
- `failed`: Sarcina a avut o eroare în timpul execuției și nu a reușit să ruleze
- `skipped`: Sarcina a fost omisă din cauza ramificării, LatestOnly sau a unor motive `similare`.
- `upstream_failed`: O sarcină upstream a eșuat și Regula de Declanșare spune că aveam nevoie de ea
- `up_for_retry`: Sarcina a eșuat, dar are încercări de reluare rămase și va fi reprogramată.
- `up_for_reschedule`: Sarcina este un Senzor aflat în modul de reprogramare
- `deferred`: Sarcina a fost amânată pentru o declanșare ulterioară
- `removed`: Sarcina a dispărut din DAG de la începutul rulării

![task](https://airflow.apache.org/docs/apache-airflow/stable/_images/task_lifecycle_diagram.png)


Ideal, o sarcină ar trebui să treacă de la starea "`none`", la "`scheduled`", apoi la "`queued`", "`running`" și în cele din urmă la "`success`".

Atunci când rulează orice `Task` personalizat (`Operator`), acesta va primi o copie a instanței sarcinii; în plus față de capacitatea de a inspecta metadatele sarcinii, conține și metode pentru lucruri precum `XComs`.

### Terminologiea relațiilor
Pentru orice instanță de sarcină dată, există două tipuri de relații pe care le are cu alte instanțe.

În primul rând, poate avea sarcini `upstream` și `downstream`:

```python
task1 >> task2 >> task3
```

Când rulează un DAG, acesta va crea instanțe pentru fiecare dintre aceste task-uri care sunt `upstream`/`downstream` una de cealaltă, dar toate au același interval de date.

Pot exista, de asemenea, instanțe ale aceleiași task, dar pentru intervale de date diferite - din alte rulări ale aceluiași DAG. Le numim "`previous`" și "`next`" - este o relație diferită față de `upstream` și `downstream`!

## Timeout-uri

Dacă dorești ca o sarcină să aibă un timp maxim de execuție, setează atributul `execution_timeout` la o valoare `datetime.timedelta` care reprezintă durata maximă permisă. Aceasta se aplică tuturor sarcinilor Airflow, inclusiv senzorilor. `execution_timeout` controlează timpul maxim permis pentru fiecare execuție. Dacă `execution_timeout` este depășit, sarcina expiră și se generează `AirflowTaskTimeout`.

În plus, senzorii au un parametru de `timeout`. Acest lucru contează doar pentru senzorii în modul de reprogramare. `timeout` controlează timpul maxim permis pentru ca senzorul să reușească. Dacă `timeout` este depășit, se va genera `AirflowSensorTimeout` și senzorul va eșua imediat, fără a încerca din nou.

Exemplul următor de `SFTPSensor` ilustrează acest lucru. `Senzorul` este în modul de reprogramare, ceea ce înseamnă că este executat periodic și reprogramat până când reușește.

- De fiecare dată când senzorul "`poke`"-ează serverul `SFTP`, i se permite un timp maxim de **60 de secunde**, așa cum este definit de `execution_timeout`.

- Dacă senzorul durează mai mult de **60 de secunde** pentru a "`poka`" serverul `SFTP`, va fi generat `AirflowTaskTimeout`. Senzorul are voie să încerce din nou atunci când acest lucru se întâmplă. Poate încerca de până la 2 ori, așa cum este definit de `retries`.

- De la începutul primei execuții până când reușește în cele din urmă (adică după ce apare fișierul '`root/test`'), senzorul are permisiunea de a dura maxim 3600 de secunde, așa cum este definit de `timeout`. Cu alte cuvinte, dacă fișierul nu apare pe serverul `SFTP` în decurs de 3600 de secunde, senzorul va genera `AirflowSensorTimeout`. Nu va încerca să se reînceapă atunci când apare această eroare.

- Dacă senzorul eșuează din alte motive, cum ar fi probleme de rețea în timpul intervalului de 3600 de secunde, poate încerca de până la 2 ori, așa cum este definit de `retries`. Reîncercarea nu resetează `timeout`-ul. Senzorul va avea totuși până la 3600 de secunde în total pentru a reuși.

```python
sensor = SFTPSensor(
    task_id="sensor",
    path="/root/test",
    execution_timeout=timedelta(seconds=60),
    timeout=3600,
    retries=2,
    mode="reschedule",
)
```

## SLA-uri

Un `SLA`, sau un **Service Level Agreement**, reprezintă așteptarea pentru timpul maxim în care o sarcină ar trebui să fie finalizată în raport cu ora de începere a `Dag Run`. Dacă o sarcină durează mai mult decât acest timp, ea devine vizibilă în partea "SLA Misses" a interfeței utilizatorului, și, de asemenea, se trimite printr-un email cu toate sarcinile care au depășit SLA-ul lor.

Sarcinile care depășesc SLA-ul nu sunt anulate, totuși - li se permite să ruleze până la finalizare. Dacă dorești să anulezi o sarcină după ce a atins o anumită durată de execuție, atunci ar trebui să folosești `Timeout`-uri în schimb.

Pentru a seta un SLA pentru o sarcină, transmite un obiect `datetime.timedelta` parametrului sla al `Task/Operator`. Poți, de asemenea, furniza un `sla_miss_callback` care va fi apelat atunci când SLA este depășit, dacă dorești să rulezi logica ta personalizată.

Dacă dorești să dezactivezi complet verificarea `SLA`, poți seta `check_slas = False` în configurarea `[core]` a Airflow.

### `sla_miss_callback`

Poți, de asemenea, furniza un `sla_miss_callback` care va fi apelat atunci când `SLA` este depășit, dacă dorești să rulezi logica ta personalizată. Semnătura funcției `sla_miss_callback` necesită 5 parametri.

- `dag`

  Obiectul DAG părinte pentru DAGRun în care sarcinile au depășit SLA-ul lor.

- `task_list`

  Listă de șiruri (separate de linii noi, \n) ale tuturor sarcinilor care au depășit SLA-ul lor de la ultima rulare a `sla_miss_callback`.

- `blocking_task_list`

  Orice sarcină în DAGRun(s) (cu aceeași data de execuție ca o sarcină care a depășit SLA-ul) care nu este într-o stare SUCCESS în momentul în care sla_miss_callback rulează, adică '`running`', '`failed`'. Aceste sarcini sunt descrise ca sarcini care blochează propria lor finalizare sau a altei sarcini înainte ca fereastra lor SLA să fie completă.

- `slas`

  Listă de obiecte SlaMiss asociate sarcinilor din parametrul `task_list`.

- `blocking_tis`

  Listă de obiecte TaskInstance asociate sarcinilor din parametrul `blocking_task_list`.

Exemple de semnătură a funcției `sla_miss_callback`:

```python
def my_sla_miss_callback(dag, task_list, blocking_task_list, slas, blocking_tis):
    ...
```

```python
def my_sla_miss_callback(*args):
    ...
```

### Exemplu DAG

```python
def sla_callback(dag, task_list, blocking_task_list, slas, blocking_tis):
    print(
        "The callback arguments are: ",
        {
            "dag": dag,
            "task_list": task_list,
            "blocking_task_list": blocking_task_list,
            "slas": slas,
            "blocking_tis": blocking_tis,
        },
    )


@dag(
    schedule="*/2 * * * *",
    start_date=pendulum.datetime(2021, 1, 1, tz="UTC"),
    catchup=False,
    sla_miss_callback=sla_callback,
    default_args={"email": "email@example.com"},
)
def example_sla_dag():
    @task(sla=datetime.timedelta(seconds=10))
    def sleep_20():
        """Sleep for 20 seconds"""
        time.sleep(20)

    @task
    def sleep_30():
        """Sleep for 30 seconds"""
        time.sleep(30)

    sleep_20() >> sleep_30()


example_dag = example_sla_dag()
```
### Excepții speciale

Dacă dorești să controlezi starea sarcinii tale din interiorul codului personalizat al `Task/Operator`, Airflow oferă două excepții speciale pe care le poți ridica:

- `AirflowSkipException` va marca sarcina curentă ca fiind omisă.
  
- `AirflowFailException` va marca sarcina curentă ca fiind eșuată, ignorând orice încercare de reluare rămasă.

Acestea pot fi utile dacă codul tău are cunoștințe suplimentare despre mediul său și dorește să eșueze/omoare mai repede - de exemplu, să ocolească atunci când știe că nu există date disponibile sau să eșueze rapid atunci când detectează că cheia API este invalidă (deoarece aceasta nu va fi rezolvată printr-o reluare).

## Zombie/Undead Tasks

Niciun sistem nu rulează perfect, iar instanțele de sarcină sunt de așteptat să se oprească din când în când. Airflow detectează două tipuri de neconcordanțe între sarcini/procese:

- `Zombie tasks` sunt instanțe de sarcină blocate într-o stare de execuție, în ciuda faptului că job-urile asociate sunt inactive (de exemplu, procesul lor nu a trimis un semnal recent de viață deoarece a fost oprit sau mașina a picat). Airflow le va găsi periodic, le va curăța și va eșua sau va încerca să repornească sarcina în funcție de setările sale.

- `Undead tasks` sunt sarcini care nu ar trebui să ruleze, dar o fac, adesea cauzate atunci când editezi manual instanțe de sarcină prin interfața utilizatorului. Airflow le va găsi periodic și le va încheia.

Mai jos este un fragment de cod din planificatorul Airflow care rulează periodic pentru a detecta sarcini `zombie/undead`.

```python
    def _find_zombies(self) -> None:
        """
        Find zombie task instances and create a TaskCallbackRequest to be handled by the DAG processor.

        Zombie instances are tasks haven't heartbeated for too long or have a no-longer-running LocalTaskJob.
        """
        from airflow.jobs.job import Job

        self.log.debug("Finding 'running' jobs without a recent heartbeat")
        limit_dttm = timezone.utcnow() - timedelta(seconds=self._zombie_threshold_secs)

        with create_session() as session:
            zombies: list[tuple[TI, str, str]] = (
                session.execute(
                    select(TI, DM.fileloc, DM.processor_subdir)
                    .with_hint(TI, "USE INDEX (ti_state)", dialect_name="mysql")
                    .join(Job, TI.job_id == Job.id)
                    .join(DM, TI.dag_id == DM.dag_id)
                    .where(TI.state == TaskInstanceState.RUNNING)
                    .where(
                        or_(
                            Job.state != JobState.RUNNING,
                            Job.latest_heartbeat < limit_dttm,
                        )
                    )
                    .where(Job.job_type == "LocalTaskJob")
                    .where(TI.queued_by_job_id == self.job.id)
                )
                .unique()
                .all()
            )

        if zombies:
            self.log.warning("Failing (%s) jobs without heartbeat after %s", len(zombies), limit_dttm)

        for ti, file_loc, processor_subdir in zombies:
            zombie_message_details = self._generate_zombie_message_details(ti)
            request = TaskCallbackRequest(
                full_filepath=file_loc,
                processor_subdir=processor_subdir,
                simple_task_instance=SimpleTaskInstance.from_ti(ti),
                msg=str(zombie_message_details),
            )
            log_message = (
                f"Detected zombie job: {request} "
                "(See https://airflow.apache.org/docs/apache-airflow/"
                "stable/core-concepts/tasks.html#zombie-undead-tasks)"
            )
            self._task_context_logger.error(log_message, ti=ti)
            self.job.executor.send_callback(request)
            Stats.incr("zombies_killed", tags={"dag_id": ti.dag_id, "task_id": ti.task_id})
```

Explicația criteriilor folosite în fragmentul de mai sus pentru detectarea sarcinilor `zombie` este următoarea:

1. `Task Instance State`

Numai instanțele de sarcină în starea `RUNNING` sunt considerate potențiale `zombie`.

2. `Job State and Heartbeat Check`

Task-urile `zombie` sunt identificate dacă job-ul asociat nu se află în starea `RUNNING` sau dacă ultimul semnal de viață al job-ului este anterior pragului de timp calculat (`limit_dttm`). `Heartbeat`-ul este un mecanism pentru a indica faptul că o sarcină sau un job este încă activ și în execuție.

3. `Job Type`

Job-ul asociat sarcinii trebuie să fie de tip "`LocalTaskJob`."

4. `Queued by Job ID`

Numai sarcinile puse în coadă de același job care este procesat în prezent sunt luate în considerare.

Aceste condiții ajută colectiv la identificarea sarcinilor în execuție care pot fi `zombie` în funcție de starea lor, starea job-ului asociat, statusul `heartbeat`-ului, tipul job-ului și job-ul specific care le-a pus în coadă. Dacă o sarcină îndeplinește aceste criterii, este considerată o potențială `zombie`, și se iau măsuri ulterioare, cum ar fi înregistrarea și trimiterea unei solicitări de callback.

### Reproducerea locală a Task-urilor zombie
Dacă doriți să reproduceți task-uri zombi pentru procesele de dezvoltare/testare, urmați pașii de mai jos:

1. Setați variabilele de mediu de mai jos pentru configurația locală a fluxului de aer (în mod alternativ, puteți modifica valorile de configurare corespunzătoare în `airflow.cfg`)

```python
export AIRFLOW__SCHEDULER__LOCAL_TASK_JOB_HEARTBEAT_SEC=600
export AIRFLOW__SCHEDULER__SCHEDULER_ZOMBIE_TASK_THRESHOLD=2
export AIRFLOW__SCHEDULER__ZOMBIE_DETECTION_INTERVAL=5
```

2. Aveți un DAG cu un task care durează aproximativ 10 minute (adică un task de lungă durată). De exemplu, puteți utiliza DAG de mai jos:

```python
from airflow.decorators import dag
from airflow.operators.bash import BashOperator
from datetime import datetime


@dag(start_date=datetime(2021, 1, 1), schedule="@once", catchup=False)
def sleep_dag():
    t1 = BashOperator(
        task_id="sleep_10_minutes",
        bash_command="sleep 600",
    )


sleep_dag()
```

Rulați DAG-ul de mai sus și așteptați puțin. Ar trebui să vedeți că instanța task-ului devine un task zombi și apoi este killed de programator.

### Configurarea executor
Unii Executori permit configurarea opțională per task - cum ar fi `KubernetesExecutor`, care vă permite să setați o imagine pe care să rulați sarcina.

Acest lucru se realizează prin argumentul `executor_config` către o sarcină sau un `operator`. Iată un exemplu de setare a imaginii `Docker` pentru o sarcină care va rula pe `KubernetesExecutor`:

```python
MyOperator(...,
    executor_config={
        "KubernetesExecutor":
            {"image": "myCustomDockerImage"}
    }
)
```

