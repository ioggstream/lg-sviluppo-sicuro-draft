.. _figura-12-input-ed-output-della-fase-threat-modeling-attack-surface-analysis:

Figura 12: Input ed Output della fase Threat Modeling Attack Surface Analysis
=============================================================================

Le linee guida di progettazione sicura sono oggetto del deliverable
**D04.Fase1-SP2 - Linee Guida per la modellazione delle minacce ed
individuazione delle azioni di mitigazione conformi ai principi del
Secure/Privacy by Design**. Si rinvia a quest'ultimo per ulteriori
dettagli della metodologia da adottare.

.. _identificazione-degli-strumenti-a-supporto-1:

.. _identificazione-degli-strumenti-a-supporto-1:

9.2.1 Identificazione degli strumenti a supporto
------------------------------------------------

Dopo aver identificato e documentato le esigenze di sicurezza, viene
eseguita la modellazione delle minacce col fine di riconoscere e
assegnare delle priorità a queste ed individuare le opportune
contromisure per la loro mitigazione.

Nel paragrafo 6.3.2 sono stati presentati i tool a supporto di questa
fase. Tra questi si evidenzia il **Microsoft Threat Modeling Tool** il
quale consente di creare un modello di minacce tramite una
rappresentazione del sistema o dei componenti del sistema, dei dati
scambiati tra i componenti e i limiti di attendibilità nel sistema
stesso.

A differenza delle tecniche di verifica, come ad esempio il penetration
testing, il modello di minacce ottenuto attraverso la relativa
modellazione, deve essere eseguito prima che un prodotto o un servizio
venga implementato. Questo contribuisce a realizzare un prodotto finale
più sicuro indirizzando problematiche di sicurezza ad un early-stage del
ciclo di sviluppo. Il processo per la costruzione di un modello di
minacce consiste dei seguenti step:

-  Disegno dell'architettura del sistema;

-  Individuazione dei confini di fiducia;

-  Identificazione delle minacce;

-  Individuazione delle contromisure da attuare per mitigare le minacce;

-  Eventuale riprogettazione dei componenti per mitigare le minacce;

-  Convalida del modello architetturale;

-  Verifica dell'esistenza di una contromisura per ogni potenziale
   minaccia identificata.

.. _implementazione-di-applicazioni-sicure:

9.3 IMPLEMENTAZIONE DI APPLICAZIONI SICURE
------------------------------------------

Le azioni di sicurezza che devono essere intraprese in questa sono così
sintetizzate:

-  **Data Validation:** verificare la presenza di vulnerabilità che
   possono riguardare eventuali dati corrotti in ingresso e che possono
   portare a un comportamento anomalo dell'applicazione;

-  **Control Flow** : verificare i rischi collegati all'assenza di
   specifiche sequenze di operazioni che, se non eseguite nel corretto
   ordine, possono portare a violazioni sulla memoria o sull'uso
   scorretto di determinati componenti;

-  **Analisi Semantica** : rilevare eventuali problematiche legate
   all'uso pericoloso di determinate funzioni o API (es. funzioni
   deprecate);

.. _threat-modeling:

Threat Modeling
---------------

.. _attack-surface-analysis:

Attack Surface Analysis
-----------------------

-  **Requisitiutentee software**

-  **Specifica eHLD (soloper** **applicazioneesistente)**

-  **Specifica dei Requisiti di** **Sicurezza** -
   **SpecificheSoftwarecomprensive** **dellecontromisure**

::

   Pag. 83 of 121

-  **Controllo Configurazioni** : verificare i parametri intrinseci di
   configurazione dell'applicazione;

-  **Buffer Validation** : verificare la presenza di buffer overflow
   exploitabile attraverso la scrittura o la lettura di un numero di
   dati superiore alla reale capacità del buffer stesso.

L'esame del codice sorgente applicativo deve portare alla produzione,
mediante la Static Analysis, delle seguenti tipologie di documenti:

-  **Report delle Vulnerabilità riscontrate** : report di dettaglio
   delle vulnerabilità riscontrate nella fase di analisi statica del
   codice tramite gli strumenti a supporto;

-  **Remediation Plan** : report che analizza i falsi positivi ed
   indirizza la risoluzione delle problematiche riscontrate nell'analisi
   stessa.

La figura che segue sintetizza gli elementi in input e l'output prodotto
dal processo SAST:
