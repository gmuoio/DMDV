<<GUIDELINES PROGETTO DATA MANAGEMENT AND VISUALIZATION>>

Il bike sharing nella Grande Mela ai tempi della pandemia: 
Analisi trasversale dell’evoluzione del noleggio di biciclette 
nella città di New York tra 2019 e 2020

A cura di:
Francesco Fustini - 830697
Anna Mattiroli - 826381
Guglielmo Muoio - 826029
Laura Rapino - 831346

*Guida per la riproducibilità del progetto*

Software utilizzati: Python (Jupyter), Apache Kafka, MongoDB, Docker, Tableau Desktop

1) Simulazione di un ambiente in sharding tramite dei container Docker.
Si è utilizzata la seguente configurazione:  
	2 shard (ciascuno con 3 nodi replica), 
	1 config server (con 3 nodi replica), 
	1 router mongos,
	chiave di tipo hashed.
Una volta creata una collezione e abilitato lo sharding, utilizzare la libreria pymongo per connettersi e caricare progressivamente i dati su mongoDB (punto 2).
N.B. il caricamento in sharding richiede più tempo dovuto alla replicazione dei dati e alla creazione di una sharding key per ogni singolo documento.

2) Acquisizione dei dati.
I dati json dell’utilizzo del servizio CitiBike possono essere acquisiti e caricati nella collezione MongoDB tramite lo script data_loading.ipynb.
Questo stesso codice contiene i comandi per recuperare e salvare in locale 
i dati riguardanti le informazioni sulle stazioni di noleggio, 
le serie storiche dei dati meteo e COVID-19 giornalieri della città di New York in formato csv.

3) Simulazione raccolta dati in tempo reale.
Lanciare lo script kafka_consumer.ipynb che configura il consumer che legge i dati che verranno inseriti nella coda Kafka e li carica progressivamente nella collezione MongoDB.
Lo script kafka_producer.ipynb crea un producer che legge i dati json relativi al solo mese di Dicembre 2020 e li scrive nella coda Kafka che leggerà il consumer.

4) Integrazione.
Lo script pymongo_query.ipynb si connette alla collezione di dati MongoDB ed estrae tramite apposite query 
due dataset contenenti diverse dimensioni aggregate a livello giornaliero ed uno contenente il traffico orario per stazione del mese di Settembre 2019 e 2020.
I dataset ottenuti sono integrati alle altre fonti dati su base temporale tramite lo script integration.ipynb e salvati in locale in formato csv.

5) Creazione delle visualizzazioni.
I dataset ottenuti al punto 4 devono essere utilizzati per la costruzione delle infografiche su Tableau.
È possibile scaricare la cartella di lavoro compressa Tableau per riprodurre le visualizzazioni.



