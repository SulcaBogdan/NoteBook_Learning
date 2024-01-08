# Executor in Airflow

Executorii sunt mecanismul prin care instanțele de task sunt executate. Aceștia au un API comun și sunt "`pluggable`", ceea ce înseamnă că poți schimba executorii în funcție de nevoile instalației tale.

Airflow poate avea configurat doar un singur executor în același timp; acesta este setat de opțiunea executor în secțiunea `[core]` a fișierului de configurare.

Executorii încorporați sunt referiți prin nume, de exemplu:

```python
[core]
executor = KubernetesExecutor
```

Dacă vrei să verifici ce executor este configurat în prezent, poți folosi comanda `airflow config get-value core executor`:

```
$ airflow config get-value core executor
SequentialExecutor
```

## Tipuri de Executori

Există două tipuri de executori - cei care `rulează task-urile local` (în interiorul procesului de planificator) și cei care rulează `task-urile la distanță` (de obicei printr-un grup de `workeri`). 

Airflow vine configurat implicit cu `SequentialExecutor`, care este un `executor local` și cea mai simplă opțiune pentru execuție. Cu toate acestea, `SequentialExecutor` nu este potrivit pentru producție, deoarece nu permite rularea task-urilor în paralel și din acest motiv, unele caracteristici Airflow (de exemplu, rulează `sensors`) nu vor funcționa corect. Ar trebui să folosești în schimb `LocalExecutor` pentru instalații de producție mici, pe o singură mașină, sau unul dintre executorii la distanță pentru o instalare multi-mașină/cloud.

`Executori Locali`

- Debug Executor (deprecated)
- Local Executor
- Sequential Executor

`Executori la Distanță`

- Celery Executor
- CeleryKubernetes Executor
- Dask Executor
- Kubernetes Executor
- LocalKubernetes Executor


Utilizatorii noi Airflow pot presupune că au nevoie să ruleze un proces executor separat folosind unul dintre `Executorii Locali` sau `Executorii la Distanță`. Acest lucru nu este corect. Logica executorului rulează în interiorul procesului de planificator și va rula task-urile local sau nu, în funcție de executorul selectat.

## Scrierea Propriului Executor

Toți executorii Airflow implementează o interfață comună astfel încât să poată fi plasați și orice executor are acces la toate capacitățile și integrările din Airflow. În principal, planificatorul Airflow folosește această interfață pentru a interacționa cu executorul, dar și alte componente precum jurnalizarea, `CLI` și `backfill` o fac de asemenea. Interfața publică este `BaseExecutor`. Poți analiza codul pentru cea mai detaliată și actualizată interfață, dar mai jos sunt prezentate câteva aspecte importante.


Unele motive pentru care ai vrea să scrii un executor personalizat includ:

- Nu există un executor care să se potrivească cazului tău specific, cum ar fi o unealtă sau serviciu specific pentru calcul.

- Ai vrea să folosești un executor care să profite de un serviciu de calcul de la furnizorul tău de cloud preferat.

- Ai o unealtă/serviciu privat pentru executarea task-urilor care este disponibil doar pentru tine sau organizația ta.

### Metode Importante ale BaseExecutor

Aceste metode nu necesită să fie suprascrise pentru a implementa propriul executor, dar sunt utile să fie cunoscute:

| Metodă             | Descriere                                                                                                                                                     |
|--------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `heartbeat`        | Ciclul de lucru al Job-ului planificatorului Airflow va apela periodic heartbeat pe executor. Această metodă actualizează metrici, declanșează execuția task-urilor noi și actualizează starea task-urilor în execuție/terminate.                  |
| `queue_command`    | Executorul Airflow va apela această metodă a BaseExecutor pentru a furniza sarcini care să fie executate de executor. BaseExecutor pur și simplu adaugă TaskInstances la o listă internă de sarcini așteptate în cadrul executorului.       |
| `get_event_buffer` | Planificatorul Airflow apelează această metodă pentru a prelua starea curentă a TaskInstances pe care executorul le execută.                                      |
| `has_task`         | Planificatorul folosește această metodă BaseExecutor pentru a determina dacă un executor are deja o instanță de task specifică așteptată sau în execuție.      |
| `send_callback`    | Trimite orice apeluri de retur către sursa configurată pe executor.                                                                                             |



## Metode Obligatorii de Implementat

Următoarele metode trebuie să fie suprascrise cel puțin pentru a avea suport pentru executorul tău în Airflow:

`sync`: Metoda `sync` va fi apelată periodic în timpul bătăilor de inimă ale executorului. Implementează această metodă pentru a actualiza starea task-urilor pe care executorul le cunoaște. Opțional, încearcă să execute sarcini așteptate care au fost primite de la planificator.

`execute_async`: Execută o comandă în mod asincron. O comandă în acest context este o comandă CLI Airflow pentru a rula o task Airflow. Această metodă este apelată (după câteva straturi) în timpul bătăilor de inimă ale executorului care rulează periodic de către planificator. În practică, această metodă adaugă adesea sarcini într-o coadă internă sau externă de sarcini de rulat (de exemplu, `KubernetesExecutor`). Dar poate, de asemenea, să execute task-urile direct (de exemplu, `LocalExecutor`). Acest lucru va depinde de executor.

## Metode Opționale ale Interfeței de Implementat

Următoarele metode nu sunt necesare de suprascris pentru a avea un executor funcțional în Airflow. Cu toate acestea, implementarea lor poate aduce capacități puternice și stabilitate:


| Metode | Descriere |
|--------|-----------|
| `sync` | Metoda `sync` va fi apelată periodic în timpul bătăilor de inimă ale executorului. Implementează această metodă pentru a actualiza starea task-urilor pe care executorul le cunoaște. Opțional, încearcă să execute sarcini așteptate care au fost primite de la planificator. |
| `execute_async` | Execută o comandă în mod asincron. O comandă în acest context este o comandă CLI Airflow pentru a rula o task Airflow. Această metodă este apelată (după câteva straturi) în timpul bătăilor de inimă ale executorului care rulează periodic de către planificator. În practică, această metodă adaugă adesea sarcini într-o coadă internă sau externă de sarcini de rulat (de exemplu, KubernetesExecutor). Dar poate, de asemenea, să execute task-urile direct (de exemplu, LocalExecutor). Acest lucru va depinde de executor. |
| `start` | Job-ul planificatorului Airflow (și backfill) va apela această metodă după ce a inițializat obiectul executor. Aici se pot finaliza orice configurări suplimentare necesare de către executor. |
| `end` | Job-ul planificatorului Airflow (și backfill) va apela această metodă în timpul dezactivării. Orice curățare sincronă necesară pentru a finaliza task-urile în curs trebuie făcută aici. |
| `terminate` | Oprește mai forțat executorul, oprind/chinuind task-urile în curs de desfășurare în loc să aștepte sincron completarea lor. |
| `cleanup_stuck_queued_tasks` | Dacă task-urile sunt blocate în starea de așteptare pentru mai mult timp decât `task_queued_timeout`, acestea sunt colectate de către planificator și furnizate executorului pentru a avea oportunitatea de a le gestiona (efectua orice curățare/grupare elegantă) prin intermediul acestei metode și de a returna instanțele de task pentru un mesaj de avertizare afișat utilizatorilor. |
| `try_adopt_task_instances` | Sarcinile care au fost abandonate (de exemplu, de la un job al planificatorului care a murit) sunt furnizate executorului pentru a le adopta sau pentru a le gestiona în alt mod prin această metodă. Orice sarcini care nu pot fi adoptate (implicit, BaseExector presupune că niciuna nu poate fi adoptată) ar trebui returnate. |
| `get_cli_commands` | Executorii pot furniza comenzi CLI utilizatorilor prin implementarea acestei metode, consultați secțiunea CLI mai jos pentru mai multe detalii. |
| `get_task_log` | Executorii pot furniza mesaje de jurnal către jurnalele de sarcini Airflow prin implementarea acestei metode, consultați secțiunea Logging mai jos pentru mai multe detalii. |




## Atribute de Compatibilitate
Interfața clasei `BaseExecutor` conține un set de atribute pe care codul central Airflow le utilizează pentru a verifica caracteristicile cu care executorul dvs. este compatibil. Atunci când scrieți propriul executor Airflow, asigurați-vă că le setați corect pentru cazul dvs. de utilizare. Fiecare atribut este pur și simplu un boolean care activează/dezactivează o funcționalitate sau indică dacă o funcționalitate este acceptată/neacceptată de către executor.

| Atribut                     | Descriere                                                                                                                          |
|-----------------------------|------------------------------------------------------------------------------------------------------------------------------------|
| `supports_pickling`         | Indică dacă executorul acceptă sau nu citirea DAG-urilor pickled din baza de date înainte de execuție (în loc să citească definiția DAG din sistemul de fișiere).                              |
| `supports_sentry`           | Indică dacă executorul acceptă sau nu Sentry.                                                                                     |
| `is_local`                  | Indică dacă executorul este sau nu local sau la distanță. Consultați secțiunea Tipuri de Executori mai sus.                      |
| `is_single_threaded`        | Indică dacă executorul este sau nu cu un singur fir de execuție. Acest lucru este relevant în special pentru ce backend-uri de bază de date sunt acceptate. Executorii cu un singur fir de execuție pot rula cu orice backend, inclusiv SQLite. |
| `is_production`             | Indică dacă executorul ar trebui sau nu să fie utilizat în scopuri de producție. Un mesaj UI este afișat utilizatorilor când utilizează un executor care nu este gata pentru producție. |
| `change_sensor_mode_to_reschedule` | Rulează senzorii Airflow în modul poke poate bloca firul executorilor și, în unele cazuri, Airflow.                                  |


## CLI
Executorii pot furniza comenzi CLI care vor fi incluse în instrumentul de linie de comandă al Airflow prin implementarea metodei `get_cli_commands`. Executori precum `CeleryExecutor` și `KubernetesExecutor`, de exemplu, utilizează acest mecanism. Comenzile pot fi utilizate pentru a configura muncitorii necesari, a inițializa mediul sau a seta alte configurații. Comenzile sunt furnizate doar pentru executorul configurat în prezent. Un exemplu de pseudo-cod pentru implementarea furnizării de comenzi CLI dintr-un executor poate fi observat mai jos:

```python
@staticmethod
def get_cli_commands() -> list[GroupCommand]:
    sub_commands = [
        ActionCommand(
            name="command_name",
            help="Description of what this specific command does",
            func=lazy_load_command("path.to.python.function.for.command"),
            args=(),
        ),
    ]

    return [
        GroupCommand(
            name="my_cool_executor",
            help="Description of what this group of commands do",
            subcommands=sub_commands,
        ),
    ]
```
`Notă`

În prezent, nu există reguli stricte pentru spațiul de nume al comenzilor Airflow. Este responsabilitatea dezvoltatorilor să folosească nume pentru comenzile lor CLI care sunt suficient de unice pentru a nu cauza conflicte cu alți executori sau componente Airflow.

`Notă`

Atunci când creați un nou executor sau actualizați orice executor existent, asigurați-vă că nu importați sau executați operații/cod costisitoare la nivel de modul. Clasele executorilor sunt importate în mai multe locuri și, dacă sunt lente la import, acest lucru va afecta negativ performanța mediului dvs. Airflow, în special pentru comenzile CLI.

## Logging
Executorii pot furniza mesaje de jurnal care vor fi incluse în jurnalele de sarcini Airflow prin implementarea metodei `get_task_logs`. Acest lucru poate fi util dacă mediul de execuție are un context suplimentar în cazul eșecurilor sarcinii, care pot fi cauzate de mediul de execuție în sine și nu de codul sarcinii Airflow. De asemenea, poate fi util să includăți jurnalizarea configurării/dezinstalării din mediul de execuție. KubernetesExecutor folosește această capacitate pentru a include jurnalele din podul care a rulat o anumită task Airflow și pentru a le afișa în jurnalele acelei sarcini Airflow. Un exemplu de pseudo-cod pentru implementarea furnizării de jurnale pentru sarcini dintr-un executor poate fi observat mai jos:

```python
def get_task_log(self, ti: TaskInstance, try_number: int) -> tuple[list[str], list[str]]:
    messages = []
    log = []
    try:
        res = helper_function_to_fetch_logs_from_execution_env(ti, try_number)
        for line in res:
            log.append(remove_escape_codes(line.decode()))
        if log:
            messages.append("Found logs from execution environment!")
    except Exception as e:  # No exception should cause task logs to fail
        messages.append(f"Failed to find logs from execution environment: {e}")
    return messages, ["\n".join(log)]
```

Pașii următori ar fi să configurați Airflow pentru a utiliza noul executor pe care l-ați creat, setând valoarea de configurare core.executor la calea modulului executorului dvs.:

```python
[core]
executor = my_company.executors.MyCustomExecutor
```