.. _esigenze-e-ambiti-di-applicazione:

4 ESIGENZE E AMBITI DI APPLICAZIONE
===================================

.. _il-panorama-delle-vulnerabilità-applicative:

4.1 IL PANORAMA DELLE VULNERABILITÀ APPLICATIVE
-----------------------------------------------

Il panorama delle minacce per la sicurezza delle applicazioni è in
costante evoluzione.

Secondo la fonte Gartner^1 , negli ultimi tempi **OLTRE IL 75% DEGLI
ATTACCHI SONO STATI INDIRIZZATI DIRETTAMENTE VERSO LE APPLICAZIONI**.

I fattori chiave di questa evoluzione sono i progressi fatti dagli
attaccanti, il rilascio di nuove tecnologie, l'uso di sistemi sempre più
complessi.

Gli obiettivi degli attacchi sono le vulnerabilità che si celano
all'interno delle applicazioni software che forniscono un facile
percorso d'ingresso per compromettere i sistemi o lanciare ulteriori
attacchi e malware. Tra le cause c'è anche il fatto che fino ad ora si è
seguito un approccio concentrato soprattutto sulla correzione delle
difettosità funzionali e sulle performance delle logiche applicative,
trascurando l'attuazione di pratiche di progettazione e programmazione
che garantiscono la sicurezza del codice.

Da qui anche l'appello della comunità OWASP^2 che sottolinea la
necessità di accrescere la consapevolezza sulla sicurezza delle
applicazioni in quanto il SW non sicuro mette a repentaglio le
infrastrutture anche più critiche (finanziarie, sanitarie e difensive).

Per rispondere in modo efficace alle sfide di sicurezza delle
applicazioni, è necessario dotarsi di soluzioni adeguate per:

-  Migliorare la gestione del programma di sicurezza delle applicazioni.
   Le componenti chiave di un programma di sicurezza devono includere: o
   Risk Management Integration, o Architect & Developer Guidance, o
   Process Improvement (SDLC), o Secure Development Activities, o
   Vulnerability Management Integration;

-  Valutare il codice software e le applicazioni al fine di identificare
   le vulnerabilità;

-  Automatizzare la correlazione dei risultati della verifica della
   sicurezza per applicazioni interattive, statiche e dinamiche.

.. _sviluppo-applicazioni-sicure:

4.2 SVILUPPO APPLICAZIONI SICURE
--------------------------------

La sicurezza informatica è l'insieme delle tecniche che mirano a
proteggere l'ambiente informatico che include gli utenti, le reti, le
applicazioni, i processi, e i dati; è una sicurezza “integrata” che
implica una visione della security a 360° e il cui obiettivo principale
è di ridurre i rischi, compresa la prevenzione o mitigazione degli
attacchi informatici.

Le applicazioni software dovrebbero avere caratteristiche di sicurezza
base di default ( **Secure By Default** ) quali ad esempio,
l'abilitazione automatica di meccanismi di costruzione di password
complesse piuttosto che procedure di rinnovo delle stesse secondo una
scadenza di natura temporale.

(^1) https://www.gartner.com/ (^2) A free and open software security
community (https://www.owasp.org)

::

   Pag. 11 of 121

Allo scopo di proteggere un sistema informativo, è pertanto necessario
che ogni sua componente disponga di un proprio meccanismo di protezione.
La costruzione di strati multipli di controlli di sicurezza posti lungo
un sistema è definita **Defence in Depth**.

La Defense-in-Depth è l'approccio alla sicurezza delle informazioni che
prevede il raggiungimento di una adeguato livello di sicurezza
attraverso l'utilizzo coordinato e combinato di molteplici contromisure.

Questa strategia difensiva si fonda sull'integrazione di differenti
categorie di elementi: persone, tecnologie e modalità operative. La
ridondanza e la distribuzione delle contromisure possono essere
sintetizzate in una “difesa a differenti livelli” (“Layered Defenses”).
Il concetto è di derivazione militare e si basa sull'assunto che nel
caso in cui un attacco abbia successo, a causa del fallimento di un
meccanismo di sicurezza, altri meccanismi di sicurezza possono
intervenire per consentire un'adeguata protezione dell'intero Sistema.

Diverse sono le iniziative che si sono incentrate sulle problematiche
Secure Development promuovendo azioni di sensibilizzazione (indirizzate
ad aziende e community di sviluppatori) quali:

-  la diffusione delle fondamentali best practices in materia di
   sicurezza applicativa (le prime tra tutte riconducibili ad una buona
   ingegnerizzazione del software);

-  una piena comprensione delle minacce più comuni (compresi i difetti
   propri dei linguaggi di programmazione);

-  ancora più importante, una considerazione della problematica fin
   dalle prime fasi del ciclo di sviluppo.

L'adozione di un Secure Software Development Life Cycle (SSDLC) atto a
considerare ed implementare opportune attività di sicurezza nel corso di
tutte le sue fasi del ciclo di vita del SW, dalla analisi alla
progettazione, sviluppo, test fino alla manutenzione è una necessità
inderogabile per rispondere alla domanda di sicurezza e per ridurre i
costi che comporta trascurarla.

.. _security-tools:

4.3 SECURITY TOOLS
------------------

Nell'ambito della cybersecurity, **Forrester** nel suo report " **Five
steps to reinforce and harden application security** "^3 sottolinea la
necessità di cooperazione tra i team Security & Risk (S&R) e gli IT
manager (I&O), ribadendo più volte come i primi non siano in grado, da
soli, di coprire tutte le vulnerabilità scaturite dalle nuove esigenze
in ambiti IT e digital business. Dal punto di vista dell'analista,
infatti, l'IT team deve adottare, attraverso opportuni meccanismi di
automazione e integrazione, le **security practices** all'interno di una
‘ **continuous delivery pipeline** '. Questo garantisce una maggiore
visibilità nelle interaizoni tra hardware, software, servizi web e
customer data. I professionisti I&O hanno quindi l'obiettivo di creare
un ambiente di sicurezza ‘responsive’.

A tal fine, Forrester propone 5 step per costruire un **responsive
security environment** :

(^3)
https://www.forrester.com/report/Five+Steps+To+Reinforce+And+Harden+Application+Security/-/E-RES
**Physical Perimeter Internal Network Host Application Data Layered
Approch to IT Security Policies Procedure Awareness** **Figura 1 -
Defence-in-Depth model for IT**

(^) Pag. 12 of 121 Innanzitutto è necessario eliminare tutte le
problematiche di sicurezza spesso derivanti da vulnerabilità
riconducibili a servizi non più utilizzati e non più mantenuti o una
cattiva gestione degli accessi e delle autorizzazioni. Tale attività
deve essere svolta attraverso la collaborazione tra i team dedicati (I&O
e S&R). In aggiunta, il censimento delle componenti applicative
(attraverso un approccio ‘application modeling’) consente di ottenere
ulteriori benefici in termini di: riduzione del mean-time-to-repair
(attraverso l'impiego di strumenti di gestione della configurazione a
sostegno del processo di monitoraggio delle modifiche applicative e
dell'infrastruttura a supporto); utilizzo limitato di software per
l'analisi delle vulnerabilità di terze parti (la visione completa
dell'applicazione e di come interagisce con gli altri sistemi esistenti
consente di limitare l'uso di ulteriori strumenti); rapida rimozione dei
‘difetti’ che possono generare vulnerabilità. Generalmente l'accesso non
autorizzato ai dati consegue essenzialmente da vulnerabilità derivanti
da un hardening non adeguato, da problematiche di sicurezza nel
software/hardware e/o da una cattiva progettazione del sistema stesso;
consentendo l'accesso intenzionale, non autorizzato, ai dati presenti
all'interno della propria organizzazione. E' necessario lavorare a
livello infrastrutturale per bloccare tutti gli accessi non autorizzati
monitorando costantemente network e traffico sui sistemi. I team di
infrastruttura e quelli della sicurezza dovrebbero cooperare nel
processo di identificazione delle policy e dei tool per il monitoraggio,
delle applicazioni in particolare, per verificare in tempo reale
eventuali cambiamenti prima che questi si traducano in vulnerabilità. E'
richiesto l'impiego di sistemi infrastrutturali e tool tecnologici a
supporto delle politiche di sicurezza. Questi svolgono un ruolo
determinante nella prevenzione (e nella risposta) delle intrusioni in
quanto, a fronte di anomalie (legate ad esempio all'utilizzo delle Cpu o
al numero delle transazioni di sistema), avendo il controllo di tutto lo
stack tecnologico, riescono a fornire in tempo utile alert ed
informazioni al team di sicurezza. Un sistema di controllo di questo
tipo, accelera il mean-time-to-detection (il tempo di localizzazione di
una vulnerabilità o di un attacco) e il tempo di risposta. Inoltre, cosa
molto importante, riduce il range dei falsi allarmi di sicurezza (grazie
ai controlli incrociati tra i team di infrastruttura e i team della
sicurezza). E' estremamente importante l'attività di tracciamento e di
monitoraggio in tutte le fasi del ciclo di vita di sviluppo
dell'applicazione. L'obiettivo è di analizzare tutte le fonti dati
nonché il materiale di ciascuna applicazione, e monitorarne ogni minimo
cambiamento. A tal fine, dal punto di vista tecnologico, Forrester
suggerisce: i) l'integrazione degli Application Release Automation tool
nei processi di auditing; ii) ii) adottare sistemi di Automate Change
Tracking e dashboard a supporto dei team di I&O e S&R. Le azioni
precedenti concorrono alla creazione di un vero e proprio stack
tecnologico incentrato sulla sicurezza applicativa. Al fine di
indirizzare correttamente una protezione efficace delle applicazioni, è
di fondamentale importanza individuare le vulnerabilità (e porvi
rimedio) sin dalle prime fasi del ciclo di vita dello sviluppo, quando è
ancora poco costoso e poco rischioso intervenire. **Step 1** : rimuovere
le ‘inconsistenze’ e creare un ‘conto’ dei materiali **Step 2** :
limitare e rinforzare l'accesso ai sistemi e ai network device;
monitorare i cambiamenti **Step 3** : assistere i team di Security&Risk
sul fronte intrusion detection & response **Step 4** : ‘loggare’ quanto
più possibile **Step 5** : creare uno stack di application security tool

(^) Pag. 13 of 121 **Figura 2 - Augment the life cycle with security
tools** [Fonte: Forrester, Five Steps To Reinforce And Harden
Application Security] Per comporre lo stack, queste le tecnologie cui
gli I&O professional dovrebbero porre attenzione:

-  **Static Application Security Testing (SAST)** , tool che esaminano
   il codice binario e il codice di programmazione delle applicazioni
   senza ‘mandare in esecuzione’ l'applicazione (ossia senza la
   necessità di farla girare sui sistemi nei processi di testing);

-  **Software composition analysis (SCA) tool** , tecnologie che
   consentono di analizzare le building block applicative per scovare
   vulnerabilità all'interno, per esempio, delle librerie, dei
   componenti open source o dei vari ‘blocchi’ di software che
   compongono l'applicazione.

-  **Dynamic Application Security Testing (DAST)** , sistemi che
   permettono di osservare in dettaglio come si comporta l'applicazione
   quando è in funzione per scovarne imperfezioni o vulnerabilità prima
   che si prosegua con lo step di sviluppo successivo;

-  **Fuzz testing tool** , sistemi che analizzano le vulnerabilità sul
   fronte di protocolli network, application data e input location
   (sempre durante i cicli di testing applicativo);

-  **Hybrid analysis tool** , si tratta di tecnologie di testing per la
   sicurezza delle applicazioni che integrano funzionalità di
   Instrumented application security testing (Iast) e Runtime
   application security testing (Rasp) utili per ridurre i falsi
   positivi e i falsi negativi generalmente evidenziati dai sistemi
   Dast;

-  **Vulnerability assessment tool** , sistemi utili a rendere visibili
   eventuali criticità a livello di sistema operativo, configurazione
   dei sistemi, micro-configurazioni dei server e delle altre
   architetture con cui l'applicazione in sviluppo dovrà interagire una
   volta messa in produzione;

(^) Pag. 14 of 121

-  **Penetration testing tool** , tecnologie utili a ‘validare’
   l'assessment delle vulnerabilità perché mostrano come potrebbero
   avvenire gli attacchi simulando la penetrazione nei sistemi e nelle
   applicazioni.

::

   Pag. 15 of 121
