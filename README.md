# SQL-ripasso


SQL - Structured Query Language

Introduzione

SQL (Structured Query Language) è un linguaggio standard per la gestione dei database relazionali. Permette di creare, leggere, aggiornare ed eliminare dati all'interno di un database (operazioni CRUD: Create, Read, Update, Delete).

Tipi di Comandi SQL

SQL è suddiviso in diverse categorie principali:

1. DDL (Data Definition Language) - Definizione della struttura del database

CREATE TABLE - Crea una nuova tabella

ALTER TABLE - Modifica la struttura di una tabella

DROP TABLE - Elimina una tabella

esempio:

CREATE TABLE utenti (
    id INT PRIMARY KEY AUTO_INCREMENT,
    nome VARCHAR(50) NOT NULL,
    email VARCHAR(100) UNIQUE NOT NULL,
    eta INT CHECK (eta > 0)
);

----------------------------------------------------------------------------------------------------------------------------------------------------

2. DML (Data Manipulation Language) - Manipolazione dei dati

INSERT INTO - Inserisce nuovi dati

UPDATE - Modifica i dati esistenti

DELETE - Cancella dati

Esempio:

INSERT INTO utenti (nome, email, eta) VALUES ('Mario Rossi', 'mario@email.com', 30);

----------------------------------------------------------------------------------------------------------------------------------------------------

3. DQL (Data Query Language) - Interrogazione dei dati

SELECT - Estrae dati da una tabella

Esempio:

SELECT * FROM utenti WHERE eta > 25;

----------------------------------------------------------------------------------------------------------------------------------------------------

DCL (Data Control Language) - Controllo degli accessi

GRANT - Concede permessi

REVOKE - Revoca permessi

Esempio:

GRANT SELECT, INSERT ON utenti TO 'utente'@'localhost';

----------------------------------------------------------------------------------------------------------------------------------------------------

5. TCL (Transaction Control Language) - Gestione delle transazioni

COMMIT - Conferma una transazione

ROLLBACK - Annulla una transazione

Esempio:

START TRANSACTION;
UPDATE utenti SET eta = 35 WHERE id = 1;
COMMIT;

----------------------------------------------------------------------------------------------------------------------------------------------------

Relazioni tra Tabelle

Le relazioni tra tabelle vengono gestite con chiavi primarie e chiavi esterne.

Esempio di relazione tra due tabelle:

CREATE TABLE ordini (
    id INT PRIMARY KEY AUTO_INCREMENT,
    utente_id INT,
    prodotto VARCHAR(100),
    FOREIGN KEY (utente_id) REFERENCES utenti(id)
);

JOIN tra Tabelle

INNER JOIN - Ritorna solo i dati che hanno corrispondenze in entrambe le tabelle

LEFT JOIN - Ritorna tutti i record della prima tabella e solo quelli corrispondenti della seconda

Esempio di INNER JOIN:

SELECT utenti.nome, ordini.prodotto
FROM utenti
INNER JOIN ordini ON utenti.id = ordini.utente_id;

----------------------------------------------------------------------------------------------------------------------------------------------------

Funzioni Aggregate

COUNT(*) - Conta il numero di righe

SUM(colonna) - Somma i valori di una colonna

AVG(colonna) - Calcola la media

MAX(colonna), MIN(colonna) - Restituiscono il valore massimo e minimo

Esempio:

SELECT COUNT(*) FROM utenti;

Subquery

Le subquery sono query annidate all'interno di un'altra query.

Esempio:

SELECT * FROM utenti WHERE eta > (SELECT AVG(eta) FROM utenti);


----------------------------------------------------------------------------------------------------------------------------------------------------

TIPO DI DATI SQL


1. Tipi di Dati Numerici
TINYINT (1 byte) → Intero molto piccolo (-128 a 127 o 0-255 per UNSIGNED)

SMALLINT (2 byte) → Intero piccolo (-32,768 a 32,767)

MEDIUMINT (3 byte) → Intero medio (-8,388,608 a 8,388,607)

INT o INTEGER (4 byte) → Intero standard (-2,147,483,648 a 2,147,483,647)

BIGINT (8 byte) → Intero grande (-9,223,372,036,854,775,808 a 9,223,372,036,854,775,807)

DECIMAL(p, s) o NUMERIC(p, s) → Numero decimale con precisione fissa

FLOAT (4 byte) → Numero a virgola mobile (meno preciso)

DOUBLE (8 byte) → Numero a virgola mobile con più precisione

----------------------------------------------------------------------------------------------------------------------------------------------------

2. Tipi di Dati per il Testo
CHAR(n) → Stringa a lunghezza fissa (da 1 a 255 caratteri)

VARCHAR(n) → Stringa a lunghezza variabile (fino a 65,535 caratteri, dipende dalla configurazione del database)

TEXT → Testo di grandi dimensioni (fino a 65,535 caratteri)

TINYTEXT (255 caratteri)

MEDIUMTEXT (16,777,215 caratteri)

LONGTEXT (4,294,967,295 caratteri)

----------------------------------------------------------------------------------------------------------------------------------------------------

3. Tipi di Dati Booleani
BOOLEAN o BOOL → È uno pseudotipo in SQL (spesso memorizzato come TINYINT(1), con 0 = FALSE e 1 = TRUE)

----------------------------------------------------------------------------------------------------------------------------------------------------

4. Tipi di Dati per Data e Ora
DATE → Data nel formato YYYY-MM-DD

DATETIME → Data e ora YYYY-MM-DD HH:MI:SS

TIMESTAMP → Simile a DATETIME, ma cambia automaticamente con l'orario del server

TIME → Solo ora HH:MI:SS

YEAR → Solo anno YYYY

----------------------------------------------------------------------------------------------------------------------------------------------------

5. Tipi di Dati per Dati Binari
BLOB → Memorizza dati binari (immagini, file, ecc.)

TINYBLOB (fino a 255 byte)

MEDIUMBLOB (fino a 16 MB)

LONGBLOB (fino a 4 GB)
