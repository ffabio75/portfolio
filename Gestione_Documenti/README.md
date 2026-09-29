Analisi Applicativo – Importatore PDF Delibere (Python + PyQt5)
🧩 Descrizione generale
Questo progetto è un applicativo desktop sviluppato in Python, con interfaccia grafica basata su PyQt5, progettato per automatizzare il processo di:

scansione di una cartella contenente file PDF,

rinomina automatica dei documenti in base ai dati presenti nel database,

importazione del contenuto PDF nel campo BLOB della tabella delibere,

aggiornamento dei metadati del record (nome file, flag download, data import),

monitoraggio del processo tramite barra di avanzamento e log in tempo reale.

L’applicativo è pensato per ambienti amministrativi dove è necessario gestire grandi volumi di documenti ufficiali (delibere, determine, atti amministrativi).

⚙️ Tecnologie utilizzate
Python 3.x

PyQt5 per l’interfaccia grafica

pymysql per la connessione al database MySQL

Threading (QThread) per mantenere l’interfaccia reattiva durante l’elaborazione

Gestione file system (os, sys)

🏗️ Architettura del software
1. Interfaccia grafica (GUI)
La finestra principale include:

selezione cartella PDF

pulsante START/STOP

barra di avanzamento

area di log in tempo reale

messaggi di stato e completamento

La GUI rimane sempre reattiva grazie all’uso di un thread dedicato.

2. Thread di importazione (ImportThread)
Il thread esegue tutte le operazioni pesanti:

connessione al database

scansione dei PDF

rinomina dei file

lettura binaria del PDF

aggiornamento del record nel database

invio dei log alla GUI

gestione dello stop manuale

Questo evita blocchi dell’interfaccia e permette all’utente di interrompere il processo.

3. Log e monitoraggio
Ogni operazione viene registrata:

file rinominati

record aggiornati

errori di importazione

avanzamento percentuale

Il log è fondamentale per verificare eventuali anomalie nei documenti.

🗂️ Funzionamento della rinomina
Il programma:

legge il nome originale del PDF (es. 123.pdf)

cerca nel database il record con NOME_FILE = 123.pdf

recupera NUMERO_DELIBERA

rinomina il file in:

Codice
DELIBERA_<NUMERO_DELIBERA>.pdf
importa il PDF nel campo BLOB DELIBERA

🛡️ Gestione errori
Il software gestisce:

file non validi

PDF non presenti nel database

errori di rinomina

errori di lettura/scrittura

errori SQL

Ogni eccezione viene mostrata nel log con stack trace.

🚀 Vantaggi operativi
Automazione completa del processo di importazione

Riduzione drastica degli errori manuali

Rinominazione coerente e standardizzata

Importazione massiva di documenti

Interfaccia semplice e utilizzabile da personale amministrativo

📌 Possibili estensioni future
Validazione automatica dei PDF

Esportazione report di importazione

Integrazione con sistemi documentali esterni

Logging avanzato su file

Gestione multi-cartella
