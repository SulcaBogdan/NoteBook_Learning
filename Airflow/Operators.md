# Operatorii in AirFlow


Un `Operator` este conceptual un șablon pentru un Task predefinit, pe care o poți defini declarativ în interiorul DAG-ului tău.

```python
with DAG("my-dag") as dag:
    ping = HttpOperator(endpoint="http://example.com/update/")
    email = EmailOperator(to="admin@example.com", subject="Update complete")

    ping >> email
```

## Operatori

Airflow dispune de un set foarte extins de operatori, cu unele integrate în modul de bază sau furnizate de provideri pre-instalați. Câteva operatori populare din modul de bază includ:

- **BashOperator**: execută o comandă bash

- **PythonOperator**: apelează o funcție Python arbitrară

- **EmailOperator**: trimite un email

Utilizează decoratorul `@task` pentru a executa o funcție Python arbitrară. Acesta nu suportă redarea șabloanelor Jinja transmise ca argumente.

Decoratorul `@task` este recomandat în locul clasicului `PythonOperator` pentru a executa apeluri Python fără redarea șabloanelor în argumente.

Pentru o listă a tuturor operatorilor de bază, vezi: Referința la Operatori și Hook-uri de Bază.

Dacă operatorul de care ai nevoie nu este instalat implicit cu Airflow, probabil îl vei găsi ca parte a setului nostru extins de pachete de furnizori comunitari. Câțiva operatori populari de aici includ:

- **HttpOperator**
- **MySqlOperator**
- **PostgresOperator**
- **MsSqlOperator**
- **OracleOperator**
- **JdbcOperator**
- **DockerOperator**
- **HiveOperator**
- **S3FileTransformOperator**
- **PrestoToMySqlOperator**
- **SlackAPIOperator**

Dar există multe, multe altele - poți vedea lista completă a tuturor operatorilor, hook-urilor, senzorilor și transferurilor gestionate de comunitate în documentația noastră pentru pachetele de furnizori.

În interiorul codului Airflow, amestecăm adesea conceptele de `Tasks` și `Operators`, ele fiind în mare măsură interschimbabile. Cu toate acestea, atunci când vorbim despre o task, ne referim la "unitatea de execuție" generică a unui DAG; când vorbim despre un `Operator`, ne referim la un șablon de task reutilizabil, deja realizat pentru tine, care are toată logica deja implementată și care are nevoie doar de niște argumente.

## Templating cu Jinja
Airflow folosește puterea templating-ului Jinja, iar acesta poate fi un instrument puternic atunci când este combinat cu macro-uri.

De exemplu, să spunem că vrei să transmiți începutul intervalului de date ca o variabilă de mediu către un script `Bash` folosind `BashOperator`:

```python
# The start of the data interval as YYYY-MM-DD
date = "{{ ds }}"
t = BashOperator(
    task_id="test_env",
    bash_command="/tmp/test.sh ",
    dag=dag,
    env={"DATA_INTERVAL_START": date},
)
```

Aici, `{{ ds }}` este o variabilă template, iar datorită faptului că parametrul `env` al `BashOperator` este templated cu `Jinja`, data de început a intervalului va fi disponibilă ca o variabilă de mediu numită `DATA_INTERVAL_START` în scriptul tău `Bash`.

Poți utiliza templatingul `Jinja` cu fiecare parametru marcat ca "`templated`" în documentație. Substituția șabloanelor are loc chiar înainte ca funcția `pre_execute` a operatorului tău să fie apelată.

Poți folosi, de asemenea, templating-ul `Jinja` cu câmpuri `nested`, atât timp cât aceste câmpuri nested sunt marcate ca templated în structura din care fac parte: câmpurile înregistrate în proprietatea `template_fields` vor fi supuse substituției de șabloane, cum ar fi câmpul path în exemplul de mai jos:

```python
class MyDataReader:
    template_fields: Sequence[str] = ("path",)

    def __init__(self, my_path):
        self.path = my_path

    # [additional code here...]


t = PythonOperator(
    task_id="transform_data",
    python_callable=transform_data,
    op_args=[MyDataReader("/tmp/{{ ds }}/my_file")],
    dag=dag,
)
```

Proprietatea `template_fields` este o variabilă de clasă și este garantată să fie de tip Sequence[str] (adică o listă sau tuplu de șiruri).

De asemenea, pot fi înlocuite și câmpurile nested în profunzime, atâta timp cât toate câmpurile intermediare sunt marcate ca câmpuri de șabloane:

```python
class MyDataTransformer:
    template_fields: Sequence[str] = ("reader",)

    def __init__(self, my_reader):
        self.reader = my_reader

    # [additional code here...]


class MyDataReader:
    template_fields: Sequence[str] = ("path",)

    def __init__(self, my_path):
        self.path = my_path

    # [additional code here...]


t = PythonOperator(
    task_id="transform_data",
    python_callable=transform_data,
    op_args=[MyDataTransformer(MyDataReader("/tmp/{{ ds }}/my_file"))],
    dag=dag,
)
```

Poți transmite opțiuni personalizate către mediul `Jinja` atunci când creezi DAG-ul tău. Un uz obișnuit este să eviți ca `Jinja` să elimine o linie nouă de la sfârșitul unui șir de șablon:

```python
my_dag = DAG(
    dag_id="my-dag",
    jinja_environment_kwargs={
        "keep_trailing_newline": True,
        # some other jinja2 Environment options here
    },
)
```

Unii operatori vor considera, de asemenea, că șirurile care se termină cu sufixe specifice (definite în `template_ext`) sunt referințe la fișiere atunci când se randează câmpurile. Acest lucru poate fi util pentru încărcarea scripturilor sau interogărilor direct din fișiere în loc să le includă în codul DAG.

De exemplu, ia în considerare un `BashOperator` care rulează un script bash cu mai multe linii, acesta va încărca fișierul script.sh și își va folosi conținutul ca valoare pentru `bash_command`:

```python
run_script = BashOperator(
    task_id="run_script",
    bash_command="script.sh",
)
```

În mod implicit, căile furnizate în acest mod ar trebui să fie relative la folderul DAG-ului (deoarece acesta este directorul implicit de căutare pentru șabloane Jinja), dar pot fi adăugate căi suplimentare prin setarea argumentului `template_searchpath` pe DAG.

În unele cazuri, poate doriți să excludeți un șir de la templating și să îl utilizați direct. Ia în considerare următoarea sarcină:

```python
print_script = BashOperator(
    task_id="print_script",
    bash_command="cat script.sh",
)
```

Acest lucru va eșua cu `TemplateNotFound`: `cat script.sh`, deoarece Airflow ar trata șirul ca pe o cale către un fișier, nu ca pe o comandă. Putem preveni Airflow să trateze această valoare ca o referință la un fișier înfășurând-o în `literal()`. Această abordare dezactivează randarea atât a macro-urilor, cât și a fișierelor și poate fi aplicată pe câmpuri nested selectate, păstrând regulile implicite de templating pentru restul conținutului.

```python
from airflow.utils.template import literal


fixed_print_script = BashOperator(
    task_id="fixed_print_script",
    bash_command=literal("cat script.sh"),
)
```

Alternativ, dacă dorești să împiedici Airflow să trateze o valoare ca o referință la un fișier, poți suprascrie `template_ext`:


```python
fixed_print_script = BashOperator(
    task_id="fixed_print_script",
    bash_command="cat script.sh",
)
fixed_print_script.template_ext = ()
```


### Randarea Câmpurilor ca Obiecte Python Native

În mod implicit, toate câmpurile de șabloane sunt randate ca șiruri.

De exemplu, să spunem că sarcina extract push-ează un dicționar (Exemplu: `{"1001": 301.27, "1002": 433.21, "1003": 502.22}`) în tabela `XCom`. Acum, când rulezi sarcina următoare, argumentul order_data este transmis ca un șir, exemplu: '`{"1001": 301.27, "1002": 433.21, "1003": 502.22}`'.


```python
transform = PythonOperator(
    task_id="transform",
    op_kwargs={"order_data": "{{ti.xcom_pull('extract')}}"},
    python_callable=transform,
)
```

Dacă, în schimb, dorești ca câmpul șablon randat să returneze un obiect Python nativ (dict în exemplul nostru), poți transmite `render_template_as_native_obj` `=` `True` la DAG în felul următor:


```python
dag = DAG(
    dag_id="example_template_as_python_object",
    schedule=None,
    start_date=pendulum.datetime(2021, 1, 1, tz="UTC"),
    catchup=False,
    render_template_as_native_obj=True,
)


@task(task_id="extract")
def extract():
    data_string = '{"1001": 301.27, "1002": 433.21, "1003": 502.22}'
    return json.loads(data_string)


@task(task_id="transform")
def transform(order_data):
    print(type(order_data))
    for value in order_data.values():
        total_order_value += value
    return {"total_order_value": total_order_value}


extract_task = extract()

transform_task = PythonOperator(
    task_id="transform",
    op_kwargs={"order_data": "{{ti.xcom_pull('extract')}}"},
    python_callable=transform,
)

extract_task >> transform_task
```

În acest caz, argumentul `order_data` este transmis: `{"1001": 301.27, "1002": 433.21, "1003": 502.22}`.

Airflow folosește `NativeEnvironment` din `Jinja` atunci când `render_template_as_native_obj` este setat la `True`. Cu `NativeEnvironment`, randarea unui șablon produce un tip Python nativ.

### Cuvânt cheie reserved: `params`
În Apache Airflow 2.2.0, variabila params este folosită în timpul serializării DAG-ului. Te rog să nu folosești acest nume în operatorii terți. Dacă faci upgrade la mediul tău și primești următoarea eroare:

```python
AttributeError: 'str' object has no attribute '__module__'
```

Schimbă numele de la `params` în operatorii tăi.














