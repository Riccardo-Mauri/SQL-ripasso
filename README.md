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