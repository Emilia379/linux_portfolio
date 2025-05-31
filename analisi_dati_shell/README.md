# Esercizio: Navigazione, Esplorazione e Visualizzazione di Dati con la Shell

Questo esercizio dimostra le capacità di navigazione nel filesystem Linux e l'uso di comandi per ispezionare il 
contenuto di directory e file. Simula un contesto di analisi dati, dove è necessario accedere e visualizzare 
informazioni da file di log e elenchi utenti.

---

## Obiettivi dell'Esercizio

* Utilizzare `pwd` per conoscere la directory corrente.
* Elencare il contenuto di directory con `ls`.
* Cambiare directory usando percorsi relativi e assoluti con `cd`.
* Visualizzare il contenuto completo di un file con `cat`.
* Visualizzare le prime righe di un file con `head`.
* Dimostrare la gestione degli errori comuni (es. directory non trovata).

---

## Scenario

Simuliamo di essere un analista di sistema o dati che deve esplorare alcune directory di progetto, verificare 
l'esistenza di file di log e file utente, e visualizzarne il contenuto per una prima analisi.

---

## Passaggi Eseguiti e Output

Di seguito è riportata una schermata del terminale che documenta i passaggi eseguiti e i relativi output. Ogni 
comando è spiegato per chiarezza.

![Screenshot del Terminale che mostra l'esercizio](images/schermata_navigazione_log.png) 
*(Nota: L'immagine è stata rinominata per chiarezza nel portfolio e si trova nella directory `images/`)*

### Spiegazione dei Comandi Eseguiti:

1.  **`pwd`**
    * **Comando:** `pwd`
    * **Descrizione:** Stampa la directory di lavoro corrente. Utile per orientarsi.
    * **Output:** `/home/analyst`

2.  **`ls`**
    * **Comando:** `ls`
    * **Descrizione:** Elenca il contenuto della directory corrente.
    * **Output:** `logs projects reports temp` (mostra le sottodirectory principali)

3.  **`cd reports`**
    * **Comando:** `cd reports`
    * **Descrizione:** Cambia la directory corrente in `reports` (percorso relativo alla directory attuale 
`/home/analyst`).
    * **Output:** Nessun output specifico, ma il prompt cambia, indicando la nuova directory.

4.  **`ls` (in `reports`)**
    * **Comando:** `ls`
    * **Descrizione:** Elenca il contenuto della nuova directory corrente (`reports`).
    * **Output:** `users` (mostra una sottodirectory all'interno di `reports`)

5.  **`cd users`**
    * **Comando:** `cd users`
    * **Descrizione:** Cambia la directory corrente in `users` (percorso relativo alla directory attuale 
`/home/analyst/reports`).
    * **Output:** Nessun output specifico.

6.  **`ls` (in `reports/users`)**
    * **Comando:** `ls`
    * **Descrizione:** Elenca il contenuto della directory `reports/users`.
    * **Output:** `Q1_added_users.txt Q1_deleted_users.txt` (mostra i file degli utenti)

7.  **`cat Q1_added_users.txt`**
    * **Comando:** `cat Q1_added_users.txt`
    * **Descrizione:** Visualizza l'intero contenuto del file `Q1_added_users.txt`. Questo file sembra contenere un 
elenco di utenti con employee ID, username e dipartimento.
    * **Output:** Dati tabulari degli utenti.

8.  **`cd logs` (tentativo fallito)**
    * **Comando:** `cd logs`
    * **Descrizione:** Tentativo di cambiare directory in `logs` usando un percorso relativo. La directory `logs` non 
esiste in `/home/analyst/reports/users`. Questo dimostra la gestione degli errori.
    * **Output:** `-bash: cd: logs: No such file or directory` (messaggio di errore)

9.  **`cd /home/analyst/logs`**
    * **Comando:** `cd /home/analyst/logs`
    * **Descrizione:** Cambia la directory in `logs` usando un **percorso assoluto**. Questo supera l'errore 
precedente navigando direttamente alla directory `logs` dalla radice del filesystem.
    * **Output:** Nessun output specifico.

10. **`ls` (in `logs`)**
    * **Comando:** `ls`
    * **Descrizione:** Elenca il contenuto della directory `logs`.
    * **Output:** `server_logs.txt`

11. **`head server_logs.txt`**
    * **Comando:** `head server_logs.txt`
    * **Descrizione:** Visualizza le prime 10 righe (di default) del file `server_logs.txt`. Questo è utile per avere 
una rapida panoramica di un file di log senza caricarlo interamente.
    * **Output:** Le prime righe del file di log, che mostrano timestamp, livelli di log (info, error, warning) e 
messaggi.

---

## Riflessioni e Miglioramenti Futuri

Questa schermata rappresenta un punto di partenza per l'analisi dei log. In futuro, potrei estendere questo esercizio 
per:
* Filtrare i log per livello di gravità (es. solo `error` o `warning`) usando `grep`.
* Contare le occorrenze di eventi specifici.
* Analizzare i log per username o IP usando una combinazione di `grep`, `awk`, `cut`.
* Automatizzare queste operazioni con uno script Bash.

---
