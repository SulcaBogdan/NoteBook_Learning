# DAG in Apache Airflow


### Un DAG (Directed Acyclic Graph) este conceptul central al Airflow, adunând Task-urile împreună, organizate cu dependențe și relații pentru a specifica modul în care ar trebui să ruleze.

Aici este un exemplu de bază al unui DAG:

![dag](https://airflow.apache.org/docs/apache-airflow/stable/_images/basic-dag.png)

Defineste patru Sarcini - `A`, `B`, `C` și `D` - și dictează ordinea în care trebuie să ruleze, precum și care sarcini depind de altele. De asemenea, va preciza cât de des să ruleze `DAG`-ul - poate fi "la fiecare 5 minute începând de mâine" sau "în fiecare zi începând de la 1 ianuarie 2020".

`DAG`-ul în sine nu se preocupă de ceea ce se întâmplă în interiorul sarcinilor; este interesat doar de modul în care să le execute - ordinea în care să le ruleze, de câte ori să le reîncerce, dacă au limite de timp, și așa mai departe.

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
Un `Task/Operator` nu trăiește de obicei singură; are dependențe de alte sarcini (cele de deasupra sa), iar alte sarcini depind de ea (cele de dedesubtul sa). Declararea acestor dependențe între sarcini constituie structura `DAG` (*the edges of the directed acyclic graph*).

Există două modalități principale de a declara dependențele individuale ale sarcinilor. Cea recomandată este utilizarea operatorilor `>>` și `<<`:


```python
first_task >> [second_task, third_task]
third_task << fourth_task
```

Sau poți utiliza și metodele mai explicite `set_upstream` și `set_downstream`:

```python
first_task.set_downstream([second_task, third_task])
third_task.set_upstream(fourth_task)
```

Există și scurtături pentru a declara dependențe mai complexe. Dacă vrei să faci ca două liste de sarcini să depindă de toate părțile fiecare, nu poți utiliza niciuna dintre abordările de mai sus, așa că trebuie să folosești `cross_downstream`:

```python
from airflow.models.baseoperator import cross_downstream

# Replaces
# [op1, op2] >> op3
# [op1, op2] >> op4
cross_downstream([op1, op2], [op3, op4])
```


Și dacă vrei să le legești împreună pe baza dependențelor, poți utiliza `chain`:

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

Rularea DAG-urilor
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

De fiecare dată când rulezi un DAG, creezi o nouă instanță a acelui DAG, pe care Airflow o numește o Execuție a DAG-ului (DAG Run). Execuțiile DAG pot rula în paralel pentru același DAG, iar fiecare are un interval de date definit, care identifică perioada de date asupra căreia sarcinile ar trebui să opereze.

Ca exemplu pentru utilitatea acestui aspect, consideră scrierea unui DAG care procesează un set zilnic de date experimentale. A fost rescris, și vrei să-l rulezi pe ultimele 3 luni de date — nicio problemă, deoarece Airflow poate alimenta DAG-ul și să ruleze copii ale acestuia pentru fiecare zi din acele 3 luni anterioare, toate simultan.

Toate aceste Execuții DAG vor fi pornite în aceeași zi reală, dar fiecare Execuție DAG va avea un interval de date care acoperă o singură zi în acea perioadă de 3 luni, iar acest interval de date este la care se uită toate sarcinile, operatorii și senzorii din interiorul DAG-ului atunci când rulează.

În mod similar cu modul în care un DAG se instanțiază într-o Execuție DAG de fiecare dată când este rulat, Sarcinile specificate într-un DAG sunt, de asemenea, instanțiate în Instanțe de Sarcină împreună cu acesta.

O Execuție DAG va avea o dată de început când începe și o dată de sfârșit când se termină. Această perioadă descrie momentul când DAG-ul a fost efectiv 'rulat'. În afara datei de început și de sfârșit a Execuției DAG, există o altă dată numită dată logică (cunoscută formal ca dată de execuție), care descrie momentul la care o Execuție DAG este programată sau declanșată. Motivul pentru care aceasta este numită logică este datorită naturii sale abstracte, având multiple semnificații, în funcție de contextul Execuției DAG în sine.

De exemplu, dacă o Execuție DAG este declanșată manual de către utilizator, data sa logică ar fi data și ora la care a fost declanșată Execuția DAG, iar valoarea ar trebui să fie egală cu data de început a Execuției DAG. Cu toate acestea, atunci când DAG-ul este programat automat, cu un anumit interval de programare stabilit, data logică va indica momentul la care marchează începutul intervalului de date, unde data de început a Execuției DAG va fi apoi data logică + intervalul programat.

## Alocare DAG
Reține că fiecare Operator/Sarcină trebuie să fie asignat unui DAG pentru a putea fi rulat. Airflow are mai multe moduri de a calcula DAG-ul fără a-l pasa explicit:

1. Dacă declari Operatorul tău într-un bloc with DAG
2. Dacă declari Operatorul tău într-un decorator `@dag`
3. Dacă plasezi Operatorul tău în amonte sau în aval de un Operator care are un DAG

În caz contrar, trebuie să-l pasezi fiecărui Operator cu argumentul `dag=`.

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

Pe lângă metodele mai tradiționale de a declara un singur `DAG` folosind un manager de context sau constructorul `DAG()`, poți de asemenea să decorezi o funcție cu @dag pentru a o transforma într-o funcție generator de DAG:


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
În mod implicit, un DAG va rula o sarcină doar atunci când toate sarcinile de care depinde sunt de succes. Există însă mai multe modalități de a modifica acest comportament:

Ramificarea - selectarea căreia Sarcină să treacă în funcție de o condiție

Reguli de Declanșare - stabilirea condițiilor în care un DAG va rula o sarcină

Configurare și Închidere - definirea relațiilor de configurare și închidere

Numai Ultima - o formă specială de ramificare care rulează doar pe DAG-urile care rulează împotriva prezentului

Depinde de Trecut - sarcinile pot depinde de ele însele dintr-o rulare anterioară

### Ramificarea
Poți folosi ramificarea pentru a-i spune DAG-ului să nu ruleze toate sarcinile dependente, ci să aleagă în schimb una sau mai multe căi de a urma. Aici intră în joc decoratorul `@task.branch`.

Decoratorul `@task.branch` este foarte asemănător cu `@task`, cu excepția faptului că se așteaptă ca funcția decorată să returneze un ID către o sarcină (sau o listă de ID-uri). Sarcina specificată este urmată, în timp ce toate celelalte căi sunt trecute cu vederea. Poate returna, de asemenea, None pentru a trece cu vederea toate sarcinile în aval.

task_id returnat de funcția Python trebuie să facă referire la o sarcină direct în aval de sarcina decorată cu `@task.branch`.


Când o Sarcină este în aval atât de operatorul de ramificare, cât și în aval de una sau mai multe dintre sarcinile selectate, nu va fi trecută cu vederea:


![branch](https://airflow.apache.org/docs/apache-airflow/stable/_images/branch_note.png)


Cărțile sarcinii de ramificare sunt `branch_a`, `join` și b`ranch_b`. Deoarece `join` este o sarcină în aval a `branch_a`, totuși va fi rulată, chiar dacă nu a fost returnată ca parte a deciziei de ramificare.

Decoratorul `@task.branch` poate fi, de asemenea, folosit cu `XComs`, permițând contextului de ramificare să decidă dinamic ce ramură să urmeze în funcție de sarcinile în amonte. De exemplu:

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

Dacă dorești să implementezi propriile tale operatori cu funcționalitate de ramificare, poți moșteni de la `BaseBranchOperator`, care se comportă similar cu decoratorul `@task.branch`, dar se așteaptă să furnizezi o implementare a metodei `choose_branch`.

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

Similar cu decoratorul `@task.branch` pentru codul Python obișnuit, există și decoratori de ramificare care utilizează un mediu virtual numit `@task.branch_virtualenv` sau Python extern numit `@task.branch_external_python`.

## Latest only
De multe ori, DAG-urile în Airflow sunt rulate pentru o dată care nu este aceeași cu data curentă - de exemplu, rulează o copie a unui DAG pentru fiecare zi din ultima lună pentru a încărca unele date.

Există situații, totuși, în care nu vrei să lași să ruleze unele (sau toate) părțile unui DAG pentru o dată anterioară; în acest caz, poți folosi `LatestOnlyOperator`.

Acest `Operator` special sare peste toate sarcinile în aval dacă nu te afli în "ultima" rulare a DAG-ului (dacă timpul curent de perete este între `execution_time` și următoarea `execution_time` programată, și nu a fost o rulare declanșată extern).

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

Poți spune, de asemenea, că o sarcină poate fi rulată doar dacă rularea anterioară a sarcinii în DAG Run-ul anterior a avut succes. Pentru a utiliza aceasta, trebuie doar să setezi argumentul depends_on_past al sarcinii tale la True.

Reține că, dacă rulezi DAG-ul la începutul vieții sale - în special, la prima sa rulare automată vreodată - atunci sarcina tot va rula, deoarece nu există nicio rulare anterioară de care să depindă.

### Trigger Rules
----------------

În mod implicit, Airflow va aștepta ca toate sarcinile upstream (părinții direcți) pentru o sarcină să aibă succes înainte de a rula acea sarcină.

Cu toate acestea, aceasta este doar comportamentul implicit și îl poți controla folosind argumentul trigger_rule pentru o sarcină. Opțiunile pentru trigger_rule sunt:

| **`Trigger Rule`** | **`Descriere`** |
| ---------------- | -------------- |
| all_success (implicit) | Toate sarcinile upstream au avut succes. |
| all_failed | Toate sarcinile upstream sunt într-o stare de eșec sau upstream_failed. |
| all_done | Toate sarcinile upstream au terminat execuția. |
| all_skipped | Toate sarcinile upstream sunt într-o stare de trecere cu vederea. |
| one_failed | Cel puțin o sarcină upstream a eșuat (nu așteaptă ca toate sarcinile upstream să se termine). |
| one_success | Cel puțin o sarcină upstream a avut succes (nu așteaptă ca toate sarcinile upstream să se termine). |
| one_done | Cel puțin o sarcină upstream a avut succes sau a eșuat. |
| none_failed | Toate sarcinile upstream nu au eșuat sau sunt în upstream_failed - adică, toate sarcinile upstream au avut succes sau au fost trecute cu vederea. |
| none_failed_min_one_success | Toate sarcinile upstream nu au eșuat sau sunt în upstream_failed, și cel puțin o sarcină upstream a avut succes. |
| none_skipped | Nicio sarcină upstream nu este într-o stare de trecere cu vederea - adică, toate sarcinile upstream sunt într-o stare de succes, eșec sau upstream_failed. |
| always | Fără dependențe deloc, rulează această sarcină în orice moment. |


Poți, de asemenea, combina aceasta cu funcționalitatea Depends On Past dacă dorești.

Este important să fim conștienți de interacțiunea dintre regulile de declanșare și sarcinile trecute cu vederea, în special sarcinile care sunt trecute cu vederea în cadrul unei operațiuni de ramificare. Cu puține excepții, nu dorim să utilizăm `all_success` sau `all_failed` în avalul unei operațiuni de ramificare.

Sarcinile trecute cu vederea vor fi propagate prin regulile de declanșare `all_success` și `all_failed`, determinându-le să fie trecute cu vederea, de asemenea. Să luăm în considerare următorul DAG:

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

`join` este în avalul lui `follow_branch_a` și `branch_false`. Sarcina `join` va apărea ca fiind trecută cu vederea pentru că regulă de declanșare implicită este setată la `all_success`, iar trecerea cu vederea cauzată de operațiunea de ramificare se propagă în jos pentru a omite o sarcină marcată ca `all_success`.

![dag](https://airflow.apache.org/docs/apache-airflow/stable/_images/branch_without_trigger.png)

Prin setarea regulii de declanșare la `none_failed_min_one_success` în sarcina `join`, putem obține comportamentul dorit:


![dag](https://airflow.apache.org/docs/apache-airflow/stable/_images/branch_with_trigger.png)

## Configurare și dezinstalare
În fluxurile de lucru de date este obișnuit să creați un resursă (cum ar fi o resursă de calcul), să o utilizați pentru a efectua o anumită activitate și apoi să o dezinstalați. Airflow oferă sarcini de configurare și dezinstalare pentru a susține această nevoie.

Vă rugăm să consultați articolul principal Configurare și dezinstalare pentru detalii despre cum să utilizați această caracteristică.

## DAG-uri dinamice
Deoarece un DAG este definit de codul Python, nu este nevoie să fie pur declarativ; sunteți liber să utilizați bucle, funcții și altele pentru a defini DAG-ul.

De exemplu, iată un DAG care folosește o buclă `for` pentru a defini unele sarcini:

```python
 with DAG("loop_example", ...):
     first = EmptyOperator(task_id="first")
     last = EmptyOperator(task_id="last")

     options = ["branch_a", "branch_b", "branch_c", "branch_d"]
     for option in options:
         t = EmptyOperator(task_id=option)
         first >> t >> last
```
În general, vă sfătuim să încercați să mențineți topologia (configurația) sarcinilor din DAG relativ stabilă; DAG-urile dinamice sunt de obicei mai bine folosite pentru încărcarea dinamică a opțiunilor de configurare sau modificarea opțiunilor operatorilor.

## Vizualizarea DAG-urilor
Dacă doriți să vizualizați o reprezentare grafică a unui DAG, aveți două opțiuni:

1. Puteți deschide interfața utilizator Airflow, navigați la DAG-ul dvs. și selectați "Grafic"
2. Puteți rula comanda `airflow dags show`, care o afișează sub formă de fișier imagine

În general, vă recomandăm să utilizați vederea Grafic, deoarece vă va arăta și starea tuturor instanțelor de sarcini în cadrul oricărei rulări a DAG-ului pe care o selectați.

Bineînțeles, pe măsură ce dezvoltați DAG-urile, acestea vor deveni tot mai complexe, așa că oferim câteva modalități de modificare a acestor vizualizări ale DAG-urilor pentru a le face mai ușor de înțeles.

## Grupuri de sarcini (TaskGroups)
Un `TaskGroup` poate fi utilizat pentru a organiza sarcinile în grupuri ierarhice în vizualizarea Grafic. Este util pentru crearea de modele repetitive și reducerea aglomerației vizuale.

Spre deosebire de SubDAG-uri, TaskGroups sunt pur și simplu un concept de grupare UI. Sarcinile din TaskGroups se află în același DAG original și respectă toate setările DAG și configurațiile de pool.

![gif](https://airflow.apache.org/docs/apache-airflow/stable/_images/task_group.gif)


Relațiile de dependență pot fi aplicate pentru toate sarcinile dintr-un `TaskGroup` cu operatorii `>>` și `<<`. De exemplu, următorul cod plasează `task1` și `task2` în `TaskGroup` group1 și apoi pune ambele sarcini în amonte de `task3`:

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

Pentru a dezactiva prefixarea, treci `prefix_group_id=False` la crearea `TaskGroup`, dar reține că acum vei fi responsabil pentru asigurarea unicității fiecărei sarcini și grup.

Când folosești decorarea `@task_group`, docstring-ul funcției decorate va fi folosit ca o sugestie de ecran în UI pentru `TaskGroup`, cu excepția cazului în care se furnizează în mod explicit o valoare pentru sugestie.


### Edge Labels
Pe lângă gruparea sarcinilor în grupuri, poți eticheta, de asemenea, muchiile de dependență dintre diferite sarcini în vizualizarea grafică - acest lucru poate fi deosebit de util pentru zonele de ramificare ale DAG-ului tău, astfel încât să poți eticheta condițiile sub care anumite ramuri ar putea rula.

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
Este posibil să adaugi documentare sau note la DAG-urile și obiectele de sarcini care sunt vizibile în interfața web ("`Graph`" și "`Tree`" pentru DAG-uri, "Detalii instanță sarcină" pentru sarcini).

Există un set de atribute speciale pentru sarcini care sunt afișate ca conținut bogat dacă sunt definite:

| Atribut | Renderează la |  
| ------- | ------------ |  
| `doc` | monospace |  
| `doc_json` | JSON |  
| `doc_yaml` | YAML |  
| `doc_md` | Markdown |  
| `doc_rst` | reStructuredText |  

Rețineți că pentru DAG-uri, `doc_md` este singurul atribut interpretat. Pentru DAG-uri, acesta poate conține un șir de caractere sau referința către un fișier de tip șablon. Referințele către șabloane sunt recunoscute prin șirul care se încheie în `.md`. Dacă este furnizat un traseu relativ, acesta va începe din dosarul fișierului DAG. De asemenea, fișierul șablon trebuie să existe, altfel Airflow va genera o excepție `jinja2.exceptions.TemplateNotFound`.

Acest lucru este util în special dacă sarcinile tale sunt create dinamic din fișiere de configurare, deoarece îți permite să expui configurarea care a condus la sarcinile relevante în Airflow.

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

`SubDAG`-urile sunt deprecate, prin urmare, TaskGroup este întotdeauna opțiunea preferată.

Uneori, vei constata că adaugi în mod regulat exact aceeași serie de sarcini la fiecare DAG sau vrei să grupezi multe sarcini într-o singură unitate logică. Acesta este rolul `SubDAG`-urilor.

De exemplu, iată un DAG care are multe sarcini paralele în două secțiuni:

![subdag](https://airflow.apache.org/docs/apache-airflow/stable/_images/subdag_before.png)

Putem combina toate operatorii paraleli task-* într-un singur SubDAG, astfel încât DAG-ul rezultat să semene cu cel de mai jos:

![subdag](https://airflow.apache.org/docs/apache-airflow/stable/_images/subdag_after.png)

#### Rețineți că operatorii SubDAG ar trebui să conțină o metodă de fabrică care returnează un obiect DAG. Acest lucru va împiedica tratarea SubDAG-ului ca pe un DAG separat în interfața principală - amintește-ți că, dacă Airflow vede un DAG la nivelul superior al unui fișier Python, îl va încărca ca pe propriul său DAG. De exemplu:

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

Poți să faci zoom pe un `SubDagOperator` din vizualizarea grafică a DAG-ului principal pentru a vedea sarcinile conținute în `SubDAG`:

![gdag](https://airflow.apache.org/docs/apache-airflow/stable/_images/subdag_zoom.png)

Câteva sfaturi suplimentare când folosești SubDAGs:

- Prin convenție, id-ul unui SubDAG ar trebui să aibă un prefix format din numele DAG-ului principal și un punct (parinte.copil)
- Ar trebui să partajezi argumente între DAG-ul principal și SubDAG prin transmiterea acestora către operatorul SubDAG (așa cum este demonstrat mai sus)
- SubDAGs trebuie să aibă un program și să fie activate. Dacă programul SubDAG-ului este setat la None sau @once, SubDAG-ul va avea succes fără să facă nimic.
- Curățarea unui SubDagOperator curăță și starea sarcinilor din interiorul său.
- Marcarea succesului pe un SubDagOperator nu afectează starea sarcinilor din interiorul său.
- Abține-te să folosești Depends On Past în sarcinile din interiorul SubDAG-ului, deoarece acest lucru poate fi confuz.
- Poți specifica un executor pentru SubDAG. Este obișnuit să folosești SequentialExecutor dacă vrei să rulezi SubDAG-ul în proces și să îi limitezi eficient paralelismul la unul. Folosirea LocalExecutor poate fi problematică, deoarece poate suprasolicita worker-ul, rulând mai multe sarcini într-un singur slot.

Vezi airflow/example_dags pentru o demonstrație.

#### Note

`Paralelismul` nu este respectat de `SubDagOperator`, astfel că resursele ar putea fi consumate de `SubdagOperators` dincolo de orice limite ai putea seta.

## TaskGroups și SubDAGs 

**SubDAGs**, deși au un scop similar, introduc atât probleme de performanță, cât și probleme funcționale din cauza implementării lor.

- SubDagOperator pornește un BackfillJob, care ignoră configurațiile existente de paralelism, putând supraabona mediul de lucru.

- SubDAGs au propriile atribute DAG. Atunci când atributele DAG ale SubDAG sunt inconsistente cu cele ale părintelui său, pot apărea comportamente neașteptate.

- Nu se poate vedea "întreaga" DAG într-o singură vedere, deoarece SubDAGs există ca o DAG completă.

- SubDAGs introduc tot felul de cazuri și avertismente speciale. Acest lucru poate perturba experiența și așteptările utilizatorilor.

TaskGroups, pe de altă parte, reprezintă o opțiune mai bună, având în vedere că este doar un concept de grupare în interfața utilizatorului. Toate sarcinile din TaskGroup se comportă încă ca oricare alte sarcini în afara TaskGroup.

Poți observa diferențele cheie între aceste două construcții.

**TaskGroup**

- Repeating patterns as part of the same DAG
- One set of views and statistics for the DAG
- One set of DAG configuration
- Honors parallelism configurations through existing SchedulerJob
- Simple construct declaration with context manager

**SubDAG**

- Repeating patterns as a separate DAG
- Separate set of views and statistics between parent and child DAGs
- Several sets of DAG configurations
- Does not honor parallelism configurations due to newly spawned BackfillJob
- Complex DAG factory with naming restrictions


## Ambalarea DAG-urilor

În timp ce DAG-urile mai simple sunt de obicei într-un singur fișier Python, nu este neobișnuit ca DAG-urile mai complexe să fie răspândite în mai multe fișiere și să aibă dependențe care ar trebui să fie incluse cu ele ("vendorate").

Puteți face acest lucru fie în DAG_FOLDER, cu o structură standard a sistemului de fișiere, fie puteți împacheta DAG-ul și toate fișierele sale Python ca un singur fișier zip. De exemplu, ați putea trimite două DAG-uri împreună cu o dependență de care au nevoie într-un fișier zip cu următorul conținut:


```python
my_dag1.py
my_dag2.py
package1/__init__.py
package1/functions.py
```

Rețineți că DAG-urile împachetate vin cu câteva avertismente:

- Nu pot fi folosite dacă aveți activată serializarea prin pickling.
- Nu pot conține biblioteci compilate (de exemplu, libz.so), doar Python pur.
- Vor fi introduse în sys.path al lui Python și pot fi importate de orice alt cod din procesul Airflow, așa că asigurați-vă că numele pachetelor nu intră în conflict cu alte pachete deja instalate în sistemul dvs.

În general, dacă aveți un set complex de dependențe și module compilate, este probabil mai bine să utilizați sistemul Python virtualenv și să instalați pachetele necesare pe sistemele țintă cu ajutorul lui pip.
