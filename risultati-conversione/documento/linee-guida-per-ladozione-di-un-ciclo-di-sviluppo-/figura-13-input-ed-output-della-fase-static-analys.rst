.. _figura-13-input-ed-output-della-fase-static-analysis:

Figura 13: Input ed Output della fase Static Analysis
=====================================================

.. _identificazione-degli-strumenti-a-supporto-2:

.. _identificazione-degli-strumenti-a-supporto-2:

9.3.1 Identificazione degli strumenti a supporto
------------------------------------------------

Nel paragrafo 6.4.16.3.2 sono stati presentati i tool a supporto di
questa fase. Tra questi si raccomandano:

-  closed source o IBM App Scan (versione SAST), o Checkmarx, o CodeDx,
   o HP fortify.

-  open source o SonarQube, o FxCop (.NET), o BRAKEMAN (Ruby on Rails),
   o PMD (Java, XML e XSL), o PYLINT (Python), o CppCheck (C/C++), o
   FindBugs (Java), o JSHint (Javascript), o OWASP Dependency-Check
   (Java,.NET, Ruby, Node.js, Python, supporto limitato per C/C++).

L'utilizzo combinato dei tool sopra indicati consente una copertura ad
ampio spettro eliminando quasi del tutto la revisione manuale che
richiederebbe molto tempo.

La tabella che segue mette a catalogo i risultati finali della
valutazione di alcuni tool sopra indicati:

::

   Tools Categoria Fase Report

**Checkmarx** (^) SAST Implementation / Verification (^) Vedi Appendice
2.a **CodeDx** SAST/DAST Implementation/Verification (^) Vedi Appendice
2.b

.. _static-analysis-report-delle-vulnerabilita:

Static Analysis • Report delle Vulnerabilita'
---------------------------------------------

::

   riscontrate

-  **Specifiche Softwarecomprensive** **dellecontromisure**

::

   Pag. 84 of 121
   Tools Categoria Fase Report

**SonarQube/SonarLint** SAST Implementation (^) Vedi Appendice 2.c 1)
**Checkmarx** , è un tool per l'analisi statica del codice, posizionato
da Gartner nel quadrante Challengers nell'ambito dell'Application
Security Testing (AST). Supporta numerosi linguaggi (vedi scheda nella
tabella di cui sopra). Può essere integrato a vari livelli nell'ambito
della fase di Implementation: IDE, build server, bug tracking tools. 2)
**CodeDx** consente di effettuare la verifica di eventuali vulnerabilità
di programmi e software presi in considerazione. CodeDx riunisce una
serie di strumenti di analisi del codice (Checkmarx, **IBM App Scan** ,
**Veracode** ), sia gratuiti che commerciali, che consentono a loro
volta di individuare e correggere agevolmente eventuali bugs nel codice
da analizzare. Uno screenshot dell'interfaccia CodeDx è riportata nella
figura che segue: 3) **SonarQube** , consente di introdurre il controllo
formale fin dall'inizio del ciclo di vita del software, attraverso
l'introduzione di Quality Gate nelle fasi tipiche di passaggio tra lo
sviluppo e la verifica e tra la verifica e la produzione.

.. _verifica-della-sicurezza-delle-applicazioni:

9.4 VERIFICA DELLA SICUREZZA DELLE APPLICAZIONI
-----------------------------------------------

Le azioni di sicurezza da intraprendere in questa fase sono così
sintetizzate:

-  **Analisi dinamica** : attraverso l'attuazione di test dinamici di
   sicurezza sull'applicazione in esecuzione in ambiente controllato;

-  **Penetration Test** : attraverso l'esecuzione di scansioni ed
   analisi della superficie di attacco;

-  **Test di autenticazione multilivello** : attraverso la verifica
   delle modalità di gestione dell'accesso degli utenti;

-  **Business Logic test** : attraverso l'esecuzione di test manuali
   sulle applicazioni in fase di esecuzione;

-  **Analisi dei risultati** : attraverso l'individuazione e la
   rimozione dei falsi positivi;

::

   Pag. 85 of 121

-  **Remediation Plan** : attraverso la definizione del piano di rientro
   e la produzione di reportistica di sintesi e di dettaglio; Proof of
   Concept delle vulnerabilità riscontrate comprensiva di azioni per la
   riduzione della superfice d'attacco.

L'esame delle Applicazioni in esecuzione in ambiente di test, deve
portare alla produzione, mediante la Dinamic Analisys delle seguenti
tipologie di documenti:

-  **Vulnerability Assessment** : report di dettaglio delle
   vulnerabilità riscontrate nella fase di analisi dinamica
   dell'applicazione tramite gli strumenti a supporto;

-  **Remediation Plan:** report che analizza i falsi positivi ed
   indirizza la risoluzione delle problematiche riscontrate nell'analisi
   stessa.

La figura che segue sintetizza gli elementi in input e l'output prodotto
dal processo DAST:
