.. _linee-guida-per-ladozione-di-un-ciclo-di-sviluppo-software-sicuro:

9 LINEE GUIDA PER L'ADOZIONE DI UN CICLO DI SVILUPPO SOFTWARE SICURO
====================================================================

.. _definizione-dei-requisiti-di-sicurezza:

9.1 DEFINIZIONE DEI REQUISITI DI SICUREZZA
------------------------------------------

I principali requisiti di sicurezza da definire sono:

-  **Riservatezza e Integrità.** I due più importanti aspetti della
   sicurezza sono Riservatezza e Integrità. La Riservatezza significa
   che le risorse possono essere utilizzate solo dalla parte legittima.
   L'integrità dei dati significa che devono essere modificabili solo
   dalle persone autorizzate.

-  **Autenticità.** Il terzo requisito di sicurezza principale è
   l'Autenticità: *Message authenticity* (o *data* origin authenticity),
   *entity authenticity* (chiamata anche *authentication* )\ *.*

-  **Non-ripudio.** Garantisce che qualsiasi azione sul sistema non
   possa essere successivamente rinnegata.

-  **Flusso Informativo**. Il livello di sicurezza può avere regole
   diverse. Generalmente si considerano due livelli: alto (altamente
   sensibile o altamente attendibile) e basso (meno sensibile o meno
   attendibile). Laddove componenti di sistema considerati di alto
   livello interagiscono con parti meno attendibili, si deve garantire
   che non vi sia alcuno scambio di dati dall'alto verso il basso (vale
   invece il contrario ossia ci può essere lo scambio di dati dal basso
   verso l'alto *non up-flow* ).

-  **Controllo Accessi**. Uno dei requisiti di sicurezza principali è il
   controllo degli accessi, il che significa che solo un utente fidato
   può avere accesso ad un sistema sicuro. **Role-Based Access Control**
   **(RBAC)** : realizza un importante meccanismo di controllo degli
   accessi per tutelare i beni. I privilegi di accesso alle risorse
   dipendono dal ruolo che assumono nel tempo gli individui all'interno
   dell'Organizzazione. Ai ruoli sono associati profili che definiscono
   comandi, transazioni e accessi ai dati. L'assegnazione dei ruoli è
   centralizzata.

Le principali azioni di sicurezza da attuare sono:

-  **Definizione degli elementi di sicurezza applicativa** , finalizzata
   alla valutazione dei requisiti relativamente a **:** o Integrità,

::

   o Autenticità,
   o Riservatezza,
   o Disponibilità,
   o Non-ripudio,
   o Autorizzazione.

-  **Definizione dei requisiti di privacy** , attraverso la raccolta
   strutturata delle seguenti categorie di informazioni:

::

   o Dati personali,
   o Servizi di terze parti,
   o Policy.

-  **Risk assessment** , finalizzato alla valutazione del rischio (vedi
   Paragrafo 9.1.1).

::

   o Consolidamento dei Requisiti , che consiste nella review dei requisiti di sicurezza e privacy a
   seguito del Risk Assessment;

-  A completamento di questa fase è necessario produrre la
   Reportistica/documentazione completa che sintetizza i risultati per
   ogni punto precedente.

::

   Pag. 78 of 121

Si evidenzia che in questa fase devono essere tenuti in considerazione
anche gli aspetti di integrazione e di interfaccia con gli eventuali
altri moduli dell'ecosistema software.

Inoltre vanno considerati i requisiti di sicurezza applicativa di
carattere generale attraverso l'attuazione di best practices che
individuano i requisiti di sicurezza che devono essere adottati nel
processo di sviluppo di un'applicazione sicura: Performance, Password
nel codice sorgente, Privilegi esecutivi minimi, Fattore di integrità,
Input data validation, Gestione dell'output, etc. (per ulteriori
dettagli si rinvia al deliverable **D03.Fase1-SP2 - Linee Guida per lo
sviluppo sicuro di codice** , paragrafo **4.1 Progettazione e sviluppo
dell'Applicazione: direttive standard** ). Tali requisiti di sicurezza
applicativa devono essere mutuati in questa fase sulla base dei
requisiti, funzionali e non funzionali, individuati.

.. _risk-assessment:

9.1.1 Risk Assessment
~~~~~~~~~~~~~~~~~~~~~

L'obiettivo dell'analisi del rischio è da una parte identificare,
valutare e misurare la probabilità e la gravità dei rischi (ciò che
viene generalmente indicato con il nome di *Risk Assessment* ) e
dall'altra decidere come comportarsi a fronte dei rischi identificati
(ciò che viene generalmente indicato con il nome di *Risk Management* ).
Si riporta di seguito uno schema per il *Risk Assessment* :

Si sottolinea che la fase di Risk Assessment è quella che concorre a
generare i requisiti di sicurezza che saranno gestiti, insieme con gli
altri individuati non necessariamente durante la Risk Analysis, con
l'ausilio dei “Software Requirements Tools”.

La figura che segue sintetizza gli elementi in input e l'output prodotto
dal processo di Risk Assessment:
