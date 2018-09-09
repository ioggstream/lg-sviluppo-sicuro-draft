.. _figura-5-modello-fasi-ssdlc:

Figura 5: Modello fasi SSDLC
============================

**Requisiti** : in questa fase vengono effettuate le analisi dei
requisiti di sicurezza, dei rischi, delle probabilità di impatto delle
minacce, dei casi di abuso tramite rappresentazione UML. In questa fase
inoltre si considerano le best practices di carattere generale nella
definizione dei requisiti di sicurezza;

**Progettazione** : in questa fase si esamina il sistema in divenire con
l'ausilio di tecniche di analisi e modellazione delle minacce,
producendo requisiti di sicurezza di dettaglio che si aggiungono a
quelli prodotti dalla precedente fase;

::

   Requisiti Progettazione Implementazione Verifica Validazione Supporto
   Risk

.. _assessment:

Assessment
----------

::

   Threat

.. _modeling:

Modeling
--------

::

   Static
   Analysis
   Dynamic
   Analysis
   Final Review
   Secure
   Security
   Monitoring
   Pag. 44 of 121

**Implementazione** : in questa fase si realizza il sistema attraverso
la programmazione di codice sicuro, test di sicurezza basati
sull'analisi delle minacce ed analisi statica del codice sorgente.
Quest'ultima può produrre nuovi requisiti di sicurezza che indirizzano
la revisione del codice;

**Verifica** : in questa fase si analizzano gli aspetti di sicurezza del
sistema in esecuzione in un ambiente controllato impiegando tecniche e
strumenti di analisi dinamica;

**Validazione:** è la fase immediatamente prima del rilascio, viene
effettuta una final security review per al verifica del rispetto dei
requisiti dati;

**Supporto** : in questa fase si esamina il sistema in essere con
l'ausilio di tecniche di: analisi e modellazione delle minacce e/o
verifica statica/dinamica del codice applicativo, al fine di produrre
nuovi requisiti di sicurezza di dettaglio che indirizzano una eventuale
fase di reingegnerizzazione e/o di patching del sistema in oggetto.

.. _requisiti:

6.2 REQUISITI
-------------

La fase di analisi e specifica dei requisiti è fondamentale nel ciclo di
vita dello sviluppo software.

Di seguito si riportano i linguaggi e gli strumenti utili alla fase di
definizione dei requisiti di sicurezza del software.

.. _linguaggi-per-la-specifica-dei-requisiti:

6.2.1 Linguaggi per la specifica dei requisiti
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Un linguaggio di specifica in ambito security può essere considerato:

-  un linguaggio di specifica software utilizzato per indicare gli
   attacchi (AsmL e UML state charts ),

-  l'estensione di un linguaggio di specifica software utilizzato per
   rappresentare gli attacchi (Misuse Cases , Abuse Cases, AsmLSec, and
   UMLintr ) e i requisiti di sicurezza (UMLsec, SecureUML, Secure
   Tropos, and Misuse Cases),

-  un *attack specification language* (e.g., STATL and Snort Rules ).

**UMLsec** è un'estensione di UML per lo sviluppo di sistemi sicuri e
usa stereotypes, tags e constraints per specificare i requisiti di
sicurezza. Gli stereotipi servono come etichette per gli elementi del
modello UML per introdurre informazioni al modello e specificare i
vincoli che devono essere soddisfatti dal modello. I tag sono associati
con gli stereotipi e sono utilizzati per specificare in modo esplicito
una semplice proprietà di un elemento del modello. UMLsec definisce 21
stereotipi da utilizzare per rappresentare i seguenti requisiti di
sicurezza:

-  fair exchange (non barare tra le parti),

-  non-repudiation (un'azione non si può negare),

-  role-based access control,

-  secure communication link,

-  confidentiality,

-  integrity,

-  authenticity,

-  freshness of a message (ad esempio nonce),

-  secure information flow among components,

-  guarded access (uso di protezioni per imporre il controllo di
   accesso)

Sette di questi stereotipi hanno associati tag e nove stereotipi hanno
vincoli. Questi stereotipi possono essere utilizzati per i diagrammi dei
casi d'uso, i diagrammi delle classi, diagrammi di stato, diagrammi di
attività, diagrammi di sequenza, diagrammi e implementazioni per
specificare i requisiti di sicurezza in un modello UML (per entrambe le
specifiche relative ai requisiti e al design). Un insieme di **tools**
sono stati

(^) Pag. 45 of 121 realizzati per consentire agli sviluppatori la
modellazione attraverso l'impiego di UMLsec e quindi di verificare
questi modelli (utilizzando il model checking). **SecureUML** SecureUML
è un'altra estensione di UML che si concentra sulla specifica delle
politiche di controllo degli accessi basati sui ruoli (queste politiche
possono essere considerati come requisiti di sicurezza) in un modello.
SecureUML propone nove stereotipi che possono essere utilizzati per
annotare un diagramma delle classi, con informazioni di controllo di
accesso basato sui ruoli. SecureUML utilizza l'oggetto Constraint
Language (OCL) per specificare i vincoli per le risorse, le azioni e le
autorizzazioni. Contrariamente a UMLsec, questi vincoli possono essere
specificati in base alle esigenze del singolo componente software.
**Snort Rules** è un network intrusion detection system (IDS) ampiamente
utilizzato. Esso utilizza scenari di attacchi specificati come regole
per rilevare gli attacchi attraverso la rete. Una Snort rule specifica
quale azione deve essere intrapresa se la regola è associata ad un
pacchetto di rete, gli indirizzi IP di origine e destinazione e le
porte, il protocollo della rete osservato, e la direzione del pacchetto
di rete. Un certo numero di opzioni possono anche essere specificate.
Queste opzioni vanno dalla registrazione di un messaggio alla ricerca di
una particolare stringa nel pacchetto. **Secure Tropos** può essere
utilizzato per lo sviluppo di software sicuro ed è un'estensione della
metodologia di sviluppo Tropos. Secure Tropos utilizza le nozioni di
*actor* (person(s), organization(s), software), *goal* (obiettivi che
gli attori vogliono ottenere), *soft goal* (un obiettivo la cui
realizzazione non può essere determinata in modo esplicito), *task* (un
compito per raggiungere un obiettivo), *resource* (fi sica o dati),
*security constraint* (specificato come le dichiarazioni di alto
livello), *secure goal* (utilizzato per soddisfare un vincolo di
sicurezza), *secure task* (un compito per raggiungere un obiettivo di
sicurezza), *secure resource* (una risorsa che è connessa a *security
constraints* , *secure goal* , *secure task* , oppure ad un'altra
*secure resource* ). Un *actor* può dipendere da un altro *actor* per
raggiungere un *goal/soft goal* , per svolgere un *task* , o rilaasciare
una risorsa. La notazione SecureTropos può essere utilizzato per
rappresentare vincoli di sicurezza (requisiti) sulle interazioni tra gli
attori durante la fase di specifica dei requisiti. **Misuse Cases** è un
tipologia di Use Case UML utilizzata per descrivere comportamenti
indesiderati del software. Un *misuse case* è avviato da un particolare
tipo di attore chiamato *mis-actor* (ad esempio, l'attore con intenti
maliziosi). *Misuse cases* e *mis-actors* possono essere utilizzati per
suscitare più casi d'uso per neutralizzare le minacce poste dai casi di
uso improprio. *Misuse cases* e *mis-actors* sono rappresentati in
colore nero pieno per distinguerli dai casi d'uso e dagli attori UML.
Due relazioni speciali chiamati “prevents” e " detects" mettono in
relazione *use cases* e *misuse cases*. Il processo può essere
utilizzato in modo graduale per sviluppare un diagramma dei casi d'uso
(compresi i *misuse cases* ) oppure, se necessario, può essere
utilizzato anche in modo iterativo. Secondo tale processo, dovrebbero
essere specificati prima gli *use cases* e poi i *misuse cases*. Dopo di
che, devono essere identificate le relazioni potenziali tra gli *use
cases* e i *misuse cases* perché spesso la funzionalità del software
viene utilizzata per attaccarlo. Infine, i nuovi *use case* devono
essere specificati per individuare o prevenire i *misuse cases*. Questi
nuovi use case costituiscono i requisiti di sicurezza di alto livello
del software e sono chiamati come " security use cases". **Abuse Cases**
Un altro modo per specificare il comportamento indesiderato di un pezzo
di software utilizzando i diagrammi UML è quello di sviluppare un *abuse
case model*. Un *abuse case model* specifica le interazioni pericolose
usando attori e *abuse case*. Non c'è differenza di notazione tra i
componenti di un *UML use case diagram* e un *abuse case model*. Si
raccomanda l'utilizzo di una struttura ad albero per gli approcci
multipli. Questo aggiunge ulteriori dettagli al modello e permette di
identificare tutte le possibili misure di sicurezza. Dettagli sugli
attori come le loro risorse, le competenze, e l'obiettivo dovrebbero
essere inclusi come testo. Gli *abuse case model* possono essere
utilizzati nelle fasi di progettazione e collaudo. **UMLintr** è
un'estensione di UML che utilizza stereotipi e tag per specificare
intrusioni (attacchi) utilizzando use case diagrams, class diagrams,
state charts, package diagrams. Gli attacchi vengono divisi in quattro
tipologie diverse. Ogni tipo è rappresentato come un pacchetto
stereotipato. Ci sono tre stereotipi definiti per le classi e dodici per
lo use case diagram. Gli stereotipi per le classi hanno anche i tag.

::

   Pag. 46 of 121

**Abstract State Machine Language (AsmL)** ASML è un linguaggio a stati
finiti machine-based eseguibile utilizzato anche per specificare scenari
di attacco. In generale, attacchi con step multipli possono essere
specificati in ASML. Tali scenari di attacco possono essere tradotti
automaticamente in *Snort rules* che possono poi essere utilizzati con
un'estensione di IDS Snort. Tali scenari di attacco sono in grado di
catturare più attacchi con step multipli, utilizzando le informazioni di
contesto. Le Snort rules, l'input standard di Snort, non possono
rappresentare attacchi con step multipli.

**AsmLSec** è un'estensione di ASML sviluppata per specificare scenari
di attacco. AsmLSec utilizza stati, eventi e transizioni per
rappresentare gli attacchi. Ogni transizione ha una origine e uno stato
di destinazione, una serie di condizioni da soddisfare e le azioni da
compiere. Gli scenari di attacco rappresentati in AsmLSec possono essere
tradotti automaticamente in ASML attraverso un compilatore appositamente
sviluppato. E' stato sviluppato un IDS che prende in input gli scenari
di attacco tradotti.

**UML State Charts for Security** i diagrammi di stato UML (senza alcuna
estensione) sono stati utilizzati per specificare gli attacchi. Gli
attacchi specificati nei diagrammi di stato possono essere collegati
alle Snort rules. Questi diagrammi di stato possono essere tradotti
manualmente nelle Snort rules e quindi possono essere poi utilizzati con
un'estensione di IDS Snort. Attraverso l'impiego dei diagrammi di stato,
è possibile rappresentare attacchi complessi con step multipli che
normalmente non possono essere rappresentati con ordinarie regole di
Snort rules.

**STATL** è un linguaggio di specifica a stati finiti machine-based
eseguibile. STATL utilizza due costrutti principali per specificare un
attacco: Stato e transizione. Ogni transizione deve avere un evento
associato che, quando si verifica, avvia la transizione. Le transizioni
hanno anche azioni facoltative che vengono eseguite una volta che una
transizione è avviata. Stato e transizione specifiche possono anche
avere il codice eseguibile al loro interno. Un ambiente di sviluppo per
STATL è inoltre disponibile e può essere utilizzato, tra le altre cose,
per visualizzare scenario di attacco specificati come macchina a stati.

.. _tool-per-la-specifica-dei-requisiti:

6.2.2 Tool per la specifica dei requisiti
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Il CATALOGO SECURITY TOOLS 6.8 raccoglie i tool disponibili, divisi per
fase del processo SSDLC, che offrono funzionalità applicabili in ambito
secure application development.

Si riporta di seguito la tabella ‘Software Requirements Tools’:

**Prodotto Categoria Fase SSE Tipo Licenza**

::

   Sito Web

**Analyst Pro** Requirements management Requirements
http://www.analysttool.com

**aNimble** Requirements management Requirements Free
http://sourceforge.net/projects/nmble/

**CaseComplete** Requirements management Requirements
http://casecomplete.com

**Code Assure Solo** Requirements management Requirements

**GMARC**

Requirements management Requirements^ **IBM DOORS Next Generation**

Requirements management Requirements^ http://ibm.com\ ^ **IBM Rational
RequisitePro solution**

::

   Requirements
   management
   Requirements http://ibm.com

**IrqA** Requirements management Requirements

**Objectives** Requirements management Requirements Available by
http://www.objectiver.com

::

   Pag. 47 of 121
   Request

**Open Source Requirements Management Tool (OSRMT)**

::

   Requirements
   management Requirements^
   Open
   Source http://sourceforge.net/projects/osrmt/^

**Optimaltrace** Requirements management Requirements
http://www.compuware.com/products/optimaltrace

**Polarion**

::

   Application
   Lifecycle
   Management (ALM)
   Requirements http://www.emerasoft.com/agilelifecycle-management/polarion-alm/-application -

**Reqtify** Requirements management Requirements
http://users.reqtify.tni-software.com/?p=home

**rmtoo** Requirements management requirements Free
http://sourceforge.net/projects/rmtoo/

**RTD** Requirements management Requirements http://www.igatech.com/rdt

**RTM** Requirements management Requirements
http://www.serena.com/Products/rtm/home.asp

**SeaMonster** Requirements management

::

   Requirements https://sourceforge.net/projects/seamonster/

**TcSE (Teamcenter Systems Engineering)**

::

   Requirements
   management Requirements^

**Telelogic DOORS** Requirements Management

::

   Requirements Free http://telelogic-doors.software.informer.com/

**6.2.2.1 Tool per l'analisi del rischio**

**Microsoft Security Assessment Tool (MSAT)**. E ́ uno strumento
Microsoft gratuito progettato per aiutare le organizzazioni a valutare i
rischi di sicurezza, individuare un elenco di problemi in ordine di
priorità e a fornire raccomandazioni specifiche per ridurre al minimo
tali rischi. Lo strumento si basa su un approccio olistico per valutare
le condizioni di sicurezza generali e copre aspetti che riguardano gli
utenti, i processi e la tecnologia.

MSAT risponde ad una gmma di 200 domande che riguardano
l'infrastruttura, le applicazioni, le attività e gli utenti. Le relative
risposte e le raccomandazioni si basano su procedure consigliate e
comunemente accettate da standard quali ISO 17799 e NIST-800.x, oltre
che da raccomandazioni e indicazioni del Microsoft Trustworthy Computing
Group e di altre fonti di protezione esterne.

Lo strumento genera un profilo del rischio aziendale **(BRP, Business
Risk Profile)** , misurando il rischio dell'attività in base al modello
aziendale e di settore, ed un indice delle capacità difensive, dato
dalla sovrapposizione delle diverse misure di protezione, detto **Indice
di Difesa in Profondità (DiDI, Defense-in- Depth Index)**. I valori BRP
e DiDI vengono quindi confrontati per misurare la distribuzione dei
rischi nelle varie aree di analisi: infrastruttura, applicazioni,
attività e utenti.

.. _progettazione:

6.3 PROGETTAZIONE
-----------------

La fase di progettazione identifica i requisiti generali e la struttura
per il software. In questa fase viene definita l'architettura di
sicurezza e le linee guida di progettazione; vengono documentati gli
elementi della superficie d'attacco; vengono modellate le minacce.

.. _secure-design-languages.:

6.3.1 Secure Design Languages…………………………………………………………………………………………………………….
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Molti dei linguaggi per specificare i requisiti di sicurezza sono
utilizzati anche per le specifiche di design. Ciò è dovuto al fatto che
i requisiti di basso livello sono davvero vicini alla progettazione
statica e dinamica.

::

   Pag. 48 of 121

Questi linguaggi (ad esempio, UMLsec, SecureUML, e SecureTropos) sono
già stati discussi nella Sezione precedente. Ci sono due principali
punti che dovrebbero essere considerati nella scelta di un linguaggio di
design sicuro; essi sono:

-  la varietà di schemi disponibili per rappresentare un disegno da vari
   aspetti e livelli di astrazione

-  la disponibilità degli strumenti.

**UMLsec** fornisce una varietà di schemi e ha strumenti disponibili.
**SecureUML** può essere utilizzato anche per la progettazione di
software sicuro; tuttavia, si limita a rappresentare solo nozioni di
controllo degli accessi basati sui ruoli in un diagramma delle classi
UML. **Sicure Tropos** propone di utilizzare gli Agent UML capability
diagrams. Questi schemi sono simili ai diagrammi di attività UML (piano
e capacità) e diagrammi di sequenza (interazione agente).

.. _software-design-tools:

6.3.2 Software Design Tools
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Il CATALOGO SECURITY TOOLS 6.8 raccoglie i tool disponibili, divisi per
fase del processo SSDLC, che offrono funzionalità applicabili in ambito
secure application development.

Si riporta di seguito la tabella ‘Software Design Tools’:

**Prodotto Categoria Fase SSE Tipo Licenza**

::

   Sito Web

Coras

::

   Threat Modeling
   tool/practies
   Design
   Open
   Source
   coras.sourceforge.net

Microsoft Threat Modeling Tool

::

   Threat Modeling tool Design Free https://www.microsoft.com

MyAppSecurity ThreatModeler Threat Modeling tool^ Design^

::

   Available
   by
   Request
   myappsecurity.com

.. _trike:

TRIKE
^^^^^

::

   Threat Modeling
   tool/practies
   Design
   Open
   Source
   http://octotrike.org/tools.shtml

.. _implementazione:

6.4 IMPLEMENTAZIONE
-------------------

Durante questa fase il team di sviluppatori mette in atto le
contromisure secondo le specifiche della fase precedente ed effettua dei
test sul codice sorgente per verificare l'assenza di security flaws.

.. _software-implementation-tools:

6.4.1 Software Implementation Tools
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Il CATALOGO SECURITY TOOLS 6.8 raccoglie i tool disponibili, divisi per
fase del processo SSDLC, che offrono funzionalità applicabili in ambito
secure application development.

Si riporta di seguito la tabella ‘Software Implementation Tools’:

**Prodotto Categoria Fase SSE**

::

   Tipo
   Licenza Sito Web^

**BRAKEMAN** SAST Implementation Open Source

::

   https:// brakemanscanner.org

**Burp Suite by PortSwigger**

.. _sast-dast:

SAST, DAST,
^^^^^^^^^^^

::

   Penetration Testing
   Implementation
   / Verification
   Free Tier https:// portswigger.net

(^) Pag. 49 of 121 **Checkmarx** SAST, DAST, RASP Implementation /
Verification Available by Request https://www. checkmarx.com **Cigital**
SAST, DAST Implementation / Verification N/A https://www.cigital.com
**CodeDx** SAST, DAST Implementation / Verification Available by Request
https://codedx.com **CodeProfiler by Virtual Forge** SAST Implementation
Available by Request https://www.virtualforge.com **Contrast
Enterprise** IAST, RASP Implementation / Verification Available by
Request https://www.contrastsecurity.com **CppCheck** SAST
Implementation Open Source cppcheck.sourceforge.net **Dependency
Checker** Library Inspection Implementation Open Source
https://www.owasp.org **FindBugs** SAST Implementation Open Source
findbugs.sourceforge.net **FxCop** SAST Implementation Open Source
http://www. microsoft.com^ **HP Fortify Static Code Analyzer**

.. _sast-dast-iast:

SAST, DAST, IAST,
^^^^^^^^^^^^^^^^^

.. _rasp:

RASP
^^^^

::

   Implementation
   / Verification
   Available
   by
   Request
   http://www.hp.com

**IBM Security AppScan**

::

   SAST, DAST, IAST Implementation
   / Verification
   Available
   by
   Request
   https://www.ibm.com

**JSHint**

.. _sast:

SAST
^^^^

::

   Implementation
   Open
   Source
   jshint.com

**Gendarme** SAST Implementation

::

   Open
   Source
   http://www.mono-
   project.com/Gendarme

**MetaFlows**

::

   Cloud Security
   Scanning Implementation^
   14 Day
   Free Trial https://www.metaflows.com^

**Metascan by OPSWAT**

::

   SAST Implementation
   Available
   by
   Request
   https://www opswat.com

**Microsoft BinScope**

::

   SAST Implementation Free http://www.microsoft.com

**Microsoft Code Analysis Tool** SAST^ Implementation Free^
http://www.microsoft.com\ ^

**Microsoft FxCop** Library Inspection Implementation Free
http://www.microsoft.com

**Microsoft SDL Regex Fuzzer**

::

   SAST Implementation Free http://www.microsoft.com

**Microsoft SDL MiniFuzz File Fuzzer**

::

   SAST Implementation Free http://www.microsoft.com

**ModSecurity** WAF Implementation / Verification

::

   Open
   Source
   https://www.modsecurity.org
   Pag. 50 of 121

**N-Stalker Cloud Web Scan**

.. _sast-dast-1:

.. _sast-dast-1:

SAST, DAST
^^^^^^^^^^

::

   Implementation
   / Verification
   Free Tier
   Available
   https://www.nstalker.com

**OWASP Dependency Check**

::

   SAST Implementation
   Open
   Source
   http://www.owasp.org

**PMD** SAST Implementation

::

   Open
   Source https://pmd.github.io^

**PYLINT** SAST Implementation

::

   Open
   Source https://www.pylint.org^

**Risk Fabric by Bay Dynamics**

::

   Predictive Security
   Analytics
   Implementation
   / Verification /
   Response
   Available
   by
   Request
   https://baydynamics.com

**RSA ECAT by EMC** DAST

::

   Implementation
   / Verification
   Available
   by
   Request
   https://www.emc.com

**Security AppScan by IBM**

.. _sast-dast-iast-1:

.. _sast-dast-iast-1:

SAST, DAST, IAST
^^^^^^^^^^^^^^^^

::

   Implementation
   / Verification
   Available
   by
   Request
   https://www.ibm.com

**SiteLock TrueCode SAST**

.. _sast-dast-2:

.. _sast-dast-2:

SAST, DAST
^^^^^^^^^^

::

   Implementation
   / Verification
   Available
   by
   Request
   https://www.sitelock.com

**SonarLint** SAST Implementation

::

   Open
   Source https://www.sonarlint.org

**SonarQube** SAST Implementation Open Source

::

   https://www.sonarqube.org

**Symantec Advanced Threat Protection**

.. _iast-rasp:

IAST, RASP
^^^^^^^^^^

::

   Implementation
   / Verification
   60 Day
   Free Trial
   https://www symantec.com

**Tanium Endpoint Platform**

::

   Endpoint Security,
   App Security
   Scanning
   Implementation
   / Verification
   Available
   by
   Request
   https://www tanium.com

**Trend Micro Deep Security Platform**

.. _sast-dast-3:

.. _sast-dast-3:

SAST, DAST
^^^^^^^^^^

::

   Implementation
   / Verification
   N/A https://www.trendmicro.com

**Tripwire Enterprise** IAST, RASP Implementation / Verification

::

   Available
   by
   Request
   https://www.tripwire.com

**Veracode Cloud Platform**

::

   SAST, DAST, Mobile
   AST, Penetration
   Testing
   Implementation
   / Verification
   Available
   by
   Request
   https://www.veracode.com

**WhiteHat Sentinel** SAST, DAST Implementation / Verification

::

   30 Day
   Free Trial
   https://www.whitehatsec.com

.. _verifica:

6.5 VERIFICA
------------

Prima della fase di rilascio definitiva del software i team che lavorano
in sicurezza effettuano un ulteriore verifica del codice elaborato
mediante test di sicurezza. I test di sicurezza mirano a controllare la
vulnerabilità delle superficie di attacco, in modo da agire in via
preventiva alla correzione di eventuali problemi che potrebbero
verificarsi in fase di rilascio.

::

   Pag. 51 of 121

.. _software-verification-tools:

6.5.1 Software Verification Tools
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Il CATALOGO SECURITY TOOLS 6.8 raccoglie i tool disponibili, divisi per
fase del processo SSDLC, che offrono funzionalità applicabili in ambito
secure application development.

Si riporta di seguito la tabella ‘Software Verification Tools’:

**Prodotto Categoria Fase SSE**

::

   Tipo
   Licenza
   Sito Web

Acunetix Web Vulnerability Scanner

::

   DAST, IAST Verification
   14 Day
   Free Trial http://www.acunetix.com^

Adallom Cloud Access Security Broker

::

   Verification Available
   by Request
   adallom.com

AppSpider Pro by Rapid7

::

   DAST Verification
   Available
   by Request
   https://www.rapid7.com

Appthority Mobile AST Verification

::

   Available
   by Request
   https://www.appthority.com

AuditMyApps by Pradeo

::

   Mobile AST Verification
   Available
   by Request
   https://auditmyapps.com

Backtrack-linux

::

   Penetration
   Testing
   Verification
   Open
   Source
   http://www.backtrack-linux.org

BeEF

::

   Penetration
   Testing Verification^
   Open
   Source beefproject.com^

Bit9 + Carbon Black Endpoint Security

::

   Verification /
   Response
   Available
   by Request
   http://www.bit9.com

Black Duck Hub Open Source Scanning

::

   Verification Available
   by Request

https://www.blackducksoftware.co m BrightCloud Threat Intelligence by
Webroot

::

   DAST Verification N/A https://www.brightcloud.com

Checkmarx SAST, DAST, RASP

::

   Implementatio
   n / Verification
   Available
   by Request
   http://www.checkmarx.com

CloudSOC by Elastica

::

   Cloud Security
   Testing/Scannin
   g
   Verification
   Free Risk
   Assessmen
   t
   https://www.elastica.net

CodeDx SAST, DAST

::

   Implementatio
   n / Verification
   Available
   by Request https://codedx.com^

ContextIntelligenc e by Yottaa

::

   CDN, DDoS
   Protection, WAF
   Verification N/A http://www.yottaa.com

Defendpoint by Avecto

::

   Endpoint
   Security
   Verification /
   Response
   Available
   by Request
   https://www.avecto.com

Falcon Host by CrowdStrike

::

   Endpoint
   Security
   Verification /
   Response
   Available
   by Request
   https://www.crowdstrike.com

Hillstone Networks Verification

::

   Available
   by Request
   hillstonenet.com

Kali Linux

::

   Penetration
   Testing
   Verification
   Open
   Source
   kali.org

Security AppScan by IBM SAST, DAST, IAST^

::

   Implementatio
   n / Verification
   Available
   by Request https://www.ibm.com^

(^) Pag. 52 of 121 LogRhythm Security Intelligence Platform Predictive
Security Analytics Verification / Response Available by Request
http://www.logrhythm.com Malwarebytes Endpoint Security Endpoint
Security Verification^ N/A^ http://www.malwarebytes.org\ ^ Metasploit by
Rapid7 Penetration Testing Verification^ Open Source
http://www.metasploit.com\ ^ Microsoft Application Verifier DAST^
Verification^ Free^ http://www.microsoft.com\ ^ Microsoft Attack Surface
Analyzer Intrusion Prevention Verification Free http://www.microsoft.com
NetScaler AppFirewall by Citrix WAF Verification N/A citrix.com Nevis
Security and Compliance Suite by

.. _waf:

WAF,
^^^^

::

   Authentication,
   Identity mngt
   Verification
   Available
   by Request
   http://www.adnovum.ch

AdNovum Management Verification

Nikto2 Web Server Scanner

::

   Verification Open
   Source
   cirt.net

Nmap

::

   Penetration
   Testing and
   Network
   Mapping
   Verification /
   Response
   Open
   Source http://www.nmap.org

NSFOCUS Web Application Firewall

::

   DAST, WAF Verification N/A http://www.nsfocus.com

OWASP Zed Attack Proxy (ZAP)

.. _sast-dast-4:

.. _sast-dast-4:

SAST, DAST/
^^^^^^^^^^^

::

   Penetration
   Testing
   Verification /
   Response
   Open
   Source
   http://www.owasp.org

PA-7000 Series Firewall by Palo Alto

::

   WAF Verification N/A https://www.paloaltonetworks.com

Networks Verification

Peach Fuzzer

::

   Penetration
   Testing
   Verification /
   Response
   Available
   by Request
   http://www.peachfuzzer.com

Prevoty RASP

::

   Verification /
   Response
   Available
   by Request
   http://www.prevoty.com

ProtectWise Cloud Network DVR

::

   CDN, App
   Security
   Scanning
   Verification
   Available
   by Request http://www.protectwise.com^

Qualys Security & Compliance Suite

.. _dast-waf:

DAST, WAF
^^^^^^^^^

::

   Verification /
   Response
   Available
   by Request
   https://www.qualys.com

Samurai Web Testing Framework

.. _dast:

DAST,
^^^^^

::

   Penetration
   testing
   Verification
   Open
   Source https://www.samurai-wtf.org^

SRX Series Firewall by Juniper

::

   WAF Verification N/A http://www.juniper.net
   Pag. 53 of 121

Networks

Sucuri WAF Verification N/A http://www.sucuri.net

Thunder TPS by A10 Networks

::

   DDoS Protection
   Verification /
   Response
   N/A https://www.at10networks.com

Trustwave Secure Web Gateway

::

   CDN, DAST Verification N/A http://www.trustwave.com

Trustwave Web Application Firewall

.. _waf-1:

.. _waf-1:

WAF,
^^^^

::

   Penetration
   Testing
   Verification N/A http://www.trustwave.com

Veracode DAST Verification

::

   Available
   by Request
   http://www.veracode.com

vSentry by Bromium

::

   Endpoint
   Security
   Verification /
   Response
   Available
   by Request
   http://www.bromium.com

vThreat Platform

::

   Penetration
   Testing, App
   Security
   Scanning
   Verification Available
   by Request
   http://www.vthreat.com

Wireshark

::

   Penetration
   Testing and
   Packet-level
   Monitoring
   Verification
   Open
   Source
   http://www.wireshark.org

.. _validazione:

6.6 VALIDAZIONE
---------------

Durante questa fase il software è oggetto di una Final Security Review
finalizzato a stabilire se il software soddisfa tutti i requisiti di
sicurezza individuati nella fase iniziale del progetto.

In questa fase si verifica, inoltre, che i bug di sicurezza
precedentemente identificati siano stati risolti e che il SW sia
sufficientemente robusto di fronte a nuove vulnerabilità.

Le azioni di sicurezza di questa fase possono essere così sintetizzate:

-  **Software Remediation dopo un'analisi statica (SAST)**

::

   o Analisi della reportistica e classificazione degli errori, rilevati nella fase di analisi statica del
   codice;
   o Rimozione degli errori di sicurezza legati all’uso di librerie esterne a rischio di vulnerabilità,
   sostituendole con le versioni sanate;
   o Ristrutturazione delle classi e funzioni identificate come vulnerabili alle varie injection, al cross
   site scripting, etc.
   o Applicazione delle modifiche nei costrutti sintattici che rendono il software vulnerabile;
   o Considerare i «warning» sulla qualità del codice e procedere con le modifiche;

-  **Software Remediation dopo un'analisi dinamica (DAST)**

::

   o Analisi della reportistica e classificazione degli errori, rilevati nella fase di analisi dinamica del
   codice.
   o Rimozione degli errori messi in evidenza dal fuzzy testing, ad esempio aumentando i controlli
   applicativi.
   Pag. 54 of 121
   o Correzioni degli errori, eventualmente tramite implementazione di nuove funzioni, per
   esempio aggiungendo meccanismi di autenticazione o rivedendo la struttura delle classi e
   funzioni.

-  Definizione di un **Incident Responce Plan** cioè produrre la
   documentazione contenente le istruzioni per rispondere e limitare gli
   effetti di un incidente di sicurezza.

-  Security Review: configurazione finale, aggiornamento delle procedure
   di sicurezza, certificazione del rilascio software, testing e
   archiviazione.
