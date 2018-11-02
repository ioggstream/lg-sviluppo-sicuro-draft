.. _figura-17---esempio-di-flusso-informativo-del-trattamento:

Figura 17 - Esempio di flusso informativo del trattamento
=========================================================

.. _privacy-implementation-strategy:

10.1.6 Privacy Implementation Strategy
--------------------------------------

La Privacy Implementation Strategy prevede che i progettisti del
software definiscano e selezionino un modello di ciclo di vita adeguato
all'ambiente di produzione e di sviluppo, all'ambito, all'ampiezza e
alla complessità del progetto, parametrato sulle necessità emerse dai
risultati della data protection impact assessment per la privacy
(10.1.4).

Dovranno essere documentate:

-  I principi generali della privacy applicabili alla progettazione del
   software (10.1.1)

-  Gli obiettivi di protezione che il software dovrebbe garantire
   (10.1.2)

-  I principi della privacy by design applicabili alla progettazione del
   software (10.1.3.2)

-  I risultati della data protection impact assessment per il software e
   l'individuazione dei requisiti di protezione per la privacy (10.1.4)

-  Le tipologie di Informazioni Personali Identificabili (PII) trattate
   nell'ambiente software (10.1.4.1)

-  La descrizione del flusso informativo derivante dal trattamento
   all'interno del software (10.1.5)

.. _implementazione-della-strategia-nelle-fasi-di-sviluppo-del-software:

10.2 IMPLEMENTAZIONE DELLA STRATEGIA NELLE FASI DI SVILUPPO DEL SOFTWARE
------------------------------------------------------------------------

.. _scopo-1:

.. _scopo-1:

10.2.1 Scopo
~~~~~~~~~~~~

Gli elementi definiti all'interno della Privacy Implementation Strategy
(10.1.6), i requisiti di protezione della privacy e le strategie di
design per la privacy (ricavabili sulla base di quelli individuati da
ENISA in DR-4 ), dovranno essere inquadrati all'interno di ciascuna fase
della Engineering privacy by design (10.2.3) e rimappati per ciascuna
fase del ciclo di vita dei software (10.2.2), così come definiti nelle
fasi *Software life Cycle Processes* (cfr. DR-3 ).

.. _le-fasi-di-implementazione-della-engineering-privacy-by-design:

10.2.2 Le fasi di implementazione della Engineering Privacy by Design
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

La seguente impostazione è stata maturata dal *Privacy Engineering
Framework* del MITRE (cfr. DR-9 ), prevedendo le seguenti attività:

Attività Descrizione **Definizione dei requisiti privacy:** Definizione
delle proprietà della privacy di un software in modo che possa essere
integrato con il design e lo sviluppo **Design e sviluppo privacy:**
Definizione del design e sviluppo dei requisiti previsti

**Verifica e validazione privacy:** Riscontro della conferma che i
requisiti di privacy sono stati correttamente implementati e validati
attraverso delle verifiche **Tabella 9 - Fasi dell'Engineering Privacy
by Design**

**Trasferisce** (^) **Trasferisce Riceve Fruizione Servizio Utilizza**
(^) **Tratta Cancella Dato Dato Dato Dato** Legenda Flusso dei dati
Istruzione Servizio **Cancella**

::

   Pag. 96 of 121

**10.2.2.1 Definizione dei requisiti privacy**

**Input** : Requisiti di privacy di base e test; Normative, best
practice e procedure applicabili sulla privacy; requisiti funzionali;
Profili di rischio per la privacy.

**Attività** : Svolgere una Data Protection Impact Assessment
parametrata sugli obiettivi di protezione individuati; Selezionare e
perfezionare i requisiti di protezione per la privacy di base e
effetturare dei test; Sviluppare dei requisiti di protezione della
privacy personalizzati e testarli sulla base dei risultati della DPIA.

**Output** : Requisiti di protezione per la privacy specifici per il
software.

**10.2.2.2 Design e sviluppo privacy**

**Input** : Requisiti Architetturali e funzionali specifici per la
privacy

**Attività** : Identificare delle strategie e dei modelli di design
della privacy; Identificare dei controlli di privacy, dei criteri
tecnici e delle policy; Sviluppare dei dati e dei modelli di processo
che riflettano i controlli di privacy identificati; Allineare, integrare
e implementare i controlli di privacy con gli elementi funzionali;
Analizzare il rischio del design di privacy complessivo.

**Output** : Componenti del software implementati; Mitigazione dei
rischi accettabili per la privacy residua

**10.2.2.3 Verifica e validazione privacy**

**Input** : Componenti del software implementati; Requisiti di privacy
specifici del sistema e test]; Politiche e procedure di privacy
applicabili.

**Attività** : Sviluppare / perfezionare dei test sulla privacy;
Eseguire delle verifiche sulla privacy; Verificare il comportamento
operativo rispetto alle politiche e alle procedure sulla privacy
applicabili.

**Output** : Risultati dei test di privacy; Documentazione delle
Incoerenze sulla privacy documentate; Descrizione del piano di
trattamento della privacy.

.. _integrazione-della-engineering-privacy-by-design-nel-software-life-cycle-process:

10.3 INTEGRAZIONE DELLA ENGINEERING PRIVACY BY DESIGN NEL SOFTWARE LIFE CYCLE PROCESS
-------------------------------------------------------------------------------------

Il diagramma illustrato nella Figura 18, definisce la mappatura delle
fasi della Engineering Privacy by Design sulle fasi del Software Life
Cycle Process:

::

   Pag. 97 of 121
