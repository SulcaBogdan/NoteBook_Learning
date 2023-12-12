# Python datetime

O dată în Python nu este un tip de date propriu, dar putem importa un modul numit **datetime** pentru a lucra cu datele ca obiecte date.

```python
import datetime

x = datetime.datetime.now()
print(x)

output:
2023-12-12 19:46:59.570853
```

## Date output

Când executăm codul din exemplul de mai sus, rezultatul va fi:

2023-12-12 19:45:31.844513
Data conține an, lună, zi, oră, minut, secundă și microsecundă.

Modulul datetime are multe metode de a returna informații despre obiectul date.

Iată câteva exemple, veți afla mai multe despre ele mai târziu în acest capitol:


Returnează anul și numele zilei săptămânii:
```python
import datetime

x = datetime.datetime.now()

print(x.year)
print(x.strftime("%A"))

output:
2023
Tuesday
```

## Crearea de obiecte datetime()

Pentru a crea o dată, putem folosi clasa datetime() (constructor) a modulului datetime.

Clasa datetime() necesită trei parametri pentru a crea o dată: an, lună, zi

```python
import datetime

x = datetime.datetime(2020, 5, 17)

print(x)

output:
2020-05-17 00:00:00
```
Clasa datetime() preia, de asemenea, parametri pentru oră și fus orar (oră, minut, secundă, microsecundă, tzone), dar aceștia sunt opționali și au o valoare implicită de 0 (Niciunul pentru fusul orar).


## Metoda strftime()
Obiectul datetime are o metodă de formatare a obiectelor date în strings care pot fi citite.

Metoda se numește **strftime**() și ia un parametru, format, pentru a specifica formatul șirului returnat:

```python
import datetime

x = datetime.datetime(2018, 6, 1)

print(x.strftime("%B"))

output:
June
```
### O referință a tuturor codurilor de format legal:

| Cod | Descriere                                | Exemplu          |
|-----|------------------------------------------|------------------|
| %a  | Weekday, short version                   | Wed              |
| %A  | Weekday, full version                    | Wednesday        |
| %w  | Weekday as a number 0-6, 0 is Sunday     | 3                |
| %d  | Day of month 01-31                       | 31               |
| %b  | Month name, short version                | Dec              |
| %B  | Month name, full version                 | December         |
| %m  | Month as a number 01-12                  | 12               |
| %y  | Year, short version, without century     | 18               |
| %Y  | Year, full version                       | 2018             |
| %H  | Hour 00-23                               | 17               |
| %I  | Hour 00-12                               | 05               |
| %p  | AM/PM                                    | PM               |
| %M  | Minute 00-59                             | 41               |
| %S  | Second 00-59                             | 08               |
| %f  | Microsecond 000000-999999                 | 548513           |
| %z  | UTC offset                               | +0100            |
| %Z  | Timezone                                 | CST              |
| %j  | Day number of year 001-366               | 365              |
| %U  | Week number of year, Sunday as 1st day    | 52               |
| %W  | Week number of year, Monday as 1st day    | 52               |
| %c  | Local version of date and time           | Mon Dec 31 17:41:00 2018 |
| %C  | Century                                  | 20               |
| %x  | Local version of date                    | 12/31/18         |
| %X  | Local version of time                    | 17:41:00         |
| %%  | A % character                            | %                |
| %G  | ISO 8601 year                            | 2018             |
| %u  | ISO 8601 weekday (1-7)                   | 1                |
| %V  | ISO 8601 weeknumber (01-53)              | 01               |
