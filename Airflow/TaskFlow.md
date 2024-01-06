# TaskFlow in Airflow

## TaskFlow


Dacă scrii majoritatea DAG-urilor tale folosind cod Python simplu în loc de Operatori, atunci API-ul `TaskFlow` îți va face mult mai ușor să scrii DAG-uri curate fără boilerplate suplimentar, totul folosind decoratorul `@task`.

`TaskFlow` se ocupă de mutarea intrărilor și ieșirilor între Task-urile tale folosind `XComs` pentru tine, precum și de calcularea automată a dependențelor - atunci când apelezi o funcție `TaskFlow` în fișierul tău DAG, în loc să o execute, vei primi un obiect care reprezintă `XCom`-ul pentru rezultat (un `XComArg`), pe care îl poți folosi apoi ca intrare pentru sarcinile sau operatorii downstream. De exemplu:

```python
from airflow.decorators import task
from airflow.operators.email import EmailOperator

@task
def get_ip():
    return my_ip_service.get_main_ip()

@task(multiple_outputs=True)
def compose_email(external_ip):
    return {
        'subject':f'Server connected from {external_ip}',
        'body': f'Your server executing Airflow is connected from the external IP {external_ip}<br>'
    }

email_info = compose_email(get_ip())

EmailOperator(
    task_id='send_email',
    to='example@example.com',
    subject=email_info['subject'],
    html_content=email_info['body']
)
```

Aici, există trei sarcini - `get_ip`, `compose_email` și `send_email`.

Primele două sunt declarate folosind `TaskFlow` și trec automat valoarea returnată de `get_ip` în `compose_email`, nu numai legând `XCom`-ul între ele, ci declarând automat că `compose_email` este în aval de `get_ip`.

`send_email` este un Operator mai tradițional, dar chiar și el poate folosi valoarea returnată de `compose_email` pentru a-și seta parametrii și din nou, deducând automat că trebuie să fie în aval de `compose_email`.

De asemenea, poți folosi o valoare sau o variabilă simplă pentru a apela o funcție TaskFlow - de exemplu, asta va funcționa așa cum te aștepți (dar, desigur, nu va rula codul din interiorul sarcinii până când DAG-ul este executat - valoarea numelui este persistată ca un parametru de sarcină până în acel moment):

```python
@task
def hello_name(name: str):
    print(f'Hello {name}!')

hello_name('Airflow users')
```

## Context

Poți accesa variabilele de context Airflow adăugându-le ca argumente de cuvânt cheie, așa cum este arătat în exemplul următor:


```python
from airflow.models.taskinstance import TaskInstance
from airflow.models.dagrun import DagRun


@task
def print_ti_info(task_instance: TaskInstance | None = None, dag_run: DagRun | None = None):
    print(f"Run ID: {task_instance.run_id}")  # Run ID: scheduled__2023-08-09T00:00:00+00:00
    print(f"Duration: {task_instance.duration}")  # Duration: 0.972019
    print(f"DAG Run queued at: {dag_run.queued_at}")  # 2023-08-10 00:00:01+02:20
```

Sau, poți adăuga `**kwargs` la semnătura sarcinii tale și toate variabilele de context Airflow vor fi accesibile în dicționarul `kwargs`:

```python
from airflow.models.taskinstance import TaskInstance
from airflow.models.dagrun import DagRun


@task
def print_ti_info(**kwargs):
    ti: TaskInstance = kwargs["task_instance"]
    print(f"Run ID: {ti.run_id}")  # Run ID: scheduled__2023-08-09T00:00:00+00:00
    print(f"Duration: {ti.duration}")  # Duration: 0.972019

    dr: DagRun = kwargs["dag_run"]
    print(f"DAG Run queued at: {dr.queued_at}")  # 2023-08-10 00:00:01+02:20
```

## Logging 

Pentru a folosi logging din funcțiile tale de task-uri, pur și simplu importă și folosește sistemul de logging al lui Python:


```python
logger = logging.getLogger("airflow.task")
```

Fiecare linie de logging creată în acest fel va fi înregistrată în jurnalul task-ului.

## Transmiterea de Obiecte Arbitrare ca Argumente

Așa cum s-a menționat, `TaskFlow` folosește `XCom` pentru a transmite variabile la fiecare sarcină. Acest lucru necesită ca variabilele folosite ca argumente să poată fi serializate. Airflow suportă implicit toate tipurile încorporate (cum ar fi `int` sau `str`) și suportă obiecte care sunt decorate cu @`dataclass` sau `@attr.define`. Exemplul următor arată utilizarea unui set de date, care este decorat cu `@attr.define`, împreună cu `TaskFlow`.


### Nota

Un beneficiu suplimentar al folosirii `Dataset` este că se înregistrează automat ca intrare în cazul în care este folosit ca argument de intrare. De asemenea, se înregistrează automat ca ieșire dacă valoarea returnată a sarcinii tale este un dataset sau o listă de `[Dataset]`.

```python
import json
import pendulum
import requests

from airflow import Dataset
from airflow.decorators import dag, task

SRC = Dataset(
    "https://www.ncei.noaa.gov/access/monitoring/climate-at-a-glance/global/time-series/globe/land_ocean/ytd/12/1880-2022.json"
)
now = pendulum.now()


@dag(start_date=now, schedule="@daily", catchup=False)
def etl():
    @task()
    def retrieve(src: Dataset) -> dict:
        resp = requests.get(url=src.uri)
        data = resp.json()
        return data["data"]

    @task()
    def to_fahrenheit(temps: dict[int, float]) -> dict[int, float]:
        ret: dict[int, float] = {}
        for year, celsius in temps.items():
            ret[year] = float(celsius) * 1.8 + 32

        return ret

    @task()
    def load(fahrenheit: dict[int, float]) -> Dataset:
        filename = "/tmp/fahrenheit.json"
        s = json.dumps(fahrenheit)
        f = open(filename, "w")
        f.write(s)
        f.close()

        return Dataset(f"file:///{filename}")

    data = retrieve(SRC)
    fahrenheit = to_fahrenheit(data)
    load(fahrenheit)


etl()
```

## Obiecte Personalizate

S-ar putea să vrei să transmiți obiecte personalizate. În mod obișnuit, ai decora clasele tale cu `@dataclass` sau `@attr.define` și Airflow va descoperi ce trebuie să facă. În unele cazuri, ai putea dori să controlezi serializarea singur. Pentru a face acest lucru, adaugă metoda `serialize()` la clasa ta și metoda staticmethod deserialize(`data: dict`, `version: int`) la clasa ta. Astfel:


```python
from typing import ClassVar


class MyCustom:
    __version__: ClassVar[int] = 1

    def __init__(self, x):
        self.x = x

    def serialize(self) -> dict:
        return dict({"x": self.x})

    @staticmethod
    def deserialize(data: dict, version: int):
        if version > 1:
            raise TypeError(f"version > {MyCustom.version}")
        return MyCustom(data["x"])
```

## Versiunea Obiectelor

Este o practică bună să versionezi obiectele care vor fi folosite în serializare. Pentru a face acest lucru, adaugă `__version__: ClassVar[int] = <x>` la clasa ta. Airflow presupune că clasele tale sunt compatibile în sens invers, astfel încât o versiune 2 să poată deserializa o versiune 1. În cazul în care ai nevoie de logica personalizată pentru deserializare, asigură-te că este specificată metoda deserialize(`data: dict, version: int`).

Tipizarea pentru `__version__`este necesară și trebuie să fie de tip `ClassVar[int]`.

## Senzorii și API-ul TaskFlow

Pentru un exemplu de scriere a unui `Senzor` folosind API-ul `TaskFlow`, vezi Utilizarea API-ului `TaskFlow` cu operatorii de senzor.

## Istoric

API-ul `TaskFlow` este nou începând cu Airflow 2.0, și este posibil să întâlnești DAG-uri scrise pentru versiunile anterioare ale Airflow care folosesc în schimb `PythonOperator` pentru a atinge obiective similare, cu mult mai mult cod.

Mai mult context despre adăugarea și proiectarea API-ului TaskFlow poate fi găsit în cadrul Propunerii de Îmbunătățire Airflow AIP-31: "TaskFlow API" pentru o definiție mai clară/simplă a DAG-ului.
