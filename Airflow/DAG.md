# DAG in Apache Airflow


### Un DAG (Directed Acyclic Graph) este conceptul central al Airflow, adunând Task-urile împreună, organizate cu dependențe și relații pentru a specifica modul în care ar trebui să ruleze.

Aici este un exemplu de bază al unui DAG:

![dag](https://airflow.apache.org/docs/apache-airflow/stable/_images/basic-dag.png)

Defineste patru Sarcini - `A`, `B`, `C` și `D` - și dictează ordinea în care trebuie să ruleze, precum și care task-uri depind de altele. De asemenea, va preciza cât de des să ruleze `DAG`-ul - poate fi "la fiecare 5 minute începând de mâine" sau "în fiecare zi începând de la 1 ianuarie 2020".

`DAG`-ul în sine nu se preocupă de ceea ce se întâmplă în interiorul task-urilor; este interesat doar de modul în care să le execute - ordinea în care să le ruleze, de câte ori să le reîncerce, dacă au limite de timp, și așa mai departe.

## Declarația unui DAG
Există trei modalități de a declara un `DAG` - poți folosi un **context manager**, care va adăuga implicit DAG-ul la orice se află în interiorul său:

```python
 import datetime

 from airflow import DAG
 from airflow.operators.empty import EmptyOperator

 with DAG(
     dag_id="my_dag_name",
     start_date=datetime.datetime(2021, 1, 1),
     schedule="@daily",
 ):
     EmptyOperator(task_id="task")

```
Sau poți utiliza un constructor standard, transmitând DAG-ul la orice operatori folosești:

```python
 import datetime

 from airflow import DAG
 from airflow.operators.empty import EmptyOperator

 my_dag = DAG(
     dag_id="my_dag_name",
     start_date=datetime.datetime(2021, 1, 1),
     schedule="@daily",
 )
 EmptyOperator(task_id="task", dag=my_dag)
```

Sau poți utiliza decoratorul `@dag` pentru a transforma o funcție într-un generator `DAG`:

```python
import datetime

from airflow.decorators import dag
from airflow.operators.empty import EmptyOperator


@dag(start_date=datetime.datetime(2021, 1, 1), schedule="@daily")
def generate_dag():
    EmptyOperator(task_id="task")


generate_dag()
```

`DAG`-urile nu sunt nimic fără Task-uri de rulat, și acestea vor veni în mod obișnuit sub forma `Operators`, `Sensors` sau `TaskFlow`.

## Dependențe între Sarcini
Un `Task/Operator` nu trăiește de obicei singură; are dependențe de alte task-uri (cele de deasupra sa), iar alte task-uri depind de ea (cele de dedesubtul sa). Declararea acestor dependențe între task-uri constituie structura `DAG` (*the edges of the directed acyclic graph*).

Există două modalități principale de a declara dependențele individuale ale task-urilor. Cea recomandată este utilizarea operatorilor `>>` și `<<`:


```python
first_task >> [second_task, third_task]
third_task << fourth_task
```

Sau poți utiliza și metodele mai explicite `set_upstream` și `set_downstream`:

```python
first_task.set_downstream([second_task, third_task])
third_task.set_upstream(fourth_task)
```

Există și scurtături pentru a declara dependențe mai complexe. Dacă vrei să faci ca două liste de task-uri să depindă de toate părțile fiecare, nu poți utiliza niciuna dintre abordările de mai sus, așa că trebuie să folosești `cross_downstream`:

```python
from airflow.models.baseoperator import cross_downstream

# Replaces
# [op1, op2] >> op3
# [op1, op2] >> op4
cross_downstream([op1, op2], [op3, op4])
```


Și dacă vrei să le legati împreună pe baza dependențelor, poți utiliza `chain`:

```python
from airflow.models.baseoperator import chain

# Replaces op1 >> op2 >> op3 >> op4
chain(op1, op2, op3, op4)

# You can also do it dynamically
chain(*[EmptyOperator(task_id='op' + i) for i in range(1, 6)])
```

`Chain` poate realiza și dependențe pe perechi pentru liste de aceeași dimensiune (aceasta este diferită de dependențele incrucisate create de `cross_downstream`!):

```python
from airflow.models.baseoperator import chain

# Replaces
# op1 >> op2 >> op4 >> op6
# op1 >> op3 >> op5 >> op6
chain(op1, [op2, op3], [op4, op5], op6)
```


## Încărcarea DAG-urilor

Airflow încarcă DAG-urile din fișierele sursă Python, pe care le caută în interiorul directorului configurat `DAG_FOLDER`. Va lua fiecare fișier, îl va executa, și apoi va încărca orice obiecte `DAG` din acel fișier.

Acest lucru înseamnă că poți defini mai multe DAG-uri per fișier Python, sau poți chiar împărți un `DAG` foarte complex pe mai multe fișiere Python folosind importuri.

Totuși, trebuie să ții cont că atunci când Airflow vine să încarce `DAG`-uri dintr-un fișier Python, va extrage doar obiectele de la nivelul superior care sunt o instanță `DAG`. De exemplu, ia în considerare acest fișier:

```python
dag_1 = DAG('this_dag_will_be_discovered')

def my_function():
    dag_2 = DAG('but_this_dag_will_not')

my_function()
```

În timp ce ambii constructori de DAG sunt apelați când fișierul este accesat, doar dag_1 este la nivelul superior (în globals()), și astfel doar el este adăugat la Airflow. dag_2 nu este încărcat.


**NOTA**
Când caută `DAG`-uri în interiorul directorului `DAG_FOLDER`, Airflow ia în considerare doar fișierele Python care conțin `șirurile airflow` și `dag` (fără a ține cont de sensibilitatea la majuscule/minusculă) ca o optimizare.

Pentru a lua în considerare toate fișierele Python în schimb, dezactivează `DAG_DISCOVERY_SAFE_MODE` configuration flag.

Poți furniza și un fișier `.airflowignore` în interiorul directorului `DAG_FOLDER` sau în oricare dintre subdirectoarele sale, care descrie modelele de fișiere pe care încărcătorul trebuie să le ignore. Acoperă directorul în care se află plus toate subdirectoarele sub el. Vezi `.airflowignore` de mai jos pentru detalii despre sintaxa fișierului.

În cazul în care `.airflowignore` nu îndeplinește cerințele tale și dorești o modalitate mai flexibilă de a controla dacă un fișier Python trebuie să fie analizat de Airflow. Poți conecta funcția ta apelând `might_contain_dag_callable` în fișierul de configurare. Notă, această funcție apelabilă va înlocui euristica implicită Airflow, adică verificarea dacă șirurile airflow și dag se găsesc în fișier (fără a ține cont de sensibilitatea la majuscule/minusculă).

```python
def might_contain_dag(file_path: str, zip_file: zipfile.ZipFile | None = None) -> bool:
    # Your logic to check if there are DAGs defined in the file_path
    # Return True if the file_path needs to be parsed, otherwise False
```

## Rularea DAG-urilor

DAG-urile vor rula în una din cele două moduri:

1. Atunci când sunt declanșate manual sau prin intermediul API-ului
2. După un program definit, care este stabilit ca parte a DAG-ului

DAG-urile nu necesită un program, dar este foarte obișnuit să se definească unul. Îl definești prin argumentul `schedule`, astfel:

```python
with DAG("my_daily_dag", schedule="@daily"):
    ...  
```

Argumentul `schedule` acceptă orice valoare care este o valoare validă de program `Crontab`, așa că poți face și:

```python
with DAG("my_daily_dag", schedule="0 0 * * *"):
    ...
```

De fiecare dată când rulezi un DAG, creezi o nouă instanță a acelui DAG, pe care Airflow o numește un `Run` al DAG-ului (`DAG Run`). Execuțiile DAG pot rula în paralel pentru același DAG, iar fiecare are un interval de date definit, care identifică perioada de date asupra căreia task-urile ar trebui să opereze.

Ca exemplu pentru utilitatea acestui aspect, consideră scrierea unui DAG care procesează un set zilnic de date experimentale. A fost rescris, și vrei să-l rulezi pe ultimele 3 luni de date — nicio problemă, deoarece Airflow poate alimenta DAG-ul și să ruleze copii acestuia pentru fiecare zi din acele 3 luni anterioare, toate simultan.

Toate aceste `DAG Run`-uri vor fi pornite în aceeași zi reală, dar fiecare `DAG Run` va avea un interval de date care acoperă o singură zi în acea perioadă de 3 luni, iar acest interval de date este cel la care se uită toate `task`-urile, `operatorii` și `senzorii` din interiorul DAG-ului atunci când rulează.

În mod similar cu modul în care un DAG se instanțiază într-un `DAG Run` de fiecare dată când este rulat, `Task`-urile specificate într-un DAG sunt, de asemenea, instanțiate în **Instanțe de Task-uri** împreună cu acesta.

Un `DAG Run` va avea o dată de început (când începe) și o dată de sfârșit (când se termină). Această perioadă descrie momentul când DAG-ul a fost efectiv `rulat`. În afara datei de început și de sfârșit a `DAG Run`-ului, există o altă dată numită `dată logică` (cunoscută formal ca `date run`), care descrie momentul la care un `DAG Run` este **programată** sau **declanșată**. Motivul pentru care aceasta este numită `logică`, este datorită naturii sale abstracte, având multiple semnificații, în funcție de contextul `DAG Run`-ului în sine.

De exemplu, dacă un `DAG Run` este declanșat manual de către utilizator, data sa logică ar fi data și ora la care a fost declanșată `DAG Run`-ul, iar valoarea ar trebui să fie egală cu data de început a `DAG Run`. Cu toate acestea, atunci când DAG-ul este programat automat, cu un anumit interval de programare stabilit, data logică va indica momentul la care marchează începutul intervalului de date, unde data de început a `DAG Run`-ului va fi apoi `data logică + intervalul programat`.

## Alocare DAG
Reține că fiecare `Operator`/`Task` trebuie să fie asignat unui DAG pentru a putea fi rulat. Airflow are mai multe moduri de a calcula DAG-ul fără a-l pasa explicit:

1. Dacă declari Operatorul tău într-un bloc with DAG
2. Dacă declari Operatorul tău într-un decorator `@dag`
3. Dacă plasezi Operatorul tău în `upstream` sau în `downstream` de un Operator care are un DAG

În caz contrar, trebuie să-l pasezi fiecărui `Operator` cu argumentul `dag=`.

## Argumente implicite (Default Arguments)
De multe ori, multe Operatoare într-un DAG au nevoie de același set de argumente implicite (cum ar fi reîncercările lor). În loc să le specifici individual pentru fiecare `Operator`, poți să pasezi în schimb `default_args` la `DAG` atunci când îl creezi, iar acestea vor fi aplicate automat oricărui `operator` legat de el:

```python
import pendulum

with DAG(
    dag_id="my_dag",
    start_date=pendulum.datetime(2016, 1, 1),
    schedule="@daily",
    default_args={"retries": 2},
):
    op = BashOperator(task_id="hello_world", bash_command="Hello World!")
    print(op.retries)  # 2
```
## Decoaratorul DAG
Nou în versiunea 2.0.

Pe lângă metodele mai tradiționale de a declara un singur `DAG` folosind un `context manager` sau constructorul `DAG()`, poți de asemenea să decorezi o funcție cu `@dag` pentru a o transforma într-o funcție generator de DAG:


```python
@dag(
    schedule=None,
    start_date=pendulum.datetime(2021, 1, 1, tz="UTC"),
    catchup=False,
    tags=["example"],
)
def example_dag_decorator(email: str = "example@example.com"):
    """
    DAG to send server IP to email.

    :param email: Email to send IP to. Defaults to example@example.com.
    """
    get_ip = GetRequestOperator(task_id="get_ip", url="http://httpbin.org/get")

    @task(multiple_outputs=True)
    def prepare_email(raw_json: dict[str, Any]) -> dict[str, str]:
        external_ip = raw_json["origin"]
        return {
            "subject": f"Server connected from {external_ip}",
            "body": f"Seems like today your server executing Airflow is connected from IP {external_ip}<br>",
        }

    email_info = prepare_email(get_ip.output)

    EmailOperator(
        task_id="send_email", to=email, subject=email_info["subject"], html_content=email_info["body"]
    )


example_dag = example_dag_decorator()
```

Pe lângă faptul că este o nouă modalitate de a crea DAG-uri în mod curat, decoratorul configurează, de asemenea, orice parametri pe care îi ai în funcția ta ca parametri DAG, permițându-ți să setezi acei parametri atunci când declanșezi DAG-ul. Poți apoi accesa parametrii din codul Python sau din {{ `context.params` }} într-un șablon `Jinja`.

Airflow va încărca doar DAG-urile care apar în nivelul superior al unui fișier DAG. Aceasta înseamnă că nu poți doar să declari o funcție cu `@dag` - trebuie să o și apelezi cel puțin o dată în fișierul DAG și să o atribui unui obiect de nivel superior, așa cum poți vedea în exemplul de mai sus.

## Controlul Fluxului
În mod implicit, un DAG va rula un task doar atunci când toate task-urile de care depinde, sunt de succes. Există însă mai multe modalități de a modifica acest comportament:

- `Branching` - selecteaza care Task să treacă în funcție de o condiție;

- `Trigger rules` - stabilirea condițiilor în care un DAG va rula un task;

- `Setup and Teardown` - definirea relațiilor de setup și teardown;

- `Latest Only` - o formă specială de `branching` care rulează doar pe DAG-urile care rulează împotriva prezentului;

- `Depends On Past` - task-urile pot depinde de ele însele dintr-o rulare anterioară.

### Branching
Poți folosi `Branching` pentru a-i spune DAG-ului să nu ruleze toate Task-urile dependente, ci să aleagă în schimb una sau mai multe căi de a urma. Aici intră în joc decoratorul `@task.branch`.

Decoratorul `@task.branch` este foarte asemănător cu `@task`, cu excepția faptului că se așteaptă ca funcția decorată să returneze un ID către o task (sau o listă de ID-uri). Task-ul specificat este urmat, în timp ce toate celelalte căi sunt trecute cu vederea. Poate returna, de asemenea, `None` pentru a trece cu vederea toate task-urile în `downstream`.

`task_id` este returnat de funcția Python trebuie să facă referire la un task direct în `downstream` de task decorată cu `@task.branch`.


Când un task este `downstream` atât de **operatorul de branching**, cât și `downstream` de una sau mai multe dintre task-urile selectate, nu va fi trecută cu vederea:


![branch](https://airflow.apache.org/docs/apache-airflow/stable/_images/branch_note.png)


Caile task-ului de branching sunt `branch_a`, `join` și `branch_b`. Deoarece `join` este o task `downstream` a `branch_a`, totuși va fi rulată, chiar dacă nu a fost returnată ca parte a deciziei de branching.

Decoratorul `@task.branch` poate fi, de asemenea, folosit cu `XComs`, permițând contextului de branching să decidă dinamic ce ramură să urmeze în funcție de task-urile `upstream`. De exemplu:

```python
@task.branch(task_id="branch_task")
def branch_func(ti=None):
    xcom_value = int(ti.xcom_pull(task_ids="start_task"))
    if xcom_value >= 5:
        return "continue_task"
    elif xcom_value >= 3:
        return "stop_task"
    else:
        return None


start_op = BashOperator(
    task_id="start_task",
    bash_command="echo 5",
    do_xcom_push=True,
    dag=dag,
)

branch_op = branch_func()

continue_op = EmptyOperator(task_id="continue_task", dag=dag)
stop_op = EmptyOperator(task_id="stop_task", dag=dag)

start_op >> branch_op >> [continue_op, stop_op]
```

Dacă dorești să implementezi proprii tai operatori cu funcționalitate de branching, poți moșteni de la `BaseBranchOperator`, care se comportă similar cu decoratorul `@task.branch`, dar se așteaptă să furnizezi o implementare a metodei `choose_branch`.

Decoratorul `@task.branch` este recomandat în locul instanțierii directe a `BranchPythonOperator` într-un `DAG`. Acesta din urmă ar trebui, în general, să fie subclasat doar pentru a implementa un operator personalizat.

```python
class MyBranchOperator(BaseBranchOperator):
    def choose_branch(self, context):
        """
        Run an extra branch on the first day of the month
        """
        if context['data_interval_start'].day == 1:
            return ['daily_task_id', 'monthly_task_id']
        elif context['data_interval_start'].day == 2:
            return 'daily_task_id'
        else:
            return None
```

Similar cu decoratorul `@task.branch` pentru codul Python obișnuit, există și decoratori de branching care utilizează un mediu virtual numit `@task.branch_virtualenv` sau Python extern numit `@task.branch_external_python`.

## Latest only
De multe ori, DAG-urile în Airflow sunt rulate pentru o dată care nu este aceeași cu data curentă - de exemplu, rulează o copie a unui DAG pentru fiecare zi din ultima lună pentru a încărca unele date.

Există situații, totuși, în care nu vrei să lași să ruleze unele (sau toate) părțile unui DAG pentru o dată anterioară; în acest caz, poți folosi `LatestOnlyOperator`.

Acest `Operator` special sare peste toate task-urile în aval dacă nu te afli în "ultima" rulare a DAG-ului (dacă timpul curent este între `execution_time` și următoarea `execution_time` programată, și nu a fost o rulare declanșată extern).

```python
import datetime

import pendulum

from airflow.models.dag import DAG
from airflow.operators.empty import EmptyOperator
from airflow.operators.latest_only import LatestOnlyOperator
from airflow.utils.trigger_rule import TriggerRule

with DAG(
    dag_id="latest_only_with_trigger",
    schedule=datetime.timedelta(hours=4),
    start_date=pendulum.datetime(2021, 1, 1, tz="UTC"),
    catchup=False,
    tags=["example3"],
) as dag:
    latest_only = LatestOnlyOperator(task_id="latest_only")
    task1 = EmptyOperator(task_id="task1")
    task2 = EmptyOperator(task_id="task2")
    task3 = EmptyOperator(task_id="task3")
    task4 = EmptyOperator(task_id="task4", trigger_rule=TriggerRule.ALL_DONE)

    latest_only >> task1 >> [task3, task4]
    task2 >> [task3, task4]
```
În cazul acestui DAG:
- `task1` este direct în aval de `latest_only` și va fi trecut cu vederea pentru toate rulările cu excepția celei mai recente.
- `task2` este complet independent de `latest_only` și va rula în toate perioadele programate.
- `task3` este în aval de `task1` și `task2` și datorită regulii implicite de declanșare `all_success` va primi un `skip` cascaded de la `task1`.
- `task4` este în aval de `task1` și `task2`, dar nu va fi trecut cu vederea, deoarece regula de declanșare este setată la `all_done`.

![latestonly](https://airflow.apache.org/docs/apache-airflow/stable/_images/latest_only_with_trigger.png)


### Depends On Past
----------------

Poți spune, de asemenea, că un task poate fi rulat doar dacă rularea anterioară a task-ului în `DAG Run`-ul anterior a avut succes. Pentru a utiliza aceasta, trebuie doar să setezi argumentul `depends_on_past` al task-urii tale la `True`.

Reține că, dacă rulezi DAG-ul la începutul vieții sale - în special, la prima sa rulare automată vreodată - atunci task-ul tot va rula, deoarece nu există nicio rulare anterioară de care să depindă.

### Trigger Rules
----------------

În mod implicit, Airflow va aștepta ca toate task-urile `upstream` (părinții direcți) pentru un task să aibă succes înainte de a rula acel task.

Cu toate acestea, aceasta este doar comportamentul implicit și îl poți controla folosind argumentul `trigger_rule` pentru un task. Opțiunile pentru `trigger_rule` sunt:

| **`Trigger Rule`** | **`Descriere`** |
| ---------------- | -------------- |
| `all_success` (implicit) | Toate task-urile upstream au avut succes. |
| `all_failed` | Toate task-urile upstream sunt într-o stare de eșec sau upstream_failed. |
| `all_done` | Toate task-urile upstream au terminat execuția. |
| `all_skipped` | Toate task-urile upstream sunt într-o stare de trecere cu vederea. |
| `one_failed` | Cel puțin un task upstream a eșuat (nu așteaptă ca toate task-urile upstream să se termine). |
| `one_success` | Cel puțin un task upstream a avut succes (nu așteaptă ca toate task-urile upstream să se termine). |
| `one_done` | Cel puțin un task upstream a avut succes sau a eșuat. |
| `none_failed` | Toate task-urile upstream nu au eșuat sau sunt în `upstream_failed` - adică, toate task-urile upstream au avut succes sau au fost trecute cu vederea. |
| `none_failed_min_one_success` | Toate task-urile upstream nu au eșuat sau sunt în `upstream_failed`, și cel puțin un task upstream a avut succes. |
| `none_skipped` | Niciun task upstream nu este într-o stare de trecere cu vederea - adică, toate task-urile upstream sunt într-o stare de succes, eșec sau `upstream_failed`. |
| `always` | Fără dependențe deloc, rulează aceast task în orice moment. |


Poți, de asemenea, combina aceasta cu funcționalitatea `Depends On Past` dacă dorești.

Este important să fim conștienți de interacțiunea dintre regulile de declanșare și task-urile trecute cu vederea, în special task-urile care sunt trecute cu vederea în cadrul unei operațiuni de branching. Cu puține excepții, nu dorim să utilizăm `all_success` sau `all_failed` în avalul unei operațiuni de branching.

Task-urile trecute cu vederea vor fi propagate prin regulile de declanșare `all_success` și `all_failed`, determinându-le să fie trecute cu vederea, de asemenea. Să luăm în considerare următorul DAG:

```python
# dags/branch_without_trigger.py
import pendulum

from airflow.decorators import task
from airflow.models import DAG
from airflow.operators.empty import EmptyOperator

dag = DAG(
    dag_id="branch_without_trigger",
    schedule="@once",
    start_date=pendulum.datetime(2019, 2, 28, tz="UTC"),
)

run_this_first = EmptyOperator(task_id="run_this_first", dag=dag)


@task.branch(task_id="branching")
def do_branching():
    return "branch_a"


branching = do_branching()

branch_a = EmptyOperator(task_id="branch_a", dag=dag)
follow_branch_a = EmptyOperator(task_id="follow_branch_a", dag=dag)

branch_false = EmptyOperator(task_id="branch_false", dag=dag)

join = EmptyOperator(task_id="join", dag=dag)

run_this_first >> branching
branching >> branch_a >> follow_branch_a >> join
branching >> branch_false >> join
```

`join` este `downstream`-ul lui `follow_branch_a` și `branch_false`. Task-ul `join` va apărea ca fiind trecută cu vederea pentru că regulă de declanșare implicită este setată la `all_success`, iar trecerea cu vederea cauzată de operațiunea de branching se propagă în jos pentru a omite un task marcat ca `all_success`.

![dag](https://airflow.apache.org/docs/apache-airflow/stable/_images/branch_without_trigger.png)

Prin setarea regulii de declanșare la `none_failed_min_one_success` în task-ul `join`, putem obține comportamentul dorit:


![dag](https://airflow.apache.org/docs/apache-airflow/stable/_images/branch_with_trigger.png)

## Configurare și dezinstalare
În fluxurile de lucru de date este obișnuit să creați o resursă (cum ar fi o resursă de calcul), să o utilizați pentru a efectua o anumită activitate și apoi să o dezinstalați. Airflow oferă task-uri de `configurare` și `dezinstalare` pentru a susține această nevoie.

## DAG-uri dinamice
Deoarece un DAG este definit de codul Python, nu este nevoie să fie pur declarativ; sunteți liber să utilizați loop-uri, funcții și altele pentru a defini DAG-ul.

De exemplu, iată un DAG care folosește un `for loop` pentru a defini unele task-uri:

```python
 with DAG("loop_example", ...):
     first = EmptyOperator(task_id="first")
     last = EmptyOperator(task_id="last")

     options = ["branch_a", "branch_b", "branch_c", "branch_d"]
     for option in options:
         t = EmptyOperator(task_id=option)
         first >> t >> last
```
În general, vă sfătuim să încercați să mențineți topologia (configurația) task-urilor din DAG relativ stabilă; **DAG-urile dinamice** sunt de obicei mai bine folosite pentru încărcarea dinamică a opțiunilor de configurare sau modificarea opțiunilor operatorilor.

## Vizualizarea DAG-urilor
Dacă doriți să vizualizați o reprezentare grafică a unui DAG, aveți două opțiuni:

1. Puteți deschide interfața utilizator Airflow, navigați la DAG-ul dvs. și selectați "`Graph`"
2. Puteți rula comanda `airflow dags show`, care o afișează sub formă de fișier imagine

În general, vă recomandăm să utilizați vederea `Graph`, deoarece vă va arăta și starea tuturor instanțelor de task-uri în cadrul oricărei rulări a DAG-ului pe care o selectați.

Bineînțeles, pe măsură ce dezvoltați DAG-urile, acestea vor deveni tot mai complexe, așa că oferim câteva modalități de modificare a acestor vizualizări ale DAG-urilor pentru a le face mai ușor de înțeles.

## Grupuri de task-uri (TaskGroups)
Un `TaskGroup` poate fi utilizat pentru a organiza task-urile în grupuri ierarhice în vizualizarea `Graph`. Este util pentru crearea de modele repetitive și reducerea aglomerației vizuale.

Spre deosebire de SubDAG-uri, `TaskGroups` sunt pur și simplu un concept de grupare UI. Task-urile din `TaskGroups` se află în același DAG original și respectă toate setările DAG și configurațiile de pool.

![gif](https://airflow.apache.org/docs/apache-airflow/stable/_images/task_group.gif)


Relațiile de dependență pot fi aplicate pentru toate task-urile dintr-un `TaskGroup` cu operatorii `>>` și `<<`. De exemplu, următorul cod plasează `task1` și `task2` în `TaskGroup` group1 și apoi pune ambele task-uri în amonte de `task3`:

```python
 from airflow.decorators import task_group


 @task_group()
 def group1():
     task1 = EmptyOperator(task_id="task1")
     task2 = EmptyOperator(task_id="task2")


 task3 = EmptyOperator(task_id="task3")

 group1() >> task3
```

`TaskGroup` suportă, de asemenea, `default_args` ca DAG, acesta va suprascrie `default_args` la nivelul DAG-ului:

```python
import datetime

from airflow import DAG
from airflow.decorators import task_group
from airflow.operators.bash import BashOperator
from airflow.operators.empty import EmptyOperator

with DAG(
    dag_id="dag1",
    start_date=datetime.datetime(2016, 1, 1),
    schedule="@daily",
    default_args={"retries": 1},
):

    @task_group(default_args={"retries": 3})
    def group1():
        """This docstring will become the tooltip for the TaskGroup."""
        task1 = EmptyOperator(task_id="task1")
        task2 = BashOperator(task_id="task2", bash_command="echo Hello World!", retries=2)
        print(task1.retries)  # 3
        print(task2.retries)  # 2
```

Dacă dorești să vezi o utilizare mai avansată a `TaskGroup`, poți să te uiți la exemplul `example_task_group_decorator.py` care vine cu Airflow.

### Nota

În mod implicit, `child tasks/TaskGroups` au ID-urile prefixate cu `group_id` al TaskGroup părinte. Acest lucru ajută la asigurarea unicității `group_id` și `task_id` în întregul DAG.

Pentru a dezactiva prefixarea, treci `prefix_group_id=False` la crearea `TaskGroup`, dar reține că acum vei fi responsabil pentru asigurarea unicității fiecărei task și grup.

Când folosești decorarea `@task_group`, docstring-ul funcției decorate va fi folosit ca o sugestie de ecran în UI pentru `TaskGroup`, cu excepția cazului în care se furnizează în mod explicit o valoare pentru sugestie.


### Edge Labels
Pe lângă gruparea task-urilor în grupuri, poți eticheta, de asemenea, muchiile de dependență dintre diferite task-uri în vizualizarea grafică - acest lucru poate fi deosebit de util pentru zonele de branching ale DAG-ului tău, astfel încât să poți eticheta condițiile sub care anumite branch-uri ar putea rula.

Pentru a adăuga etichete, le poți utiliza direct încorporate cu operatorii `>>` și `<<`:


```python
from airflow.utils.edgemodifier import Label

my_task >> Label("When empty") >> other_task
```

Sau, poți furniza un obiect `Label` pentru `set_upstream/set_downstream`:

```python
from airflow.utils.edgemodifier import Label

my_task.set_downstream(other_task, Label("When empty"))
```

![xsx](https://airflow.apache.org/docs/apache-airflow/stable/_images/edge_label_example.png)

```python
with DAG(
    "example_branch_labels",
    schedule="@daily",
    start_date=pendulum.datetime(2021, 1, 1, tz="UTC"),
    catchup=False,
) as dag:
    ingest = EmptyOperator(task_id="ingest")
    analyse = EmptyOperator(task_id="analyze")
    check = EmptyOperator(task_id="check_integrity")
    describe = EmptyOperator(task_id="describe_integrity")
    error = EmptyOperator(task_id="email_error")
    save = EmptyOperator(task_id="save")
    report = EmptyOperator(task_id="report")

    ingest >> analyse >> check
    check >> Label("No errors") >> save >> report
    check >> Label("Errors found") >> describe >> error >> report
```

**Documentare DAG și Sarcini**
Este posibil să adaugi documentare sau note la DAG-urile și obiectele de task-uri care sunt vizibile în interfața web ("`Graph`" și "`Tree`" pentru DAG-uri, "**Task Instance Details**" pentru task-uri).

Există un set de atribute speciale pentru task-uri care sunt afișate ca conținut bogat dacă sunt definite:

| Atribut | Renderează la |  
| ------- | ------------ |  
| `doc` | monospace |  
| `doc_json` | JSON |  
| `doc_yaml` | YAML |  
| `doc_md` | Markdown |  
| `doc_rst` | reStructuredText |  

Rețineți că pentru DAG-uri, `doc_md` este singurul atribut interpretat. Pentru DAG-uri, acesta poate conține un șir de caractere sau referința către un fișier de tip șablon. Referințele către șabloane sunt recunoscute prin șirul care se încheie în `.md`. Dacă este furnizat un traseu relativ, acesta va începe din dosarul fișierului DAG. De asemenea, fișierul șablon trebuie să existe, altfel Airflow va genera o excepție `jinja2.exceptions.TemplateNotFound`.

Acest lucru este util în special dacă task-urile tale sunt create dinamic din fișiere de configurare, deoarece îți permite să expui configurarea care a condus la task-urile relevante în Airflow.

```python
"""
### My great DAG
"""
import pendulum

dag = DAG(
    "my_dag",
    start_date=pendulum.datetime(2021, 1, 1, tz="UTC"),
    schedule="@daily",
    catchup=False,
)
dag.doc_md = __doc__

t = BashOperator("foo", dag=dag)
t.doc_md = """\
#Title"
Here's a [url](www.airbnb.com)
"""
```

## SubDAG's

`SubDAG`-urile sunt deprecate, prin urmare, `TaskGroup` este întotdeauna opțiunea preferată.

Uneori, vei constata că adaugi în mod regulat exact aceeași serie de task-uri la fiecare DAG sau vrei să grupezi multe task-uri într-o singură unitate logică. Acesta este rolul `SubDAG`-urilor.

De exemplu, iată un DAG care are multe task-uri paralele în două secțiuni:

![subdag](https://airflow.apache.org/docs/apache-airflow/stable/_images/subdag_before.png)

Putem combina toate operatorii paraleli task-* într-un singur SubDAG, astfel încât DAG-ul rezultat să semene cu cel de mai jos:

![subdag](https://airflow.apache.org/docs/apache-airflow/stable/_images/subdag_after.png)

#### Rețineți că operatorii SubDAG ar trebui să conțină o metodă default care returnează un obiect DAG. Acest lucru va împiedica tratarea SubDAG-ului ca pe un DAG separat în interfața principală - amintește-ți că, dacă Airflow vede un DAG la nivelul superior al unui fișier Python, îl va încărca ca pe propriul său DAG. De exemplu:

```python
import pendulum

from airflow.models.dag import DAG
from airflow.operators.empty import EmptyOperator


def subdag(parent_dag_name, child_dag_name, args) -> DAG:
    """
    Generate a DAG to be used as a subdag.

    :param str parent_dag_name: Id of the parent DAG
    :param str child_dag_name: Id of the child DAG
    :param dict args: Default arguments to provide to the subdag
    :return: DAG to use as a subdag
    """
    dag_subdag = DAG(
        dag_id=f"{parent_dag_name}.{child_dag_name}",
        default_args=args,
        start_date=pendulum.datetime(2021, 1, 1, tz="UTC"),
        catchup=False,
        schedule="@daily",
    )

    for i in range(5):
        EmptyOperator(
            task_id=f"{child_dag_name}-task-{i + 1}",
            default_args=args,
            dag=dag_subdag,
        )

    return dag_subdag
```

Acest `SubDAG` poate apoi fi referențiat în fișierul principal al DAG-ului tău:

```python
import datetime

from airflow.example_dags.subdags.subdag import subdag
from airflow.models.dag import DAG
from airflow.operators.empty import EmptyOperator
from airflow.operators.subdag import SubDagOperator

DAG_NAME = "example_subdag_operator"

with DAG(
    dag_id=DAG_NAME,
    default_args={"retries": 2},
    start_date=datetime.datetime(2022, 1, 1),
    schedule="@once",
    tags=["example"],
) as dag:
    start = EmptyOperator(
        task_id="start",
    )

    section_1 = SubDagOperator(
        task_id="section-1",
        subdag=subdag(DAG_NAME, "section-1", dag.default_args),
    )

    some_other_task = EmptyOperator(
        task_id="some-other-task",
    )

    section_2 = SubDagOperator(
        task_id="section-2",
        subdag=subdag(DAG_NAME, "section-2", dag.default_args),
    )

    end = EmptyOperator(
        task_id="end",
    )

    start >> section_1 >> some_other_task >> section_2 >> end
```

Poți să faci zoom pe un `SubDagOperator` din vizualizarea grafică a DAG-ului principal pentru a vedea task-urile conținute în `SubDAG`:

![gdag](https://airflow.apache.org/docs/apache-airflow/stable/_images/subdag_zoom.png)

Câteva sfaturi suplimentare când folosești SubDAGs:

- Prin convenție, id-ul unui `SubDAG` ar trebui să aibă un prefix format din numele DAG-ului principal și un punct (parinte.copil)
- Ar trebui să partajezi argumente între DAG-ul principal și `SubDAG` prin transmiterea acestora către operatorul `SubDAG` (așa cum este demonstrat mai sus)
- `SubDAGs` trebuie să aibă un program și să fie activate. Dacă programul `SubDAG`-ului este setat la `None` sau `@once`, `SubDAG`-ul va avea succes fără să facă nimic.
- Curățarea unui `SubDagOperator` curăță și starea task-urilor din interiorul său.
- Marcarea succesului pe un `SubDagOperator` nu afectează starea task-urilor din interiorul său.
- Abține-te să folosești `Depends On Past` în task-urile din interiorul `SubDAG`-ului, deoarece acest lucru poate fi confuz.
- Poți specifica un executor pentru `SubDAG`. Este obișnuit să folosești `SequentialExecutor` dacă vrei să rulezi `SubDAG`-ul în proces și să îi limitezi eficient paralelismul la unul. Folosirea `LocalExecutor` poate fi problematică, deoarece poate suprasolicita worker-ul, rulând mai multe task-uri într-un singur slot.


#### Note

`Paralelismul` nu este respectat de `SubDagOperator`, astfel că resursele ar putea fi consumate de `SubdagOperators` dincolo de orice limite ai putea seta.

## TaskGroups și SubDAGs 

**SubDAGs**, deși au un scop similar, introduc atât probleme de performanță, cât și probleme funcționale din cauza implementării lor.

- `SubDagOperator` pornește un `BackfillJob`, care ignoră configurațiile existente de paralelism, putând supraabona mediul de lucru.

- `SubDAGs` au propriile atribute `DAG`. Atunci când atributele `DAG` ale `SubDAG` sunt inconsistente cu cele ale părintelui său, pot apărea comportamente neașteptate.

- Nu se poate vedea "întreaga" DAG într-o singură vedere, deoarece `SubDAGs` există ca o `DAG` completă.

- `SubDAGs` introduc tot felul de cazuri și avertismente speciale. Acest lucru poate perturba experiența și așteptările utilizatorilor.

`TaskGroups`, pe de altă parte, reprezintă o opțiune mai bună, având în vedere că este doar un concept de grupare în interfața utilizatorului. Toate task-urile din `TaskGroup` se comportă încă ca oricare alte task-uri în afara `TaskGroup`.

Poți observa diferențele cheie între aceste două construcții.

**TaskGroup**

- Modele repetitive ca parte a aceluiași DAG
- Un set de vederi și statistici pentru DAG
- Un set de configurări DAG
- Onorează configurațiile de paralelism prin `SchedulerJob` existent
- Declarație simplă a construcției cu context manager

**SubDAG**

- Modele repetitive ca un DAG separat
- Set separat de vederi și statistici între DAG-urile părinte și copil
- Mai multe seturi de configurări DAG
- Nu onorează configurațiile de paralelism din cauza `BackfillJob` nou generat
- Fabrică DAG complexă cu restricții de denumire


## Ambalarea DAG-urilor

În timp ce DAG-urile mai simple sunt de obicei într-un singur fișier Python, nu este neobișnuit ca DAG-urile mai complexe să fie răspândite în mai multe fișiere și să aibă dependențe care ar trebui să fie incluse cu ele ("vendorate").

Puteți face acest lucru fie în `DAG_FOLDER`, cu o structură standard a sistemului de fișiere, fie puteți împacheta DAG-ul și toate fișierele sale Python ca un singur fișier zip. De exemplu, ați putea trimite două DAG-uri împreună cu o dependență de care au nevoie într-un fișier zip cu următorul conținut:


```python
my_dag1.py
my_dag2.py
package1/__init__.py
package1/functions.py
```

### Rețineți că DAG-urile împachetate vin cu câteva avertismente:

- Nu pot fi folosite dacă aveți activată `serializarea` prin `pickling`.
- Nu pot conține biblioteci compilate (de exemplu, `libz.so`), doar Python pur.
- Vor fi introduse în `sys.path` al lui Python și pot fi importate de orice alt cod din procesul Airflow, așa că asigurați-vă că numele pachetelor nu intră în conflict cu alte pachete deja instalate în sistemul dvs.

În general, dacă aveți un set complex de dependențe și module compilate, este probabil mai bine să utilizați sistemul Python `virtualenv` și să instalați pachetele necesare pe sistemele țintă cu ajutorul lui `pip`.


Un fișier `.airflowignore` specifică directoarele sau fișierele din `DAG_FOLDER` sau `PLUGINS_FOLDER` pe care Airflow intenționează să le ignore. Airflow acceptă două variante de sintaxă pentru modelele din fișier, așa cum este specificat de parametrul de configurare `DAG_IGNORE_FILE_SYNTAX` (adăugat în Airflow 2.3): `regexp` și `glob`.

### Nota

Sintaxa implicită pentru `DAG_IGNORE_FILE_SYNTAX` este `regexp` pentru a asigura compatibilitatea înapoi.

Pentru sintaxa tipului `regexp` (implicit), fiecare linie din `.airflowignore` specifică un șablon de expresie regulată, iar directoarele sau fișierele ale căror nume (nu ID-ul DAG) se potrivesc cu oricare dintre șabloane vor fi ignorate (in background, se folosește `Pattern.search()` pentru a potrivi șablonul). Utilizați caracterul `#` pentru a indica un comentariu; toate caracterele de pe o linie care urmează unui `#` vor fi ignorate.

Pentru majoritatea potrivirilor de tip `regexp` în Airflow, motorul de expresii regulate este `re2`, care nu suportă explicit multe funcționalități avansate, vă rugăm să consultați documentația sa pentru mai multe informații.

Cu sintaxa `glob`, șabloanele funcționează la fel ca într-un fișier `.gitignore`:

- Caracterul `*` se potrivește cu orice număr de caractere, cu excepția `/`
- Caracterul `?` se potrivește cu orice caracter singular, cu excepția `/`
- Notația pentru interval, de exemplu [a-zA-Z], poate fi utilizată pentru a se potrivi cu unul dintre caracterele dintr-un interval
- Un șablon poate fi negat prin prefixare cu `!`. Șabloanele sunt evaluate în ordine, astfel încât o negare poate anula un șablon definit anterior în același fișier sau șabloane definite într-un director părinte.
- Două asteriscuri (`**`) pot fi utilizate pentru a face potriviri în întregul arbore de directoare. De exemplu, `**/__pycache__/` va ignora directoarele `__pycache__` în fiecare subdirector la o adâncime infinită.
- Dacă există un `/` la început sau în mijloc (sau ambele) ale șablonului, atunci șablonul este relativ la nivelul directorului particular .`airflowignore` în sine. În caz contrar, șablonul se poate potrivi și la orice nivel sub nivelul .`airflowignore`.

Fișierul .`airflowignore` ar trebui plasat în `DAG_FOLDER`. De exemplu, puteți pregăti un fișier .`airflowignore` folosind sintaxa regexp cu conținut:


```glob
project_a
tenant_[\d]
```

Sau, echivalent, în sintaxa `glob`


```glob
**/*project_a*
tenant_[0-9]*
```

Apoi, fișierele precum `project_a_dag_1.py`, `TESTING_project_a.py`, `tenant_1.py`, `project_a/dag_1.py` și `tenant_1/dag_1.py` din `DAG_FOLDER `vor fi ignorate (dacă numele unui director se potrivește cu oricare dintre șabloane, acest director și toate subdirectoarele sale nu vor fi scanate deloc de către Airflow. Acest lucru îmbunătățește eficiența găsirii DAG).

Domeniul de aplicare al unui fișier `.airflowignore` este directorul în care se află, plus toate subdirectoarele sale. Puteți pregăti, de asemenea, un fișier `.airflowignore` pentru un subfolder din `DAG_FOLDER` și acesta va fi aplicabil doar pentru acel subfolder.

## Dependente între DAG-uri
`Adăugat în Airflow 2.1`

În timp ce dependențele între task-urile dintr-un DAG sunt definite în mod explicit prin relațiile de `down` și `up`, dependențele între DAG-uri sunt puțin mai complexe. În general, există două moduri în care un DAG poate depinde de altul:

- declanșarea - `TriggerDagRunOperator`
- așteptarea - `ExternalTaskSensor`

O dificultate suplimentară este că un DAG ar putea să aștepte sau să declanșeze mai multe rulări ale celuilalt DAG cu intervale de date diferite. Meniul Vizualizare dependențe DAG -> Răsfoire -> Dependințe DAG ajută la vizualizarea dependențelor dintre DAG-uri. Dependințele sunt calculate de planificator în timpul serializării DAG și serverul web le folosește pentru a construi graful de dependențe.

Detectorul de dependențe este configurabil, astfel încât puteți implementa propria logică diferită de cea implicită în `DependencyDetector`.

## Pauzarea, Dezactivarea și Ștergerea DAG-urilor

DAG-urile au mai multe stări când nu rulează. DAG-urile pot fi puse pe pauză, dezactivate și, în final, toate metadatele pentru DAG pot fi șterse.


Un DAG poate fi pus pe pauză prin intermediul UI-ului atunci când este prezent în `DAGS_FOLDER`, iar planificatorul îl salvează în baza de date, dar utilizatorul alege să-l dezactiveze prin intermediul UI-ului. Acțiunile "`pause`" și "`unpause`" sunt disponibile atât prin UI, cât și prin API. Un DAG pus pe `pause` nu este programat de planificator, dar îl puteți declanșa prin UI pentru rulări manuale. În UI, puteți vedea DAG-urile puse pe pauză (în fila Puse pe pauză). DAG-urile care nu sunt pe pauză pot fi găsite în fila Activ.

Un DAG poate fi dezactivat (nu îl confundați cu eticheta `Active` în UI) prin eliminarea sa din `DAGS_FOLDER`. Când planificatorul parsează `DAGS_FOLDER` și nu găsește DAG-ul pe care l-a văzut anterior și l-a salvat în baza de date, îl va seta ca **dezactivat**. Metadatele și istoricul DAG-ului sunt păstrate pentru DAG-urile dezactivate, iar când DAG-ul este adăugat din nou în `DAGS_FOLDER`, acesta va fi din nou activat, iar istoricul va fi vizibil. Nu puteți `activa/dezactiva` un DAG prin intermediul UI-ului sau API-ului, acest lucru poate fi făcut doar prin eliminarea fișierelor din `DAGS_FOLDER`. Încă o dată - niciun `data` pentru rulările istorice ale DAG-ului nu sunt pierdute atunci când este dezactivat de către planificator. Notați că fila `Activ` în interfața de utilizare Airflow se referă la DAG-uri care nu sunt în același timp activate și ne-puse pe pauză, astfel că acest lucru poate fi inițial puțin confuz.

Nu puteți vedea DAG-urile dezactivate în UI - uneori puteți vedea rulările istorice, dar atunci când încercați să vizualizați informații despre acestea, veți vedea eroarea că DAG-ul lipsește.

De asemenea, puteți șterge metadatele DAG-ului din baza de date de metadate folosind UI-ul sau API-ul, dar acest lucru nu duce întotdeauna la dispariția DAG-ului din UI - ceea ce poate fi, de asemenea, inițial puțin confuz. Dacă DAG-ul este încă în `DAGS_FOLDER` atunci când ștergeți metadatele, DAG-ul va reapărea deoarece planificatorul va parsa folderul, doar informațiile despre rulările istorice pentru DAG vor fi eliminate.

Toate acestea înseamnă că dacă doriți să ștergeți efectiv un DAG și toate metadatele sale istorice, trebuie să urmați acești pași:

1. Puneți DAG-ul pe pauză.
2. Ștergeți metadatele istorice din baza de date, prin intermediul UI-ului sau API-ului.
3. Ștergeți fișierul DAG din `DAGS_FOLDER` și așteptați până când devine inactiv.

## DAG Runs

Un `DAG Run` este un obiect care reprezintă o instanțiere a DAG-ului într-un moment dat. Ori de câte ori DAG-ul este executat, este creată o DAG Run și toate task-urile din interiorul său sunt executate. 

Starea `DAG Run` depinde de stările task-urilor. Fiecare DAG Run este rulat separat de celelalte, ceea ce înseamnă că puteți avea multe rulări ale unui DAG în același timp.

### Starea Rulării DAG

Starea unei DAG Run este determinată atunci când execuția DAG-ului este finalizată. Execuția DAG-ului depinde de task-urile sale și de dependențele acestora. Starea este atribuită DAG Run atunci când toate task-urile se află într-una dintre stările terminale (adică dacă nu există o tranziție posibilă către o altă stare), cum ar fi `success`, `failed` sau `skipped`. Starea unei DAG Run este atribuită pe baza a ceea ce se numește "`leaf nodes`" sau simplu "`leaves`". `Leaf Nodes` sunt task-urile fără copii.


### Există două stări terminale posibile pentru DAG Run:

- **success** dacă toate stările a leaf nodes sunt fie `success`, fie `skipped`;

- **failed** dacă oricare dintre stările leaf nodes este fie `failed`, fie `upstream_failed`.

**Notă**

Fii atent dacă unele dintre task-urile tale au definite reguli de declanșare specifice. Acestea pot duce la un comportament neașteptat, de exemplu, dacă ai un `leaf task` cu regulă de declanșare "`all_done`", ea va fi executată indiferent de stările celorlalte task-uri, iar dacă va reuși, întreaga DAG Run va fi marcată ca `success`, chiar dacă ceva a eșuat pe parcurs.

`Adăugat în Airflow 2.7`

DAG-urile care au o DAG Run în desfășurare pot fi afișate pe tabloul de bord al interfeței de utilizator în fila "`Running`". Similar, DAG-urile al căror ultim DAG Run este marcat ca eșuat pot fi găsite în fila "`Failed`".

### Presete Cron

Puteți seta DAG-ul să ruleze pe un schedule simplu setând argumentul său de `schedule` la o `expresie cron`, un obiect `datetime.timedelta` sau la unul dintre următoarele "`preseturi`" `cron`. Pentru cerințe de programare mai elaborate, puteți implementa un program personalizat. 

`Notați` că Airflow parsează expresiile cron cu ajutorul bibliotecii croniter, care acceptă o sintaxă extinsă pentru șirurile cron. De exemplu, puteți crea un program DAG să ruleze la 12 noaptea în prima zi de luni a lunii cu sintaxa cron extinsă: `0 0 * * MON#1`.


| Preset      | Semnificație                                               | Expresie Cron | 
|-------------|------------------------------------------------------------|---------------| 
| `None`      | Nu programați, utilizați pentru DAG-urile exclusiv „externally triggered” | -             | 
| `@once`     | Programați o singură dată și numai o dată                      | -             | 
| `@continuous`| Rulează imediat ce se termină rularea anterioară               | -             | 
| `@hourly`   | Rulează o dată pe oră, la sfârșitul orei                       | `0 * * * *`   | 
| `@daily`    | Rulează o dată pe zi la miezul nopții (24:00)                  | `0 0 * * *`   | 
| `@weekly`   | Rulează o dată pe săptămână la miezul nopții (24:00) în ziua de duminică | `0 0 * * 0`   | 
| `@monthly`  | Rulează o dată pe lună la miezul nopții (24:00) în prima zi a lunii | `0 0 1 * *`   | 
| `@quarterly`| Rulează o dată la un sfert la miezul nopții (24:00) în prima zi a trimestrului | `0 0 1 */3 *` | 
| `@yearly`   | Rulează o dată pe an la miezul nopții (24:00) în 1 ianuarie    | `0 0 1 1 *`   | 


## Programare și Interval de Date

Fiecare rulare a DAG-ului în Airflow are un "interval de date" asignat, care reprezintă intervalul de timp în care operează. Pentru un DAG programat cu `@daily`, de exemplu, fiecare interval de date începe în fiecare zi la miezul nopții (00:00) și se încheie la miezul nopții (24:00).

O rulare a DAG-ului este de obicei programată după ce intervalul de date asociat s-a încheiat, pentru a se asigura că rularea este capabilă să colecteze toate datele în timpul perioadei de timp. Cu alte cuvinte, o rulare care acoperă perioada de date 2020-01-01 de obicei nu începe să ruleze decât după ce s-a încheiat 2020-01-02 00:00:00.

Toate datele în Airflow sunt legate de conceptul de interval de date într-un fel. "Data logică" (numită și `execution_date` în versiunile Airflow anterioare versiunii 2.2) a unei rulări a DAG-ului, de exemplu, indică începutul intervalului de date, nu momentul când DAG-ul este efectiv executat.

La fel, deoarece argumentul `start_date` pentru DAG și task-urile sale arată către aceeași dată logică, marchează începutul primului interval de date al DAG-ului, nu când încep să ruleze task-urile în DAG. Cu alte cuvinte, o rulare a DAG-ului va fi programată numai un interval după `start_date`.

## Re-run DAG
Pot exista cazuri în care veți dori să executați din nou DAG. Un astfel de caz este atunci când rularea DAG programată eșuează.

### Catchup
Un DAG Airflow definit cu un `start_date`, eventual o `end_date` și un program care nu este un set de date, definește o serie de intervale pe care planificatorul le transformă în DAG individual, care rulează și le execută. Planificatorul, în mod implicit, va lansa o rulare DAG pentru orice interval de date care nu a fost rulat de la ultimul interval de date (sau a fost șters). Acest concept se numește `Catchup`.

Dacă DAG-ul dvs. nu este scris pentru a-și gestiona recuperarea (adică, nu se limitează la interval, ci în schimb la Acum, de exemplu), atunci veți dori să dezactivați recuperarea. Acest lucru se poate face setând `catchup=False` în DAG sau `catchup_by_default=False` în fișierul de configurare. Când este dezactivat, planificatorul creează o rulare DAG numai pentru cel mai recent interval.

```python
"""
Code that goes along with the Airflow tutorial located at:
https://github.com/apache/airflow/blob/main/airflow/example_dags/tutorial.py
"""
from airflow.models.dag import DAG
from airflow.operators.bash import BashOperator

import datetime
import pendulum

dag = DAG(
    "tutorial",
    default_args={
        "depends_on_past": True,
        "retries": 1,
        "retry_delay": datetime.timedelta(minutes=3),
    },
    start_date=pendulum.datetime(2015, 12, 1, tz="UTC"),
    description="A simple tutorial DAG",
    schedule="@daily",
    catchup=False,
)
```

În exemplul de mai sus, dacă DAG este preluat de scheduler daemon pe 2016-01-02 la 6 AM, (sau din linia de comandă), va fi creată un singur `DAG Run` cu date între 2016-01-01 și 2016-01-02, iar următorul va fi creat imediat după miezul nopții în dimineața zilei de 2016-01-03 cu un interval de date între 2016-01-02 și 2016-01-03.

Rețineți că utilizarea unui obiect `datetime.timedelta` ca program poate duce la un comportament diferit. Într-un astfel de caz, singurul DAG Run creat va acoperi date între 2016-01-01 06:00 și 2016-01-02 06:00 (un interval de program care se termină acum). Pentru o descriere mai detaliată a diferențelor dintre un program cron și un program bazat pe delta, aruncați o privire la comparația orarelor

Dacă valoarea `dag.catchup` ar fi fost `True`, planificatorul ar fi creat o Execuție DAG pentru fiecare interval finalizat între 2015-12-01 și 2016-01-02 (dar nu încă unul pentru 2016-01-02, ca acel interval nu s-a finalizat) iar planificatorul le va executa secvenţial.

`Catchup` este declanșat și atunci când dezactivați un DAG pentru o perioadă specificată și apoi îl reactivați.

Acest comportament este excelent pentru seturile de date atomice care pot fi împărțite cu ușurință în perioade. Dezactivarea catchup-ului este grozavă dacă DAG-ul dvs. efectuează catchup intern.

### Backfill
Poate fi cazul în care doriți să rulați DAG pentru o perioadă istorică specificată, de exemplu, un DAG de completare a datelor este creat cu `start_date` 2019-11-21, dar un alt utilizator necesită datele de ieșire de acum o lună, adică 2019-10 -21. Acest proces este cunoscut sub numele de `Backfill`.

Este posibil să doriți să completați datele chiar și în cazurile în care `catchup` este dezactivat. Acest lucru se poate face prin CLI. Rulați comanda de mai jos

```python
airflow dags backfill \
    --start-date START_DATE \
    --end-date END_DATE \
    dag_id
```

### Re-run Tasks

Unele dintre task-uri pot eșua în timpul rulării programate. Odată ce ați remediat erorile după ce ați consultat jurnalele, puteți să rulați din nou task-urile prin ștergerea lor pentru data programată. Ștergerea unei instanțe de task nu șterge înregistrarea instanței de task. În schimb, actualizează `max_tries` la 0 și setează starea actuală a instanței de task la `None`, ceea ce determină rularea din nou a task-ului.

Faceți clic pe task-ul eșuat în vizualizările `Tree` sau `Graph` și apoi faceți clic pe `Clear`. Executorul îl va rula din nou.

Există mai multe opțiuni pe care le puteți selecta pentru a rula din nou:

- **Past** - Toate instanțele task-ului în rulările anterioare ale intervalului de date cel mai recent al DAG-ului
- **Future** - Toate instanțele task-ului în rulările după intervalul de date cel mai recent al DAG-ului
- **Upstream** - Task-urile upstream în DAG-ul curent
- **Downstream** - Task-urile downstream în DAG-ul curent
- **Recursive** - Toate task-urile din DAG-urile copil și DAG-urile părinte
- **Failed** - Doar task-urile eșuate în cea mai recentă rulare a DAG-ului

Puteți șterge task-ul și prin intermediul CLI folosind comanda:

```python
airflow tasks clear dag_id \
    --task-regex task_regex \
    --start-date START_DATE \
    --end-date END_DATE
```
Pentru `dag_id` și intervalul de timp specificate, comanda șterge toate instanțele task-urilor care se potrivesc cu `regex`. Pentru mai multe opțiuni, puteți verifica ajutorul comenzii clear:


```python
airflow tasks clear --help
```
### External triggers
Rețineți că DAG Runs pot fi create și manual prin CLI. Doar rulați comanda -

```python
airflow dags trigger --exec-date logical_date run_id
```

Execuțiile DAG create extern planificatorului sunt asociate cu marcajul de timp al declanșatorului și sunt afișate în interfața de utilizare alături de rulările DAG programate. Data logică transmisă în interiorul DAG poate fi specificată folosind argumentul `-e`. Valoarea implicită este data curentă în fusul orar UTC.

În plus, puteți, de asemenea, să declanșați manual o rulare DAG folosind interfața de utilizare web (fila DAG-uri -> coloana Linkuri -> butonul `Trigger Dag`)

### Transmiterea parametrilor la declanșarea DAG-urilor
Când declanșați un DAG din CLI, API-ul REST sau UI, este posibil să treceți configurația pentru o rulare DAG ca blob JSON.

Exemplu de DAG parametrizat:

```python
import pendulum

from airflow import DAG
from airflow.operators.bash import BashOperator

dag = DAG(
    "example_parameterized_dag",
    schedule=None,
    start_date=pendulum.datetime(2021, 1, 1, tz="UTC"),
    catchup=False,
)

parameterized_task = BashOperator(
    task_id="parameterized_task",
    bash_command="echo value: {{ dag_run.conf['conf1'] }}",
    dag=dag,
)
```

Notă: Parametrii din `dag_run.conf` pot fi utilizați numai într-un câmp șablon al unui operator.

### Folosind CLI

```python
airflow dags trigger --conf '{"conf1": "value1"}' example_parameterized_dag
```

### Folosind UI

![ui](https://airflow.apache.org/docs/apache-airflow/stable/_images/example_passing_conf.png)


## A tine minte
**Marcarea instanțelor de activitate ca eșuate se poate face prin interfața de utilizare. Aceasta poate fi folosită pentru a opri rularea instanțelor de activitate.**

**Marcarea instanțelor de activitate ca reușite se poate face prin interfața de utilizare. Acest lucru este în principal pentru a remedia negative false sau, de exemplu, atunci când remedierea a fost aplicată în afara Airflow.**