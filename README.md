# SQL - Ripasso

## Introduzione
SQL (Structured Query Language) è un linguaggio standard per la gestione dei database relazionali. Permette di creare, leggere, aggiornare ed eliminare dati all'interno di un database (operazioni CRUD: Create, Read, Update, Delete).

---

## Tipi di Comandi SQL

### DDL (Data Definition Language) - Definizione della struttura del database
- **CREATE TABLE** - Crea una nuova tabella
- **ALTER TABLE** - Modifica la struttura di una tabella
- **DROP TABLE** - Elimina una tabella

**Esempio:**
```sql
CREATE TABLE utenti (
    id INT PRIMARY KEY AUTO_INCREMENT,
    nome VARCHAR(50) NOT NULL,
    email VARCHAR(100) UNIQUE NOT NULL,
    eta INT CHECK (eta > 0)
);
```

### DML (Data Manipulation Language) - Manipolazione dei dati
- **INSERT INTO** - Inserisce nuovi dati
- **UPDATE** - Modifica i dati esistenti
- **DELETE** - Cancella dati

**Esempio:**
```sql
INSERT INTO utenti (nome, email, eta) VALUES ('Mario Rossi', 'mario@email.com', 30);
```

### DQL (Data Query Language) - Interrogazione dei dati
- **SELECT** - Estrae dati da una tabella

**Esempio:**
```sql
SELECT * FROM utenti WHERE eta > 25;
```

### DCL (Data Control Language) - Controllo degli accessi
- **GRANT** - Concede permessi
- **REVOKE** - Revoca permessi

**Esempio:**
```sql
GRANT SELECT, INSERT ON utenti TO 'utente'@'localhost';
```

### TCL (Transaction Control Language) - Gestione delle transazioni
- **COMMIT** - Conferma una transazione
- **ROLLBACK** - Annulla una transazione

**Esempio:**
```sql
START TRANSACTION;
UPDATE utenti SET eta = 35 WHERE id = 1;
COMMIT;
```

---

## Query di base

### Filtrare i risultati
```sql
SELECT * FROM utenti WHERE nome LIKE 'M%';
SELECT * FROM utenti WHERE eta BETWEEN 20 AND 30;
SELECT * FROM utenti WHERE id IN (1, 3, 5);
```

### Ordinare i risultati
```sql
SELECT * FROM utenti ORDER BY nome ASC;
SELECT * FROM utenti ORDER BY eta DESC;
```

### Limitare il numero di risultati
```sql
SELECT * FROM utenti LIMIT 10;
```

---

## Operazioni avanzate

### GROUP BY e HAVING
```sql
SELECT eta, COUNT(*) FROM utenti GROUP BY eta HAVING COUNT(*) > 2;
```

### CASE per condizioni nelle query
```sql
SELECT nome, eta,
    CASE
        WHEN eta < 18 THEN 'Minorenne'
        WHEN eta BETWEEN 18 AND 65 THEN 'Adulto'
        ELSE 'Anziano'
    END AS categoria
FROM utenti;
```

### INDEX per migliorare le performance
```sql
CREATE INDEX idx_nome ON utenti(nome);
```

---

## Relazioni tra Tabelle

Le relazioni tra tabelle vengono gestite con chiavi primarie e chiavi esterne.

**Esempio di relazione tra due tabelle:**
```sql
CREATE TABLE ordini (
    id INT PRIMARY KEY AUTO_INCREMENT,
    utente_id INT,
    prodotto VARCHAR(100),
    FOREIGN KEY (utente_id) REFERENCES utenti(id)
);
```

### JOIN tra Tabelle
- **INNER JOIN** - Ritorna solo i dati che hanno corrispondenze in entrambe le tabelle
- **LEFT JOIN** - Ritorna tutti i record della prima tabella e solo quelli corrispondenti della seconda

**Esempio di INNER JOIN:**
```sql
SELECT utenti.nome, ordini.prodotto
FROM utenti
INNER JOIN ordini ON utenti.id = ordini.utente_id;
```

---

## Funzioni Aggregate

- **COUNT(*)** - Conta il numero di righe
- **SUM(colonna)** - Somma i valori di una colonna
- **AVG(colonna)** - Calcola la media
- **MAX(colonna), MIN(colonna)** - Restituiscono il valore massimo e minimo

**Esempio:**
```sql
SELECT COUNT(*) FROM utenti;
```

---

## Subquery

Le subquery sono query annidate all'interno di un'altra query.

**Esempio:**
```sql
SELECT * FROM utenti WHERE eta > (SELECT AVG(eta) FROM utenti);
```

---

## Stored Procedures & Views

### Creazione e utilizzo di una VIEW
```sql
CREATE VIEW utenti_maggiorenni AS
SELECT * FROM utenti WHERE eta >= 18;
```

### Creazione di una Stored Procedure
```sql
DELIMITER //
CREATE PROCEDURE GetUtenti()
BEGIN
    SELECT * FROM utenti;
END //
DELIMITER ;
```

---

## Backup & Restore

### Backup del database
```sh
mysqldump -u utente -p nome_database > backup.sql
```

### Ripristino del database
```sh
mysql -u utente -p nome_database < backup.sql
```

---

## Ottimizzazione e Performance

### Creazione di un indice
```sql
CREATE INDEX idx_nome ON utenti(nome);
```

### Analizzare una query per ottimizzazione
```sql
EXPLAIN SELECT * FROM utenti WHERE nome = 'Mario';
```

---

## Tipi di Dati SQL

### Tipi di Dati Numerici
- **TINYINT, SMALLINT, MEDIUMINT, INT, BIGINT** - Numeri interi
- **DECIMAL(p, s), FLOAT, DOUBLE** - Numeri decimali

### Tipi di Dati per il Testo
- **CHAR(n), VARCHAR(n)** - Stringhe
- **TEXT, TINYTEXT, MEDIUMTEXT, LONGTEXT** - Testi lunghi

### Tipi di Dati Booleani
- **BOOLEAN o BOOL** (spesso memorizzato come TINYINT(1))

### Tipi di Dati per Data e Ora
- **DATE, DATETIME, TIMESTAMP, TIME, YEAR**

### Tipi di Dati per Dati Binari
- **BLOB, TINYBLOB, MEDIUMBLOB, LONGBLOB**

---



