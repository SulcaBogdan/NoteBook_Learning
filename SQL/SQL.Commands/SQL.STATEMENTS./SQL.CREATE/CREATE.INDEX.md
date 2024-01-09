# CREATE INDEX in SQL

Instrucțiunea `CREATE INDEX` este folosită pentru a crea `index`-uri în tabele.

Index-urile sunt utilizați pentru a prelua datele din baza de date mai rapid decât altfel. Utilizatorii nu pot vedea index-urile, acestea sunt doar folosite pentru a accelera căutările/interogările.

`Notă`: **Actualizarea unui tabel cu indici durează mai mult timp decât actualizarea unui tabel fără (deoarece index necesită și o actualizare). Deci, creați numai index pe coloanele care vor fi căutate frecvent.**

## Sintaxa CREATE INDEX

```SQL
CREATE INDEX index_name
ON table_name (column1, column2, ...);
```

## Sintaxa CREATE UNIQUE INDEX

```sql
CREATE UNIQUE INDEX index_name
ON table_name (column1, column2, ...);
```

`Notă`: **Sintaxa pentru crearea index-urilor variază între diferitele baze de date. Prin urmare: Verificați sintaxa pentru crearea index-urilor în baza de date.**

## Exemplu CREATE INDEX 

Instrucțiunea SQL de mai jos creează un index numit `idx_lastname` în coloana `LastName` din tabelul `Persons`:

```sql
CREATE INDEX idx_lastname
ON Persons (LastName);
```

Dacă doriți să creați un index pe o combinație de coloane, puteți enumera numele coloanelor în paranteze, separate prin virgule:

```sql
CREATE INDEX idx_pname
ON Persons (LastName, FirstName);
```

## DROP INDEX

Instrucțiunea `DROP INDEX` este folosită pentru a șterge un index dintr-un tabel.

### MS Access:

```sql
DROP INDEX index_name ON table_name;
```

### SQL Server:

```sql
DROP INDEX table_name.index_name;
```

### DB2/Oracle:

```sql
DROP INDEX index_name;
```
### MySQL:

```sql
ALTER TABLE table_name
DROP INDEX index_name;
```