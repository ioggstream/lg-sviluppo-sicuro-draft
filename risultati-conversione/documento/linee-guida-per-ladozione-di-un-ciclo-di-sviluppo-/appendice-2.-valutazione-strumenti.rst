.. _appendice-2.-valutazione-strumenti:

APPENDICE 2. VALUTAZIONE STRUMENTI
==================================

.. _a.-checkmarx:

A. CHECKMARX
------------

.. _prodotto-categoria-fase-sse-sito-web:

PRODOTTO CATEGORIA FASE SSE SITO WEB
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

::

   CHECKMARX SAST Implementation https://www.checkmarx.co
   m/
   DESCRIZIONE
   È un tool a pagamento, per l’analisi statica del codice, posizionato da Gartner nel quadrante Challengers
   nell’ambito dell’Application Security Testing (AST). Supporta numerosi linguaggi (vedi oltre). Può essere
   integrato a vari livelli nell’ambito della fase di Implementation: IDE, build server, bug tracking tools.
   Orientato alla facilità d’uso da parte del team di sviluppo.inserire una descrizione del prodotto
   Tainted analysis, Pattern matching , "scan rules" (customizable)inserire il meccanismo d'azione

.. _analisi-del-valutatore-score:

ANALISI DEL VALUTATORE SCORE
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

::

   Livello di integrazione con i seguenti prodotti
   a. IDEs Esistono plugin per i seguenti IDE:
   Eclipse,
   Visual Studio e
   IntelliJ.
   I plugin consentono la scansione del codice, l'analisi e la navigazione dei
   risultati in modo integrato con l'IDE.

.. _section:

7
~

::

   b. source repository, TFS,
   SVN,
   GIT,
   Perforce.

.. _section-1:

.. _section-1:

7
~

::

   c. build server, Jenkins,
   Bamboo,
   TeamCity,
   TFS,
   Anthill Pro,
   Maven.

.. _section-2:

.. _section-2:

7
~

::

   d. bug tracking tools
   Jira. 4
   I linguaggi di
   programmazione
   supportati
   Java
   C#
   JavaScript and commonly used frameworks
   Node.JS and commonly used frameworks
   VB.NET
   ASP.NET
   VB6
   PHP

.. _section-3:

.. _section-3:

7
~

.. _interno-22:

.. _interno-22:

INTERNO
-------

Linee guida per l'adozione di un ciclo di sviluppo software sicuro -
D01.Fase1.SP2 Draft2 04/12/2017 EQ4A56036T05 Rev. 0.1

::

   Pag. 110 of 121

.. _interno-23:

.. _interno-23:

INTERNO
-------

.. _cc:

C/C++
~~~~~

::

   Apex and VisualForce
   Ruby
   VBScript
   Perl
   HTML5
   Python
   Groovy
   Scala
   I framework applicativi
   supportati (es. Spring,
   Hibernate, ...)
   [*] Requires minor adjustments
   Platform/Enviroment: Java
   Struts, Spring MVC, iBatis*, GWT, Hibernate, OWASP ESAPI, JSTL FMT
   Taglib, ATG DSP Taglib, Java Server Faces (JSF), JavaScript
   Platform/Enviroment: .NET
   Enterprise Libraries, Telerik, ComponentArt, Infragistics, FarPoint, iBatis*,
   Hibernate.Net [*], Entity framework up to 4.3.1
   Platform/Enviroment: PHP
   Zend, Kohana, CakePHP, Symfony, Smarty, OWASP ESAPI
   Platform/Enviroment: C/C++
   MISRA
   Platform/Enviroment: Ruby
   Ruby on Rails
   Platform/Enviroment: JavaScript
   JQuery, Node.js, Ajax, Knockout, AngularJS, ExpressJS, Jade, Backbone,
   Handlebars, Hapi.JS
   Platform/Enviroment: iOS
   iOS mobile applications
   Platform/Enviroment: Python
   Django
   Platform/Enviroment: Groovy
   Grails

.. _section-4:

.. _section-4:

7
~

::

   Le tipologie di
   applicazione
   supportate (Web,
   Mobile, Client-
   Server...)
   Web application, Mobile (Android, iOS, Windows mobile), Client-Server 7

.. _interno-24:

.. _interno-24:

INTERNO
-------

Linee guida per l'adozione di un ciclo di sviluppo software sicuro -
D01.Fase1.SP2 Draft2 04/12/2017 EQ4A56036T05 Rev. 0.1

::

   Pag. 111 of 121

.. _interno-25:

.. _interno-25:

INTERNO
-------

::

   Le vulnerabilità
   riconosciute (Sql
   injection, Cross-site
   scripting, Code
   injection...)
   SQL Injection, Cross-site scripting, Code injection, Buffer Overflow,
   Parameter tampering, Cross-site request forgery, HTTP splitting, Log
   forgery, DoS, Session Fixation, Session poisoning, Unhandled exceptions,
   Unreleased resources, unvalidated input, URL redirection attack,
   Dangerous Files Upload, Hardcoded password

.. _section-5:

.. _section-5:

7
~

::

   Gli Standard supportati
   (OWASP Top 10, SANS
   25, ...)
   OSWAP Top 10 2013, OSWAP Mobile Top 10, SANS 25, HIPAA, FISMA,
   BSIMM, PCI DSS, Mitre CWE

.. _section-6:

.. _section-6:

7
~

::

   L’integrazione di
   “Custom rules”
   E' possibile definire Custom Rules (per esempio per dichiarare che una
   funzione esegue sanitizzazione)

.. _section-7:

.. _section-7:

4
~

::

   L’incidenza dei “Falsi
   positivi”
   In primo luogo, è possibile “spegnere” falsi positivi estendendo la lista dei
   “sanitizer” fornita out of the box da checkmarx (con pochi colpi di click).
   In secondo luogo, è possibile “spegnere” falsi positivi dichiarandoli come
   “Not Exploitable”.
   In terzo luogo, è stato possibile apprezzare un approccio messo in atto da
   Checkmarx atto a limitare il numero di segnalazioni. La prova eseguita ha
   evidenziato che: in presenza di codice evidentemente prono a una SQL
   INJECTION, ma in assenza di un vettore di attacco, la segnalazione della
   vulnerabilità viene soppressa. Viceversa la segnalazione viene prodotta se
   viene individuato anche un vettore di attacco. Il side effect è che in una
   scansione parziale che considera il codice vulnerabile ma esclude in tutto o
   in parte il vettore d’attacco, non vengono prodotte segnalazioni.

.. _section-8:

.. _section-8:

4
~

::

   La capacità di analisi
   “raw source code” vs
   “need to compile”
   Lo strumento è in grado di funzionare in modalità “raw source code”. E'
   quindi possibile sottoporre anche porzioni di codice "out-of-context".
   Tuttavia, in questo caso potrebbero non essere segnalate certe
   vulnerablità che invece si manifestano in una scansione "in-context". E' una
   scelta by design per limitare falsi positivi.
   Raw
   Source
   La capacità di
   analizzare le
   dipendenze da librerie
   esterne al fine di
   controllare se sono
   presenti vulnerabilità
   note
   Esiste un add-on di CheckMarx (acquistabile a parte) che analizza le
   dipendenze da librerie esterne al fine di controllare se sono presenti
   vulnerabilità note, interrogando una base dati esterna.

.. _section-9:

.. _section-9:

1
~

::

   La capacità di correlare
   lo scan statico con
   l’esito di uno scan
   dinamico (correlazione
   White Box con Black
   Box)

.. _no-1:

NO 1
~~~~

.. _le-performance:

LE PERFORMANCE
~~~~~~~~~~~~~~

::

   a. Full scan vs
   Incremental scan
   Sono supportati sia Full sia Incremental scanning 7

.. _interno-26:

.. _interno-26:

INTERNO
-------

Linee guida per l'adozione di un ciclo di sviluppo software sicuro -
D01.Fase1.SP2 Draft2 04/12/2017 EQ4A56036T05 Rev. 0.1

::

   Pag. 112 of 121

.. _interno-27:

.. _interno-27:

INTERNO
-------

::

   b. Client-side scan
   vs Server-side scan
   Server-side scanning: i sorgenti in tutti le configurazioni (anche in quella di
   plug-in integrato con l'ambiente di sviluppo) vengono compressi e inviati al
   server dove avviene effettivamente lo scan. Ne consegue il beneficio
   dell'allegerimento dell'occupazione della potenza di calcolo dei Client.

.. _section-10:

.. _section-10:

7
~

::

   Eventuali funzionalità
   di prioritizzazione delle
   remediation
   Le vulnerabilità individuate vengono ordinate secondo 4 livelli: High,
   Medium, Low, Information che indirizzano la priorità della remediation.

.. _section-11:

.. _section-11:

7
~

::

   La facilità d’uso Lo strumento è fortemente orientato alla facilità d’uso da parte del team di
   sviluppo
   (partendo dalla cosapevolezza -preso dalla homepage- che "Getting
   developers to use application security testing is one of the biggest
   challenges facing security professionals today").
   Alla prova dei fatti, lo strumento è davvero molto fruibie

.. _section-12:

.. _section-12:

7
~

::

   I costi di licenza Esistono varie forme di licenza: per numero progetti e per numero di
   sviluppatori. Ad esempio, la licenza a 6 mesi, per 5 sviluppatori e senza
   limiti sul numero di progetti (ma con un numero di linee di codice (LOC)
   fino a 1.000.0000) costa per 11.062,50 €

.. _alto:

ALTO
~~~~

::

   Il supporto alla
   reportistica
   E' supportata una reportistica di tipo custom (non sono espressamente
   disponibili report pre-definiti, ad esempio specificamente orientati a CWE
   SANS Top 25, OWASP Top 10, PCI Data Security Standard, ecc). I formati
   supportati sono: PDF, CSV, RTF, XML.

.. _section-13:

.. _section-13:

4
~

::

   La classificazione degli
   errori riportati
   Sono riferiti agli standard supportati (es. "PCI DSS (3.1) - 6.5.1 - Injection
   flaws - particularly SQL injection", OWASP Top 10 2013 - A1-Injection)

.. _section-14:

.. _section-14:

7
~

.. _considerazioni-finali-del-valutatore:

CONSIDERAZIONI FINALI DEL VALUTATORE
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. _considerazioni-generali:

CONSIDERAZIONI GENERALI
~~~~~~~~~~~~~~~~~~~~~~~

.. _interno-28:

.. _interno-28:

INTERNO
-------

Linee guida per l'adozione di un ciclo di sviluppo software sicuro -
D01.Fase1.SP2 Draft2 04/12/2017 EQ4A56036T05 Rev. 0.1

::

   Pag. 113 of 121

.. _interno-29:

.. _interno-29:

INTERNO
-------

::

   Considerazioni generali:

**1. Installazione agevole 2. Fruizione da Browser agevole (apprezzabile
il riconoscimento automatico del linguaggio: è sufficiente eseguire lo
zip dei sorgenti) 3. Fruizione da plug-in integrato con IDE agevole e
intuitiva (tasto destro su un punto del progetto e si può eseguire lo
scan) 4. Supporto alla remediation in tutti gli ambienti: CxAudit,
plug-in, browser 5. Inserimento di regole custom agevole (esaminato il
caso “sanitizer”) 6. Reporting custom 7. Sinottico minimale 8. Scan full
e incrementale 9. No need to compile (ma anche nessun check sulle
librerie linkate, a meno di integrare un componente licenziato a parte)
10. Integrazione con Jenkins, come step aggiuntivo della fase di build
(Continuous Integration), agevole attraverso plug-in**

::

   Punti di forza:

**1. Vettore di attacco 2. Funzionlità “Full Graph” che raccorda più
vettori di attacco mostrando eventuali punti di intersezione (candidati
ideali per il fix)** **APPROCCIO PER LA VALUTAZIONE** L'approccio
seguito è stato quello di costruire un programma di benchmark che
presentasse XSS e SQL Injection: XSS e SQL Injection sono le
vulnerabilità rispettivamente al primo e al secondo posto nella OWASP
TOP Ten 2010. Condizione necessaria per candidare un tool alla Leonardo
Suite è la capacità del tool di identificare (anche solo parzialmente)
le vulnerabilità inserite. In caso contrario l'analisi del tool si
conclude con esito negativo. La scelta di costruire un programma di
benchmark (in vece di utilizzare benchmark preconfezionati, come ad
esempio https://github.com/OWASP/Benchmark) nasce dalla volontà di
evitare overfitting dei tool sottoposti ad analisi. L'utilizzo dello
stesso programma di benchmark consente di avere risultati comparabili
tra i vari tool sottoposti ad analisi. Nel caso di Checkmarx, le SQL
Injection sono state individuate ad eccezione di una (1 falso negativo).
Segnalato il problema all'assistenza, si è stabilito che la mancata
individuazione della SQL Injection era dovuta al fatto che essa
sfruttava una feature introdotta in Java 7 (“With Java 7, you can create
one or more "resources” in the try statement. A “resources” is something
that implements the java.lang.AutoCloseable interface. This resource
would be automatically closed and the end of the try block." Vedi
https://dzone.com/articles/java-7-new-feature-%E2%80%93), non ancora
integrata nel Virtual Compiler di Checkmarx. Putroppo nella successiva
versione di Checkmarx (8.1.0) il problema non risulta ancora risolto.
Nel caso di Checkmarx, l'XSS (di tipo reflected) è stato individuato
insieme a 2 problemi di “Sensitive Cookie in HTTPS Session Without
Secure Attribute”. Entrambi i problemi, tuttavia, vengono classificati
come “Low” (benché l'XSS sia sfruttabile). Estremamente interessante è
l'esito della scansione con Checkmarx a valle della risoluzione dei
problemi XSS e Cookie attraverso l'impiego delle ESAPI (OWASP): le
segnalazioni correttamente scompaiono, segno che Checkmarx riconosce
nativamente la sanitizzazione del codice attraverso l'adozione del
framework ESAPI. **INTERPRETAZIONE DEI RISULTATI**

.. _interno-30:

.. _interno-30:

INTERNO
-------

Linee guida per l'adozione di un ciclo di sviluppo software sicuro -
D01.Fase1.SP2 Draft2 04/12/2017 EQ4A56036T05 Rev. 0.1

::

   Pag. 114 of 121

.. _interno-31:

.. _interno-31:

INTERNO
-------

::

   Valutazione molto positiva, eccetto il falso negativo, al cui riguardo si svolgono ancora queste
   considerazioni (avallate da ulteriori prove). Se si elimina l’uso del nuovo costrutto sintattico introdotta in
   Java 7, Checkmarx individua la SQL INJECTION. Quindi sembra verosimile che la mancata interpretazione
   del nuovo costrutto sintattico, impedisca in sostanza a Checkmarx di individuare l’attack vector, senza il
   quale –by design- un vulnerabilità non viene segnalata.
   TEAM DI VALUTAZIONE Leonardo Software Security team

.. _b.-codedx:

B. CODEDX
---------

.. _prodotto-categoria-fase-sse-sito-web-1:

.. _prodotto-categoria-fase-sse-sito-web-1:

PRODOTTO CATEGORIA FASE SSE SITO WEB
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

::

   CodeDx SAST/DAST Implementation/Verification https://codedx.com/

.. _descrizione:

DESCRIZIONE
~~~~~~~~~~~

::

   CodeDx e' un Tool commerciale che serve ad effettuare la verifica di eventuali vulnerabilità di programmi
   e software presi in considerazione. CodeDx riunisce una serie di strumenti di analisi del codice (sia gratuiti
   che commerciali) che consentono a loro volta di individuare e correggere agevolmente eventuali bugs nel
   codice da analizzare.inserire una descrizione del prodotto
   Source analysis, Pattern matching , "scan rules" (customizable)inserire il meccanismo d'azione
   ANALISI DEL VALUTATORE SCORE
   Livello di integrazione con i seguenti prodotti
   a. IDEs CodeDx si integra con i seguenti ide: Eclipse, Visual Studio 8
   b. source
   repository,
   CodeDx si integra i seguenti repository:
   Git (direttamente); Subversion, Mercurial, o Team Foundation
   Version Control (TFVC) (tramite zip del "source outside" di CodeDx e
   successivo upload verso CodeDx)

.. _section-15:

.. _section-15:

8
~

::

   c. build server,
   CodeDx si integra con i seguenti build server:
   Jenkins, Maven 7
   d. bug tracking
   tools
   CodeDx supporta il tool Bug Issue Tracker JIRA
   Le tipologie di
   applicazione
   supportate (Web,
   Mobile, Client-
   Server...)
   Client Server, Web, Mobile (Android Studio) 7
   I linguaggi di
   programmazione
   supportati
   C/C++, Java, Javascript, JSP, .NET(C#, Visual Basic), Python, Ruby 8
   I framework
   applicativi supportati
   (es. Spring,
   Il tool supporta i piu' popolari frameworks tra i quali Spring-MVC,
   JQuery e molti altri. 7

.. _interno-32:

.. _interno-32:

INTERNO
-------

Linee guida per l'adozione di un ciclo di sviluppo software sicuro -
D01.Fase1.SP2 Draft2 04/12/2017 EQ4A56036T05 Rev. 0.1

::

   Pag. 115 of 121

.. _interno-33:

.. _interno-33:

INTERNO
-------

::

   Hibernate, ...)
   Gli Standard
   supportati (OWASP
   Top 10, SANS 25, ...)
   CodeDx supporta sia lo standard CWE che altri standard come
   OWASP Top 10, SANS Top 25 e PCI-DSS. 8
   Le vulnerabilità
   riconosciute (Sql
   injection, Cross-site
   scripting, Code
   injection...)
   Tutte le vulnerabilità descritte negli standard di cui al punto 5 7
   L’integrazione di
   “Custom rules” E' possibile all'interno di CodeDx creare delle regole personalizzate^7
   Possibilita' di inibire
   la segnalazione di
   particolari
   vulnerabilita'
   E' possibile all'interno del Tool gestire la segnalazione di una
   particolare vulnerabilità 7
   L’incidenza dei “Falsi
   positivi” Dai riscontri, l'incidenza di falsi positivi è accettabile^8
   La capacità di analisi
   “raw source code” vs
   “need to compile”
   CodeDx (a seconda dei tool embedded che vengono invocati)
   permette di analizzare il codice in entrambe le modalita'
   (sia source-code che raw-code).
   entrambe
   La capacità di
   analizzare le
   dipendenze da
   librerie esterne al
   fine di controllare se
   sono presenti
   vulnerabilità note
   CodeDx permette (tramite l'utilizzo di tool embedded come
   Dependency Check) di analizzare le dipendenze da librerie esterne al
   fine di controllare se sono presenti vulnerabilità note

.. _section-16:

.. _section-16:

8
~

::

   La capacità di
   correlare lo scan
   statico con l’esito di
   uno scan dinamico
   (correlazione White
   Box con Black Box)
   Il prodotto è in grado di effettuare correlazioni tra entrambe le
   tipologie di scan del codice

.. _section-17:

.. _section-17:

7
~

::

   Le performance
   a. Full scan vs
   Incremental scan
   Il prodotto è in grado di effettuare entrambe le tipologie di scan del
   codice

.. _section-18:

.. _section-18:

8
~

::

   b. Client-side
   scan vs Server-side
   scan
   Il prodotto consente di effettuare scan sia lato server che client 7
   Supporto alla
   Remediation
   Il tool guida nella localizzazione del problema ed offre supporto
   informativo utile per sanarlo.

.. _section-19:

.. _section-19:

6
~

::

   Funzionalità di
   prioritizzazione delle
   Remediation
   Il tool permete di evidenziare i bugs in base a delle priorita' di
   intervento

.. _section-20:

.. _section-20:

7
~

.. _interno-34:

.. _interno-34:

INTERNO
-------

Linee guida per l'adozione di un ciclo di sviluppo software sicuro -
D01.Fase1.SP2 Draft2 04/12/2017 EQ4A56036T05 Rev. 0.1

::

   Pag. 116 of 121

.. _interno-35:

.. _interno-35:

INTERNO
-------

::

   La facilità d’uso
   Il prodotto è piuttosto facile da installare e assolutamente intuitivo
   da utilizzare

.. _section-21:

.. _section-21:

8
~

::

   I costi di licenza
   CodeDx e' un prodotto commerciale a pagamento dai costi non
   eccessivi rispetto a strumenti similari commerciali. L'argomento
   andrebbe comunque analizzato in una logica commerciale
   complessiva aziendale.

.. _medio:

MEDIO
~~~~~

::

   Il supporto alla
   reportistica
   Il tool consente di produrre un'ottima reportistica in vari tipi di
   formato (Pdf, xml, Excel)

.. _section-22:

.. _section-22:

8
~

::

   La classificazione
   degli errori riportati
   Il Tool CodeDx permette di classificare gli errori secondo quattro
   tipologie di gravita': High, Medium, Low e Info 7
   CONSIDERAZIONI FINALI DEL VALUTATORE
   Dopo aver preso in considerazione tutti i vari punti descritti nella scheda si ritiene che il Tool CodeDx sia
   un ottimo tool di facile uso e integrabile con molti altri tool sia gratuiti che a pagamento. Il tool permette
   agli sviluppatori di software, tester e analisti della sicurezza diindividuare e gestire con modalita'
   abbastanza semplici le vulnerabilità nel software. Il tool permette di integrare una quantita' molto ampia
   di plugin e altri tool che danno una copertura quasi completa di tutti i linguaggi e gli ide presenti sul
   mercato. La Reportistica e' molto dettagliata e disponibile in vari formati. Dalle evidenze riscontrate, è
   emerso che il prodotto sia adeguatamente affidabile. Si ritiene pertanto che CodeDx sia utilizzabile
   proficuamente per gli scopi aziendali.
   TEAM DI
   VALUTAZIONE Leonardo Software Security team^

.. _c.-sast:

C. SAST
-------

.. _prodotto-categoria-fase-sse-sito-web-2:

.. _prodotto-categoria-fase-sse-sito-web-2:

PRODOTTO CATEGORIA FASE SSE SITO WEB
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

::

   SonarQube SAST Implementation http://www.sonarqube.org

.. _descrizione-1:

.. _descrizione-1:

DESCRIZIONE
~~~~~~~~~~~

::

   SonarQube è un prodotto avanzato per l'analisi statica del codice sorgente, finalizzato alla ricerca di errori
   di programmazione e di costrutti che costituiscono delle bad practise. I Bug rilevati sono tracciati ed
   evidenziati in un'interfaccia web intuitiva, in modo da poter seguire e gestire il processo di remediation.
   Dato che si tratta di un prodotto open source, il miglioramento dei pattern per il riconoscimento dei
   problemi è demandato all'ampia community in rete.inserire una descrizione del prodotto
   SonarQube effettua le sue analisi attraverso appositi plugin che applicano al codice
   sorgente dei pattern match pre-definiti.inserire il meccanismo d'azione
   ANALISI DEL VALUTATORE SCORE
   Livello di integrazione con i seguenti prodotti

.. _interno-36:

.. _interno-36:

INTERNO
-------

Linee guida per l'adozione di un ciclo di sviluppo software sicuro -
D01.Fase1.SP2 Draft2 04/12/2017 EQ4A56036T05 Rev. 0.1

::

   Pag. 117 of 121

.. _interno-37:

.. _interno-37:

INTERNO
-------

::

   a. IDEs Si integra tramite il plugin SonarLint con Eclipse, Visual Studio,
   IntelliJ. SonarLint è uno strumento che analizza il codice dal punto
   di vista della qualità, ma è possile utilizzarlo in collegamento con
   SonarQube, per sfruttare le regole di sicurezza di quest'ultimo.

.. _section-23:

.. _section-23:

8
~

::

   b. source repository, Si integra, tramite plugin, a Git, Svn, CVS, TFVC, Jazz RTC,
   ClearCase

.. _section-24:

.. _section-24:

8
~

::

   c. build server,
   d. bug tracking tools
   SonarQube comprende la gestione completa dei bug
   riscontrati (tracciamento incluso)

.. _section-25:

.. _section-25:

8
~

::

   Le tipologie di applicazione
   supportate (Web, Mobile,
   Client-Server...)
   Web, Mobile Android 8
   I linguaggi di
   programmazione supportati
   ABAP, C/C++, C#, COBOL, Flex, Groovy, HTML, Java, JavaScript,
   JSP, JSF, Objective-C, PHP, PL/I, PL/SQL, Python, RPG, Swift,
   VB.NET, Visual Basic 6, XML

.. _section-26:

.. _section-26:

10
~~

::

   I framework applicativi
   supportati (es. Spring,
   Hibernate, ...)
   Gli Standard supportati
   (OWASP Top 10, SANS 25, ...)
   SonarQube comprende fra le sue rules CWE, SANS TOP 25 e
   OWASP TOP 10

.. _section-27:

.. _section-27:

10
~~

::

   Le vulnerabilità riconosciute
   (Sql injection, Cross-site
   scripting, Code injection...)
   Le SQL Injection non sono state individuate (2 falsi negativi). L’XSS
   (di tipo reflected) non è stato individuato (1 falso negativo) così
   come non sono stati individuati i 2 problemi relativi a “Cookie
   without the secure flag” (2 falsi negativi).

.. _section-28:

.. _section-28:

10
~~

::

   L’integrazione di “Custom
   rules”
   SonarQube offre la possibilità di creare delle regole
   personalizzate, attraverso dei custom templates

.. _section-29:

.. _section-29:

10
~~

::

   Possibilita' di inibire la
   segnalazione di particolari
   vulnerabilita'
   Il tool consente di "sopprimere" la segnalazione di una particolare
   vulnerabilità in maniera agevole

.. _section-30:

.. _section-30:

9
~

::

   L’incidenza dei “Falsi
   positivi”
   Coloro che scoprono un falso positivo possono segnalarlo alla
   Community. Per questo motivo l'incidenza dei falsi positivi è
   tenuta bassa.

.. _section-31:

.. _section-31:

7
~

::

   La capacità di analisi “raw
   source code” vs “need to
   compile”
   SonarQube fa le sue valutazioni su bytecode, per cui presuppone
   un rebuild del codice modificato
   Need
   to
   Compil
   e
   La capacità di analizzare le
   dipendenze da librerie
   esterne al fine di controllare
   se sono presenti
   vulnerabilità note
   Non dispone di questa funzionalità 1

.. _interno-38:

.. _interno-38:

INTERNO
-------

Linee guida per l'adozione di un ciclo di sviluppo software sicuro -
D01.Fase1.SP2 Draft2 04/12/2017 EQ4A56036T05 Rev. 0.1

::

   Pag. 118 of 121

.. _interno-39:

.. _interno-39:

INTERNO
-------

::

   La capacità di correlare lo
   scan statico con l’esito di
   uno scan dinamico
   (correlazione White Box con
   Black Box)
   LE PERFORMANCE
   a. Full scan vs Incremental scan Il prodotto è in grado di effettuare entrambe le tipologie di
   scan del codice

.. _section-32:

.. _section-32:

8
~

::

   b. Client-side scan vs Server-side
   scan
   Il prodotto consente di effettuare scan sia lato server, sia
   lato client

.. _section-33:

.. _section-33:

8
~

::

   Supporto alla Remediation SonarQube offre la possibilità di organizzare e seguire la
   fase di correzione dei bugs

.. _section-34:

.. _section-34:

9
~

::

   Funzionalità di prioritizzazione
   delle Remediation
   SonarQube classifica i bugs in base all'urgenza con la quale
   debbono essere corretti

.. _section-35:

.. _section-35:

8
~

::

   La facilità d’uso Il prodotto è piuttosto facile da installare e assolutamente
   intuitivo da utilizzare

.. _section-36:

.. _section-36:

7
~

::

   I costi di licenza SonarQube è Open Source, con licenza GNU Lesser GPL
   License, Version 3, quindi non comporta alcun costo di
   licenza
   free
   Il supporto alla reportistica Si realizza tramite plugin open source o commerciali. La
   dashboard e l'interfaccia web costituiscono, di per sé, una
   valida reportistica

.. _section-37:

.. _section-37:

7
~

.. _considerazioni-finali-del-valutatore-1:

.. _considerazioni-finali-del-valutatore-1:

CONSIDERAZIONI FINALI DEL VALUTATORE
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

::

   Riguardo a XSS, SonarQube non implementa nessuna regola per l’individuazione di XSS, quindi il falso
   negativo è atteso a priori.
   Riguardo a SQL Injection: SonarQube implementa la regola “S2077 SQL binding mechanisms should be
   used” per l’individuazione di SQL Injection. Eseguendo ulteriori prove, atte ad introdurre nel codice altri
   pattern di SQL Injection, si è osservato che la regola funziona segnalando le ulteriori vulnerabilità.
   Riguardo alla problematica "Cookie without the secure flag" SonarQube implementa la regola “S2092
   Cookies should be secure” per l’individuazione di tali cookie. Tale regola tuttavia non ha individuato le 2
   vulnerabilità presenti nel benchmark.
   Nonostante queste attuali carenze, SonarQube rimane una scelta da considerare, nell'analisi statica, sia
   pure affiancandolo ad altri strumenti che colmano le lacune sopra citate. È infatti uno strumento
   completo, dall'interfaccia moderna e user-friendly, gratuito e aperto alla collaborazione di una grande e
   attiva community.
   SonarQube, tramite plugin, si integra con i più importanti ambienti di sviluppo per consentire quello che
   viene definito "continuous inspection" del codice.
   Un’altra caratteristica che rende SonarQube molto interessante è la sua capacità, attraverso altri plugin,
   di poter analizzare il codice scritto in un’ampia gamma di linguaggi, compresi quelli di Microsoft.
   Altro punto a favore di SonarQube è la gestione dei bug rinvenuti, classificati per priorità e tracciabili; è
   possibile infatti pianificare e seguire la fase di remediation, con una valutazione del tempo richiesto e
   l’assegnazione dei task ai vari sviluppatori.
   user-friendly e soprattutto gratuito e aperto alla collaborazione di una grande e attiva community.
   Il tool, tramite plugin, si integra con i più importanti ambienti di sviluppo per consentire quello che viene
   definito un “continuous inspection” del codice.
   Un’altra caratteristica he rende SonarQube molto interessante è la sua capacità, attraverso, appositi

.. _interno-40:

.. _interno-40:

INTERNO
-------

Linee guida per l'adozione di un ciclo di sviluppo software sicuro -
D01.Fase1.SP2 Draft2 04/12/2017 EQ4A56036T05 Rev. 0.1

::

   Pag. 119 of 121

.. _interno-41:

.. _interno-41:

INTERNO
-------

::

   plugin, di poter analizzare il codice scritto in un’ampia gamma di linguaggi, compresi quelli di Microsoft.
   Altro punto a favore di SonarQube è la gestione dei bug rinvenuti, classificati per priorità; è possibile
   infatti pianificare e seguire la fase di remediation, con una valutazione del tempo richiesto e
   l’assegnazione dei task ai vari sviluppatori.
   Per contro, il tool non fa l’analisi delle vulnerabilità delle librerie che vengono utilizzate nel codice. Per
   questo scopo si possono utilizzare tool appositi, quali l’open source.friendly. Il punto di forza del tool è
   rappresenta
   TEAM DI VALUTAZIONE Leonardo Software Security
   team

.. _interno-42:

.. _interno-42:

INTERNO
-------

Linee guida per l'adozione di un ciclo di sviluppo software sicuro -
D01.Fase1.SP2 Draft2 04/12/2017 EQ4A56036T05 Rev. 0.1

::

   Pag. 120 of 121

.. _interno-43:

.. _interno-43:

INTERNO
-------
