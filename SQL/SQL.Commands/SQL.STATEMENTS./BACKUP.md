# BACKUP DATABASE in SQL

Instrucțiunea `BACKUP DATABASE` este utilizată în SQL Server pentru a crea o copie de rezervă completă a unei baze de date SQL existente.

### Sintaxă

```sql
BACKUP DATABASE databasename
TO DISK = 'filepath';
```

## Instrucțiunea SQL BACKUP WITH DIFERENTIAL
O copie de rezervă diferențială face doar copii de siguranță ale părților din baza de date care s-au modificat de la ultima copie de rezervă completă a bazei de date.

### Sintaxă

```sql
BACKUP DATABASE databasename
TO DISK = 'filepath'
WITH DIFFERENTIAL;
```

## Exemplu BACKUP BAZĂ DE DATE
Următoarea instrucțiune SQL creează o copie de rezervă completă a bazei de date existente `„testDB”` pe discul D:

```sql
BACKUP DATABASE testDB
TO DISK = 'D:\backups\testDB.bak';
```

`Nota`: **faceți întotdeauna copii de rezervă ale bazei de date pe o altă unitate decât baza de date reală. Apoi, dacă întâmpinați o blocare a discului, nu veți pierde fișierul de rezervă împreună cu baza de date.**

## Exemplu BACKUP CU DIFERENȚIAL 
Următoarea instrucțiune SQL creează o copie de rezervă diferențială a bazei de date `„testDB”`:

```sql
BACKUP DATABASE testDB
TO DISK = 'D:\backups\testDB.bak'
WITH DIFFERENTIAL;
```

`Nota`: **o copie de rezervă diferențială reduce timpul de rezervă (deoarece doar modificările sunt susținute).**