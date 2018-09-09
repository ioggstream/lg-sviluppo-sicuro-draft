.. _figura-11-input-ed-output-della-fase-risk-assessment:

Figura 11: Input ed Output della fase Risk Assessment
=====================================================

::

   Risk
   Assessment

-  **Requisitiutentee software**

-  **Specificae HLD(soloperapplicazione** **esistente)** -
   **SpecificadeiRequisitidiSicurezza**

::

   Pag. 79 of 121

.. _identificazione-degli-strumenti-a-supporto:

9.1.2 Identificazione degli strumenti a supporto
------------------------------------------------

I tools riportati nel paragrafo 6.2.2 sono stati comparati^24 sulla base
dei parametri riportati nella tabella che segue (in particolare vengono
identificati 8 parametri per ogni sezione):

::

   Software Functional Requirements
   (Software Requirement Engineering)
   Requirement Elicitation

-  Interview

-  Joint Application Development (JAD)

-  Brainstorming

-  Questionnaire and Checklist

-  Case Modeling

-  Scalability Requirement Specification

-  Use Case Modeling

-  Tradition Requirement Specification

-  Templates

-  Glossary and Ontology

-  Prototype Requirement Validation

-  Audit

-  Walkthrough

-  Prototyping **Software Security Requirements (Security Requirement
   Engineering)**

-  Fair Exchange requirement

-  Non-repudiation security requirement

-  Role-based access control security requirement

-  Secrecy (Confidentiality) and Integrity

-  Authenticity

-  Freshness

-  Secure Information Flow

-  Guarded Access

**Software Functional Requirements (Product)**

::

   Tools Glossary &
   Ontology
   Checklist Templates Use Case
   Modeling
   Prototyping
   & Audit
   TRS Scalability External
   Interface
   RequisitePro X X √ √ √ √ X √
   CaseComplete √^ X^ √^ √^ √^ √^ X^ √^
   Analyst Pro X X X √ X √ √ √
   Optimal Trace X X √ √ √ √ X √
   DOORS X X √ √ √ √ √ √
   GMARC X X √ X √ √ X √
   Objectiver √ √ √ X √ √ X √
   RDT √ X √ X √ √ √ √
   RDD- 100 √^ X^ √^ X^ X^ √^ X^ √^

(^24) https://www.researchgate.net/publication/233952819

(^) Pag. 80 of 121 **Tools Glossary & Ontology Checklist Templates Use
Case Modeling Prototyping & Audit TRS Scalability External Interface
RTM** X X √ X X √ X √ **Reqtify** X X X √ √ √ X √ **TcSE** X^ X^ X^ √^
X^ √^ X^ √^ **Code Assure** X X X X X √ X √ **IRqA** X √ X √ X √ X √
**Software Security Requirements (Security)** Tools **Fair Exchange Non-
repudiation Rbac Secrecy & Integrity Authenticity Secure Informat. Flow
Guarded Access Freshness RequisitePro** √^ X^ X^ X^ X^ X^ X^ √^
**CaseComplete** √ X X X X X X √ **Analyst Pro** √ X √ X √ X X X
**Optimal Trace** √ X X X X X X X **DOORS** √^ X^ √^ X^ √^ X^ √^ √^
**GMARC** X X X X X X X √ **Objectiver** X X X X X X X √ **RDT** X^ X^
X^ X^ X^ X^ X^ √^ **RDD- 100** √ X X X X X X √ **RTM** X X √ √ √ X √ √
**Reqtify** √^ X^ X^ X^ X^ X^ X^ √^ **TcSE** X √ √ √ √ √ √ √ **Code
Assure** X √ √ √ √ √ √ √ **IRqA** X X √ X X X X X Ad ogni parametro
viene assegnato un punteggio di 12,5 (100/8). Il tool che presenta un
punteggio totale maggiore (il punteggio di 12,5 viene moltiplicato per
il numero totale di parametri soddisfatti) è da considerarsi quindi il
migliore.

::

   Pag. 81 of 121

**Valutazione dei tool:**

::

   Tools Product Security

**RequisitePro** (^) 62.5 25.0 **Case Complete** (^) **75.0** 25.0
**Analyst Pro** (^) 50.0 37.5 **Optimal Trace** (^) 62.5 12.5 **DOORS**
(^) **75.0** 62.5 **GMARC** (^) 50.0 12.5 **Objectiver** (^) 62.5 12.5
**RDT** (^) 62.5 12.5 **RDD-** (^100) 50.0 25.0 **RTM** (^) 37.5 50.0
**Reqtify** (^) 50.0 25.0 **TcSE** (^) 37.5 62.5 **Code Assure** (^)
25.0 **87.5 IRqA** (^) 50.0 12.5 Secondo la metodologia adottata, come
si evince dalla tabelle di sintesi:

-  **DOORS** risulta essere il tool migliore sotto entrambi i punti di
   vista;

-  **CodeAssure** risulta essere il migliore dal punto di vista
   prettamente legato ad aspetti di sicurezza.

.. _progettazione-di-applicazioni-sicure:

9.2 PROGETTAZIONE DI APPLICAZIONI SICURE
----------------------------------------

Le azioni di sicurezza di questa fase possono essere così sintetizzate
**:**

-  **Analisi e modellazione delle minacce** , attraverso
   l'identificazione dei componenti applicativi coinvolti, delle
   interfacce e degli agenti che potrebbero minacciare il sistema;

-  **Analisi della superficie d'attacco e della finestra di
   opportunità,** allo scopo di individuare le parti del sistema che
   possono essere esposte ad attacchi e pertanto lo rendono vulnerabile;

-  **Piano di mitigation,** attraverso l'identificazione delle
   contromisure da adottare in questa fase al fine di mitigare le
   potenziali minacce individuate (utilizzando anche tool automatici e
   semiautomatici);

-  **Secure Design Refactoring** , revisione progettuale che attua le
   contromisure individuate; produzione di un High Level Design conforme
   ai principi del Secure by Design;

-  Questa fase produce come output finale la Reportistica/documentazione
   completa che sintetizza i risultati per ogni punto precedente
   (Specifiche Software comprensive delle contromisure).

Questa fase è inoltre responsabile della revisione dei requisiti di
sicurezza individuate nella fase precedente di definizione dei requisiti
di sicurezza (paragrafo 9.1).

La figura che segue sintetizza gli elementi in input e l'output prodotto
dal processo di Progettazione di software sicuro:

::

   Pag. 82 of 121
