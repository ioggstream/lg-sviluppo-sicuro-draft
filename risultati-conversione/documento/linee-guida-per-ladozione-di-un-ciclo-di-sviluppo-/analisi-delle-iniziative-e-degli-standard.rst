.. _analisi-delle-iniziative-e-degli-standard:

5 ANALISI DELLE INIZIATIVE E DEGLI STANDARD……………………………………………………………………………………
===========================================================================

.. _iniziative-internazionali:

5.1 INIZIATIVE INTERNAZIONALI
-----------------------------

.. _open-web-application-security-project-owasp:

5.1.1 Open Web Application Security Project (OWASP)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

L'Open Web Application Security Project (chiamato semplicemente OWASP) è
un progetto open-source per la sicurezza delle applicazioni Web. L'OWASP
offre anche guide con consigli sulla creazione di applicazioni Internet
sicure, e indicazioni per i test a cui andrebbero sottoposte. È stato
anche pubblicato un WebGoat, un progetto che insegna la sicurezza sulle
applicazioni web. Nel 2004 fu istituita una fondazione no-profit che
supporta l'OWASP, che persegue l'obiettivo di aumentare la sicurezza
delle applicazioni consentendo di prendere le decisioni in base ai
rischi. In Europa è un'organizzazione no-profit registrata a partire da
giugno 2011 ed è presente anche in Italia.

::

   URL http://www.owasp.org
   Country of HQ location
   Geographic Scope

.. _us:

US
^^

::

   International
   Type Various Industry (not for profit)

L'iniziativa è organizzata come una comunità collaborativa che produce
tools e documenti in tre aree principali:

-  Protection,

-  Detection,

-  Life-cycle security.

Relativamente a queste 3 aree, OWASP ha prodotto un insieme di guide
sulle buone pratiche quali: OWASP Testing Guide, OWASP Code Review,
Software Assurance Maturity Model.

Tra le uscite anche il Report ‘ OWASP Top 10' sui rischi per le
applicazioni web. Le altre attività OWASP.

Risultati più rilevanti:

::

   Good Practice [Protection Area] OWASP Secure Coding Practices Quick Reference Guide v2.0 - A
   technology-agnostic set of general software security coding practices, in a
   comprehensive checklist format, that can be integrated into the development life
   cycle.
   [Protection Area] OWASP Developers Guide v2.0 (2005) - An extensive document
   covering all aspects of web application and web service security.
   [Detection Area] OWASP Code Review Guide v1.1 A guide that captures best practice
   for reviewing code.
   [Detection Area] OWASP Testing Guide v3.0 - A guide on application security testing
   procedures and checklists.
   Standards [Detection Area] Application Security Verification Standard (ASVS) The ASVS defines
   an international standard for conducting application security assessments. It covers
   both automated and manual approaches for assessing (verifying) applications, using
   both security testing and code review techniques.
   Tools [Protection Area] AntiSamy - Java and .NET APIs validating rich HTML/CSS input from
   users to prevent cross-site scripting and phishing attacks.
   Enterprise Security API (ESAPI) Project - A collection of free and open source security
   libraries that can be used by developers to build secure web applications.
   [Detection Area] JBroFuzz Project - A web application fuzzer for performing testing
   Pag. 16 of 121
   over HTTP and/or HTTPS. Its purpose is to provide a single, portable application that
   offers stable web protocol fuzzing capabilities.
   [Detection Area] Live CD Project This CD collects some open source security projects
   in a single environment. Web developers, testers and security professionals can boot
   from this Live CD and have access to a full security testing suite.
   [Detection Area] WebScarab Project.An intercepting proxy tool for performing all
   types of security testing on web applications and web services.
   [Detection Area] Zed Attack Proxy Project - Another intercepting proxy tool for
   finding vulnerabilities in web applications. It is designed to be used by people with a
   wide range of security experience and, as such, is ideal for developers and functional
   testers who are new to penetration testing.
   [Detection Area] DirBuster Project.An application designed to apply brute force to
   directories and file names on web/application servers.
   [Detection Area] SWF Intruder Project.Is a tool for analysing and testing security of
   flash applications at run time.
   [Life cycle security Area] WebGoat Project - An insecure web application for teaching
   web application security through interactive practical lessons.In the future, it is
   expected to become a security benchmarking platform.
   [Protection Area] OWASP Back-End Security Project.This project aims to create a new
   guide that could allow developers, administrators and testers to understand any part
   of the security process of back-end components that communicate directly with web
   applications, databases, ldaps, payment gateways and much more. The project
   comprises three sections: security development, security hardening and security
   testing. Currently the document is not in guide format.
   OWASP Backend Security OWASP O2 PlatformA highly-customisable platform for
   linking, managing and consuming IT security data, tools and applications.
   ProjectInventory 2017:Tools [Health Check January 2017];OWASP Zed Attack
   Proxy;OWASP Web Testing Environment Project;OWASP OWTF;OWASP Dependency
   CheckOWASP Security Schepherd
   Code [Health Check January 2017]:OWASP ModSecurity Core Rule Set
   Project;OWASP CSRFGuard Project;OWASP AppSensor
   ProjectDocumentation[Health Check January 2017];OWASP Application Security
   Verification Standard Project;OWASP Software Assurance Maturity Model
   (SAMM);OWASP AppSensor Project;OWASP Top Ten Project;OWASP Testing Project

.. _common-criteria-cc:

5.1.2 Common Criteria (CC)
~~~~~~~~~~~~~~~~~~~~~~~~~~

I Common Criteria sono uno standard pubblicato dall'ISO (ISO/IEC
15408:2005) e sono costituiti da tre parti:

-  Introduzione e modello generale.

-  Requisiti di sicurezza funzionali.

-  Requisiti di sicurezza di assurance.

Con i CC viene fornita anche una metodologia per la valutazione, la
Common Criteria Evaluation Methodology (CEM), anch'essa standardizzata
dall'ISO (ISO/IEC 18405:2005). Il processo di valutazione CC di un
prodotto (software o hardware) riguarda diverse fasi SDLC:

-  Requisiti (Protection Profile document - PP),

-  Implementazione (Security Target document – ST),

-  Test.

::

   Pag. 17 of 121

Le verifiche previste durante il processo di valutazione mirano ad
accertare che siano stati soddisfatti, da parte del sistema/prodotto,
del suo sviluppatore e del valutatore, opportuni requisiti di assurance
che diventano sempre più severi al crescere del livello di valutazione.
I CC definiscono una scala di 7 livelli di valutazione:

-  EAL1. Functionally tested

-  EAL2. Structurally tested

-  EAL3. Methodically tested and checked

-  EAL4. Methodically designed, tested and reviewed

-  EAL5. Semi-formally designed and tested

-  EAL6. Semi-formally verified design and tested

-  EAL7. Formally verified design and tested.

I seguenti paesi hanno firmato l'accordo Common Criteria Recognition
Agreement (CCRA) che si applica da EAL1 to EAL4:

-  Paesi EU/EFTA: Austria, Repubblica Ceca, Danimarca, Finlandia,
   Francia, Germania, Grecia, Ungaria, Italia, Paesi Bassi, Norvegia,
   Spagna, Svezia e Regno Unito;

-  Paesi Non-EU/EFTA: Australia, Canada, India, Israele, Giappone,
   Corea, Malesia, Nuova Zelanda, Pakistan, Singapore, Turchia e Stati
   Uniti.

L'European Mutual Recognition Agreement of IT Security Evaluation
Certificates o ‘SOGIS-agreement’ è un accordo tra alcune nazioni europee
con l'adesione dell'UE o dell'EFTA relativo al mutuo riconoscimento dei
certificati di valutazione secondo gli standard CC per tutti i livelli
di valutazione (EAL1 EAL7).

::

   URL http://www.commoncriteriaportal.org/
   Country of HQ location
   Geographic Scope
   International
   Type Government

I criteri comuni per la valutazione della sicurezza informatica e la
metodologia comune per la sicurezza delle tecnologie di valutazione sono
stati pubblicati come standard ISO.

Risultati più rilevanti:

::

   Standard Common Methodology for Information Technology Security Evaluation and Common
   Criteria for Information Technology Security Evaluation
   These form the technical basis for an international agreement (the CCRA). Version 2.
   has also been published as ISO/IEC 15408:2005 and ISO/IEC 18045:
   Future
   Related Standard

.. _jtc-1sc-27:

JTC 1/SC 27
^^^^^^^^^^^

.. _isoiec-np-20004:

ISO/IEC NP 20004
^^^^^^^^^^^^^^^^

::

   Information technology, Security techniques, Secure software development and
   evaluation under ISO/IEC 15408 and ISO/IEC 18405.

.. _ieee-computer-society-cs:

5.1.3 IEEE Computer Society (CS)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

L'Iniziativa IEEE Computer Society è un'organizzazione senza fini di
lucro ed i suoi principali progetti sono finalizzati alla pubblicazione
di standard su tecnologie IT.

::

   Pag. 18 of 121
   URL http://www.computer.org /
   Country of HQ location
   Geographic Scope

.. _us-1:

.. _us-1:

US
^^

::

   International
   Type Academic (not for profit)

I principali risultati di questa iniziativa sono libri, conferenze,
pubblicazioni su conferenze, riviste, corsi on- line, certificazioni di
sviluppo software, standard e riviste tecniche.

Risultati più rilevanti:

::

   Good Practice Guide to the Software Engineering Body of Knowledge (SWEBOK)
   The SWEBOK Version 3, alpha version, will include Security as one of the proposed
   Supplemental Knowledge Areas.
   Standard Software & Systems Engineering Standards Committee (S2ESC)
   Formal Liaisons with ISO/IEC JTC1/SC7.

.. _international-organisation-for-standarditation-iso:

5.1.4 International Organisation for Standarditation (ISO)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

ISO è il più grande sviluppatore ed editore al mondo di standard
internazionali. Industrie ed esperti del settore generalmente
contribuiscono come membri dei comitati tecnici ISO proponendo nuove
normative che devono essere approvate almeno dal 70% dei membri ISO.

Il comitato tecnico che opera nell'ambito degli standard IT è il JTC 1.
Questo comitato è a sua volta organizzato nei seguenti 3 sotto-comitati:

-  JTC 1 / SC 7: software e ingegneria dei sistemi,

-  JTC 1 / SC 22: linguaggi di programmazione, compresi ambienti e
   interfacce software di sistema

-  JTC 1 / SC 27: tecniche di sicurezza IT.

Relativamente agli ambiti SSE le uscite principali ISO riguardano:

-  pubblicazione di rapporti tecnici e standard -ISO / IEC TR 15026-1:
   2010, ISO / IEC TR 24731-1: 2007, ISO / IEC TR 24772: 2010, ISO / IEC
   15408 e ISO / IEC 18405

-  2 progetti in corso.

::

   URL http://www.iso.org
   Geographic Scope International
   Type Network of national standards institutes

(^) Pag. 19 of 121 Risultati più rilevanti: **JTC 1/SC 7** ISO/IEC
15026-1:2013 Systems and software engineering – Systems and software
assurance – Part 1: Concepts and vocabulary ISO/IEC TR 15026-1:2010
Systems and software engineering - Systems and software assurance Part
1: Concepts and vocabulary. **JTC 1/SC 22** ISO/IEC TR 24731-1:2007
Information technology Programming languages, their environments and
system software interfaces -Extensions to the C library

-  Part 1: Bounds-checking interfaces. Specifica una serie di estensioni
   del linguaggio di programmazione C, specificato dalla norma
   internazionale ISO/IEC 9899: 1999. Queste estensioni possono essere
   utili nella mitigazione delle vulnerabilità di sicurezza nei
   programmi. ISO/IEC TR 24772:2010 Information technology - Programming
   languages - Guidance on avoiding vulnerabilities in programming
   languages through language selection and use. Specifica le
   vulnerabilità del linguaggio di programmazione software da evitare
   nello sviluppo di sistemi in cui è richiesto un comportamento sicuro
   ai fini security/safety, mission critical e software
   business-critical. In generale, questa guida è applicabile al
   software sviluppato, rivisto, o mantenuto per qualsiasi applicazione.
   Le vulnerabilità sono descritte in modo generico, applicabili ad una
   vasta gamma di linguaggi di programmazione. Questa guida può essere
   anche utilizzata dagli sviluppatori per produrre o selezionare gli
   strumenti di valutazione del codice sorgente capaci di scoprire ed
   eliminare alcuni costrutti che potrebbero portare alla vulnerabilità
   del software o per selezionare un linguaggio di programmazione che
   consente di evitare i problemi attesi.

::

   Pag. 20 of 121

Progetti in corso:

::

   JTC 1/SC 7
   ISO/IEC FCD 15026- 2 - Systems and software engineering - Systems and
   software assurance -- Part 2: Assurance case.
   Specifica i requisiti minimi per la struttura e il contenuto di un Assurance Case
   per migliorare la coerenza e la comparabilità degli Assurance Case e per
   facilitare le comunicazioni delle parti interessate, le decisioni di ingegneria e
   altri Assurance Case.
   Secondo questo documento ISO “ An assurance case includes a top-level claim
   for a property of a system or product (or set of claims), systematic
   argumentation regarding this claim, and the evidence and explicit assumptions
   that underly this argumentation. Arguing through multiple levels of
   subordinate claims, this structured argumentation connects the top-level claim
   to the evidence and assumptions ”.
   ISO/IEC CD 15026-3 Systems and software engineering -- Systems and software
   assurance -- Part 3: Integrity levels.
   Si riferisce ai livelli di integrità dell’Assurance Case ed include i requisiti relativi
   al loro utilizzo con e senza un Assurance Case.
   Secondo questo documento ISO “ A software integrity level denotes a range of
   values of a software property necessary to maintain system risks within
   tolerable limits ”.
   JTC 1/SC 27
   ISO/IEC 27021:2017 Preview
   Information technology -- Security techniques -- Competence requirements for
   information security management systems professionals
   ISO/IEC 15026-1:2013:Systems and software engineering -- Systems and
   software assurance -- Part 1: Concepts and vocabulary
   ISO/IEC NP 20004: Information technology - Security techniques - Secure
   software development and evaluation under ISO/IEC 15408 and ISO/IEC 18405.
   Si riferisce ad un problema differente e più urgente associato all’uso pratico
   dei Common Criteria, ossia la relazione tra i processi di sviluppo e di
   valutazione con l’analisi dei potenziali attacchi. E’ legato all’iniziativa CAPEC.

.. _international-society-of-automation-isa:

5.1.5 International Society of Automation (ISA)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

L'ISA è un'organizzazione globale no-profit che sviluppa standard per
l'industria, certifica i professionisti di settore, offre istruzione e
formazione, pubblica libri e articoli tecnici, e ospita convegni e fiere
per i professionisti dell'automazione.

::

   URL http://www.isa.org /
   Country of HQ location
   Geographic Scope

.. _us-2:

.. _us-2:

US
^^

::

   International
   Type Industry (not for profit)

ISA99 standard “Manufacturing and Control Systems Security” ha alcune
parti relative a SSE. Attualmente sono pubblicate solo le parti
“99.01.01 Terminology, Concepts, and Models”, “99.02.01 - Establishing
an Industrial Automation and Control Systems Security Program” e
“99.03.01 Security technologies for Industrial Automation and Control
Systems”. ISA e la Commissione Elettrotecnica Internazionale (IEC) hanno
negoziato l'adozione degli standard ISA 99 e IEC 62443. I membri ISA
pagano una tassa regolare (annuale o biennale), in base al loro tipo di
appartenenza, al fine di ottenere i benefici ISA come l'accesso alle
informazioni tecniche e alle risorse per lo sviluppo professionale.

::

   Pag. 21 of 121

Risultati più rilevanti:

::

   Proposed Standards ISA TR99.02.03 Patch Management in the IACS Environment. This technical
   report addresses the topic of patch management in an Industrial Automation
   and Control Systems (IACS) environment for asset owner and vendor
   communities. It is aimed at providing guidance in patch-testing and patch-
   management according to an acceptable level of risk.
   ISA 99.03.04 Product Development Requirements. This standard will address
   the security requirements for product development
   Draft Standards ISA 99.03.03 System Security Requirements and Security Assurance Levels
   This standard defines security requirements that are grouped into seven
   categories:
   1) Access control, 2) Use control, 3) Data integrity, 4) Data confidentiality, 5)
   Restrict data flows, 6) Timely response to an event and 7) Network resource
   availability. Each category includes a mapping of security requirements to
   security assurance levels.

.. _software-assurance-forum-for-excellence-in-code-safecode:

5.1.6 Software Assurance Forum for Excellence in Code (SAFECODE)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

SAFECode è un'iniziativa privata creata da sviluppatori software e
fornitori. Individuando e promuovendo le migliori pratiche in SSE,
questa iniziativa sostiene che l'industria del software potrebbe
rilasciare software, hardware e servizi più sicuri e affidabili. Tra le
sue uscite principali, ci sono i documenti che raccolgono le migliori
pratiche, tenendo conto del ciclo di vita di sviluppo del software.

::

   URL http://www.safecode.org
   Country of HQ location
   Geographic Scope

.. _us-3:

.. _us-3:

US
^^

::

   International
   Type Industry (not for profit)

SAFECode afferma che i suoi obiettivi futuri sono:

1. Identificare e condividere collaudate pratiche di garanzia del
   software

2. Promuovere una più ampia adozione di tali pratiche nell'ecosistema
   informatico,

3. Lavorare con istituzioni e fornitori di infrastrutture critiche per
   sfruttare le pratiche nella gestione dei rischi aziendali.

::

   Pag. 22 of 121

Risultati più rilevanti:

::

   Training Security Engineering Training
   A framework for corporate training programs on the principles of secure
   software development.
   Good Practice Software Integrity Controls
   An assurance-based approach to minimizing risks in the software supply chain.
   Based on the practices of SAFECode members, the report provides software
   integrity controls for software sourcing, software development, software
   testing, software delivery and software resilience.
   The Software Supply Chain Integrity Framework
   This defines risks and responsibilities for making software secure in the global
   supply chain. Based on the experience of SAFECode members, it describes the
   software supply chain (staircase model of software suppliers) and the
   principles for designing software integrity controls.
   Fundamental Practices for Secure Software Development
   Based on the practices of SAFECode members, this outlines a set of practices
   for secure software development that can be applied in the different phases of
   the software development life cycle.
   Software Assurance: An Overview of Current Industry Best Practices
   This outlines the development methods and integrity controls used by
   SAFECode members to improve software assurance and security in the
   delivery.

.. _sans-software-security-institute-san-ssi:

5.1.7 SANS Software Security Institute (SAN SSI)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

SANS SSI offre una libreria di iniziative di ricerca e di community per
aiutare sviluppatori, architetti, programmatori e responsabili della
sicurezza delle applicazioni a proteggere le loro applicazioni
software/web. Questa iniziativa raccoglie e fornisce informazioni
tecniche aggiornate, come l'accesso gratuito alle risorse sui più
recenti sui vettori di attacco e sulle vulnerabilità di sicurezza delle
applicazioni, tra cui un blog aggiornato, news-letters settimanali,
Webcast, articoli e documenti in materia di sicurezza del software.

::

   URL http://www.sans.org
   Country of HQ location
   Geographic Scope

.. _us-4:

.. _us-4:

US
^^

::

   International
   Type Academic

SANS pubblica relazioni annuali (Top 25 Software Errors) con l'analisi
sugli errori di programmazione più pericolosi (vedi ad esempio
`http://www.sans.org/top25-software-errors/). <http://www.sans.org/top25-software-errors/>`__.)

Risultati più rilevanti:

::

   Resources Application Security Resources: Application security whitepapers and
   application security webcasts
   Security Laboratory: The "Security Laboratory" is an informal set of articles
   and whitepapers about security, IT and the computer security industry.
   Fundamental Practices for Secure Software Internet Storm Center (ISC)
   The ISC provides a free analysis and warning service to Internet users and
   Pag. 23 of 121
   organisations. Volunteers donate their time to analyse defects and anomalies,
   and post a daily diary of their analysis and thoughts on the Storm Center
   website.
   Application Security Procurement Language: This is a draft software contract
   for buyers of custom software. Its objective is to make code developers
   responsible for checking the code and fixing security flaws before delivery of
   the software.
   Top 25 Software Errors
   These are listed in three categories:

-  Insecure Interaction Between Components

-  Risky Resource Management

-  Porous Defences.

::

   Each error includes:

-  The ranking of each Top 25 entry

-  Links to full Common Weakness Enumeration (CWE, see section 3.4)
   entry data

-  Data fields for weakness prevalence and consequences

-  Remediation cost

-  Ease of detection

-  Code examples

-  Detection Methods

-  Attack frequency and attacker awareness

-  Related CWE entries and related patterns of attack for this weakness.
   It also includes fairly extensive prevention and remediation steps
   that developers can take to mitigate or eliminate the weakness

.. _web-application-security-consortium-wasc:

5.1.8 Web Application Security Consortium (WASC)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

WASC produce best practice per le applicazioni web. WASC riassume la sua
missione così " *to develop, adopt, and advocate standards for web
application security* ".

::

   URL http://www.webappsec.org/^
   Country of HQ location
   Geographic Scope

.. _us-5:

.. _us-5:

US
^^

::

   International
   Type Industry (not for profit)

Risultati più rilevanti:

::

   Resources Web Application Security Scanner Evaluation Criteria
   A set of criteria for evaluating web application security.
   The Web Hacking Incidents Database
   Database of web applications and related security incidents.
   The Script Mapping Project
   List of ways of executing script within a web page without using <script> tags.
   Distributed Open Proxy Honeypots
   Analysis of HTTP traffic through specially configured open proxies to categorise
   the requests into threat classifications.
   Pag. 24 of 121
   Web Security Glossary
   Index of terms and terminology relating to web applications security
   Web Security Threat Classification
   An attempt to develop and promote industry-standard terminology for
   describing threats to the security of a website.
   Web Application Firewall Evaluation Criteria
   Development of detailed criteria for evaluating a web application firewall
   (WAF).
   Web Application Security Statistics
   Collection of application vulnerability statistics for identifying and mapping
   application security issues on enterprise websites.

.. _institute-for-software-quality-ifsq:

5.1.9 Institute for Software Quality (IFSQ)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

L'Istituto per la Qualità del Software, con sede nei Paesi Bassi, è un
gruppo di professionisti coinvolti nello sviluppo e nella distribuzione
di software. IfSQ persegue un obiettivo comune: aumentare gli standard
software (e dello sviluppo software) in tutto il mondo attraverso la
promozione del Code Inspection, come prerequisito del Software Testing
nel ciclo di produzione e rilascio del software.

::

   URL http://ifsq.nl/
   Country of HQ location
   Geographic Scope
   The Netherlands
   International
   Type Industry (non profit)

IfSQ ha analizzato, quantificato e migliorato lo stato dell'arte
scientifico sulla qualità del software, e ha prodotto un insieme di
indicatori (Defect Indicators) che sono stati raccolti in un insieme
coordinato di tre standard, che sono pubblicati sul sito, in forma di
opuscolo e sotto forma di corsi e workshop. La maggior parte dei criteri
di valutazione, in particolare “major string”, “parametri non
controllati” e " unexpected state not trapped", sono rilevanti per
migliorare la sicurezza del software.

Risultati più rilevanti:

::

   Resources Software Quality Standards - Levels 1, 2 and 3 are available.

.. _iniziative-europee:

5.2 INIZIATIVE EUROPEE
----------------------

Questa sezione ha l'obiettivo di fornire una vista delle iniziative in
ambito Europeo. Le iniziative di seguito presentate sono state
classificate sulla base dell'ambito geografico e della tipologia di
appartenenza (accademiche, governative, industria).

Analizzando ambiti, obiettivi e risultati di ognuna, emerge che:

-  un insieme di iniziative rappresentano per obiettivi e risultati una
   categoria isolata. Tra queste iniziative diciamo ‘non raggruppabili’
   ci sono: NESSI, OWASP Local Chapters, MISRA e Serenity Forum.

-  altre iniziative posso essere ‘raggruppate’ sulla base di alcuni
   elementi che li caratterizzano e li accomunano: Events and
   Periodicals, Certifications, Academic Education. Queste iniziative
   potrebbero essere classificate con più tag sulla base dei loro
   risultati rilevanti o attesi in SSE: standardisation, industry
   platform, vulnerability detection, vulnerability protection,
   information sharing, specialised workshop, certification and
   training.

::

   Pag. 25 of 121

.. _networked-european-software-and-services-initiative-nessi:

5.2.1 Networked European Software and Services Initiative (NESSI)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

NESSI è la piattaforma tecnologica europea dedicata al Software e ai
Servizi. L'obiettivo principale di NESSI si indirizza sul potenziamento
dei servizi Internet attraverso attività di ricerca, standard e policy,
e contributi costruiti attraverso una community industria/università.

I partecipanti NESSI sono divisi in tre gruppi:

-  partner NESSI: prevalentemente industriale, ma ci sono anche alcuni
   profili accademici - coordinano la piattaforma e forniscono il
   sostegno finanziario per le attività NESSI;

-  I membri NESSI: industria, mondo accademico e gli utenti -
   rappresentano i principali stakeholders del dominio della fornitura
   di servizi ICT. Non è obbligatorio un contributo finanziario

-  abbonati NESSI: usano diversi canali di informazione per tenersi
   aggiornati sulle attività di NESSI.

::

   URL http://www.nessi-europe.com
   Country of HQ location
   Geographic Scope
   Belgium
   Europe
   Type Industry

Piattaforme tecnologiche nazionali e regionali sono parte della rete
NESSI: gestiscono obiettivi NESSI da un punto di vista locale.

I focus NESSI hanno alcune correlazioni SSE:

-  Identificare le direzioni della ricerca futura sui servizi

-  costruire contributi formali sui settori chiave

-  investire sulla rete NESSI per migliorare il coordinamento tra i
   programmi di ricerca europei, nazionali e regionali.

Risultati più rilevanti:

::

   Research Agenda NESSI strategic research agenda (Lastest version)
   One of the Research Priorities for 2009-2010 (Volume 3.2 - Revision 2 - May
   2009) is “End-to-end Trust, Security, Privacy and Resilience”.
   Working Group related
   to SSE
   Trust, Security and Dependability NWG
   This NWG reports on the state of play regarding web services trust, security
   and dependability (reliability), as well as giving recommendations on future
   priorities, producing guidelines and identifying best practice. Task forces in
   security areas are expected to replace this NWG.

.. _piattaforme-nazionali-nessi:

5.2.2 Piattaforme Nazionali NESSI
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

L'obiettivo generale delle Piattaforme NESSI è quello di promuovere lo
sviluppo e l'applicazione di tecnologie e servizi ICT per affrontare le
sfide future all'interno dell'industria europea e del governo.

Nella tabella che segue vengono sintetizzate le attività per ogni
piattaforma nazionale che gestisce gli obiettivi NESSI da un punto di
vista locale e pubblica la sua SRA nazionale.

::

   URL http://www.nessi-europe.com
   NESSI - Norway E’ la filiale norvegese del NESSI. Il suo obiettivo principale è quello di creare
   un'arena norvegese per gli stakeholders del settore industria, ricerca/mondo
   accademico e pubblico e di influenzare la strategia di ricerca ICT del governo

(^) Pag. 26 of 121 norvegese. **URL** http://www.nessi-europe.com
**NESSI - Slovenia** Alla base di queste attività è che NESSI assumerà
la responsabilità del contenuto e dell'attuazione del 7° programma
quadro dell'UE per R&D. Essi invitano chiunque sia coinvolto in attività
di R&D a partecipare a questo lavoro. **URL** http://www.iipsaas.nl
**IIP SaaS-Netherlands** E' la piattaforma olandese di NESSI per il
Software as a Service (SaaS). IIP SaaS lavora a stretto contatto con il
programma di ricerca Jacquard [www.jacquard.nl/]. **URL**
http://www-it.fmi.uni-sofia.bg/nessibg **NESSI-Bulgaria** NESSI-Bulgaria
è stata fondata nel 2005. Si tratta di un forum per lo scambio di
conoscenze, lo sviluppo di strategie e la ricerca di nuove potenzialità
a livello internazionale IT e servizi industriali. La visione centrale
della piattaforma è di consentire nuovi modelli di business orientate ai
servizi. I loro obiettivi sono:

-  Definire una Roadmap bulgara e l'SRA per l'evoluzione del programma
   di innovazione R&D bulgaro.

-  Supporto alle attività R&D nei settori del software e dei servizi.

-  Fornire formazione: nuovi corsi, programmi MSc, programmi PhD e
   formazione

**URL** http://www.nessi-hungary.com http://www.nessi.hu/

**NESSI- Hungary** NESSI-Ungheria è stata fondata nel 2007 con lo scopo
di evolvere la direzione della ricerca e dello sviluppo strategico nel
settore del software e dei servizi, sulla base di un approccio
unificato. Gruppi di lavoro di questa piattaforma sono divisi in due
sottogruppi: domain- oriented e technological-oriented. La piattaforma è
aperta a qualsiasi altra organizzazione ungherese.

**URL** http://www.bicc-net.de/

**Germany Bicc-Net** BICC-NET, Piattaforma di NESSI tedesca, è il Polo
ICT bavarese della Germania. Fondata nel 2007, intende stimolare
selettivamente l'innovazione. BICC-NET comprende quanto segue:

-  sviluppo e distribuzione del software

-  lo sviluppo e la distribuzione di hardware

-  Telecomunicazioni

-  sistemi software e hardware embedded nei prodotti

-  Processi basati su software in fase di sviluppo, la produzione, i
   servizi e della pubblica amministrazione

-  Servizi nelle aree di cui sopra

::

   Pag. 27 of 121
   BICC-NET viene utilizzato per garantire la crescita ICT in Baviera. Essa è guidata
   dalla BICC sede ufficiale "cluster", che è stato direttamente commissionato dal
   Ministero bavarese per gli Affari economici, infrastrutture, trasporti e
   tecnologia.
   BICC-NET supporterà i profili di innovazione delle aziende ICT bavaresi e gli
   sviluppi in corso.
   URL http://www.fi-stockholm.eu/
   NESSI- Sweden NESSI svedese è stata fondata nel 2010. L'obiettivo generale di NESSI Svezia è
   quello di promuovere lo sviluppo e l'applicazione di tecnologie e servizi ICT per
   affrontare le sfide future all'interno dell'industria svedese e del governo

**URL** (^) http://www.nessi-europe.com/ **NESSI- Romania** NESSI
Romania è stata fondata nel 2010. Gli obiettivi a breve termine di
NESSI- Romania sono:

-  istituire gruppi di lavoro nazionali su diversi argomenti definiti in
   NESSI SRA

-  Definire un SRA nazionale per l'evoluzione futura del programma
   nazionale R&D e innovazione relativamente a software e servizi

-  Diffondere i risultati NESSI dei progetti strategici e compatibili

.. _owasp-local-chapters:

5.2.3 OWASP Local Chapters
~~~~~~~~~~~~~~~~~~~~~~~~~~

Questa sezione fornisce una vista dei gruppi di lavoro OWASP distribuiti
sul territorio Europeo.

::

   URL http:// http://www.owasp.org/index.php/Belgium
   OWASP Belgium Local
   Chapter
   Le principali attività svolte riguardano l'organizzazione di incontri su come
   difendere le applicazioni web da attacchi.
   URL http://www.owasp.org/index.php/Denmark
   OWASP Denmark Local
   Chapter
   Le principali attività svolte riguardano l'organizzazione di incontri su diversi
   argomenti di sicurezza delle informazioni legate alle applicazioni web. Le
   presentazioni sono disponibili sul sito web
   URL http://www.owasp.org/index.php/France
   OWASP France Local
   Chapter
   Le principali attività svolte riguardano l'organizzazione di incontri e la
   traduzione della documentazione OWASP in francese. Questo Chapter fornisce
   anche la formazione su progetti e risorse OWASP attraverso il programma
   "OWASP projects and resources you can use today", che ha lo scopo di
   promuovere progetti OWASP, fornendo una selezione di progetti maturi ed
   enterprise-ready, insieme con esempi pratici di come usarli..
   URL http://www.owasp.org/index.php/Germany

(^) Pag. 28 of 121 **OWASP Germany Local Chapter** Le principali
attività riguardano l'organizzazione di incontri, conosciuti come AppSec
Germany Conference, che si svolge ogni anno. **URL**
http://www.owasp.org/index.php/Geneva **OWASP Geneva Local Chapter** Le
principali attività svolte da questo capitolo riguardano
l'organizzazione di incontri legati alle identità digitali e
autenticazione nelle applicazioni web. **URL**
http://www.owasp.org/index.php/Greece **OWASP Greece Local Chapter** Il
gruppo di lavoro OWASP greco è stata fondato nel 2005 con l'obiettivo di
informare la comunità greca sui rischi per la sicurezza nelle
applicazioni web. Il motivo principale che ha spinto alla sua creazione
è il sempre crescente numero di incidenti di sicurezza su Internet, come
ad esempio i tentativi di phishing a banche greche. Oggi, il gruppo
greco promuove localmente l'iniziativa OWASP attraverso il Software
Libero/Open e la traduzione in greco della documentazione OWASP.
Emettono una newsletter mensile, mantengono una mailing list per gli
aggiornamenti e gestiscono dibattiti online su problemi di sicurezza di
attualità. La comunità greca OWASP vuole riunire tutti coloro che sono
interessati e preoccupati per la sicurezza delle applicazioni web. Allo
stesso tempo, accoglie i volontari che sono disposti a lavorare su
progetti coordinati dall'OWASP, utilizzando software libero/open source.
Invitano a chiunque di condividere le proprie idee, pensieri e
riflessioni sugli attacchi, la difesa, i metodi di risposta, strumenti e
buone pratiche in materia di sicurezza di Internet. **URL**
http://www.owasp.org/index.php/Ireland-Dublin
http://www.owasp.org/index.php/Ireland-Limerick **OWASP Ireland Local
Chapter** Questo paese ha due gruppi locali: Dublino e Limerick. Il
gruppo più attivo è quello di Dublino le cui attività principali
riguardano l'organizzazione di eventi e conferenze. Questo gruppo
fornisce anche la formazione su progetti e risorse OWASP attraverso il
programma " OWASP projects and resources you can use today". Questo ha
lo scopo di promuovere i progetti OWASP, fornendo una selezione di
progetti maturi ed enterprise-ready con esempi pratici di come usarli.
**URL** http://www.owasp.org/index.php/Italy **OWASP Italy Local
Chapter** Le attività riguardano l'organizzazione di eventi e lo
sviluppo di tool. Il gruppo cerca di organizzare almeno 2 conferenze
all'anno, uno in primavera e un altro in autunno. Recentemente, hanno
lavorato sullo sviluppo di sqlmap, un *automatic SQL injection tool*
sviluppato in Python. L'iniziativa è sostenuta da partner come IsecLab,
CLUSIT e ISACA Roma. **URL** http://www.owasp.org/index.php/Latvia
**OWASP Latvia Local Chapter** E' stata creata nell'ottobre 2007. Le
attività principali riguardano l'organizzazione di eventi. Il gruppo non
si è dimostrato molto attivo negli ultimi anni.

(^) Pag. 29 of 121 **URL** http://www.owasp.org/index.php/Latvia **OWASP
Leeds/Northern Local Chapter** Questo è gruppo nuovo e molto attivo. Ha
tenuto riunioni in tutta l'Inghilterra settentrionale, tra cui a Leeds,
Manchester e Newcastle-upon-Tyne. **URL**
http://www.owasp.org/index.php/London **OWASP London Local Chapter** Le
attività di OWASP Londra si concentrano sulla preparazione e
l'organizzazione di eventi, conferenze e presentazioni. Il gruppo ha
registrato elevata attività nel corso del 2010. Esso prevede anche la
formazione su progetti e risorse OWASP attraverso il programma “OWASP
projects and resources you can use today”, che mira a promuovere
progetti OWASP, fornendo una selezione di progetti maturi ed
enterprise-ready con esempi pratici di come usarli. **URL**
http://www.owasp.org/index.php/Luxembourg **OWASP Luxembourg Local
Chapter** Le attività del gruppo riguardano la preparazione e
l'organizzazione di eventi e conferenze come il Java User Group (YAJUG)
o Chaos Computer Club Letzebuerg (C3L). Attualmente sembra che vi sia
poca attività in questo gruppo. **URL**
http://www.owasp.org/index.php/Norway **OWASP Norway Local Chapter** Le
attività di OWASP Norvegia riguardano la preparazione e l'organizzazione
di eventi e conferenze. Questo gruppo è stato molto attivo negli anni
passati, quando ha organizzato 8 conferenze in Norvegia in un anno.
**URL** http://www.owasp.org/index.php/Poland **OWASP Poland Local
Chapter** L'attività principale che questo gruppo è quella di
organizzare eventi. In questo gruppo sembra essere molto attivo, sono
stati coinvolti in 11 conferenze nel corso del 2010. L'iniziativa è
sostenuta da ISSA. **URL** http://www.owasp.org/index.php/Portuguese
**OWASP Portugal Local Chapter** Le attività di questo gruppo riguardano
l'organizzazione di conferenze e pubblicazioni. Ha organizzato uno dei
più importanti eventi di OWASP: *Ibero- American Web Application
Security Conference IBWAS'2010*. **URL**
http://www.owasp.org/index.php/Scotland **OWASP Scotland Local Chapter**
Le principali attività svolte da questo gruppo, secondo quanto riportato
sul loro sito, sono finalizzate a fonrire risposte insieme ad altri
gruppi britannici locali ai diversi uffici governativi del Regno Unito.
Questo gruppo sembra che organizzi anche incontri annuali. **URL**
http://www.owasp.org/index.php/Slovakia **OWASP Slovakia Local Chapter**
L'attività principale di questo gruppo riguarda l'organizzazione di
eventi.

::

   Pag. 30 of 121
   URL http://www.owasp.org/index.php/Spain
   OWASP Spain Local
   Chapter
   Questo gruppo svolge due attività principali. Da un lato collabora attivamente
   con OWASP su un progetto per fornire le specifiche e i requisiti legali per le
   applicazioni Web. D'altra parte, come la maggior parte degli altri gruppi locali
   di questa sezione, organizza eventi e conferenze annuali. Ha partecipato anche
   all'evento IBWAS'2010 [https://www.owasp.org/index.php/IBWAS10] in
   collaborazione con il gruppo portoghese.
   URL http://www.owasp.org/index.php/Sweden
   OWASP Sweden Local
   Chapter
   Questo gruppo si concentra sull'organizzazione di meeting ed eventi. Ha
   organizzato conferenze anche in collaborazione con altri gruppi del nord, come
   il norvegese e il finlandese.
   URL http://www.owasp.org/index.php/Switzerland
   OWASP Switzerland
   Local Chapter
   Questo gruppo organizza incontri su base periodica, soprattutto nella parte
   tedesca della Svizzera. I loro incontri e gli eventi sono principalmente su temi
   come test di sicurezza, lo sviluppo sicuro, hacking e architetture sicure. Sul loro
   sito Web sono fruibili diapositive di eventi e conferenze.
   URL http://www.owasp.org/index.php/Ukraine
   OWASP Ukraine Local
   Chapter
   E’ un gruppo di recente formazione ancora in fase di organizzazione

.. _motor-industry-software-reliability-association-misra:

5.2.4 Motor Industry Software Reliability Association (MISRA)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

MISRA è una *Motor Companies Consortium* all'interno del Regno Unito. I
suoi risultati (ricerca, i risultati della ricerca e standard de facto,
le linee guida) sono finalizzati principalmente al software sicuro e
affidabile per sistemi embedded nel settore automobilistico.

Nei primi anni 1990, il progetto MISRA era stato concepito col fine di
sviluppare linee guida per la realizzazione di software embedded nei
componenti elettronici dei veicoli stradali. Dopo la chiusura del il
finanziamento ufficiale cessato, i membri Misra hanno deciso di
continuare a lavorare insieme.

MISRA instaura quindi una collaborazione tra costruttori di veicoli,
fornitori di componenti e di consulenza ingegneristica. Esso mira a
promuovere le migliori pratiche nello sviluppo di sistemi elettronici
legati alla sicurezza dei veicoli stradali e di altri sistemi embedded.

La sua documentazione non è accessibile al pubblico, ma può essere
acquistata sul sito web del consorzio.

::

   URL http://www.misra.org.uk
   Country of HQ location
   Geographic Scope

.. _uk:

UK
^^

::

   National
   Type Industry

I lavori in corso MISRA includono:

(^) Pag. 31 of 121 Model based development and autocode – Incoraggia
alle buone pratiche ed evita le caratteristiche del linguaggio di
modellazione mal definito.

-  MISRA C++ (Produzione di una serie di linee guida per l'uso di C ++
   in sistemi critici)

-  MISRA C3 (3rd review of MISRA C)

-  Mira a promuovere le migliori pratiche nello sviluppo di sistemi
   elettronici legati alla sicurezza nei veicoli stradali e di altri
   sistemi embedded ( è stato adottato e utilizzato in una vasta gamma
   di settori e applicazioni, tra cui il settore ferroviario,
   aerospaziale, militare e medico)

MISRA Safety Analysis – Offre una guida sui requisiti della
decomposizione. Esso descrive come il ciclo di vita della sicurezza dei
sistemi automotive si inserisce nel ciclo di vita dello sviluppo dei
veicoli.

Risultati più rilevanti:

::

   Good Practice Guidelines for the Use of the C Language in Vehicle Based Software, ISBN 978- 0 -
   9524156-6-5, April 1998, October 2002
   Guidelines for the Use of the C Language in Critical Systems, ISBN 0 9524156 2 3
   (paperback), ISBN 0 9524156 4 X (PDF), October 2004
   Guidelines for safety analysis of vehicle based programmable systems, ISBN 978-0 -
   9524156-5-7 (paperback), ISBN 978-0 -9524156-7-1 (PDF), November 2007.
   Guidelines for the Use of the C++ Language in Critical Systems, ISBN 978-906400-03-3
   (paperback), ISBN 978-906400-04-0 (PDF), June 2008.
   Standard MISRA AC GMG: Generic modelling design and style guidelines, ISBN 978- 906400 - 06 -
   4 (PDF), May 2009.
   Pag. 32 of 121

.. _european-space-agency-esa:

5.2.5 European Space Agency (ESA)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Dall'inizio degli anni ‘90 l'ESA si è occupata di definire la qualità
dei prodotti software. La famiglia PSS^4 di standard (poi sostituito da
standard ECSS) include un software engineering standard e una serie di
guide.

::

   URL http://www.esa.int
   Country of HQ location
   Geographic Scope
   Paris
   European
   Type Collaboration of Several European Countries

Uno degli standard di software ampiamente utilizzato in quella serie,
chiamato “Guide to applying the ESA Software Engineering Standards to
small software projects” è disponibile all'indirizzo:
ftp://ftp.estec.esa.nl/pub/wm/wme/bssc/Bssc962.pdf

Questo standard definisce una serie di criteri di qualità per i
requisiti software e di design, che hanno una influenza diretta e
indiretta sulla sicurezza del software. Per i *quality criteria
requirements* i seguenti sono rilevanti:

-  *Are the characteristics of users and of typical usage mentioned? (No
   user categories missing)*

-  *Are all the external interfaces of the software explicitly
   mentioned? (No interfaces missing)*

-  *Is each requirement prioritised? (Is the meaning of the priority
   levels clear?)*

-  *Is each requirement verifiable (in a provisional acceptance test)?
   (Measurable: where possible,* *quantify; capacity, performance,
   accuracy)*

-  *Are the requirements consistent? (Non-conflicting)*

-  *Are the requirements sufficiently precise and unambiguous? (Which
   interfaces are involved, who* *has the initiative, who supplies what
   data, no passive voice.)*

-  *Are the requirements complete? Can everything not explicitly
   constrained indeed be viewed as* *developer freedom? Is a product
   that satisfies every requirement indeed acceptable? (No*
   *requirements missing)*

-  *Are the requirements understandable to those who will need to work
   with them later?*

-  *Are the requirements realisable within budget?*

-  *Most of the design quality criteria are relevant to software
   security.*

Risultati principali:

::

   Good
   Practice
   The PSS
   [http://www.esa.int/TEC/Software_engineering_and_standardisation/TECBUCUXBQE_2.html]
   family of standards for Software Quality.
   A guide to applying ESA Software Engineering Standards to small software projects is
   available at: ftp://ftp.estec.esa.nl/pub/wm/wme/bssc/Bssc962.pdf
   Eindhoven University of Technology provides further simplified requirements and design
   checklists. [http:// http://www.win.tue.nl/is/doku.php]

.. _serenity-forum:

5.2.6 Serenity Forum
~~~~~~~~~~~~~~~~~~~~

Questo forum è stato creato dai partner del progetto Serenity (un
progetto R&D FP6 finanziato fino a giugno 2009) per dare seguito alla
community istituita nel corso del progetto. SERENITY Forum è incaricato

(^4)
http://www.esa.int/TEC/Software_engineering_and_standardisation/TECBUCUXBQE_2.html

::

   Pag. 33 of 121

di fornire un approccio radicalmente nuovo alla Security Engineering
attraverso una vasta gamma di modelli di sicurezza e schemi di
integrazione. Si compone dei membri del progetto Serenity e di persone
individuali. Tuttavia non si evidenziano a seguire molte attività
derivanti da questo evento.

::

   URL http://www.serenity-forum.org
   Country of HQ location
   Geographic Scope
   European
   Type Academic

.. _iniziative-us:

5.3 INIZIATIVE US
-----------------

In questa sezione viene fornita una panoramica delle iniziative SSE
negli Stati Uniti. Questi sono stati classificati in base alla tipologia
(accademiche o di governo).

.. _cert-secure-coding.:

5.3.1 CERT Secure Coding…………………………………………………………………………………………………………………….
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Il CERT Secure Coding è un'iniziativa di sicurezza del programma
Computer Emergency Response Team (CERT). Questo programma fa parte del
Software Engineering Institute (SEI) alla Canergie Mellon University
(Pennsylvania, USA). Alcuni dei suoi programmi sono finanziati dal
governo degli Stati Uniti.

Nel novembre 1988, la Defense Advanced Research Projects Agency
(DARPA)incaricò il SEI, con la creazione di un centro per coordinare la
comunicazione tra gli esperti di sicurezza durante le emergenze e per
aiutare a prevenire futuri incidenti. Nell'ambito di questo compito,
CERT ha sviluppato il Software Initiative Assurance, che comprende:
Secure Coding Standards, Source Code Analysis Lab, Vulnerability
analysis, Function extraction for malicious code

Il SEI è un centro di ricerca e sviluppo finanziato dal governo
federale, che conduce ricerche di ingegneria del software in
acquisizione, architetture e linee di prodotto, miglioramento dei
processi e misurazione delle performance, sicurezza e l'interoperabilità
del sistema e l'affidabilità.

Il SEI lavora a stretto contatto con le organizzazioni di difesa e di
governo, soprattutto l'Ufficio Secretary of Defense/Acquisition,
Technology, and Logistics (OSD/AT&L)^5 , l'industria e il mondo
accademico, con l'obiettivo di migliorare continuamente i sistemi
software-intensive.

::

   URL http://www.cert.org/secure-coding/
   Country of HQ location
   Geographic Scope

.. _us-6:

.. _us-6:

US
^^

::

   National
   Type Academic

Le aree di lavoro CERT Secure Coding sono:

-  **Secure coding standards**
   [http://www.cert.org/secure-coding/research/secure-coding-
   standards.cfm] - Proposes standards for enhancing the security of
   programming languages.

-  **International Standards Development**
   [http://www.cert.org/secure-coding/standards/index.cfm] - Development
   of International Standards.

(^5) http://www.acq.osd.mil/

::

   Pag. 34 of 121

-  **Source Code Analysis Laboratory (SCALe)**
   [http://www.cert.org/secure-coding/products- services/index.cfm]
   SCALe allows source code to be assessed against a set of secure
   coding standards. SCALe issues and certifies conformance testing when
   the test‟s findings have been addressed by the developers.

-  **Development Tools and Libraries**
   [http://www.cert.org/secure-coding/devtools.html] - Tools and
   libraries for secure software development

-  **TSP Secure** [http://www.cert.org/secure-coding/secure.html] -
   Secure Team Software Process methodology.

CERT Secure Coding vuole influenzare fornitori per migliorare la
sicurezza base all'interno dei loro prodotti. Al fine di raggiungere
questo obiettivo, CERT Secure Coding lavora con sviluppatori di software
e organizzazioni di sviluppo software per ridurre le vulnerabilità
derivanti da errori di codifica (C, C ++ o linguaggi di programmazione
Java) prima di essere distribuiti. Inoltre, gli analisti CERT valutano
le cause della vulnerabilità e identificano le pratiche di secure
coding.

CERT collabora con ISO per la creazione di diversi standard su secure
coding.

Risultati più rilevanti:

::

   Training Secure Coding in C and C++
   [http://www.sei.cmu.edu/training/p63.cfm]
   Course of secure coding in C and C++ based on Addison-Wesley’s material: “Secure Coding in
   C and C++” and “The CERT C Secure Coding Standard”
   Standards
   for
   Software
   Developers
   CERT C Secure Coding Standard, Version 2.0
   CERT C++ Secure Coding Standard
   [https://www.securecoding.cert.org/confluence/pages/viewpage.action?pageId=637]
   CERT Oracle Secure Coding Standard for Java
   [https://www.securecoding.cert.org/confluence/display/java/SEI+CERT+Oracle+Coding+Sta
   ndard+for+Java]

.. _build-security-in.:

5.3. 2 Build Security In………………………………………………………………………………………………………………………….
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

E' un'iniziativa del governo degli Stati Uniti basata su un sito web
online, in cui sono raccolte informazioni relative al Software
Assurance. Si tratta del Strategic Initiatives Branch del National Cyber
Security Division (NCSD) [https://www.us-cert.gov/] del US DHS
[https://www.dhs.gov/]. Questa iniziativa mira a fornire agli
sviluppatori di software una guida pratica su come produrre software
sicuro.

Il programma Software Assurance US DHS cerca di ridurre le vulnerabilità
del software, minimizzare lo sfruttamento e indirizzare su routine di
sviluppo migliori per la distribuzione di prodotti software affidabili.
Queste attività porteranno a software più sicuro e affidabile a supporto
dei requisiti mission-critical da parte di imprese e infrastrutture
critiche.

Build Security cerca di spostare il paradigma di sicurezza dalla
gestione delle patch al Software Assurance. Questo cambiamento è stato
progettato per incoraggiare gli sviluppatori di software ad aumentare la
qualità e la sicurezza complessiva del software all'inizio, piuttosto
che applicare le patch ai sistemi all'emergere delle vulnerabilità.

Questo progetto vuole essere un luogo in cui la community US Software
Engineering (sviluppatori di software e organizzazioni di sviluppo
software) possono trovare informazioni e consigli pratici su come
produrre software sicuro e affidabile.

(^) Pag. 35 of 121 I contenuti del sito sono suddivisi in tre aree
principali:

-  Best Practice: current best thinking, available technology, industry
   practice

-  Knowledge: conoscenza effettiva security-related che tutti gli
   ingegneri dovrebbero avere sui Tools. Informazioni su classi generali
   di tool, con riferimento ai tool specifici.

::

   URL https://buildsecurityin.us-cert.gov/bsi/home.html
   Country of HQ location
   Geographic Scope

.. _us-7:

.. _us-7:

US
^^

::

   National
   Type Government

Il contenuto di Build Security In si basa sul principio che la sicurezza
del software è fondamentalmente un problema di ingegneria del software e
deve essere affrontato in modo sistematico per tutto il ciclo di vita di
sviluppo del software. Esso contiene, ed è collegato a una vasta gamma
di informazioni provenienti da diverse fonti, informazioni sulle US best
practices, tools, linee guida, regole, principi, e altre conoscenze per
aiutare le aziende a costruire software sicuro e affidabile.

Il personale della SEI della Carnegie Mellon University contribuisce e
revisiona gli articoli e mantiene il sito. Ai contenuti contribuiscono
anche ricercatori e professionisti provenienti da Cigital, Inc. e altre
organizzazioni (vedi Contributing Authors
[https://buildsecurityin.us-cert.gov/about-us/authors]).

I membri della community software assurance sono invitati a caricare gli
articoli per la pubblicazione sul sito web Build Security In o di
rivedere gli articoli caricati.

Risultati più rilevanti pubblicati in articoli:

::

   Best Practice Acquisition
   [https://buildsecurityin.us-cert.gov/articles/best-practices/acquisition] The
   objective is to raise provider awareness. The articles describe an acquisition
   life-cycle framework for security activities, products, and reviews and for
   selected acquisition contexts and life-cycle phases. The authors provide
   additional guidance on methods and resources for identifying and managing
   security risks.
   Architectural Risk Analysis
   [https://buildsecurityin.us-cert.gov/bsi/articles/best-
   practices/architecture.html] Presents best practice for reviewing, assessing,
   and validating the specification, architecture, and design of a software system
   with respect to software security, reliability and performance goals. It includes
   a discussion on the identification, assessment, prioritisation, mitigation and
   validation of the risks associated with architectural flaws.
   Code Analysis
   [https://buildsecurityin.us-cert.gov/articles/best-practices/code-analysis] -
   Presents best practice in performing code analysis to uncover errors in, and
   improve the quality of, source code. Methods include manual code auditing,
   walkthroughs, static analysis, dynamic analysis, metric analysis, testability
   analysis, crypto analysis, random number analysis and fault injection.
   Deployment and Operations
   [https://buildsecurityin.us-cert.gov/articles/best-practices/deployment-and-
   operations] - The objective is to describe, and provide pointers to, commonly
   accepted best practice and processes and the relevant characteristics of
   organisations that demonstrate competence in sustaining adequate security

(^) Pag. 36 of 121 during deployment and operations. Governance and
Management
[https://buildsecurityin.us-cert.gov/articles/best-practices/governance-and-
management] - These articles provide a recommended sequence of steps to
take in order to govern and manage enterprise, information, and software
security. Detailed “how-to” guidance is not provided. Security at the
enterprise and organisational level is addressed Incident Management
[https://buildsecurityin.us-cert.gov/articles/best-practices/incident-
management] - Incident management is defined. Examples of best practice
in building an incident management capability are presented. It also
takes a look at one particular component of an incident management
capability, a computer security incident response team (CSIRT), and
discusses its role in the systems development life cycle. Legacy Systems
[https://buildsecurityin.us-cert.gov/articles/best-practices/legacy-systems]
- Describes the kinds of security risks that can be present in legacy
systems, both in-house and commercially off-the-shelf, and offers
guidance for assessing those risks and making sound decisions about
addressing them. Measurement
[https://buildsecurityin.us-cert.gov/articles/best-practices/measurement]
- Best practice is described in relation to measurements for managing
the quality of software systems during development. Several proposed
measures for characterizing specific security-related features are
discussed, and the current extent of the practice of software
measurement with specific attention to the use of security-related
measures is described. Penetration Testing
[https://buildsecurityin.us-cert.gov/articles/best-practices/penetration-
testing] The concepts and goals of traditional penetration testing are
discussed and recommendations are made on how these can be adopted to
better suit the needs of software developers. Additionally, the present
state of the available tool base is described. Project Management
[https://buildsecurityin.us-cert.gov/bsi/articles/best-practices/project.html]
Focuses on how security influences project management tasks and suggests
refinements to existing practices. For example, project management can
affect how well security requirements are satisfied, in terms of how the
inputs from the technical, management, and operational communities are
coordinated. Planning has to reflect the resources, effort, and risks
associated with securing a new technology, such as Web Services. Design
and implementation decisions may create new security threats, which
should be represented in both project monitoring and planning.
Requirements Engineering
[https://buildsecurityin.us-cert.gov/articles/best-practices/requirements-
engineering] Best practice for security requirements engineering is
presented, including processes that are specific to eliciting,
specifying, analysing and validating security requirements. Specific
techniques that are relevant to security requirements, such as the
development of misuse/abuse cases, attack trees and specification
techniques are also discussed or referenced. Risk Management

(^) Pag. 37 of 121
[https://buildsecurityin.us-cert.gov/articles/best-practices/risk-management]
- A framework for identifying, tracking and managing software risks is
provided. Best practices associated with software risk management are
presented, together with content that discusses understanding software
risks in a business context, identifying business and technical risks,
prioritising business and technical risks, and defining risk mitigation
strategies. Security Testing
[https://buildsecurityin.us-cert.gov/articles/best-practices/security-testing]
- The primary objective is to improve the understanding of some of the
processes of security testing, such as test vector generation, test code
generation, results analysis and reporting. This will help testers to
improve the generation of test vectors and increase their confidence
when testing security function behaviours. Software Assurance
[https://buildsecurityin.us-cert.gov/swa/software-assurance-pocket-guide-
series] A series of documents on software assurance in acquisition and
outsourcing, software assurance in development, the software assurance
life cycle and software assurance measurement and information needs.
System Strategies
[https://buildsecurityin.us-cert.gov/articles/best-practices/system-strategies]
System complexity is an aggregate of technology, scale, scope,
operational, and organisational issues. Business usage, the technologies
applied, and the changing operational environment raise software risks
that are typically not addressed in current practice. It discusses the
effects of the changing operational environment on the development of
secure systems. Vulnerability analysis has typically concentrated on
errors in coding or in the interfaces among components; however, system
interactions can also be a seed bed for vulnerabilities. One article in
this content area includes discussions on the software assurance
challenges inherent in networked systems development and proposes a
structured approach, using scenarios, to analysing potential system
stresses. Training and Awareness
[https://buildsecurityin.us-cert.gov/articles/best-practices/training-and-
awareness] This examines current practice in software security training
and awareness offerings across the industry. It also briefly describes
and compares the commercial sector's training offerings with current
academic curricula in some of the US's top universities. White Box
Testing
[https://buildsecurityin.us-cert.gov/articles/best-practices/white-box-testing]
This presents best practice in performing white box activities for
testing code construction. The activities that provide the basis for
white box dynamic analysis include: specifying the operational or
expected usage or test profile; specifying key interfaces that feed data
into the software; and compiling a list (or partial list) of undesirable
output events, for which the software's behaviour should be monitored.
Also discussed are strategies for examining the internal structure of a
program, statement coverage, decision coverage, condition coverage,
decision/condition coverage, and multiple-condition coverage. **Tools**
Black Box Testing
[https://buildsecurityin.us-cert.gov/articles/tools/black-box-testing]
Information is provided about black box testing tools. This term is used
to refer

(^) Pag. 38 of 121 to tools that take a black box view of the system
under test; they do not rely on the availability of software source code
and, in general, take an outside-in view of the software, which means
that they try to explore the software's behaviour from the outside. The
focus is on black box testing technologies that are unique to software.
Modelling Tools
[https://buildsecurityin.us-cert.gov/articles/tools/modeling-tools]This
provides an introduction to modelling in the context of security
analysis and discusses how tools can support security analysis during
development. A model is an abstract representation of an object. The
decomposition of a system might be grouped into components and their
dependencies. A model can demonstrate the consistency of the system
specifications or be a predictor of system behaviour. The analysis of
system performance in data throughput or computation efficiency, so as
to meet critical real-time performance requirements, depends on how that
aspect of system behaviour is modelled. Penetration Testing Tools
[https://buildsecurityin.us-cert.gov/articles/tools/penetration-testing-tools]
Information about penetration testing tools is provided. Source Code
Analysis
[https://buildsecurityin.us-cert.gov/articles/tools/source-code-analysis]-
Outlines what automated security analysers can do, provides a business
case for their use, and provides some criteria for evaluating individual
tools. Code samples are provided for running tools against, in order to
verify that the tools are able to detect known problems in the code.
**Knowledge** Assurance Cases
[https://buildsecurityin.us-cert.gov/articles/knowledge/assurance-cases]
This introduces the concepts and benefits of creating and maintaining
assurance cases for security. A security assurance case uses a
structured set of arguments and a corresponding body of evidence to
demonstrate that a system satisfies specific claims with respect to its
security properties. Attack Patterns
[https://buildsecurityin.us-cert.gov/articles/knowledge/attack-patterns]
These articles discuss the concept of attack patterns as a mechanism for
capturing and communicating the attacker‟s perspective. Attack patterns
are descriptions of common methods of exploiting software. Business Case
Models
[https://buildsecurityin.us-cert.gov/articles/knowledge/business-case-models]

-  This presents a conceptual framework for quantifying the cost and
   benefits of investments in secure coding techniques. Guidance on
   implementing the framework will include the variables and data
   elements to focus on and the means of measuring and quantifying them.
   With these measurements, one can calculate the economic benefits
   (cost) of these investments. Details are also provided on current
   practice and current research on the case for secure coding
   techniques. Coding Practices
   [https://buildsecurityin.us-cert.gov/articles/knowledge/coding-practices]
   Describes methods, techniques, processes, tools and runtime libraries
   that can prevent or limit exploits against vulnerabilities. Each
   document describes the development and technology context in which
   the coding practice is applied, as well as the risk of not following
   the practice and the type of attacks that could result.

::

   Pag. 39 of 121
   Coding Rules
   [https://buildsecurityin.us-cert.gov/bsi/76-BSI.html].Coding rules are
   representations of knowledge gained from real-world experience of potential
   vulnerabilities that exist in programming languages like C and C++. Creating
   and using software with a given coding environment enables the discovery of,
   and learning about, vulnerabilities that exist in this environment, how to
   recognise whether they crop up in our code and how to fix them. Coding Rules
   are the codification of this knowledge. They help software developers,
   whether manually or in conjunction with tools, to discover, explore, remove
   and eventually prevent security vulnerabilities in their code.
   Guidelines
   [https://buildsecurityin.us-cert.gov/bsi/articles/knowledge/guidelines.html]
   This provides information and data for educating software development
   professionals on the concept, applicability and value of design guidelines. In
   addition, this section collects, and makes available, a set of Design Guidelines
   to assist software development professionals with identifying and removing
   potential vulnerabilities in software systems.
   They are building, as well as developing, more mature and security-knowledge-
   aware design practices for future software systems.
   Lessons Learned
   [https://buildsecurityin.us-cert.gov/articles/knowledge/lessons-learned] This
   describes the lessons learned as a result of actual project experience. Lessons
   learned can be both positive and negative, providing both the opportunity to
   learn about techniques and approaches that can be followed on future
   projects and about the pitfalls to avoid.
   Principles
   [https://buildsecurityin.us-cert.gov/articles/knowledge/principles].This
   provides information and data for educating software development
   professionals on the concept, applicability and value of software security
   principles. It also contains a set of key secure software principles that will help
   software development professionals analyse and create their software
   architectures from a security perspective and gain a greater understanding of
   the key underlying concepts and patterns that, depending on how they are
   addressed, can make software either more, or less, secure.
   SDLC Process
   [https://buildsecurityin.us-cert.gov/articles/knowledge/sdlc-process] This
   discusses the application of software assurance best practice in the context of
   various SDLC methodologies.

.. _software-assurance-metrics-and-tool-evaluation-samate:

5.3.3 Software Assurance Metrics and Tool Evaluation (SAMATE)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

SAMATE è un'iniziativa US Government software assurance, un progetto
inter-agenzie tra gli Stati Uniti e il DHS National Institute of
Standards and Technology (NIST). Il suo obiettivo è quello di migliorare
la garanzia software: (i) sviluppando metriche e metodologie per
valutare i tool di sicurezza del software; (ii) identificando le
vulnerabilità relative alla pratiche di codifica e dei metodi di
ingegneria del software.

Il progetto di riferimento di SAMATE sviluppa casi di test al fine di
esaminare il codice sorgente di strumenti e applicazioni. Rileva e
segnala le debolezze, in modo da fornire agli utenti finali e
sviluppatori tool di garanzia del software con una serie di flaws noti
attraverso i quali valutare i propri tool.

L'uscita principale di questa iniziativa è il SAMATE Reference Dataset
(SRD), che è un database online alimentato regolarmente da SAMATE.
Questa banca dati online, a disposizione del pubblico, fornisce casi di
test per gli sviluppatori e utenti finali, attraverso i quali è
possibile effettuari valutazioni di tool di sicurezza.

::

   Pag. 40 of 121
   URL http://samate.nist.gov
   Country of HQ location
   Geographic Scope

.. _us-8:

.. _us-8:

US
^^

::

   National
   Type Governement

SAMATE è finalizzato al miglioramento del software assurance attraverso
lo sviluppo di metodologie che consentano la valutazione software dei
tool, misurare l'efficacia dei tool e delle tecniche, individuare le
lacune negli strumenti e nei metodi. Il progetto sostiene Tools Software
Assurance della US DHS e R&D Requirements Identification Program (in
particolare, la Parte 3, tecnologia -strumenti e requisiti-), che
affronta l'individuazione, la valorizzazione e lo sviluppo di software
assurance tools.

Il progetto SAMATE compone di due parti:

-  sviluppo di metriche per l'efficacia dei software security assessment
   (SSA) tools

-  valutazione di metodi e strumenti SSA attuali al fine di individuare
   le carenze che possono portare a guasti dei prodotti software e
   vulnerabilità

Infine, SAMATE sta sviluppando anche alcune specifiche rivolte agli
sviluppatori di strumenti di garanzia del software, che gli consentano
di classificare e valutare questa tipologia di tool.

Risultati più significativi:

::

   Specifications Source Code Security Analysis
   [https://samate.nist.gov/index.php/Source_Code_Security_Analysis.html]
   Specifications and test plans for source code security analyser tools. This type
   of tool examines source code in order to detect and report weaknesses that
   can lead to security vulnerabilities.
   Web Application Scanner Specification
   [https://samate.nist.gov/index.php/Web_Application_Scanner.html]
   “Web Application Scanner Functional Specification Version 1.0”. These
   specifications are brought together in NIST Special Publication 500-269
   [https://samate.nist.gov/docs/webapp_scanner_spec_sp500-269.pdf].
   Test Cases SAMATE reference datasheet
   [https://samate.nist.gov/SRD/]
   Provides users, researchers, and software security assurance tool developers
   with a set of known security flaws. These will allow end users to evaluate tools,
   and tool developers to test their methods.
   SRD database
   [https://samate.nist.gov/SRD/view.php]
   A collection of test cases aimed at detecting code weaknesses.

.. _common-weakness-enumeration-cwe:

5.3.4 Common Weakness Enumeration (CWE)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

CWE è un'iniziativa sostenuta e co-sponsorizzata dalla NCSD della US DHS
e il NIST. Attualmente è mantenuta e guidata da MITRE Corporation.

Il CWE è una lista formale o tassonomia, che classifica le tipologie più
comuni di vulnerabilità del software. Gli obiettivi principali di CWE
sono:

::

   Pag. 41 of 121

-  Gestire la *common taxonomy* per la classificazione delle
   vulnerabilità comuni del software relativamente ad architettura,
   progettazionem e codice;

-  Fornire una classificazione standard per tool di protezione del
   software

-  Fornire una linea di base da cui partire per aiutare la community SSE
   ad identificare, attenuare e prevenire questo tipo di debolezza
   software.

::

   URL http://cwe.mitre.org/
   http://nvd.nist.gov/cwe.cfm
   Country of HQ location
   Geographic Scope

.. _us-9:

.. _us-9:

US
^^

::

   National
   Type Government

Questo progetto utilizza i risultati del progetto SAMATE per creare
l'elenco CWE delle vulnerabilità e la sua tassonomia associata e
l'albero di classificazione (vedi figura sotto tratta dal NIST).
