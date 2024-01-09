# CREATE Constaints

`Constaints` pot fi specificate atunci când tabelul este creat cu instrucțiunea `CREATE TABLE` sau după ce tabelul este creat cu instrucțiunea `ALTER TABLE`.

## Sintaxă

```sql
CREATE TABLE table_name (
    column1 datatype constraint,
    column2 datatype constraint,
    column3 datatype constraint,
    ....
);
```

SQL `Constaints` sunt folosite pentru a specifica reguli pentru datele dintr-un tabel.

`Constaints` sunt folosite pentru a limita tipul de date care pot intra într-un tabel. Acest lucru asigură acuratețea și fiabilitatea datelor din tabel. Dacă există vreo încălcare între constrângere și acțiunea de date, acțiunea este anulată.

`Constaints` pot fi la nivel de coloană sau la nivel de tabel. `Constaints` la nivel de coloană se aplică unei coloane, iar `Constaints` la nivel de tabel se aplică întregului tabel.

Următoarele `Constaints` sunt utilizate în mod obișnuit în SQL:


- **`NOT NULL`** - Asigură că o coloană nu poate avea o valoare NULL.
- **`UNIQUE`** - Asigură că toate valorile dintr-o coloană sunt diferite.
- **`PRIMARY KEY`** - O combinație între NOT NULL și UNIQUE. Identifică în mod unic fiecare rând dintr-o tabelă.
- **`FOREIGN KEY`** - Previne acțiuni care ar distruge legăturile dintre tabele.
- **`CHECK`** - Asigură că valorile dintr-o coloană satisfac o condiție specifică.
- **`DEFAULT`** - Setează o valoare implicită pentru o coloană în cazul în care nu este specificată nicio valoare.
- **`CREATE INDEX`** - Folosit pentru a crea și recupera date din baza de date foarte rapid.