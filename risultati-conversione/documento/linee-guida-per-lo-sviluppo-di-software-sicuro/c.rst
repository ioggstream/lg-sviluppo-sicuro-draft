.. _c:

7.6 C
=====

C# è un linguaggio di programmazione orientato agli oggetti sviluppato
da Microsoft all'interno dell'iniziativa .NET, e successivamente
approvato come standard della Ecma (ECMA-334) e ISO (norma ISO/IEC
23270). La sintassi e struttura del C# prendono spunto da vari linguaggi
nati precedentemente, in particolare Delphi, C++ e Java. Il risultato è
un linguaggio con meno simbolismo rispetto a C++, meno elelementi
decorativi rispetto a Java, ma comunque orientato agli oggetti in modo
nativo e adatto allo sviluppo di una vasta gamma di software. Vengono di
seguito analizzate le principali vulnerabilità e relative contromisure
da adottare.

.. _cross-site-scripting-xss-5:

.. _cross-site-scripting-xss-5:

7.6.1 Cross-site scripting (XSS)………………………………………………………………………………………………………………
--------------------------------------------------------------------------

**Come riconoscerla**

::

    Reflected XSS All Clients, UTF7 XSS - puo' utilizzare anche strumenti di tipo "Social engineering" per
   carpire informazioni dagli utenti web tramite tecniche di bassa tecnologia sviluppate da
   malintenzionati per ottenere informazioni personali. Ad esempio possono essere simulate pagine
   quasi identiche ad altri siti di largo utilizzo per ottenere informazioni riservate.
    Stored XSS. Attraverso questa vulnerabilità un utente malintenzionato potrebbe intercettare lo
   scambio di informazioni sensibili tra un'applicazione e i database relativi allo storage delle
   informazioni stesse. Quando un altro utente accede successivamente a questi dati, le pagine web
   possono essere riscritte e possono essere attivati script dannosi. La vulnerabilità è dovuta all'uso di
   dati prelevati da database in modo arbitrario, senza che prima queste informazioni vengano
   codificate in un formato sicuro. L'applicazione crea pagine web che includono i dati dal database
   dell'applicazione. I dati vengono incorporati direttamente nell'HTML della pagina, in modo che il
   browser visualizzerà queste informazioni come parte della pagina web. Questi dati possono essere
   originati da un altro utente. Se i dati includono frammenti HTML o Javascript, l’utente non sarà in
   grado di sapere che questa non è la pagina da lui voluta bensì un’altra pagina modificata in modo
   fraudolento. La vulnerabilità è il risultato di incorporare dati di database arbitrari, senza prima
   averli codificati in un formato che impedisca al browser di trattare queste informazioni come HTML
   anziché come testo normale.

**Come difendersi**

::

    Validare tutti gli input, indipendentemente dalla sorgente. Per la validazione, si conisglia
   l’approccio whitelist (sono accettati solo i dati che adottano una struttura specificata nella
   whitelist, scartando quelli che non la rispettano). Controllare:
   o Data type;
   o Size;
   o Range;
   o Format;
   o Expected values;
    Codificare completamente tutti i dati dinamici prima di incorporare queste informazioni nell'output
   desiderato.
    La codifica dovrebbe essere context-sensitive. Ad esempio:
   o Codifica HTML per pagine HTML
   o Attributi HTML codificati per gli output dei dati relativi
   o Codifica JavaScript per server-generated JavaScript
    Si consiglia di utilizzare la libreria di codifica ESAPI o le funzioni di libreria sistema incorporate.
    Nell'intestazione di risposta Content-Type HTTP, definire esplicitamente la codifica dei caratteri
   (charset) per l'intera pagina
    Impostare la flag httpOnly sul cookie della sessione, per impedire che eventuali tentativi di tecniche
   fraudolente di XSS possano venire in possesso del cookie stesso

Per ulteriori informazioni si veda:
http://cwe.mitre.org/data/definitions/79.html, CWE-79: Improper
Neutralization of Input During Web Page Generation (‘Cross-site
Scripting’).

.. _code-injection-2:

.. _code-injection-2:

7.6.2 Code Injection
--------------------

**Come riconoscerla**

Un utente malintenzionato potrebbe eseguire codice arbitrario nell'host
del server di applicazioni. A seconda delle autorizzazioni
dell'applicazione che potrebbero essere carpite, si potrebbero avere le
seguenti problematiche:  Alterazione dei privilegi sulla manipolazione
di File (read / create / modify / delete)  Modifiche della struttura
del sito web  Permettere delle connessioni di rete non autorizzate
verso il server da parte dell'attaccante  Permettere ad utenti
malintenzionati la gestione dei servizi con possibili Start and stop dei
servizi di sistema  Acquisizione completa del server da parte
dell'attaccante.

**Come difendersi**

::

    Se possibile, preferite sempre delle whitelist prefissate e riutilizzare l'input anziché una blacklist
    Evitare qualsiasi compilazione dinamica, esecuzione o valutazione del codice. Se è necessario
   eseguire l'esecuzione dinamica, eseguire tutto il codice dinamico in una sandbox isolata, ad
   esempio AppDomain di .NET o bloccare un thread isolato
    L'applicazione non deve compilare, eseguire o valutare i dati non attendibili, in particolare
   eventuale input dell'utente
    Validare tutti gli input, indipendentemente dalla sorgente. La convalida dovrebbe essere basata su
   una whitelist: dovrebbero essere accettati solo i dati che adattano a una struttura specificata, e
   scartati i dati che non rientrono in questa categoria. I parametri devono essere limitati a un set di
   caratteri consentito e l'ingresso non valido deve essere eliminato. Oltre ai caratteri, verificare:
   o Data type;
   o Size;
   o Range;
   o Format;
   o Expected values;
    Nel caso fosse assolutamente necessario includere i dati di input in una esecuzione dinamica,
   applicare una validazione dell'input molto rigida. Ad esempio, accettare solo interi tra determinati
   valori
    Configurare l'applicazione da eseguire utilizzando un account utente limitato che non disponga di
   privilegi non necessari all'applicativo stesso
    Se possibile, isolare tutta l'esecuzione dinamica per utilizzare un account utente separato e
   dedicato che abbia privilegi solo per le operazioni e i file specifici utilizzati dall'applicazione, in base
   al principio denominato "Principle of Least Privilege". Il principio stabilisce che agli utenti venga
   attribuito il più basso livello di “diritti” che possano detenere rimanendo comunque in grado di
   compiere il proprio lavoro.

Per ulteriori informazioni si veda:
http://cwe.mitre.org/data/definitions/94.html Improper Control of
Generation of Code (‘Code Injection’) CWE-94

.. _command-injection-3:

.. _command-injection-3:

7.6.3 Command Injection
-----------------------

**Come riconscerla**

Tramite questa vulnerabilità un aggressore potrebbe eseguire comandi di
sistema arbitrari sull'host del server dell'applicazione. In base alle
autorizzazioni dell'applicazione che potrebbero essere carpite, queste
potrebbero includere:  Alterazione dei privilegi sulla manipolazione di
File (read / create / modify / delete)  Permettere delle connessioni di
rete non autorizzate verso il server da parte dell'attaccante 
Permettere ad utenti malintenzionati la gestione dei servizi con
possibili Start and stop dei servizi di sistema  Acquisizione completa
del server da parte dell'attaccante Attraverso questa vulnerabilità
l'applicazione viene portata ad eseguire dei comandi voluti dall'utente
malintenzionato piuttosto che eseguire il proprio codice applicativo.
L'operazione spesso viene effettuato concatenando stringhe di input
dell'utente a codice dannoso. Potrebbero così essere eseguiti
direttamente sul server comandi anche molto pericolosi per il sistema o
per la sicurezza dei dati.

**Come difendersi**

::

    Rimodulare il codice per evitare una qualsiasi esecuzione diretta di script di comandi.
   Eventualmente utilizzare API fornite dalle aziende produttrici di software relativo.
    Se è non e' possibile rimuovere l'esecuzione del comando, eseguire solo stringhe statiche che non
   includono l'input dell'utente
    Validare tutti gli input, indipendentemente dalla sorgente. La convalida dovrebbe essere basata su
   una whitelist: dovrebbero essere accettati solo i dati che adattano a una struttura specificata, e
   scartati i dati che non rientrono in questa categoria. I parametri devono essere limitati a un set di
   caratteri consentito e l'ingresso non valido deve essere eliminato. Oltre ai caratteri, verificare:
   o Data type;
   o Size;
   o Range;
   o Format;
   o Expected values;
    Configurare l'applicazione da eseguire utilizzando un account utente limitato che non disponga di
   privilegi non necessari all'applicativo stesso
    Se possibile, isolare tutta l'esecuzione dinamica per utilizzare un account utente separato e
   dedicato che abbia privilegi solo per le operazioni e i file specifici utilizzati dall'applicazione, in base
   al principio denominato "Principle of Least Privilege". Il principio stabilisce che agli utenti venga
   attribuito il più basso livello di “diritti” che possano detenere rimanendo comunque in grado di
   compiere il proprio lavoro

Per ulteriori informazioni si veda:
http://cwe.mitre.org/data/definitions/77.html CWE-77: Improper
Neutralization of Special Elements used in a Command (‘Command
Injection’)

.. _connection-string-injection-3:

.. _connection-string-injection-3:

7.6.4 Connection String Injection
---------------------------------

**Come riconoscerla**

Si tratta della possibilità che venga alterata da un attaccante la
stringa di connessione al database. Un utente malintenzionato potrebbe
manipolare la stringa di connessione dell'applicazione al database
oppure al server. Utilizzando strumenti e modifiche di testo semplici,
l'aggressore potrebbe essere in grado di eseguire una delle seguenti
operazioni:  Danneggiare le performance delle applicazioni (ad esempio
incrementando il valore relativo al MIN POOL SIZE)  Manomettere la
gestione delle connessioni di rete (ad esempio, tramite TRUSTED
CONNECTION)  Dirigere l'applicazione sul database falso dell'attaccante
al posto dell'originario  Scoprire la password dell'account di sistema
nel database (tramite un brute-force attack)

Per comunicare con il proprio database o con un altro server (ad esempio
Active Directory), l'applicazione costruisce dinamicamente una sua
stringa di connessione. Questa stringa di connessione include valori
concatenati inseriti dall'utente per l'autenticazione stessa. Se i
valori immessi dall'utente non sono stati verificati né tantomeno
sanificati, l'input potrebbe essere utilizzato per manipolare malamente
la stringa di connessione.

**Come difendersi**

::

    Validare tutti gli input, indipendentemente dalla sorgente. Per la validazione, si conisglia
   l’approccio whitelist (sono accettati solo i dati che adottano una struttura specificata nella
   whitelist, scartando quelli che non la rispettano). In generale, è necessario controllare:
   o Data type;
   o Size;
   o Range;
   o Format;
   o Expected values;
    Evitare di costruire dinamicamente stringhe di connessione. Se è necessario creare dinamicamente
   una stringa di connessione, cercare di non includere l'input dell'utente. In ogni caso, utilizzare
   utilità basate sulla piattaforma, come SqlConnectionStringBuilder di .NET, o almeno codificare
   l'input validato come il piu' idoneo per la piattaforma utilizzata.

Per ulteriori informazioni si veda:
http://cwe.mitre.org/data/definitions/99.html, CWE-99: Improper Control
of Resource Identifiers (‘Resource Injection’).

.. _ldap-injection-3:

.. _ldap-injection-3:

7.6.5 LDAP Injection
--------------------

**Come riconoscerla**

Questa vulnerabilità (LDAP Injection) riguarda la gestione delle query
di tipo LDAP che vengono effettuate dalle applicazioni e che potrebbero
essere utilizzate in modo improprio da un utente malintenzionato.  Le
operazioni che potrebbero essere eseguite a tal fine sono le seguenti: 
Effettuare il login con un utente diverso da quello inserito dall'utente
 Venire in possesso di privilegi di sistema non autorizzati  Rubare le
informazioni

Per comunicare con il proprio database o con un altro server (ad esempio
Active Directory), l'applicazione costruisce dinamicamente una sua
stringa di connessione. Questa stringa di connessione include valori
concatenati inseriti dall'utente per l'autenticazione stessa. Se i
valori immessi dall'utente non sono stati verificati per la validità del
tipo di dati né successivamente sanificato, l'input potrebbe essere
utilizzato per manipolare malamente la stringa di connessione.

**Come difendersi**

::

    Validare tutti gli input, indipendentemente dalla sorgente. Per la validazione, si conisglia
   l’approccio whitelist (sono accettati solo i dati che adottano una struttura specificata nella
   whitelist, scartando quelli che non la rispettano). Controllare:
   o Data type;
   o Size;
   o Range;
   o Format;
   o Expected values.

Per ulteriori informazioni si veda:
http://cwe.mitre.org/data/definitions/90.html, CWE-90: Improper
Neutralization of Special Elements used in an LDAP Query (‘LDAP
Injection’)

.. _resource-injection-4:

.. _resource-injection-4:

7.6.6 Resource Injection
------------------------

**Come riconoscerla**

Un utente malintenzionato potrebbe aprire una backdoor che potrebbe
permettere all'attaccante di connettersi direttamente al server con
possibili conseguenze molto gravi per la sicurezza. Tramite questa
vulnerabilità un possibile malintenzionato potrebbe utilizzare eventuali
connessioni aperte dall'utente, nel caso non fossero gestite
adeguatamente.

**Come difendersi**

::

    Non consentire a un utente di definire i parametri relativi ai sockets di rete.

Per ulteriori informazioni si veda:
http://cwe.mitre.org/data/definitions/99.html, CWE-99: Improper Control
of Resource Identifiers (‘Resource Injection’).

.. _second-order-sql-injection-4:

.. _second-order-sql-injection-4:

7.6.7 (Second Order) SQL Injection
----------------------------------

**Come riconoscerla**

Tramite questa vulnerabilità un utente malintenzionato potrebbe accedere
direttamente a tutti i dati del sistema. L'attaccante potrebbe rubare
qualsiasi informazione riservata memorizzata dal sistema (ad esempio i
dati personali dell'utente o le carte di credito) e eventualmente
modificare o cancellare i dati esistenti.

L'applicazione comunica con il suo database inviando una query SQL in
formato testo. L'applicazione crea la query semplicemente concatenando
le stringhe tra cui i dati ottenuti dal database. Poiché questi dati
possono essere stati in precedenza ottenuti dall'input dell'utente e non
sono stati verificati la validità del tipo di dati né successivamente
sanificati, i dati potrebbero contenere comandi SQL che verrebbero
interpretati come tali dal database.

**Come difendersi**

::

    Validare tutti gli input, indipendentemente dalla sorgente. La validazione dovrebbe essere basata
   su una whitelist: dovrebbero essere accettati solo i dati che adattano a una struttura specificata,
   scartando quelli che non rispettano la whitelist. Controllare:
   o Data type;
   o Size;
   o Range;
   o Format;
   o Expected values.
    Invece di concatenare le stringhe si consiglia di:
   o Utilizzare componenti di database sicuri come le procedure memorizzate, query parametrizzate
   e le associazioni degli oggetti (per comandi e parametri).
   o Una soluzione ancora migliore è quella di utilizzare una libreria ORM, come EntityFramework,
   Hibernate o iBatis
    Limitare l'accesso agli oggetti e alle funzionalità di database, in base al "Principle of Least Privilege"
   (non fornire diretti agli utenti maggiori di quelli strettamente necessari).

Per ulteriori informazioni si veda:
http://cwe.mitre.org/data/definitions/89.html, CWE-89: Improper
Neutralization of Special Elements used in an SQL Command (‘SQL
Injection’).

.. _xpath-injection-2:

.. _xpath-injection-2:

7.6.8 XPath Injection
---------------------

**Come riconoscerla**

A seconda del tipo di informazioni contenute nel documento XML
interrogato, un utente malintenzionato potrebbe, manipolandole, causare
gravi danni all'utente come il furto di dati non autorizzati oppure la
sostituzione dell'utente stesso. L'applicazione interroga un documento
XML utilizzando una query XPath testuale. L'applicazione crea la query
semplicemente concatenando le stringhe tra cui l'input dell'utente.
Poiché l'input dell'utente non è stato verificato per la validità del
tipo di dati né successivamente sanificato, l'input potrebbe essere
manipolato. In tal modo potrebbe essere possibile avere delle selezioni
finali sbagliate dal documento XML durante l'esecuzione
dell'applicazione.

**Come difendersi**

::

    Validare tutti gli input, indipendentemente dalla sorgente. La validazione dovrebbe essere basata
   su una whitelist (si dovrebbero accettare solo i dati che adattano a una struttura specificata,
   scartando quelli che non rispettano la whitelist). Controllare:
   o Data type;
   o Size;
   o Range;
   o Format;
   o Expected values.
    Evitare che la costruzione della query xpath sia dipendente dalle informazioni inserite dall'utente.
   Possibilmente mappare la query di tipo XPath con i parametri utente mantenendo la separazione
   tra dati e codice. Nel caso fosse necessario includere l'input del'utente nella query, l'input stesso
   dovra' essere precedentemente validato correttamente.

Per ulteriori informazioni si veda:
http://cwe.mitre.org/data/definitions/643.html, CWE-643: Improper
Neutralization of Data within XPath Expressions (‘XPath Injection’).

.. _ulteriori-indicazioni-per-lo-sviluppo-sicuro-3:

.. _ulteriori-indicazioni-per-lo-sviluppo-sicuro-3:

7.6.9 Ulteriori indicazioni per lo sviluppo sicuro
--------------------------------------------------

Di seguito ulteriori suggerimenti per lo sviluppo sicuro in C#.

.. _managed-wrapper-per-limplementazione-del-codice-nativo:

7.6.9.1 Managed Wrapper per l'implementazione del codice nativo ……………………………………………………………………
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Alcune funzionalità utili, vengono implementate nel codice nativo che si
desidera mettere a disposizione del managed code. Managed wrappers è
facile da scrivere tuttavia, i chiamanti dei wrapper devono avere
diritti di unmanaged code per funzionare. Ciò significa che il codice
scaricato da una rete intranet o da Internet non funzionerà con i
wrapper. Piuttosto che dare a tutte le applicazioni che utilizzano
questi wrapper, i diritti di unmanaged code, è meglio dare questi
diritti solo al codice wrapper. Se la funzionalità sottostante non
espone risorse e l'implementazione è altrettanto “sicura”, il wrapper
deve solo affermare i suoi diritti consentendo a qualsiasi codice di
chiamarlo. Quando le risorse sono coinvolte, la codifica di sicurezza
dovrebbe essere la stessa del codice della libreria descritto nella
sezione successiva. Poiché il wrapper sta potenzialmente esponendo i
chiamanti a queste risorse, è necessaria una verifica accurata della
sicurezza del codice nativo che è sotto la responsabilità del wrapper.

.. _library-code-che-espone-risorse-protette:

7.6.9.2 Library Code che espone risorse protette ………………………………………………………………………………………………
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

La libreria funge da interfaccia per altri codici per l'accesso a
determinate risorse che non sono altrimenti disponibili e quindi devono
essere applicate autorizzazioni per l'accesso alle risorse che
utilizzano. In generale, laddove si espone una risorsa (qualunque essa
sia), il codice deve implementare una richiesta di autorizzazione
appropriata alla risorsa (cioè deve eseguire un controllo di
protezione).

.. _richieste-di-autorizzazione-..:

7.6.9.3 Richieste di autorizzazione …………………………………………………………………………………………………………………..
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Evitare di assegnare al codice e permessi speciali: le richieste di
autorizzazione sono il modo principale per rendere il codice sicuro. È
necessario includere richieste di autorizzazione per le applicazioni che
accedono a risorse protette. Tali richieste impongono (per il codice che
chiede l'accesso):  le autorizzazioni minime da ricevere per eseguire
l'operazione;  che riceve solo le autorizzazioni necessarie ai fini
della specifica operazione. Nell'esempio di codice riportato di seguito
viene illustrata una richiesta di autorizzazione di base.
[assembly:FileIOPermissionAttribute(SecurityAction.RequestMinimum,Write=“C:\test.t
mp”)]
[assembly:PermissionSet(SecurityAction.RequestOptional,Unrestricted=false)]

Questo esempio spiega al sistema di protezione di .NET Framework che il
codice non dovrebbe essere eseguito a meno che, non riceva
l'autorizzazione a scrivere a C:  test.tmp. Se il codice incontra sempre
criteri di protezione che non concedono quest'autorizzazione, viene
generata una PolicyException e il codice non viene eseguito. Utilizzando
questa richiesta, puoi essere sicuro che il codice verrà eseguito solo
se viene concesso tale autorizzazione e non dovrai preoccuparti di
errori causati dall'utilizzo di pochissime autorizzazioni. Questo
esempio spiega anche al sistema che non è richiesta alcuna
autorizzazione aggiuntiva. In assenza di questo, il codice sarà
concesso. Mentre le autorizzazioni aggiuntive non causano danni, avere
minori autorizzazioni potrebbe impedire alcuni problemi di sicurezza
imprevisti. Le autorizzazioni di esecuzione che il codice non
necessitano possono portare a problemi di sicurezza. Un altro modo per
limitare le autorizzazioni che il codice riceve con i minimi privilegi è
quello di elencare le autorizzazioni specifiche che si desidera
rifiutare. Le autorizzazioni vengono generalmente rifiutate quando si
chiede che tutte le autorizzazioni siano facoltative e escludono
autorizzazioni specifiche da tale richiesta.

.. _modificatori-.:

7.6.9.4 Modificatori ……………………………………………………………………………………………………………………………………….
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

::

    Securing State Data
   Le applicazioni che gestiscono dati riservati o apportano qualsiasi tipo di decisioni di sicurezza
   necessitano di mantenere tali dati sotto il proprio controllo e non possono consentire ad altri codici
   potenzialmente dannosi di accedere direttamente ai dati. Il modo migliore per proteggere i dati in
   memoria è quello di dichiarare i dati come privati o interni (con portata limitata allo stesso insieme)
   variabili. Tuttavia, anche questi dati sono soggetti all'accesso, dovresti essere a conoscenza delle
   seguenti azioni:
   o utilizzando i meccanismi di riflessione, il codice altamente attendibile che può fare riferimento
   all'oggetto può ottenere e impostare membri privati;
   o utilizzando la serializzazione, il codice altamente attendibile può ottenere e impostare i membri
   privati in modo efficace se può accedere ai dati corrispondenti nella forma serializzata
   dell'oggetto;
   o in debug, questi dati possono essere letti.
   Assicurarsi che nessuno dei propri metodi o proprietà esponga questi valori involontariamente. In
   alcuni casi i dati possono essere dichiarati "protetti", con accesso limitato alla classe ei suoi
   derivati. Tuttavia, è necessario adottare le seguenti ulteriori precauzioni a causa di ulteriori
   esposizioni:
   Controlla quale codice è consentito derivare dalla classe limitandolo allo stesso insieme o
   utilizzando la protezione dichiarativa descritta nel metodo di accesso di sicurezza, per richiedere
   alcune identità o autorizzazioni per ottenere il codice da derivare dalla classe.
   Assicurarsi che tutte le classi derivate attuino una protezione simile o siano sigillate.
    Securing Method Access
   Alcuni metodi potrebbero non essere idonei per consentire di chiamare arbitrariamente il codice
   non attendibile. Tali metodi presentano diversi rischi: il metodo potrebbe fornire alcune
   informazioni limitate; potrebbe non verificare errori sui parametri; o con i parametri sbagliati,
   potrebbe causare malfunzionamenti o fare qualcosa di dannoso. Bisognerebbe essere consapevoli
   di questi casi e agire per proteggere il metodo.
   In alcuni casi, potrebbe essere necessario limitare i metodi che non sono destinati all'utilizzo
   pubblico, ma devono ancora essere pubblici. Ad esempio, potrebbe essere un'interfaccia che deve
   essere chiamata nelle proprie DLL e quindi deve essere pubblica, ma non si desidera esporre
   pubblicamente per impedire ai clienti di utilizzarlo o di impedire che il codice dannoso sfrutti il
   punto di ingresso componente. Un altro motivo comune per limitare un metodo non destinato
   all'uso pubblico (ma che deve essere pubblico) è evitare di documentare e supportare ciò che
   potrebbe essere un'interfaccia molto interna.
   Il codice gestito offre diversi modi per limitare l'accesso al metodo:
   o Limitare l'ambito di accessibilità alle classi, alle assemblee o alle classi derivate, se possono
   essere attendibili. Questo è il modo più semplice per limitare l'accesso al metodo. Si noti che, in
   generale, le classi derivate possono essere meno affidabili della classe da cui derivano, anche se
   in alcuni casi condividono l'identità della classe padre.
   o Limitare l'accesso al metodo ai chiamanti di un'identità specificata - in sostanza, qualsiasi prova
   particolare (nome forte, editore, zona, ecc.) che scegli.
   o Limitare l'accesso al metodo ai chiamanti con qualsiasi autorizzazione selezionata.
    Allo stesso modo, la sicurezza dichiarativa consente di controllare l'ereditarietà delle classi. È
   possibile utilizzare InheritanceDemand per eseguire le seguenti operazioni:
   o richiedere alle classi derivate di avere un'identità specifica o un permesso;
   o richiedere classi derivate che sovrascrivono metodi specifici per avere un'identità specifica o un
   permesso.
   L' esempio seguente mostra come aiutare a proteggere una classe pubblica per un accesso limitato
   richiedendo che i chiamanti siano firmati con un particolare nome forte. Questo esempio utilizza lo
   StrongNameIdentityPermissionAttribute con una Richiesta per il nome forte.
   [StrongNameIdentityPermissionAttribute(SecurityAction.Demand,
   PublicKey="...hex...", Name="App1", Version="0.0.0.0")]
   public class Class1
   {

}  Protezione e campi pubblici di sola lettura Non utilizzare mai campi
pubblici di sola lettura dalle librerie managed in quanto i campi
pubblici di sola lettura possono essere modificati. Alcune classi di
framework .NET includono campi pubblici di sola lettura che contengono
parametri di confine specifici per la piattaforma. Ad esempio, il campo
InvalidPathChars è un array che descrive i caratteri che non sono
consentiti in una stringa del percorso di file. I valori dei campi
pubblici di sola lettura come InvalidPathChars possono essere modificati
dal codice o dal codice che condivide il dominio di applicazione. Se si
utilizzano i campi pubblici in sola lettura, come InvalidPathCharsi, il
codice dannoso può alterare le definizioni dei limiti e utilizzare il
codice in modi inaspettati. Nella versione 2.0 e versioni successive di
.NET Framework, è necessario utilizzare metodi che restituiscono un
nuovo array anziché utilizzare i campi di array pubblici. Ad esempio,
invece di utilizzare il campo InvalidPathChars, è necessario utilizzare
il metodo GetInvalidPathChars. Si noti che i tipi di .NET Framework non
utilizzano i campi pubblici per definire internamente i tipi di confini.
Al contrario, il framework .NET utilizza campi privati separati. La
modifica dei valori di questi campi pubblici non altera il comportamento
dei tipi di .NET Framework.  Esclusione di classi e membri utilizzati
da codice non fidato Utilizzare le dichiarazioni illustrate in questa
sezione per impedire che classi e metodi specifici, nonché proprietà e
eventi, siano utilizzati da un codice parzialmente attendibile.
Applicando queste dichiarazioni a una classe, applica la protezione a
tutti i suoi metodi, proprietà e eventi; tuttavia, si noti che l'accesso
sul campo non è influenzato dalla sicurezza dichiarativa. Si noti
inoltre che le richieste di collegamento aiutano a proteggere solo i
chiamanti immediati e potrebbero essere ancora soggetti a attacchi. In
associazioni con nome forte, un LinkDemand viene applicato a tutti i
metodi, le proprietà e gli eventi accessibili a livello pubblico per
limitarne l'uso a chiamanti affidabili. Per disattivare questa
funzionalità, è necessario applicare l'attributo
AllowPartiallyTrustedCallersAttribute. Pertanto, la selezione esplicita
di classi per escludere i chiamanti non attendibili è necessaria solo
per assemblee non assegnate o assemblee con questo attributo; è
possibile utilizzare queste dichiarazioni per contrassegnare un
sottoinsieme di tipi in esso che non sono destinati a chiamanti non
attendibili. Gli esempi seguenti mostrano come evitare che classi e
membri venga utilizzato da un codice non attendibile: o Per **classi
pubbliche non sealed** :
[System.Security.Permissions.PermissionSetAttribute(
System.Security.Permissions.SecurityAction.InheritanceDemand,
Name=“FullTrust”)] [System.Security.Permissions.PermissionSetAttribute(
System.Security.Permissions.SecurityAction.LinkDemand,
Name=“FullTrust”)] public class CanDeriveFromMe { } o Per **classi
pubbliche sealed** :
[System.Security.Permissions.PermissionSetAttribute(
System.Security.Permissions.SecurityAction.LinkDemand,
Name=“FullTrust”)] public sealed class CannotDeriveFromMe {

.. _section-44:

.. _section-44:

}
^

o Per **classi pubbliche abstract** :
[System.Security.Permissions.PermissionSetAttribute(
System.Security.Permissions.SecurityAction.InheritanceDemand,
Name=“FullTrust”)] [System.Security.Permissions.PermissionSetAttribute(
System.Security.Permissions.SecurityAction.LinkDemand,
Name=“FullTrust”)] public abstract class
CannotCreateInstanceOfMe_CanCastToMe{} o Per **funzioni pubbliche
virtual** : class Base 1 {
[System.Security.Permissions.PermissionSetAttribute(
System.Security.Permissions.SecurityAction.InheritanceDemand,
Name=“FullTrust”)] [System.Security.Permissions.PermissionSetAttribute(
System.Security.Permissions.SecurityAction.LinkDemand,
Name=“FullTrust”)] public virtual void CanOverrideOrCallMe() {} } o Per
**funzioni pubbliche abstract** : abstract class Base2{
[System.Security.Permissions.PermissionSetAttribute(
System.Security.Permissions.SecurityAction.InheritanceDemand, Name =
“FullTrust”)] [System.Security.Permissions.PermissionSetAttribute(
System.Security.Permissions.SecurityAction.LinkDemand, Name =
“FullTrust”)] public abstract void MustOverrideMe(); } o Per **funzioni
di aggiornamento pubblico in cui la classe di base non richiede una
completa fiducia:** class Derived : Base1 {
[System.Security.Permissions.PermissionSetAttribute(
System.Security.Permissions.SecurityAction.Demand, Name=“FullTrust”)]
public override void CanOverrideOrCallMe() { base.CanOverrideOrCallMe();
} } o Per **funzioni di aggiornamento pubblico in cui la classe di base
richiede una completa fiducia** : class Derived : Base1 {
[System.Security.Permissions.PermissionSetAttribute(
System.Security.Permissions.SecurityAction.LinkDemand,
Name=“FullTrust”)] public override void CanOverrideOrCallMe() {
base.CanOverrideOrCallMe(); } } o Per **pubbliche interfacce:** public
interface ICanCastToMe {
[System.Security.Permissions.PermissionSetAttribute(
System.Security.Permissions.SecurityAction.LinkDemand, Name =
“FullTrust”)]

::

   [System.Security.Permissions.PermissionSetAttribute(
   System.Security.Permissions.SecurityAction.InheritanceDemand, Name =
   "FullTrust")]
   void CanImplementMe();
   }
   [System.Security.Permissions.PermissionSetAttribute(
   System.Security.Permissions.SecurityAction.LinkDemand, Name =
   "FullTrust")]
   [System.Security.Permissions.PermissionSetAttribute(
   System.Security.Permissions.SecurityAction.InheritanceDemand, Name =
   "FullTrust")]
   class Implemented : ICanCastToMe
   {
   public void CanImplementMe()
   {
   }
   }

.. _definizione-delle-classi:

7.6.9.5 Definizione delle classi …………………………………………………………………………………………………………………………
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

::

    Evitare l’utilizzo di classi Wrapper
   Il Wrapper Code, specialmente quando il wrapper ha maggiore fiducia rispetto al codice che lo
   utilizza, può aprire un insieme unico di debolezze di sicurezza. Qualsiasi cosa fatta per conto di un
   chiamante, in cui le autorizzazioni limitate del chiamante non sono incluse nel controllo di sicurezza
   appropriato, è una potenziale debolezza da sfruttare.
    Mai abilitare qualcosa attraverso il Wrapper che il chiamante non potrebbe fare su se stesso.
   Questo è un pericolo quando si effettua qualcosa che comporta un controllo di sicurezza limitato.
   Quando i controlli a livello singolo sono coinvolti, l'interposizione del codice di Wrapper tra il
   chiamante reale e l'elemento API in questione può facilmente causare il controllo di sicurezza per
   avere successo se non dovrebbe, quindi indebolire la sicurezza.

.. _user-input-.:

7.6.9.6 User input ………………………………………………………………………………………………………………………………………….
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

I dati utente, qualsiasi tipo di input (dati da una richiesta Web o un
URL, input ai controlli di un'applicazione Microsoft Windows Form e così
via), possono influenzare negativamente il codice perché spesso i dati
vengono utilizzati direttamente come parametri per chiamare altro
codice. Questa situazione è analoga a un codice dannoso che chiama il
codice con parametri strani, e dovrebbero essere prese le stesse
precauzioni. L'input dell'utente è in realtà più difficile da fare in
modo sicuro perché non esiste un fotogramma di stack per tracciare la
presenza dei dati potenzialmente non attendibili. Per cercare questi bug
cercate di immaginare quali siano i valori possibili e valutare se il
codice che visualizza questi dati possa gestire tutti questi casi. È
possibile risolvere questi bug attraverso il controllo della gamma e
rifiutare qualsiasi input che il codice non possa gestire. Alcune
considerazioni importanti che coinvolgono i dati utente includono quanto
segue:  Tutti i dati utente in una risposta del server vengono
eseguiti, sul sito web, dal client. Se il tuo web server prende i dati
utente e li inserisce nella pagina Web restituita, potrebbe includere ad
esempio un tag

.. raw:: html

   <script> e ed essere eseguito;
    il client può richiedere qualsiasi URL;
    Eval(usardata) può fare qualsiasi cosa;
    Fare attenzione ai nomi utente che potrebbero avere più di un formato canonico. Ad esempio, in
   Microsoft Windows 2000, è possibile utilizzare spesso il modulo di nome utente MYDOMAIN \ o il
   modulo username@mydomain.example.com;
    Considera i percorsi ingannevoli o non validi:
   o ..\ , percorsi estremamente lunghi;
   o Uso sconsiderato del carattere (*);


   ```
   o Espansione del token (% token%);
   o Strani forme di percorsi con un significato speciale;
   o Versioni brevi di nomi di file come longfi ~ 1 per longfilename.
   ```
   #### 7.6.9.7 Oggetti ..................................................................................................................................................................

   ```
    Utilizzo di synchronized per la gestione della memoria
   Se un metodo di una classe Dispose non è synchronized, è possibile che il codice di
   cleanup all'interno di Dispose può essere eseguito più di una volta, come illustrato nell'esempio
   seguente.
   void Dispose()
   {
   if( myObj != null )
   {
   Cleanup(myObj);
   myObj = null;
   }
   }
   Poiché questa implementazione di Dispose non è synchronized, è possibile che Cleanup sia
   chiamato da un primo thread e poi un secondo thread prima che _myObj sia impostato su null. Se si
   tratta di un problema di sicurezza dipende da ciò che accade quando viene eseguito il codice di
   Cleanup.
    Un problema importante con l'implementazione unsynchronized Dispose comporta la gestione di
   risorse come i file.
    Lo smaltimento improprio può causare una gestione dell’utilizzo errata, che spesso conduce a
   vulnerabilità di sicurezza.
    In alcune applicazioni, potrebbe essere possibile che altri thread accedano ai membri della classe
   prima che i loro costruttori di classe siano completamente eseguiti. È necessario esaminare tutti i
   costruttori di classe per assicurarsi che non ci siano problemi di protezione o sincronizzare i thread
   se necessario.
   ```
   #### 7.6.9.8 Serializzazione e deserializzazione........................................................................................................................

   Poiché la serializzazione può consentire ad altri codici di visualizzare o modificare i dati di istanza
   dell'oggetto che altrimenti sarebbero inaccessibili, è necessaria una autorizzazione speciale per la
   serializzazione del codice. Sotto policy di default, questa autorizzazione non viene fornita al codice scaricato
   da Internet o intranet; solo il codice sul computer locale è concesso a questa autorizzazione.
   Normalmente, tutti i campi di un'istanza di oggetto vengono serializzati, il che significa che i dati sono
   rappresentati nei dati serializzati per l'istanza. È possibile che il codice possa interpretare il formato per
   determinare i valori dei dati, indipendentemente dall'accessibilità del membro. Analogamente, la
   deserializzazione estrae i dati dalla rappresentazione serializzata e imposta lo stato dell'oggetto
   direttamente, di nuovo indipendentemente dalle regole di accessibilità.
   Qualsiasi oggetto che potrebbe contenere dati sensibili alla sicurezza dovrebbe essere reso non serializable,
   se possibile. Se deve essere serializzabile, cercare di creare campi specifici che contengano dati sensibili non
   serializable. Se questo non può essere fatto, tenere presente che questi dati saranno esposti a qualsiasi
   codice che abbia l'autorizzazione a serializzare e assicurarsi che nessun codice dannoso possa ottenere tale
   autorizzazione.
   L'interfaccia ISerializable è destinata esclusivamente all'infrastruttura di serializzazione. Tuttavia, se non
   protetto, può rilasciare informazioni sensibili. Se si fornisce una serializzazione personalizzata
   implementando ISerializable, assicurarsi di adottare le seguenti precauzioni:
    Il metodo GetObjectData dovrebbe essere protetto in modo esplicito o richiedendo l'autorizzazione
   SecurityPermission con SerializationFormatter specificata o assicurandosi che non venga rilasciata
   alcuna informazione sensibile con l'output del metodo.


   ```
   Per esempio:
   [SecurityPermissionAttribute(SecurityAction.Demand,SerializationFormatter =
   true)]
   public override void GetObjectData(SerializationInfo info,
   StreamingContext context)
   {
   }
    Il costruttore speciale utilizzato per la serializzazione dovrebbe inoltre eseguire una convalida
   completa degli input e dovrebbe essere protetta o privata per proteggere dall'uso improprio da
   codice dannoso. Dovrebbe applicare gli stessi controlli di sicurezza e le autorizzazioni necessarie
   per ottenere un'istanza di tale classe con qualsiasi altro mezzo, ad esempio creando esplicitamente
   la classe o indirettamente creandola attraverso una sorta di factory.
   ```
   ## 7.7 ASP....................................................................................................................................................................

   ASP (Active Server Page) identifica non un linguaggio di programmazione, ma una tecnologia Microsoft, per
   la creazione di pagine web dinamiche attraverso linguaggi di script come VBScript e Microsoft JScript. ASP
   sfrutta non solo la connettività del web server ma, si può interfacciare (attraverso oggetti COM) con tutte le
   risorse disponibili sul server e, in maniea trasparente, sfruttare tecnologie diverse.
   Vengono di seguito analizzate le principali vulnerabilità e relative contromisure da adottare.

   ### 7.7.1 Cross-site scripting (XSS)............................................................................................................................

   **Come riconoscerla**

   ```
    Reflected XSS All Clients, UTF7 XSS. Queste vulnerabilità possono utilizzare anche strumenti di tipo
   "Social engineering" per carpire informazioni dagli utenti web tramite tecniche di bassa tecnologia
   sviluppate da malintenzionati per ottenere informazioni personali. Ad esempio possono essere
   simulate pagine quasi identiche ad altri siti di largo utilizzo per ottenere informazioni riservate.
    Stored XSS. Attraverso questa vulnerabilità un utente malintenzionato potrebbe intercettare lo
   scambio di informazioni sensibili tra un'applicazione e i database relativi allo storage delle
   informazioni stesse. Quando un altro utente accede successivamente a questi dati, le pagine web
   possono essere riscritte e possono essere attivati script dannosi. La vulnerabilità è dovuta all'uso di
   dati prelevati da database in modo arbitrario, senza che prima queste informazioni vengano
   codificate in un formato sicuro. L'applicazione crea pagine web che includono i dati dal database
   dell'applicazione. I dati vengono incorporati direttamente nell'HTML della pagina, in modo che il
   browser visualizzerà queste informazioni come parte della pagina web. Questi dati possono essere
   originati da un altro utente. Se i dati includono frammenti HTML o Javascript, l’utente non sarà in
   grado di sapere che questa non è la pagina da lui voluta bensì un’altra pagina modificata in modo
   fraudolento. La vulnerabilità è il risultato di incorporare dati di database arbitrari, senza prima
   averli codificati in un formato che impedisca al browser di trattare queste informazioni come HTML
   anziché come testo normale.
   ```
   **Come difendersi**

   ```
    Validare tutti gli input, indipendentemente dalla sorgente. La validazione dovrebbe essere basata
   su una whitelist: dovrebbero essere accettati solo i dati che adattano a una struttura specificata,
   scartando quelli che non rispettano la whitelist. Controllare:
   o Data type;
   o Size;
   o Range;
   o Format;
   o Expected values.
   ```

   ```
    Codificare completamente tutti i dati dinamici prima di incorporare queste informazioni nell'output
   desiderato. La codifica dovrebbe essere context-sensitive. Ad esempio:
   o Codifica HTML per pagine HTML;
   o Attributi HTML codificati per gli output dei dati relativi;
   o Codifica JavaScript per server-generated JavaScript.
    Si consiglia di utilizzare la libreria di codifica ESAPI o le funzioni di libreria sistema incorporate.
    Nell'intestazione di risposta Content-Type HTTP, definire esplicitamente la codifica dei caratteri
   (charset) per l'intera pagina.
    Impostare la flag httpOnly sul cookie della sessione, per impedire che eventuali tentativi di tecniche
   fraudolente di XSS possano venire in possesso del cookie stesso.
   ```
   Per ulteriori informazioni si veda: [http://cwe.mitre.org/data/definitions/79.html](http://cwe.mitre.org/data/definitions/79.html) CWE-79: Improper
   Neutralization of Input During Web Page Generation ('Cross-site Scripting')

   ### 7.7.2 Code Injection

   ```
   Come riconoscerla
   ```
   Un utente malintenzionato potrebbe eseguire codice arbitrario nell'host del server di applicazioni. A
   seconda delle autorizzazioni che potrebbero essere carpite, si potrebbero avere le seguenti problematiche:
    Alterazione dei privilegi sulla manipolazione di File (read / create / modify / delete);
    Modifiche della struttura del sito web;
    Connessioni di rete non autorizzate verso il server da parte dell'attaccante;
    Gestione, per gli utenti malintenzionati, dei servizi con possibili Start and stop dei servizi di sistema;
    Acquisizione completa del server da parte dell'attaccante.

   ```
   Come difendersi
    Se possibile, preferite sempre delle whitelist prefissate.
    Evitare qualsiasi compilazione dinamica, esecuzione o valutazione del codice. Se è necessario
   eseguire l'esecuzione dinamica, eseguire tutto il codice dinamico in una sandbox isolata, ad
   esempio AppDomain di .NET o bloccare un thread isolato.
    L'applicazione non deve compilare, eseguire o valutare i dati non attendibili, in particolare
   eventuale input dell'utente (la validazione deve essere sempre fatta lato server).
    Validare tutti gli input, indipendentemente dalla sorgente. La convalida dovrebbe essere basata su
   una whitelist: dovrebbero essere accettati solo i dati che adattano a una struttura specificata, e
   scartati i dati che non rientrono in questa categoria. I parametri devono essere limitati a un set di
   caratteri consentito e l'ingresso non valido deve essere eliminato. Oltre ai caratteri, verificare:
   o Data type;
   o Size;
   o Range;
   o Format;
   o Expected values.
    Nel caso fosse assolutamente necessario includere i dati di input in una esecuzione dinamica,
   applicare una validazione dell'input molto rigida. Ad esempio, accettare solo interi tra determinati
   valori.
    Configurare l'applicazione da eseguire utilizzando un account utente limitato che non disponga di
   privilegi non necessari all'applicativo stesso.
    Se possibile, isolare tutta l'esecuzione dinamica per utilizzare un account utente separato e
   dedicato che abbia privilegi solo per le operazioni e i file specifici utilizzati dall'applicazione, in base
   al principio denominato "Principle of Least Privilege". Il principio stabilisce che agli utenti venga
   ```

   ```
   attribuito il più basso livello di “diritti” che possano detenere rimanendo comunque in grado di
   compiere il proprio lavoro.
   ```
   Per ulteriori informazioni: [http://cwe.mitre.org/data/definitions/94.html](http://cwe.mitre.org/data/definitions/94.html) ,
   Improper Control of Generation of Code ('Code Injection') CWE-94.

   ### 7.7.3 Command Injection

   **Come riconoscerla**

   Tramite questa vulnerabilità un aggressore potrebbe eseguire comandi di sistema arbitrari sull'host del
   server dell’applicazione. Sulle base delle autorizzazioni che potrebbero essere carpite, queste potrebbero
   includere:
    Alterazione dei privilegi sulla manipolazione di File (read / create / modify / delete);
    Connessioni di rete non autorizzate verso il server da parte dell'attaccante
    Gestione, agli utenti malintenzionati, dei servizi con possibili Start and stop dei servizi di sistema.
    Acquisizione completa del server da parte dell'attaccante.

   Attraverso questa vulnerabilità l'applicazione viene portata ad eseguire dei comandi voluti dall'utente
   malintenzionato piuttosto che eseguire il proprio codice applicativo. L'operazione spesso viene effettuato
   concatenando stringhe di input dell'utente a codice dannoso.
   Potrebbero così essere eseguiti direttamente sul server comandi anche molto pericolosi per il sistema o per
   la sicurezza dei dati.

   **Come difendersi**

   ```
    Rimodulare il codice per evitare una qualsiasi esecuzione diretta di script di comandi.
   Eventualmente utilizzare API fornite dalle aziende produttrici di software relativo.
    Nel caso non sia possibile rimuovere l'esecuzione del comando, eseguire solo stringhe statiche che
   non includono l'input dell'utente.
    Validare tutti gli input, indipendentemente dalla sorgente. La convalida dovrebbe essere basata su
   una whitelist: dovrebbero essere accettati solo i dati che adattano a una struttura specificata, e
   scartati i dati che non rientrono in questa categoria. I parametri devono essere limitati a un set di
   caratteri consentito e l'ingresso non valido deve essere eliminato. Oltre ai caratteri, verificare:
   o Data type;
   o Size;
   o Range;
   o Format;
    Expected values.
    Configurare l'applicazione da eseguire utilizzando un account utente limitato che non disponga di
   privilegi non necessari all'applicativo stesso.
    Se possibile, isolare tutta l'esecuzione dinamica per utilizzare un account utente separato e
   dedicato che abbia privilegi solo per le operazioni e i file specifici utilizzati dall'applicazione, in base
   al principio denominato "Principle of Least Privilege". Il principio stabilisce che agli utenti venga
   attribuito il più basso livello di “diritti” che possano detenere rimanendo comunque in grado di
   compiere il proprio lavoro.
   ```
   Per ulteriori informazioni: [http://cwe.mitre.org/data/definitions/77.html,](http://cwe.mitre.org/data/definitions/77.html,)
   CWE-77: Improper Neutralization of Special Elements used in a Command ('Command Injection').


   ### 7.7.4 Connection String Injection

   **Come riconoscerla**

   Un utente malintenzionato potrebbe manipolare la stringa di connessione dell'applicazione al database
   oppure al server. Utilizzando strumenti e modifica di testo semplici, l'aggressore potrebbe essere in grado
   di eseguire una delle seguenti operazioni:
    Danneggiare le performance delle applicazioni (ad esempio incrementando il valore relativo al MIN
   POOL SIZE);
    Manomettere la gestione delle connessioni di rete (ad esempio, tramite TRUSTED CONNECTION);
    Dirigere l'applicazione sul database falso dell'attaccante al posto dell’originario;
    Scoprire la password dell'account di sistema nel database (tramite un brute-force attack).

   Per comunicare con il proprio database o con un altro server (ad esempio Active Directory), l'applicazione
   costruisce dinamicamente una sua stringa di connessione. Questa stringa di connessione include valori
   concatenati inseriti dall'utente per l'autenticazione stessa. Se i valori immessi dall'utente non sono stati
   verificati per la validità del tipo di dati né successivamente sanificato, l'input potrebbe essere utilizzato per
   manipolare malamente la stringa di connessione.

   **Come difendersi**

   ```
    Validare tutti gli input, indipendentemente dalla sorgente. La validazione dovrebbe essere basata
   su una whitelist: dovrebbero essere accettati solo i dati che adattano a una struttura specificata,
   scartando quelli che non rispettano la whitelist. Controllare:
   o Data type;
   o Size;
   o Range;
   o Format;
   o Expected values;
    Evitare di costruire dinamicamente stringhe di connessione. Se è necessario creare dinamicamente
   una stringa di connessione, cercare di non includere l'input dell'utente. In ogni caso, utilizzare
   utilità basate sulla piattaforma, come SqlConnectionStringBuilder di .NET, o almeno codificare
   l'input validato come il più idoneo per la piattaforma utilizzata.
   ```
   Per ulteriori informazioni si veda: [http://cwe.mitre.org/data/definitions/99.html,](http://cwe.mitre.org/data/definitions/99.html,)
   CWE-99: Improper Control of Resource Identifiers ('Resource Injection').

   ### 7.7.5 LDAP Injection

   **Come riconoscerla**

   Questa vulnerabilità (LDAP Injection) riguarda la gestione delle query di tipo LDAP che vengono effettuate
   dalle applicazioni e che potrebbero essere utilizzate in modo improprio da un utente malintenzionato.
   Le operazioni che potrebbero essere eseguite a tal fine sono le seguenti:
    Effettuare il login con un utente diverso da quello inserito dall'utente;
    Venire in possesso di privilegi di sistema non autorizzati;
    Rubare le informazioni.
   Per comunicare con il proprio database o con un altro server (ad esempio Active Directory), l'applicazione
   costruisce dinamicamente una sua stringa di connessione. Questa stringa di connessione include valori
   concatenati inseriti dall'utente per l'autenticazione stessa. Se i valori immessi dall'utente non sono stati
   verificati per la validità del tipo di dati né successivamente sanificato, l'input potrebbe essere utilizzato per
   manipolare malamente la stringa di connessione.


   **Come difendersi**

   ```
    Validare tutti gli input, indipendentemente dalla sorgente. La validazione dovrebbe essere basata
   su una whitelist: dovrebbero essere accettati solo i dati che adattano a una struttura specificata,
   scartando quelli che non rispettano la whitelist.
   ```
   Per ulteriori informazioni: [http://cwe.mitre.org/data/definitions/90.html,](http://cwe.mitre.org/data/definitions/90.html,)
   CWE-90: Improper Neutralization of Special Elements used in an LDAP Query ('LDAP Injection').

   ### 7.7.6 XPath Injection

   **Come riconoscerla**

   A seconda del tipo di informazioni contenute nel documento XML interrogato, un utente malintenzionato
   potrebbe, manipolandole, causare gravi danni all'utente come il furto di dati non autorizzati oppure la
   sostituzione dell'utente stesso.
   L'applicazione interroga un documento XML utilizzando una query XPath testuale. L'applicazione crea la
   query semplicemente concatenando le stringhe tra cui l’input dell'utente. Se l’input dell'utente non è stato
   sottoposto a verifica di validità del tipo di dati e neppure successivamente sanificato, l'input potrebbe
   essere manipolato ( si potrebbero avere delle selezioni finali sbagliate dal documento XML durante
   l'esecuzione dell'applicazione).

   **Come difendersi**

   ```
    Validare tutti gli input, indipendentemente dalla sorgente. La validazione dovrebbe essere basata
   su una whitelist: dovrebbero essere accettati solo i dati che adattano a una struttura specificata,
   scartando quelli che non rispettano la whitelist. Controllare:
   o Data type;
   o Size;
   o Range;
   o Format;
   o Expected values.
    Evitare che la costruzione della query xpath sia dipendente dalle informazioni inserite dall'utente.
   Possibilmente mappare la query di tipo XPath con i parametri utente mantenendo la separazione
   tra dati e codice. Nel caso fosse necessario includere l’input del'utente nella query, l'input stesso
   dovrà essere precedentemente validato correttamente.
   Esempio di forma corretta:
   L'applicazione utilizza una stringa inserita dall'utente per costruire una query XPath:
   from sys import stdin
   import xpath
   print 'Insert item number: '
   userInput = stdin.readline()
   xpath.find('//item' + userInput, doc)
   ```
   ```
   La stringa inserita dall'utente viene trasformata in un numero intero prima dell'uso nella query
   XPath:
   from sys import stdin
   import xpath
   print 'Insert item number: '
   userInput = stdin.readline()
   xpath.find('//item' + str(int(userInput)), doc)
   ```
   Per ulteriori informazioni si veda: [http://cwe.mitre.org/data/definitions/643.html,](http://cwe.mitre.org/data/definitions/643.html,)


   CWE-643: Improper Neutralization of Data within XPath Expressions ('XPath Injection').

   ### 7.7.7 Resource Injection

   **Come riconoscerla**

   Un utente malintenzionato potrebbe aprire una backdoor che potrebbe permettere all'attaccante di
   connettersi direttamente al server con possibili conseguenze molto gravi per la sicurezza.
   Tramite questa vulnerabilità un possibile malintenzionato potrebbe utilizzare eventuali connessioni aperte
   dall'utente, nel caso non fossero gestite adeguatamente.

   **Come difendersi**

   Non consentire a un utente di definire i parametri relativi ai sockets di rete.

   Per ulteriori informazioni si veda: [http://cwe.mitre.org/data/definitions/99.html,](http://cwe.mitre.org/data/definitions/99.html,)
   CWE-99: Improper Control of Resource Identifiers ('Resource Injection').

   ### 7.7.8 SQL Injection

   **Come riconoscerla**

   Un utente malintenzionato potrebbe accedere direttamente a tutti i dati del sistema. Utilizzando strumenti
   e modifica di testo semplici, l'aggressore potrebbe rubare qualsiasi informazione riservata memorizzata dal
   sistema (ad esempio i dati personali dell'utente o le carte di credito) e eventualmente modificare o
   cancellare i dati esistenti.
   L'applicazione comunica con il suo database inviando una query SQL in formato testo. L'applicazione crea la
   query semplicemente concatenando le stringhe tra cui i dati ottenuti dal database. Poiché questi dati
   possono essere stati precedentemente ottenuti dall'input dell'utente; se non è stata verificata la validità del
   tipo di dati e successivamente, l’input non è stato sanificato, i dati potrebbero contenere comandi SQL che
   verrebbero interpretati come tali dal database.

   **Come difendersi**

   ```
    Validare tutti gli input, indipendentemente dalla sorgente. La validazione dovrebbe essere basata
   su una whitelist: dovrebbero essere accettati solo i dati che adattano a una struttura specificata,
   scartando quelli che non rispettano la whitelist. Controllare:
   o Data type;
   o Size;
   o Range;
   o Format;
   o Expected values;
    Invece di concatenare le stringhe si consiglia di:
   o Utilizzare componenti di database sicuri come le procedure memorizzate, query parametrizzate
   e le associazioni degli oggetti (per comandi e parametri).
   o Una soluzione ancora migliore è quella di utilizzare una libreria ORM, come EntityFramework,
   Hibernate o iBatis
    Limitare l'accesso agli oggetti e alle funzionalità di database, in base al "Principle of Least Privilege"
   (non fornire diretti agli utenti maggiori di quelli strettamente necessari).
   ```
   Per ulteriori informazioni si veda: [http://cwe.mitre.org/data/definitions/89.html,](http://cwe.mitre.org/data/definitions/89.html,)
   CWE-89: Improper Neutralization of Special Elements used in an SQL Command ('SQL Injection').


   ## 7.8 ASP.NET

   ASP.NET è un insieme di tecnologie di sviluppo di software per il web, commercializzate da Microsoft.
   Utilizzando queste tecnologie gli sviluppatori possono realizzare applicazioni Web e servizi Web (Web
   Service). Sebbene il nome ASP.NET derivi da ASP (Active Server Pages), la vecchia tecnologia per lo sviluppo
   web di Microsoft, esistono sostanziali differenze fra le due. Infatti ASP.NET si basa, come tutte le
   applicazioni della famiglia Microsoft .NET, sul CLR (Common Language Runtime).

   Vengono di seguito analizzate le principali vulnerabilità e relative contromisure da adottare.

   ### 7.8.1 Cross-site scripting (XSS)............................................................................................................................

   **Come riconoscerla**

   ```
    Reflected XSS All Clients. Questa vulnerabilità possono utilizzare anche strumenti di tipo "Social
   engineering" per carpire informazioni dagli utenti web tramite tecniche di bassa tecnologia
   sviluppate da malintenzionati per ottenere informazioni personali. Ad esempio possono essere
   simulate pagine quasi identiche ad altri siti di largo utilizzo per ottenere informazioni riservate.
    Stored XSS. Attraverso questa vulnerabilità un utente malintenzionato potrebbe intercettare lo
   scambio di informazioni sensibili tra un'applicazione e i database relativi allo storage delle
   informazioni stesse. Quando un altro utente accede successivamente a questi dati, le pagine web
   possono essere riscritte e possono essere attivati script dannosi. La vulnerabilità è dovuta all'uso di
   dati prelevati da database in modo arbitrario, senza che prima queste informazioni vengano
   codificate in un formato sicuro. L'applicazione crea pagine web che includono i dati dal database
   dell'applicazione. I dati vengono incorporati direttamente nell'HTML della pagina, in modo che il
   browser visualizzerà queste informazioni come parte della pagina web. Questi dati possono essere
   originati da un altro utente. Se i dati includono frammenti HTML o Javascript, l’utente non sarà in
   grado di sapere che questa non è la pagina da lui voluta bensì un’altra pagina modificata in modo
   fraudolento. La vulnerabilità è il risultato di incorporare dati di database arbitrari, senza prima
   averli codificati in un formato che impedisca al browser di trattare queste informazioni come HTML
   anziché come testo normale.
    UTF7 XSS. Questa vulnerabilità può utilizzare anche strumenti di tipo "Social engineering" per
   carpire informazioni dagli utenti web tramite tecniche di bassa tecnologia sviluppate da
   malintenzionati per ottenere informazioni personali. Ad esempio possono essere simulate pagine
   quasi identiche ad altri siti di largo utilizzo per ottenere informazioni riservate.
   ```
   **Come difendersi**

   ```
    Validare tutti gli input, indipendentemente dalla sorgente. La validazione dovrebbe essere basata
   su una whitelist: dovrebbero essere accettati solo i dati che adattano a una struttura specificata,
   scartando quelli che non rispettano la whitelist. Controllare:
   o Data type;
   o Size;
   o Range;
   o Format;
   o Expected values;
    La validazione non è un sostituto per la codifica. E' necessario ai fini della sicurezza codificare
   completamente tutti i dati dinamici, indipendentemente dalla sorgente, prima di incorporare
   queste informazioni in un output. La codifica dovrebbe essere sensibile al contesto. Per esempio:
   o Codifica HTML per pagine HTML
   o Attributi HTML codificati per gli output dei dati relativi
   o Codifica JavaScript per server-generated JavaScript
    Si consiglia di utilizzare la libreria di codifica ESAPI o le funzioni di libreria sistema incorporate.
   ```

   ```
    Nell'intestazione di risposta Content-Type HTTP, definire esplicitamente la codifica dei caratteri
   (charset) per l'intera pagina
    Impostare la flag httpOnly sul cookie della sessione, per impedire che eventuali tentativi di tecniche
   fraudolente di XSS possano venire in possesso del cookie stesso
   ```
   Per ulteriori informazioni si veda: [http://cwe.mitre.org/data/definitions/79.html,](http://cwe.mitre.org/data/definitions/79.html,)
   CWE-79: Improper Neutralization of Input During Web Page Generation ('Cross-site Scripting').

   ### 7.8.2 Code Injection

   **Come riconoscerla**

   Un utente malintenzionato potrebbe eseguire codice arbitrario nell'host del server di applicazioni. A
   seconda delle autorizzazioni dell'applicazione che potrebbero essere carpite, si potrebbero avere le
   seguenti problematiche:
    Alterazione dei privilegi sulla manipolazione di File (read / create / modify / delete);
    Modifiche della struttura del sito web;
    Permettere delle connessioni di rete non autorizzate verso il server da parte dell'attaccante,
    Permettere ad utenti malintenzionati la gestione dei servizi con possibili Start and stop dei servizi di
   sistema,
    Acquisizione completa del server da parte dell'attaccante.

   **Come difendersi**

   ```
    Se possibile, preferite sempre delle whitelist con valori prefissati. Evitare qualsiasi compilazione
   dinamica, esecuzione o valutazione del codice. Se è necessario eseguire tutto il codice dinamico in
   una sandbox isolata, ad esempio AppDomain di .NET o bloccare un thread isolato.
    L'applicazione non deve compilare, eseguire o valutare i dati non attendibili, in particolare
   eventuale input dell'utente. Validare tutti gli input, indipendentemente dalla sorgente. La convalida
   dovrebbe essere basata su una whitelist: dovrebbero essere accettati solo i dati che adattano a una
   struttura specificata, e scartati i dati che non rientrono in questa categoria. I parametri devono
   essere limitati a un set di caratteri consentito e l'ingresso non valido deve essere eliminato. Oltre ai
   caratteri, verificare:
   o Data type;
   o Size;
   o Range;
   o Format;
   o Expected values.
    Nel caso fosse assolutamente necessario includere i dati di input in un’esecuzione dinamica,
   applicare una validazione dell'input molto rigida. Ad esempio, accettare solo interi tra determinati
   valori.
    Configurare l'applicazione da eseguire utilizzando un account utente limitato che non disponga di
   privilegi non necessari all'applicativo stesso.
    Se possibile, isolare tutta l'esecuzione dinamica per utilizzare un account utente separato e
   dedicato che abbia privilegi solo per le operazioni e i file specifici utilizzati dall'applicazione, in base
   al principio denominato "Principle of Least Privilege". Il principio stabilisce che agli utenti venga
   attribuito il più basso livello di “diritti” che possano detenere rimanendo comunque in grado di
   compiere il proprio lavoro.
   ```
   Per ulteriori informazioni si veda: [http://cwe.mitre.org/data/definitions/94.html,](http://cwe.mitre.org/data/definitions/94.html,)
   Improper Control of Generation of Code ('Code Injection') CWE-94.


   ### 7.8.3 Command Injection

   **Come riconoscerla**

   Tramite questa vulnerabilità un aggressore potrebbe eseguire comandi di sistema arbitrari sull'host del
   server dell’applicazione. Sulle base delle autorizzazioni che potrebbero essere carpite, queste potrebbero
   includere:
    Alterazione dei privilegi sulla manipolazione di File (read / create / modify / delete);
    Connessioni di rete non autorizzate verso il server da parte dell'attaccante
    Gestione, agli utenti malintenzionati, dei servizi con possibili Start and stop dei servizi di sistema.
    Acquisizione completa del server da parte dell'attaccante.

   Attraverso questa vulnerabilità l'applicazione viene portata ad eseguire dei comandi voluti dall'utente
   malintenzionato piuttosto che eseguire il proprio codice applicativo. L'operazione spesso viene effettuato
   concatenando stringhe di input dell'utente a codice dannoso.
   Potrebbero così essere eseguiti direttamente sul server comandi anche molto pericolosi per il sistema o per
   la sicurezza dei dati.

   **Come difendersi**

   ```
    Rimodulare il codice per evitare una qualsiasi esecuzione diretta di script di comandi.
   Eventualmente utilizzare API fornite dalle aziende produttrici di software relativo.
    Nel caso non sia possibile rimuovere l'esecuzione del comando, eseguire solo stringhe statiche che
   non includono l'input dell'utente.
    Validare tutti gli input, indipendentemente dalla sorgente. La convalida dovrebbe essere basata su
   una whitelist: dovrebbero essere accettati solo i dati che adattano a una struttura specificata, e
   scartati i dati che non rientrono in questa categoria. I parametri devono essere limitati a un set di
   caratteri consentito e l'ingresso non valido deve essere eliminato. Oltre ai caratteri, verificare:
   o Data type;
   o Size;
   o Range;
   o Format;
   o Expected values.
    Configurare l'applicazione da eseguire utilizzando un account utente limitato che non disponga di
   privilegi non necessari all'applicativo stesso.
    Se possibile, isolare tutta l'esecuzione dinamica per utilizzare un account utente separato e
   dedicato che abbia privilegi solo per le operazioni e i file specifici utilizzati dall'applicazione, in base
   al principio denominato "Principle of Least Privilege". Il principio stabilisce che agli utenti venga
   attribuito il più basso livello di “diritti” che possano detenere rimanendo comunque in grado di
   compiere il proprio lavoro.
   ```
   Per ulteriori informazioni: [http://cwe.mitre.org/data/definitions/77.html,](http://cwe.mitre.org/data/definitions/77.html,)
   CWE-77: Improper Neutralization of Special Elements used in a Command ('Command Injection').

   ### 7.8.4 Connection String Injection

   **Come riconoscerla**

   Un utente malintenzionato potrebbe manipolare la stringa di connessione dell'applicazione al database
   oppure al server. Utilizzando strumenti e modifica di testo semplici, l'aggressore potrebbe essere in grado
   di eseguire una delle seguenti operazioni:
   Danneggiare le performance delle applicazioni (ad esempio incrementando il valore relativo al MIN POOL
   SIZE)


   ```
    Manomettere la gestione delle connessioni di rete (ad esempio, tramite TRUSTED CONNECTION)
    Dirigere l'applicazione sul database falso dell'attaccante al posto dell’originario
    Scoprire la password dell'account di sistema nel database (tramite un brute-force attack)
   ```
   Per comunicare con il proprio database o con un altro server (ad esempio Active Directory), l'applicazione
   costruisce dinamicamente una sua stringa di connessione. Questa stringa di connessione include valori
   concatenati inseriti dall'utente per l'autenticazione stessa. Se i valori immessi dall'utente non sono stati
   verificati per la validità del tipo di dati né successivamente sanificato, l'input potrebbe essere utilizzato per
   manipolare malamente la stringa di connessione.

   **Come difendersi**

   ```
    Validare tutti gli input, indipendentemente dalla sorgente. La validazione dovrebbe essere basata
   su una whitelist: dovrebbero essere accettati solo i dati che adattano a una struttura specificata,
   scartando quelli che non rispettano la whitelist. Controllare:
   o Data type;
   o Size;
   o Range;
   o Format;
   o Expected values.
    Evitare di costruire dinamicamente stringhe di connessione. Se è necessario creare dinamicamente
   una stringa di connessione, cercare di non includere l'input dell'utente. In ogni caso, utilizzare
   utilità basate sulla piattaforma, come SqlConnectionStringBuilder di .NET, o almeno codificare
   l'input validato come il più idoneo per la piattaforma utilizzata.
   ```
   Per ulteriori informazioni: [http://cwe.mitre.org/data/definitions/99.html,](http://cwe.mitre.org/data/definitions/99.html,)
   CWE-99: Improper Control of Resource Identifiers ('Resource Injection').

   ### 7.8.5 LDAP Injection

   **Come riconoscerla**

   Questa vulnerabilità (LDAP Injection) riguarda la gestione delle query di tipo LDAP che vengono effettuate
   dalle applicazioni e che potrebbero essere utilizzate in modo improprio da un utente malintenzionato.
   Le operazioni che potrebbero essere eseguite a tal fine sono le seguenti:
    Effettuare il login con un utente diverso da quello inserito dall'utente
    Venire in possesso di privilegi di sistema non autorizzati
    Rubare le informazioni
   Per comunicare con il proprio database o con un altro server (ad esempio Active Directory), l'applicazione
   costruisce dinamicamente una sua stringa di connessione. Questa stringa di connessione include valori
   concatenati inseriti dall'utente per l'autenticazione stessa. Se i valori immessi dall'utente non sono stati
   verificati per la validità del tipo di dati né successivamente sanificato, l'input potrebbe essere utilizzato per
   manipolare malamente la stringa di connessione.

   **Come difendersi**

   Validare tutti gli input, indipendentemente dalla sorgente. La validazione dovrebbe essere basata su una
   whitelist: dovrebbero essere accettati solo i dati che adattano a una struttura specificata, scartando quelli
   che non rispettano la whitelist. Controllare:
    Data type;
    Size;
    Range;


   ```
    Format;
    Expected values;
   ```
   Per ulteriori informazioni: [http://cwe.mitre.org/data/definitions/90.html,](http://cwe.mitre.org/data/definitions/90.html,)
   CWE-90: Improper Neutralization of Special Elements used in an LDAP Query ('LDAP Injection').

   ### 7.8.6 Resource Injection

   **Come riconoscerla**

   Un utente malintenzionato potrebbe aprire una backdoor che potrebbe permettere all'attaccante di
   connettersi direttamente al server con possibili conseguenze molto gravi per la sicurezza.
   Tramite questa vulnerabilità un possibile malintenzionato potrebbe utilizzare eventuali connessioni aperte
   dall'utente, nel caso non fossero gestite adeguatamente.

   **Come difendersi**

   ```
    Non consentire a un utente di definire i parametri relativi ai sockets di rete.
   ```
   Per ulteriori informazioni si veda: [http://cwe.mitre.org/data/definitions/99.html,](http://cwe.mitre.org/data/definitions/99.html,)
   CWE-99: Improper Control of Resource Identifiers ('Resource Injection').

   ### 7.8.7 SQL Injection

   **Come riconoscerla**

   Un utente malintenzionato potrebbe accedere direttamente a tutti i dati del sistema. Utilizzando strumenti
   e modifica di testo semplici, l'aggressore potrebbe rubare qualsiasi informazione riservata memorizzata dal
   sistema (ad esempio i dati personali dell'utente o le carte di credito) ed eventualmente modificare o
   cancellare i dati esistenti.
   L'applicazione comunica con il suo database inviando una query SQL in formato testo. L'applicazione crea la
   query semplicemente concatenando le stringhe tra cui i dati ottenuti dal database. Poiché questi dati
   potrebbero essere stati precedentemente ottenuti dall'input dell'utente, se non ne è stata verificata la
   validità del tipo di dati e, successivamente, non è stato sanificato; i dati potrebbero contenere comandi SQL
   che verrebbero interpretati come tali dal database.

   **Come difendersi**

   ```
    Validare tutti gli input, indipendentemente dalla sorgente. La validazione dovrebbe essere basata
   su una whitelist: dovrebbero essere accettati solo i dati che adattano a una struttura specificata,
   scartando quelli che non rispettano la whitelist. Controllare:
   o Data type;
   o Size;
   o Range;
   o Format;
   o Expected values;
    Invece di concatenare le stringhe si consiglia di:
   o Utilizzare componenti di database sicuri come le procedure memorizzate, query parametrizzate
   e le associazioni degli oggetti (per comandi e parametri).
   o Una soluzione ancora migliore è quella di utilizzare una libreria ORM, come EntityFramework,
   Hibernate o iBatis
    Limitare l'accesso agli oggetti e alle funzionalità di database, in base al "Principle of Least Privilege"
   -non fornire diretti agli utenti maggiori di quelli strettamente necessari-.
   ```

   Per ulteriori informazioni si veda: [http://cwe.mitre.org/data/definitions/89.html,](http://cwe.mitre.org/data/definitions/89.html,)
   CWE-89: Improper Neutralization of Special Elements used in an SQL Command ('SQL Injection').

   ### 7.8.8 Xpath Injection

   **Come riconoscerla**

   A seconda del tipo di informazioni contenute nel documento XML interrogato, un utente malintenzionato
   potrebbe, manipolandole, causare gravi danni all'utente come il furto di dati non autorizzati oppure la
   sostituzione dell'utente stesso.
   L'applicazione interroga un documento XML utilizzando una query XPath testuale. L'applicazione crea la
   query semplicemente concatenando le stringhe tra cui l'input dell'utente. Poiché l'input dell'utente non è
   stato verificato per la validità del tipo di dati né successivamente sanificato, l'input potrebbe essere
   manipolato.
   In tal modo potrebbe essere possibile avere delle selezioni finali sbagliate dal documento XML durante
   l'esecuzione dell'applicazione.

   **Come difendersi**

   ```
    Validare tutti gli input, indipendentemente dalla sorgente. La validazione dovrebbe essere basata
   su una whitelist: dovrebbero essere accettati solo i dati che adattano a una struttura specificata,
   scartando quelli che non rispettano la whitelist. Controllare:
   o Data type;
   o Size;
   o Range;
   o Format;
   o Expected values;
    Evitare che la costruzione della query xpath sia dipendente dalle informazioni inserite dall'utente.
   Possibilmente mappare la query di tipo XPath con i parametri utente mantenendo la separazione
   tra dati e codice. Nel caso fosse necessario includere l'input del'utente nella query, l'input stesso
   dovra' essere precedentemente validato correttamente.
   ```
   Per ulteriori informazioni si veda: [http://cwe.mitre.org/data/definitions/643.html,](http://cwe.mitre.org/data/definitions/643.html,)
   CWE-643: Improper Neutralization of Data within XPath Expressions ('XPath Injection').

   ### 7.8.9 Ulteriori indicazioni per lo sviluppo sicuro

   #### 7.8.9.1 ASP.NET Web Form ..............................................................................................................................................

   Web form è una tecnologia basata su ASP.NET di Microsoft, in cui il codice eseguito sul server genera
   dinamicamente l'output di pagina Web al browser o al dispositivo client. E’ uno dei quattro modelli
   (assieme a ASP.NET MVC, ASP.NET Web Pages, ASP.NET Single Page Applications) di programmazione che
   possono essere utilizzati per la creazione di applicazioni web ASP.NET.
   E’ compatibile con qualsiasi browser, dispositivo mobile o linguaggio supportato da .NET ed è flessibile in
   quanto offre la possibilità di aggiungere controlli creati dall'utente e terze parti.
   Segue un elenco di best practices per lo sviluppo sicuro:
    **Concatenazione di stringhe** : Utilizzare StringBuilder. Nella concatenazione delle stringhe, l’uso di
   StringBuilder è preferibile rispetto a String.Concat o all'utilizzo dell'operatore '+'. Più nel dettaglio,
   StringBuilder è più performante nella concatenazione di un numero elevato di stringhe (>=3),
   mentre ha prestazioni equiparate a String.Concat per un minor numero (<3) di stringhe.
    **Ajax UpdatePanel** : Evitare chiamate superflue al server. Controllare Page.IsPostBack al caricamento
   della pagina per assicurarsi che la logica di inizializzazione della pagina venga eseguita quando una


   pagina viene caricata la prima volta e non in risposta ai postback dei client. Per le convalide, devono
   essere utilizzati script lato client.
    **ViewState e HiddenFields** : Mantenere i dati minimi in ViewState. ViewState è valido solo per il
   postback delle stesse pagine: i dati vengono trasmessi al client e restituiti in un campo nascosto.
   Disattiva ViewState a PageLevel utilizzando EnableViewState.
    **Sessione** : Variabili di sessione
   o Non dovrebbero esistere più di 20 variabili di sessione nel contesto applicativo.
   o Tenere TimeOut di sessione.
   o Disattivare lo stato della sessione, se non si utilizza in una particolare pagina / applicazione.
    **Reindirizzare** : Server.Trasfer vs Response.Redirect. Utilizza Server.Transfer per reindirizzare alle
   pagine della stessa applicazione e Response.Redirect per reindirizzare verso una pagina esterna o
   quando è necessario avviare un nuovo contesto.
    **DataReader** : Utilizzare DataReader per il binding dei dati. Se l'applicazione non richiede la
   memorizzazione nella cache, è possibile utilizzare DataReader.
    Utilizzare DataReader per recuperare i dati e caricarli in un DataSet. Non passare questo DataSet
   tra i diversi livelli. Passare entità personalizzate tra i diversi livelli.
    **Resource** : Chiusura delle risorse. Una delle problematiche più comuni ai programmatori è la
   sistematica chiusura delle risorse e/o connessioni aperte. Capita spesso, infatti, che per errori e/o
   eccezioni impreviste non gestite al meglio, alcune risorse rimangano in attesa di una chiusura che
   non arriverà mai. Per cui, chiudere le connessioni quando non in uso, migliora la sicurezza e le
   prestazioni. Prevedere meccanismi di chiusura automatica delle risorse (attraverso un gestore che
   viene eseguito ad ogni uscito dal blocco).
    **Inizialiazzazione delle variabili**. Inizializzare la variabile @ start e usarla in una fase successiva
   provoca molte operazioni PUSH / POP. Quindi, inizializzare le variabili al momento/posto giusto. Le
   variabili intere non devono essere inizializzate a zero perché vengono inizializzate
   automaticamente. Le variabili stringhe invece, devono essere inizializzate esplicitamente.
    **Richiesta http** : Utilizzare Fiddler. Utilizza Fiddler per intercettare le richieste HTTP e per sapere
   quale richiesta richiede più tempo. Individua anche le eccezioni causate durante ogni richiesta
   HTTP.
    **URL** : Rewriting URL. Per gli URL che dispongono di informazioni riservate, è consigliabile
   implementare URL Rewriters. Gli URL devono essere coerenti.
    **Settings** : Application settings.
   o Fissare un valore per la Content-Length. Questo impone la connessione aperta per un tempo
   limitato (prestabilito) e la chiusura automatica della stessa quando viene superato il limite
   temporale dichiarato.
   o Crittografare le stringhe di connessione sul server.
   o Assicurarsi che tutte le DLL di riferimento siano presenti nel GAC.
   o Disattivare il tracciamento e il debug. Set <retail = "true" /> nel file machine.config - obbliga il
   debug a essere falso, disattiva la traccia di output e reindirizza alla pagina di errore
   personalizzata piuttosto che alla pagina di errore effettiva.
    **Web services** : Impedire il sovraccarico dei servizi web
   o Impedire il sovraccarico dei servizi web tramite attacchi DoS (Denial of Service):
   o Controllare se si tratta di una prima visita o la visita ripetuta per la stessa funzione dal
   medesimo IP.
   o Utilizzare connessioni SQL attendibili nei servizi Web.
   o Assicurarsi che ci siano chiamate asincrone ai servizi web.
    **Eccezioni** : Gestire le eccezioni
   o Registrare le eccezioni e visualizzare il messaggio appropriato all'utente. Definire una classe
   base MyException. La classe deve definire:
   o Informazioni utili per l’utente: Cosa è successo; Cosa è stato colpito; Quali sono le azioni da
   intraprendere; Altre iInformazioni di supporto.


   ```
   o Informazioni utili per la registrazione dell’eccezione: Nome del server, Istanza id, ID utente,
   Stack di chiamata, Nome Assemblea & Versione, Fonte, tipo e messaggio di eccezione, Redirect
   secondo il livello di errore, Livello di applicazione (Cattura errori in global.asax nella funzione
   Application_Error), Livello di pagina (Utilizza la funzione Page_Error per registrare gli errori).
   ```
   #### 7.8.9.2 ASP.NET MVC ........................................................................................................................................................

   Asp.net MVC è una parte del framework .net che permette di creare siti scalabili suddividendo la logica di
   programmazione in base al metodo Model-View-Controller. Segue un elenco di best practices per lo
   sviluppo sicuro:
    Isolate Controllers. Isolare i controllers dalle dipendenze da HttpContext, dalle classi di accesso ai
   dati, dalla configurazione, dalla registrazione, ecc. L'isolamento può essere ottenuto creando classi
   di wrapper e utilizzando un contenitore IOC.
    Utilizzare IoC Container per gestire tutte le dipendenze esterne. Di seguito sono riportati alcuni dei
   contenitori / framework: Ninject, autofac, structureMap, Unity block, Castle Windor.
    Creare ViewModel per ogni View. Creare un ViewModel specifico per ogni visualizzazione. Il ruolo
   del ViewModel dovrebbe interessare solo il binding di dati e non dovrebbe contenere alcuna logica.
    Utilizzare HtmlHelper. Per generare view html utilizzare HtmlHelper. Se l'attuale HtmlHelper non è
   sufficiente estenderlo utilizzando i metodi di estensione. Questo manterrà la progettazione
   controllata.
    Decorare action methods con verbi appropriati come Get o Post, se applicabile.
    Utilizzare OutputCache attribute.
    Decorare gli action methods più utilizzati con OutputCache attribute.
    Controller e Domain logic. Cercare di separare il controller dal dominio logico. Il controller deve
   essere responsabile solo delle seguenti funzioni:
   o convalidare l'input;
   o ottenere i dati relativi alla view dal modello;
   o ritornare la view appropriata o reindirizzare ad un altro metodo di azione appropriato.
    Utilizzare il modello Post-Redirect-Get. Il modello PRG viene utilizzato per evitare l'avvio del
   browser classico quando si aggiorna una pagina dopo il POST. Ogni volta che fai una richiesta POST,
   una volta completata la richiesta, effettua un reindirizzamento. In questo modo, quando l'utente
   aggiorna la pagina, verrà eseguita l'ultima richiesta GET piuttosto che il POST. Questo consente di
   evitare problemi di usabilità non necessari e impedisce che la richiesta iniziale venga eseguita due
   volte evitando così possibili problemi di duplicazione.
    View e presentation logic: l a View non deve contenere presentation logic. Non ci dovrebbe essere
   alcuna logica di dominio nelle viste. Le viste devono essere solo, responsabili della visualizzazione
   dei dati. Per esempio se un pulsante "Elimina" deve essere visualizzato solo dall’utente con ruolo
   "Amministratore", ciò dovrebbe essere estratto in un helper HTML.

   ## 7.9 PHP

   Segue un elenco delle principali vulnerabilità e contromisure da adottare.

   ### 7.9.1 Cross-site scripting (XSS)............................................................................................................................

   **Come riconoscerla**

   ```
    Reflected XSS All Clients. Questa vulnerabilità possono utilizzare anche strumenti di tipo "Social
   engineering" per carpire informazioni dagli utenti web tramite tecniche di bassa tecnologia
   sviluppate da malintenzionati per ottenere informazioni personali. Ad esempio possono essere
   simulate pagine quasi identiche ad altri siti di largo utilizzo per ottenere informazioni riservate.
   ```

   ```
    Stored XSS. Attraverso questa vulnerabilità un utente malintenzionato potrebbe intercettare lo
   scambio di informazioni sensibili tra un'applicazione e i database relativi allo storage delle
   informazioni stesse. Quando un altro utente accede successivamente a questi dati, le pagine web
   possono essere riscritte e possono essere attivati script dannosi. La vulnerabilità è dovuta all'uso di
   dati prelevati da database in modo arbitrario, senza che prima queste informazioni vengano
   codificate in un formato sicuro. L'applicazione crea pagine web che includono i dati dal database
   dell'applicazione. I dati vengono incorporati direttamente nell'HTML della pagina, in modo che il
   browser visualizzerà queste informazioni come parte della pagina web. Questi dati possono essere
   originati da un altro utente. Se i dati includono frammenti HTML o Javascript, l’utente non sarà in
   grado di sapere che questa non è la pagina da lui voluta bensì un’altra pagina modificata in modo
   fraudolento. La vulnerabilità è il risultato di incorporare dati di database arbitrari, senza prima
   averli codificati in un formato che impedisca al browser di trattare queste informazioni come HTML
   anziché come testo normale.
   ```
   **Come difendersi**

   ```
    Validare tutti gli input, indipendentemente dalla sorgente. La validazione dovrebbe essere basata
   su una whitelist: dovrebbero essere accettati solo i dati che adattano a una struttura specificata,
   scartando quelli che non rispettano la whitelist. Controllare:
   o Data type;
   o Size;
   o Range;
   o Format;
   o Expected values;
    Codificare completamente tutti i dati dinamici prima di incorporare queste informazioni nell'output
   desiderato.
    La codifica dovrebbe essere context-sensitive. Ad esempio:
   o Codifica HTML per pagine HTML;
   o Attributi HTML codificati per gli output dei dati relativi;
   o Codifica JavaScript per server-generated JavaScript.
    Si consiglia di utilizzare la libreria di codifica ESAPI o le funzioni di libreria sistema incorporate.
    Nell'intestazione di risposta Content-Type HTTP, definire esplicitamente la codifica dei caratteri
   (charset) per l'intera pagina
    Impostare la flag httpOnly sul cookie della sessione, per impedire che eventuali tentativi di tecniche
   fraudolente di XSS possano venire in possesso del cookie stesso
   ```
   Per ulteriori informazioni si veda: [http://cwe.mitre.org/data/definitions/79.html,](http://cwe.mitre.org/data/definitions/79.html,)
   CWE-79: Improper Neutralization of Input During Web Page Generation ('Cross-site Scripting').

   ### 7.9.2 Code Injection

   **Come riconoscerla**

   Un utente malintenzionato potrebbe eseguire codice arbitrario nell'host del server di applicazioni. A
   seconda delle autorizzazioni dell'applicazione che potrebbero essere carpite, si potrebbero avere le
   seguenti problematiche:
    Alterazione dei privilegi sulla manipolazione di File (read / create / modify / delete);
    Modifiche della struttura del sito web;
    Permettere delle connessioni di rete non autorizzate verso il server da parte dell'attaccante,
    Permettere ad utenti malintenzionati la gestione dei servizi con possibili Start and stop dei servizi di
   sistema,
    Acquisizione completa del server da parte dell'attaccante.


   **Come difendersi**

   ```
    Se possibile, preferite sempre delle whitelist con valori prefissati. Evitare qualsiasi compilazione
   dinamica, esecuzione o valutazione del codice. Se è necessario eseguire tutto il codice dinamico in
   una sandbox isolata, ad esempio AppDomain di .N ET o bloccare un thread isolato.
    L'applicazione non deve compilare, eseguire o valutare i dati non attendibili, in particolare
   eventuale input dell'utente. Validare tutti gli input, indipendentemente dalla sorgente. La convalida
   dovrebbe essere basata su una whitelist: dovrebbero essere accettati solo i dati che adattano a una
   struttura specificata, e scartati i dati che non rientrono in questa categoria. I parametri devono
   essere limitati a un set di caratteri consentito e l'ingresso non valido deve essere eliminato. Oltre ai
   caratteri, verificare:
   o Data type;
   o Size;
   o Range;
   o Format;
   o Expected values.
    Nel caso fosse assolutamente necessario includere i dati di input in un’esecuzione dinamica,
   applicare una validazione dell'input molto rigida. Ad esempio, accettare solo interi tra determinati
   valori.
    Configurare l'applicazione da eseguire utilizzando un account utente limitato che non disponga di
   privilegi non necessari all'applicativo stesso.
    Se possibile, isolare tutta l'esecuzione dinamica per utilizzare un account utente separato e
   dedicato che abbia privilegi solo per le operazioni e i file specifici utilizzati dall'applicazione, in base
   al principio denominato "Principle of Least Privilege". Il principio stabilisce che agli utenti venga
   attribuito il più basso livello di “diritti” che possano detenere rimanendo comunque in grado di
   compiere il proprio lavoro.
   ```
   Per ulteriori informazioni si veda: [http://cwe.mitre.org/data/definitions/94.html,](http://cwe.mitre.org/data/definitions/94.html,)
   Improper Control of Generation of Code ('Code Injection') CWE-94.

   ### 7.9.3 Command Injection

   **Come riconoscerla**

   Tramite questa vulnerabilità un aggressore potrebbe eseguire comandi di sistema arbitrari sull'host del
   server dell’applicazione. In base alle autorizzazioni dell'applicazione che potrebbero essere carpite, queste
   potrebbero includere:
    Alterazione dei privilegi sulla manipolazione di File (read / create / modify / delete);
    Permettere delle connessioni di rete non autorizzate verso il server da parte dell'attaccante;
    Permettere ad utenti malintenzionati la gestione dei servizi con possibili Start and stop dei servizi di
   sistema;
    Acquisizione completa del server da parte dell'attaccante.
   Attraverso questa vulnerabilità l'applicazione viene portata ad eseguire dei comandi voluti dall'utente
   malintenzionato piuttosto che eseguire il proprio codice applicativo. L'operazione spesso viene effettuato
   concatenando stringhe di input dell'utente a codice dannoso.
   Potrebbero così essere eseguiti direttamente sul server comandi anche molto pericolosi per il sistema o per
   la sicurezza dei dati.

   **Come difendersi**


   ```
    Rimodulare il codice per evitare una qualsiasi esecuzione diretta di script di comandi.
   Eventualmente utilizzare API fornite dalle aziende produttrici di software relativo.
    Se non è possibile rimuovere l'esecuzione del comando, eseguire solo stringhe statiche che non
   includono l'input dell'utente.
    Validare tutti gli input, indipendentemente dalla sorgente. La convalida dovrebbe essere basata su
   una whitelist: dovrebbero essere accettati solo i dati che adattano a una struttura specificata, e
   scartati i dati che non rientrono in questa categoria. I parametri devono essere limitati a un set di
   caratteri consentito e l'ingresso non valido deve essere eliminato. Oltre ai caratteri, verificare:
   o Data type;
   o Size;
   o Range;
   o Format;
   o Expected values.
    Configurare l'applicazione da eseguire utilizzando un account utente limitato che non disponga di
   privilegi non necessari all'applicativo stesso.
    Se possibile, isolare tutta l'esecuzione dinamica per utilizzare un account utente separato e
   dedicato che abbia privilegi solo per le operazioni e i file specifici utilizzati dall'applicazione, in base
   al principio denominato "Principle of Least Privilege". Il principio stabilisce che agli utenti venga
   attribuito il più basso livello di “diritti” che possano detenere rimanendo comunque in grado di
   compiere il proprio lavoro.
   ```
   Per ulteriori informazioni: [http://cwe.mitre.org/data/definitions/77.html,](http://cwe.mitre.org/data/definitions/77.html,)
   CWE-77: Improper Neutralization of Special Elements used in a Command ('Command Injection').

   ### 7.9.4 File Disclosure

   ```
   Come riconoscerla
   ```
   Questa vulnerabilità (indicata con il nome esteso di “Files or Directories Accessible to External Parties”) ha
   come conseguenza la possibilità che file o directory siano accessibili ad utenti esterni malintenzionati.
   La problematica legata alla vulnerability di tipo "File Disclosure" è complessa, con diversi stakeholder (come
   parti coinvolte) che includono venditori, fornitori di sicurezza IT, ricercatori indipendenti, media, utenti
   malintenzionati, governi e, in ultima analisi, il pubblico in generale. Questi stakeholder hanno spesso
   interessi concorrenti, che si traducono in un lavoro di gestione della problematica impegnativo.

   ```
   Come difendersi
   ```
   Al fine di prevenire questa vulnerabilità è opportuno intervenire sui seguenti punti:
    analizzare attentamente la situazione di tutti i file e i path relativi che possono essere oggetto di
   attacco sul file system del server;
    individuare gli eventuali punti deboli individuati dall'analisi effettuata nel punto precedente;
    individuare delle buone prassi da attuare sempre in merito alle difese di file sensibili;
    proporre raccomandazioni per eventuali miglioramenti al di affrontare al meglio possibili attacchi e
   migliorare l'adozione di buone prassi come indicato nel punto precedente.

   Per ulteriori informazioni si veda: [http://cwe.mitre.org/data/definitions/552.html,](http://cwe.mitre.org/data/definitions/552.html,)
   CWE- 552: Files or Directories Accessible to External Parties.

   #### 7.9.5 Remote File Inclusion

   **Come riconoscerla**


   Un utente malintenzionato potrebbe tramite questa vulnerabilità avere accesso alle librerie di sistema
   presenti sul server. Se non protette potrebbero essere attaccate librerie di sistema installate sul server (ad
   esempio tramite un attacco da effettuare durante la fase di caricamento delle librerie stesse) rendendo il
   sistema completamente sotto controllo dell'utente malintenzionato.
   L'applicazione utilizza i dati non attendibili ricevuti tramite l'input dell'utente per caricare dinamicamente la
   libreria, senza una corretta sanitizzazione. Il framework malevolo caricherà qualsiasi codice arbitrario
   specificato dall'applicazione, e potrebbe anche scaricare file di codice remoto ospitati su un server esterno,
   se specificato. Il codice caricato verrà quindi eseguito come se fosse un software di sistema rendendo il
   sistema estremamente vulnerabile.

   **Come difendersi**

   ```
    Non caricare in modo dinamico le librerie relative a codice software, in particolare basate sull'input
   non controllato dell'utente.
    Nel caso fosse necessario utilizzare dati utente non attendibili per selezionare la libreria da
   caricare, verificare che l'input corrisponda a un insieme predefinito di nomi rigidamente indicati in
   una "white list" o comunque selezionare esclusivamente da elenchi di nomi controllati
   relativamente a possibili librerie software.
   ```
   ```
   Esempio
   o Forma non corretta (con lettura dinamica di una libreria indicate in modo arbitrario da un
   utente):
   var qs = require('querystring');
   var server = http.createServer( function (request, response) {
   var libName = qs.parse(request.url).libName;
   if ( typeof libName != "undefined") {
   var dynamicLib = require(libName);
   }
   }
   o Forma corretta tramite “whitelist”:
   var qs = require('querystring');
   var server = http.createServer( function (request, response) {
   var libName = qs.parse(request.url).libName;
   var dynamicLib;
   if ( typeof libName != "undefined") {
   if (libName == 'user')
   dynamicLib = require('userLib');
   else if (libName == 'special')
   dynamicLib = require('specialUserLib');
   else
   dynamicLib = require('anonymousLib');
   }
   }
   ```
   Per ulteriori informazioni si veda: [http://cwe.mitre.org/data/definitions/98.html,](http://cwe.mitre.org/data/definitions/98.html,)
   CWE-98: Improper Control of Filename for Include/Require Statement in PHP Program ('PHP Remote File
   Inclusion').

   #### 7.9.6 File Manipulation

   **Come riconoscerla**

   Questa vulnerabilità (indicata con il nome esteso di “Files or Directories Accessible to External Parties”) ha
   come conseguenza la possibilità che file o directory siano accessibili ad utenti esterni malintenzionati.


   E’ una variante della vulnerabilità indicata come File Disclosure con possibile manipolazione di file di
   sistema esistenti sul server attaccato.

   **Come difendersi**

   Rif. File Disclosure

   #### 7.9.7 LDAP Injection

   **Come riconoscerla**

   Questa vulnerabilità (LDAP Injection) riguarda la gestione delle query di tipo LDAP che vengono effettuate
   dalle applicazioni e che potrebbero essere utilizzate in modo improprio da un utente malintenzionato.
   Le operazioni che potrebbero essere eseguite a tal fine sono le seguenti:
    Effettuare il login con un utente diverso da quello inserito dall'utente;
    Venire in possesso di privilegi di sistema non autorizzati;
    Rubare le informazioni.
   Per comunicare con il proprio database o con un altro server (ad esempio Active Directory), l'applicazione
   costruisce dinamicamente una sua stringa di connessione. Questa stringa di connessione include valori
   concatenati inseriti dall'utente per l'autenticazione stessa. Se i valori immessi dall'utente non sono stati
   verificati per la validità del tipo di dati né successivamente sanificato, l'input potrebbe essere utilizzato per
   manipolare malamente la stringa di connessione.

   **Come difendersi**

   ```
    Validare tutti gli input, indipendentemente dalla sorgente. La validazione dovrebbe essere basata
   su una whitelist: dovrebbero essere accettati solo i dati che adattano a una struttura specificata,
   scartando quelli che non rispettano la whitelist. Controllare:
   o Data type;
   o Size;
   o Range;
   o Format;
   o Expected values;
   ```
   Per ulteriori informazioni si veda: [http://cwe.mitre.org/data/definitions/90.html,](http://cwe.mitre.org/data/definitions/90.html,)
   CWE-90: Improper Neutralization of Special Elements used in an LDAP Query ('LDAP Injection').

   #### 7.9.8 Reflected Injection

   **Come riconoscerla**

   L'applicazione utilizza un input esterno di tipo reflection (dinamico con input via web) per selezionare le
   classi o il codice da utilizzare, ma non impedisce sufficientemente un metodo protetto di selezione delle
   classi o di codice che possono risultare non corretti.
   Se l'applicazione utilizza input esterni per determinare quale classe deve essere istanziata o quale metodo
   da invocare, un utente malintenzionato potrebbe fornire valori per selezionare classi o metodi inattesi. Se
   ciò si verifica, l'aggressore potrebbe creare dei flusso di controllo non previsti dallo sviluppatore.
   Questi flussi possono ignorare i controlli di autenticazione o di controllo di accesso o causare la fine
   dell'applicazione in modo inaspettato. Questa situazione diventa uno scenario disastroso se l'attaccante
   può caricare dei file in una posizione che compare nel path di classe dell'applicazione (CWE-427) o
   aggiungere nuove voci nel path di classe dell'applicazione (CWE-426). In una di queste possibili condizioni,
   l'attaccante può utilizzare input esterno di tipo reflection per procurare danni all'applicazione.


   **Come difendersi**

   Per ulteriori informazioni si veda: [http://cwe.mitre.org/data/definitions/470.html,](http://cwe.mitre.org/data/definitions/470.html,)
   Use of Externally-Controlled Input to Select Classes or Code ('Unsafe Reflection').

   #### 7.9.9 SQL Injection

   **Come riconoscerla**

   Un utente malintenzionato potrebbe accedere direttamente a tutti i dati del sistema. Utilizzando strumenti
   e modifica di testo semplici, l'aggressore potrebbe rubare qualsiasi informazione riservata memorizzata dal
   sistema (ad esempio i dati personali dell'utente o le carte di credito) ed eventualmente modificare o
   cancellare i dati esistenti.
   L'applicazione comunica con il suo database inviando una query SQL in formato testo. L'applicazione crea la
   query semplicemente concatenando le stringhe tra cui i dati ottenuti dal database. Poiché questi dati
   potrebbero essere stati precedentemente ottenuti dall'input dell'utente, se non ne è stata verificata la
   validità del tipo di dati e, successivamente, non è stato sanificato; i dati potrebbero contenere comandi SQL
   che verrebbero interpretati come tali dal database.

   **Come difendersi**

   ```
    Validare tutti gli input, indipendentemente dalla sorgente. La validazione dovrebbe essere basata
   su una whitelist: dovrebbero essere accettati solo i dati che adattano a una struttura specificata,
   scartando quelli che non rispettano la whitelist. Controllare:
    Data type;
    Size;
    Range;
    Format;
    Expected values;
    Invece di concatenare le stringhe si consiglia di:
    Utilizzare componenti di database sicuri come le procedure memorizzate, query parametrizzate e
   le associazioni degli oggetti (per comandi e parametri).
    Una soluzione ancora migliore è quella di utilizzare una libreria ORM, come EntityFramework,
   Hibernate o iBatis
    Limitare l'accesso agli oggetti e alle funzionalità di database, in base al "Principle of Least Privilege"
   -non fornire diretti agli utenti maggiori di quelli strettamente necessari-.
   ```
   Per ulteriori informazioni si veda: [http://cwe.mitre.org/data/definitions/89.html,](http://cwe.mitre.org/data/definitions/89.html,)
   CWE-89: Improper Neutralization of Special Elements used in an SQL Command ('SQL Injection').

   #### 7.9.10 Xpath Injection

   **Come riconoscerla**

   A seconda del tipo di informazioni contenute nel documento XML interrogato, un utente malintenzionato
   potrebbe, manipolandole, causare gravi danni all'utente come il furto di dati non autorizzati oppure la
   sostituzione dell'utente stesso.
   L'applicazione interroga un documento XML utilizzando una query XPath testuale. L'applicazione crea la
   query semplicemente concatenando le stringhe tra cui l'input dell'utente. Poiché l'input dell'utente non è
   stato verificato per la validità del tipo di dati né successivamente sanificato, l'input potrebbe essere
   manipolato.
   In tal modo potrebbe essere possibile avere delle selezioni finali sbagliate dal documento XML durante
   l'esecuzione dell'applicazione.

   **Come difendersi**


   ```
    Validare tutti gli input, indipendentemente dalla sorgente. La validazione dovrebbe essere basata
   su una whitelist: dovrebbero essere accettati solo i dati che adattano a una struttura specificata,
   scartando quelli che non rispettano la whitelist. Controllare:
   o Data type;
   o Size;
   o Range;
   o Format;
   o Expected values;
    Evitare che la costruzione della query xpath sia dipendente dalle informazioni inserite dall'utente.
   Possibilmente mappare la query di tipo XPath con i parametri utente mantenendo la separazione
   tra dati e codice. Nel caso fosse necessario includere l'input del'utente nella query, l'input stesso
   dovra' essere precedentemente validato correttamente.
   Esempio - forma corretta:
   L'applicazione utilizza una stringa inserita dall'utente per costruire una query XPath:
   from sys import stdin
   import xpath
   print 'Insert item number: '
   userInput = stdin.readline()
   xpath.find('//item' + userInput, doc)
   ```
   ```
   La stringa inserita dall'utente viene trasformata in un numero intero prima dell'uso nella query
   XPath:
   from sys import stdin
   import xpath
   print 'Insert item number: '
   userInput = stdin.readline()
   xpath.find('//item' + str(int(userInput)), doc)
   ```
   Per ulteriori informazioni si veda: [http://cwe.mitre.org/data/definitions/643.html,](http://cwe.mitre.org/data/definitions/643.html,)
   CWE-643: Improper Neutralization of Data within XPath Expressions ('XPath Injection').

   ### 7.10 VBNET

   Segue un elenco delle principali vulnerabilità e contromisure da adottare.

   #### 7.10.1 Cross-site scripting (XSS)

   ```
   Come riconoscerla
   ```
   ```
    Reflected XSS All Clients, UTF7 XSS. Queste vulnerabilità possono utilizzare anche strumenti di tipo
   "Social engineering" per carpire informazioni dagli utenti web tramite tecniche di bassa tecnologia
   sviluppate da malintenzionati per ottenere informazioni personali. Ad esempio possono essere
   simulate pagine quasi identiche ad altri siti di largo utilizzo per ottenere informazioni riservate.
    Stored XSS. Attraverso questa vulnerabilità un utente malintenzionato potrebbe intercettare lo
   scambio di informazioni sensibili tra un'applicazione e i database relativi allo storage delle
   informazioni stesse. Quando un altro utente accede successivamente a questi dati, le pagine web
   possono essere riscritte e possono essere attivati script dannosi. La vulnerabilità è dovuta all'uso di
   dati prelevati da database in modo arbitrario, senza che prima queste informazioni vengano
   codificate in un formato sicuro. L'applicazione crea pagine web che includono i dati dal database
   dell'applicazione. I dati vengono incorporati direttamente nell'HTML della pagina, in modo che il
   browser visualizzerà queste informazioni come parte della pagina web. Questi dati possono essere
   originati da un altro utente. Se i dati includono frammenti HTML o Javascript, l’utente non sarà in
   grado di sapere che questa non è la pagina da lui voluta bensì un’altra pagina modificata in modo
   ```

   ```
   fraudolento. La vulnerabilità è il risultato di incorporare dati di database arbitrari, senza prima
   averli codificati in un formato che impedisca al browser di trattare queste informazioni come HTML
   anziché come testo normale.
   ```
   **Come difendersi**

   ```
    Validare tutti gli input, indipendentemente dalla sorgente. La validazione dovrebbe essere basata
   su una whitelist: dovrebbero essere accettati solo i dati che adattano a una struttura specificata,
   scartando quelli che non rispettano la whitelist. Controllare:
   o Data type;
   o Size;
   o Range;
   o Format;
   o Expected values;
    La validazione non è un sostituto per la codifica. E' necessario ai fini della sicurezza codificare
   completamente tutti i dati dinamici, indipendentemente dalla sorgente, prima di incorporare
   queste informazioni in un output. La codifica dovrebbe essere sensibile al contesto. Per esempio:
   o Codifica HTML per pagine HTML
   o Attributi HTML codificati per gli output dei dati relativi
   o Codifica JavaScript per server-generated JavaScript
    Si consiglia di utilizzare la libreria di codifica ESAPI o le funzioni di libreria sistema incorporate.
    Nell'intestazione di risposta Content-Type HTTP, definire esplicitamente la codifica dei caratteri
   (charset) per l'intera pagina.
    Impostare la flag httpOnly sul cookie della sessione, per impedire che eventuali tentativi di tecniche
   fraudolente di XSS possano venire in possesso del cookie stesso.
   ```
   Per ulteriori informazioni si veda: [http://cwe.mitre.org/data/definitions/79.html,](http://cwe.mitre.org/data/definitions/79.html,)
   CWE-79: Improper Neutralization of Input During Web Page Generation ('Cross-site Scripting').

   #### 7.10.2 Code Injection

   **Come riconoscerla**

   Un utente malintenzionato potrebbe eseguire codice arbitrario nell'host del server di applicazioni. A
   seconda delle autorizzazioni dell'applicazione che potrebbero essere carpite, si potrebbero avere le
   seguenti problematiche:
    Alterazione dei privilegi sulla manipolazione di File (read / create / modify / delete);
    Modifiche della struttura del sito web;
    Permettere delle connessioni di rete non autorizzate verso il server da parte dell'attaccante;
    Permettere ad utenti malintenzionati la gestione dei servizi con possibili Start and stop dei servizi di
   sistema;
    Acquisizione completa del server da parte dell'attaccante.

   **Come difendersi**

   ```
    Se possibile, preferite sempre delle whitelist prefissate e riutilizzare l'input anziché una blacklist.
    Evitare qualsiasi compilazione dinamica, esecuzione o valutazione del codice. Se è necessario
   eseguire l'esecuzione dinamica, eseguire tutto il codice dinamico in una sandbox isolata, ad
   esempio AppDomain di .NET o bloccare un thread isolato.
    L'applicazione non deve compilare, eseguire o valutare i dati non attendibili, in particolare
   eventuale input dell'utente.
    Validare tutti gli input, indipendentemente dalla sorgente. La convalida dovrebbe essere basata su
   una whitelist: dovrebbero essere accettati solo i dati che adattano a una struttura specificata, e
   ```

   ```
   scartati i dati che non rientrono in questa categoria. I parametri devono essere limitati a un set di
   caratteri consentito e l'ingresso non valido deve essere eliminato. Oltre ai caratteri, verificare:
   o Data type;
   o Size;
   o Range;
   o Format;
   o Expected values;
    Nel caso fosse assolutamente necessario includere i dati di input in una esecuzione dinamica,
   applicare una validazione dell'input molto rigida. Ad esempio, accettare solo interi tra determinati
   valori.
    Configurare l'applicazione da eseguire utilizzando un account utente limitato che non disponga di
   privilegi non necessari all'applicativo stesso.
    Se possibile, isolare tutta l'esecuzione dinamica per utilizzare un account utente separato e
   dedicato che abbia privilegi solo per le operazioni e i file specifici utilizzati dall'applicazione, in base
   al principio denominato "Principle of Least Privilege". Il principio stabilisce che agli utenti venga
   attribuito il più basso livello di “diritti” che possano detenere rimanendo comunque in grado di
   compiere il proprio lavoro.
   ```
   Per ulteriori informazioni si veda: [http://cwe.mitre.org/data/definitions/94.html,](http://cwe.mitre.org/data/definitions/94.html,)
   Improper Control of Generation of Code ('Code Injection') CWE-94.

   #### 7.10.3 Command Injection

   **Come riconoscerla**

   Tramite questa vulnerabilità un aggressore potrebbe eseguire comandi di sistema arbitrari sull'host del
   server dell’applicazione. In base alle autorizzazioni dell'applicazione che potrebbero essere carpite, queste
   potrebbero includere:
    Alterazione dei privilegi sulla manipolazione di File (read / create / modify / delete)
    Permettere delle connessioni di rete non autorizzate verso il server da parte dell'attaccante
    Permettere ad utenti malintenzionati la gestione dei servizi con possibili Start and stop dei servizi di
   sistema
    Acquisizione completa del server da parte dell'attaccante

   Attraverso questa vulnerabilità l'applicazione viene portata ad eseguire dei comandi voluti dall'utente
   malintenzionato piuttosto che eseguire il proprio codice applicativo. L'operazione spesso viene effettuato
   concatenando stringhe di input dell'utente a codice dannoso.
   Potrebbero così essere eseguiti direttamente sul server comandi anche molto pericolosi per il sistema o per
   la sicurezza dei dati.

   **Come difendersi**

   ```
    Rimodulare il codice per evitare una qualsiasi esecuzione diretta di script di comandi.
   Eventualmente utilizzare API fornite dalle aziende produttrici di software relativo.
    Se è non e' possibile rimuovere l'esecuzione del comando, eseguire solo stringhe statiche che non
   includono l'input dell'utente.
    Validare tutti gli input, indipendentemente dalla sorgente. La convalida dovrebbe essere basata su
   una whitelist: dovrebbero essere accettati solo i dati che adattano a una struttura specificata, e
   scartati i dati che non rientrono in questa categoria. I parametri devono essere limitati a un set di
   caratteri consentito e l'ingresso non valido deve essere eliminato. Oltre ai caratteri, verificare:
   o Data type;
   o Size;
   ```

   ```
   o Range;
   o Format;
   o Expected values;
    Configurare l'applicazione da eseguire utilizzando un account utente limitato che non disponga di
   privilegi non necessari all'applicativo stesso.
    Se possibile, isolare tutta l'esecuzione dinamica per utilizzare un account utente separato e
   dedicato che abbia privilegi solo per le operazioni e i file specifici utilizzati dall'applicazione, in base
   al principio denominato "Principle of Least Privilege". Il principio stabilisce che agli utenti venga
   attribuito il più basso livello di “diritti” che possano detenere rimanendo comunque in grado di
   compiere il proprio lavoro.
   ```
   Per ulteriori informazioni: [http://cwe.mitre.org/data/definitions/77.html,](http://cwe.mitre.org/data/definitions/77.html,)
   CWE-77: Improper Neutralization of Special Elements used in a Command ('Command Injection').

   #### 7.10.4 Connection String Injection

   **Come riconoscerla**

   Un utente malintenzionato potrebbe manipolare la stringa di connessione dell'applicazione al database
   oppure al server. Utilizzando strumenti e modifica di testo semplici, l'aggressore potrebbe essere in grado
   di eseguire una delle seguenti operazioni:
    Danneggiare le performance delle applicazioni (ad esempio incrementando il valore relativo al MIN
   POOL SIZE);
    Manomettere la gestione delle connessioni di rete (ad esempio, tramite TRUSTED CONNECTION)
    Dirigere l'applicazione sul database falso dell'attaccante al posto dell’originario;
    Scoprire la password dell'account di sistema nel database (tramite un brute-force attack).

   Per comunicare con il proprio database o con un altro server (ad esempio Active Directory), l'applicazione
   costruisce dinamicamente una sua stringa di connessione. Questa stringa di connessione include valori
   concatenati inseriti dall'utente per l'autenticazione stessa. Se i valori immessi dall'utente non sono stati
   verificati per la validità del tipo di dati né successivamente sanificato, l'input potrebbe essere utilizzato per
   manipolare malamente la stringa di connessione.

   **Come difendersi**

   ```
    Validare tutti gli input, indipendentemente dalla sorgente. La validazione dovrebbe essere basata
   su una whitelist: dovrebbero essere accettati solo i dati che adattano a una struttura specificata,
   scartando quelli che non rispettano la whitelist. Controllare:
   o Data type;
   o Size;
   o Range;
   o Format;
   o Expected values;
    Evitare di costruire dinamicamente stringhe di connessione. Se è necessario creare dinamicamente
   una stringa di connessione, cercare di non includere l'input dell'utente. In ogni caso, utilizzare
   utilità basate sulla piattaforma, come SqlConnectionStringBuilder di .NET, o almeno codificare
   l'input validato come il piu' idoneo per la piattaforma utilizzata.
   ```
   Per ulteriori informazioni si veda: [http://cwe.mitre.org/data/definitions/99.html,](http://cwe.mitre.org/data/definitions/99.html,)
   CWE-99: Improper Control of Resource Identifiers ('Resource Injection').

   #### 7.10.5 LDAP Injection

   **Come riconoscerla**


   Questa vulnerabilità (LDAP Injection) riguarda la gestione delle query di tipo LDAP che vengono effettuate
   dalle applicazioni e che potrebbero essere utilizzate in modo improprio da un utente malintenzionato.
   Le operazioni che potrebbero essere eseguite a tal fine sono le seguenti:
    Effettuare il login con un utente diverso da quello inserito dall'utente
    Venire in possesso di privilegi di sistema non autorizzati
    Rubare le informazioni
   Per comunicare con il proprio database o con un altro server (ad esempio Active Directory), l'applicazione
   costruisce dinamicamente una sua stringa di connessione. Questa stringa di connessione include valori
   concatenati inseriti dall'utente per l'autenticazione stessa. Se i valori immessi dall'utente non sono stati
   verificati per la validità del tipo di dati né successivamente sanificati, l'input potrebbe essere utilizzato per
   manipolare malamente la stringa di connessione.

   **Come difendersi**

   ```
    Validare tutti gli input, indipendentemente dalla sorgente. La validazione dovrebbe essere basata
   su una whitelist: dovrebbero essere accettati solo i dati che adattano a una struttura specificata,
   scartando quelli che non rispettano la whitelist. Controllare:
   o Data type;
   o Size;
   o Range;
   o Format;
   o Expected values.
   ```
   Per ulteriori informazioni: [http://cwe.mitre.org/data/definitions/90.html,](http://cwe.mitre.org/data/definitions/90.html,)
   CWE-90: Improper Neutralization of Special Elements used in an LDAP Query ('LDAP Injection').

   #### 7.10.6 Resource Injection

   **Come riconoscerla**

   Un utente malintenzionato potrebbe aprire una backdoor che potrebbe permettere all'attaccante di
   connettersi direttamente al server con possibili conseguenze molto gravi per la sicurezza.
   Tramite questa vulnerabilità un possibile malintenzionato potrebbe utilizzare eventuali connessioni aperte
   dall'utente, nel caso non fossero gestite adeguatamente.

   **Come difendersi**

   ```
    Non consentire a un utente di definire i parametri relativi ai sockets di rete.
   ```
   Per ulteriori informazioni si veda: [http://cwe.mitre.org/data/definitions/99.html,](http://cwe.mitre.org/data/definitions/99.html,)
   CWE-99: Improper Control of Resource Identifiers ('Resource Injection').

   #### 7.10.7 SQL Injection

   **Come riconoscerla**

   Un utente malintenzionato potrebbe accedere direttamente a tutti i dati del sistema. Utilizzando strumenti
   e modifica di testo semplici, l'aggressore potrebbe rubare qualsiasi informazione riservata memorizzata dal
   sistema (ad esempio i dati personali dell'utente o le carte di credito) e eventualmente modificare o
   cancellare i dati esistenti.
   L'applicazione comunica con il suo database inviando una query SQL in formato testo. L'applicazione crea la
   query semplicemente concatenando le stringhe tra cui i dati ottenuti dal database. Poiché questi dati
   possono essere stati precedentemente ottenuti dall'input dell'utente e non sono stati verificati la validità


   del tipo di dati né successivamente sanificati, i dati potrebbero contenere comandi SQL che verrebbero
   interpretati come tali dal database.
   Le indicazioni di cui di seguito si applicano anche per la vulnerabilità **Second Order SQL Injection**.

   **Come difendersi**

   ```
    Validare tutti gli input, indipendentemente dalla sorgente. La validazione dovrebbe essere basata
   su una whitelist: dovrebbero essere accettati solo i dati che adattano a una struttura specificata,
   scartando quelli che non rispettano la whitelist. Controllare:
   o Data type;
   o Size;
   o Range;
   o Format;
   o Expected values;
    Invece di concatenare le stringhe si consiglia di:
    Utilizzare componenti di database sicuri come le procedure memorizzate, query parametrizzate e
   le associazioni degli oggetti (per comandi e parametri).
    Una soluzione ancora migliore è quella di utilizzare una libreria ORM, come EntityFramework,
   Hibernate o iBatis
    Limitare l'accesso agli oggetti e alle funzionalità di database, in base al "Principle of Least Privilege"
   (non fornire diretti agli utenti maggiori di quelli strettamente necessari).
   ```
   Per ulteriori informazioni si veda: [http://cwe.mitre.org/data/definitions/89.html,](http://cwe.mitre.org/data/definitions/89.html,)
   CWE-89: Improper Neutralization of Special Elements used in an SQL Command ('SQL Injection').

   #### 7.10.8 Xpath Injection

   **Come riconoscerla**

   A seconda del tipo di informazioni contenute nel documento XML interrogato, un utente malintenzionato
   potrebbe, manipolandole, causare gravi danni all'utente come il furto di dati non autorizzati oppure la
   sostituzione dell'utente stesso.
   L'applicazione interroga un documento XML utilizzando una query XPath testuale. L'applicazione crea la
   query semplicemente concatenando le stringhe tra cui l'input dell'utente. Poiché l'input dell'utente non è
   stato verificato per la validità del tipo di dati né successivamente sanificato, l'input potrebbe essere
   manipolato.
   In tal modo potrebbe essere possibile avere delle selezioni finali sbagliate dal documento XML durante
   l'esecuzione dell'applicazione.

   **Come difendersi**

   ```
    Validare tutti gli input, indipendentemente dalla sorgente. La validazione dovrebbe essere basata
   su una whitelist: dovrebbero essere accettati solo i dati che adattano a una struttura specificata,
   scartando quelli che non rispettano la whitelist. Controllare:
   o Data type;
   o Size;
   o Range;
   o Format;
   o Expected values;
    Evitare che la costruzione della query xpath sia dipendente dalle informazioni inserite dall'utente.
   Possibilmente mappare la query di tipo XPath con i parametri utente mantenendo la separazione
   tra dati e codice. Nel caso fosse necessario includere l'input del'utente nella query, l'input stesso
   dovra' essere precedentemente validato correttamente.
   ```

   Per ulteriori informazioni si veda: [http://cwe.mitre.org/data/definitions/643.html,](http://cwe.mitre.org/data/definitions/643.html,)
   CWE-643: Improper Neutralization of Data within XPath Expressions ('XPath Injection').

   ### 7.11 AJAX

   AJAX, acronimo di Asynchronous JavaScript and XML, è una tecnica di sviluppo software per la realizzazione
   di applicazioni web interattive (Rich Internet Application). Le vulnerabilità di questo linguaggio sono molto
   simili a quelle presenti nel linguaggio JavaScript.
   Normalmente le funzioni richiamate sono scritte con il linguaggio JavaScript. Tuttavia, e a dispetto del
   nome, l'uso di JavaScript e di XML non è obbligatorio, ma possono essere anche usate pagine HTML, CSS e
   altro.
   Di seguito l’ elenco delle principali vulnerabilità e delle relative contromisure da adottare.

   #### 7.11.1 Client Dom Code Injection

   **Come riconoscerla**

   La vulnerabilitàdi tipo "Client DOM Code Injection" consiste nell’infettare del codice Javascript o HTML
   superando le normali protezioni del sistema contro attacchi di tipo Cross-Site Scripting (XSS).
   L’XSS, acrononimo di Cross Site scripting viene realizzato tramite l’inclusione di codice (HTML o Javascript
   per la Client DOM Code Injection) all’interno di una pagina web per effettuare operazioni malevoli quali il
   prelievo di cookies privati.
   La vulnerabilita' "Client DOM Code Injection" puo' utilizzare anche strumenti di tipo "Social engineering"
   per carpire informazioni dagli utenti web tramite tecniche di bassa tecnologia sviluppate da malintenzionati
   per ottenere informazioni personali.
   Ad esempio possono essere simulate pagine quasi identiche ad altri siti di largo utilizzo per ottenere
   informazioni riservate.

   **Come difendersi**

   ```
    Evitare di eseguire del codice dinamicamente, specialmente se costruito con input proveniente
   dall’esterno.
    Occorre verificare sempre l’input, fissando controlli rigidi che impediscano di immettere caratteri e
   tipi di dati potenzialmente dannosi. L’optimum è designare una white list di valori ammessi e
   scartare tutto ciò che non vi rientra.
    E’ necessario codificare completamente tutti i dati dinamici prima di incorporarli nella pagina web.
   La codifica deve essere sensibile al contesto. Per esempio:
    Codifica HTML per contenuti HTML e per gli attributi relativi
    Codifica JavaScript per sorgenti di tipo JavaScript
    Si consiglia di utilizzare librerie conosciute per l'output di codifica, come ad esempio le librerie di
   tipo ESAPI.
    Evitare di creare codice XML o JSON in modo dinamico.
    Proprio come la creazione di codice HTML o SQL potrebbero causare dei bug di XML Injection,
   utilizzare una libreria di codifica o delle librerie JSON o XML affidabili per rendere sicuri gli attributi
   dei dati degli elementi.
    Non eseguire la crittografia nel codice lato client. Utilizzare le tecnologie TLS/SSL e crittografare le
   informazioni sul server.
    Evitare di chiamare dinamicamente una funzione senza averne prima sanitizzato l'input.
   Esempio javascript:
   var input = document.getElementById("id").value;
   window.setInterval( myFunc(input), 1000);
   Questo il software corretto dopo la sanitizzazione:
   var input = document.getElementById("id").value;
   var trusted = escape(input);
   ```

   ```
   window.setInterval( myFunc(trusted), 1000);
   ```
   ### Esempio per un uso corretto dell’aggiornamento dinamico dell'HTML nel DOM:

   ```
   document.write("<%=Encoder.encodeForJS(Encoder.encodeForHTML(untrustedData))%
   >");
   Nel caso debba essere impostato del codice javascript per delle chiamate dinamiche vanno
   utilizzati solo metodi predefiniti o codice Javascript non influenzabile da variabili dinamiche o non
   dipendente da routine tipo “eval()” non particolarmente sicure.
   ```
   ### Esempio di codice javascript sicuro:

   ```
   window.setInterval( "timedFunction();", 1000);
   ```
   Per ulteriori informazioni si veda: [http://cwe.mitre.org/data/definitions/94.html,](http://cwe.mitre.org/data/definitions/94.html,)
   Improper Control of Generation of Code ('Code Injection') CWE-94.

   #### 7.11.2 Client DOM Stored Code Injection

   **Come riconoscerla**

   L'utente malintenzionato può attraverso questo tipo di vulnerabilità causare la riscrittura di pagine web e
   l'inserimento di script dannosi per la sicurezza.
   Una vulnerabilità XSS persistente (o stored) come la “Client DOM Stored Code Injection” è una variante più
   devastante di cross-site scripting con manipolazione di codice: si verifica quando i dati forniti
   dall'attaccante vengono salvati sul server, e quindi visualizzati in modo permanente sulle pagine
   normalmente fornite agli utenti durante la normale navigazione.

   **Come difendersi**

   ```
    Evitare qualsiasi compilazione dinamica, esecuzione o valutazione del codice. Nel caso sia
   necessaria l'esecuzione dinamica, invece di utilizzare i dati lato client (inclusi i dati
   precedentemente memorizzati dall'applicazione stessa), utilizzare solo dati rigidamente controllati
   tramite liste prefissate o dati attendibili dal server.
    Evitare di chiamare dinamicamente una funzione senza averne prima sanitizzato l'input.
    Nel caso debba essere impostato del codice javascript per delle chiamate dinamiche vanno
   utilizzati solo metodi predefiniti o codice Javascript non influenzabile da variabili dinamiche o non
   dipendente da routine tipo “eval()” non particolarmente sicure.
   Esempio di forma corretta di codice javascript sicuro:
   window.setInterval( "timedFunction();", 1000);
   ```
   Per ulteriori informazioni ed esempi si veda: [http://cwe.mitre.org/data/definitions/94.html,](http://cwe.mitre.org/data/definitions/94.html,)
   Improper Control of Generation of Code ('Code Injection') CWE-94.

   #### 7.11.3 Client Dom Stored XSS

   **Come riconoscerla**

   Attraverso questa vulnerabilità un utente malintenzionato potrebbe intercettare lo scambio di informazioni
   sensibili tra un'applicazione e i database relativi allo storage delle informazioni stesse. Quando un altro
   utente accede successivamente a questi dati, le pagine web possono essere riscritte e possono essere
   attivati script dannosi. La vulnerabilità è dovuta all'uso di dati prelevati da database in modo arbitrario,
   senza che prima queste informazioni vengano codificate in un formato sicuro. La vulnerabilità è di tipo
   Stored (permanente).
   Una vulnerabilità XSS persistente (o stored) come la “Client DOM Stored XSS” è una variante più
   devastante di cross-site scripting con manipolazione di codice: si verifica quando i dati forniti


   dall'attaccante vengono salvati sul server, e quindi visualizzati in modo permanente sulle pagine
   normalmente fornite agli utenti durante la normale navigazione.

   **Come difendersi**

   ```
    Evitare qualsiasi compilazione dinamica, esecuzione o valutazione del codice. Nel caso sia
   necessaria l'esecuzione dinamica, invece di utilizzare i dati lato client (inclusi i dati
   precedentemente memorizzati dall'applicazione stessa), utilizzare solo dati rigidamente controllati
   tramite liste prefissate o dati attendibili dal server.
    Occorre verificare sempre l’input, fissando controlli rigidi che impediscano di immettere caratteri e
   tipi di dati potenzialmente dannosi. L’optimum è designare una white list di valori ammessi e
   scartare tutto ciò che non vi rientra.
    E’ necessario quindi codificare completamente tutti i dati dinamici prima di incorporarli nella
   pagina web. La codifica deve essere sensibile al contesto. Per esempio:
   o Data type;
   o Size;
   o Range;
   o Format;
   o Expected values;
    La validazione comunque non sostituisce la codifica. Devono essere completamente codificati tutti i
   dati dinamici, indipendentemente dalla sorgente, prima di incorporare idati stessi in un output. La
   codifica dovrebbe essere sensibile al contesto. Per esempio:
   o Codifica HTML per un contesto di tipo HTML;
   o Codifica degli attributi HTML per output degli attributi relativi;
   o Codifica Javascript per server-generated di tipo Javascript;
    Utilizzare .innerText invece di .innerHtml: l'uso di .innerHtml impedirà la maggior parte dei
   problemi di XSS in quanto codifica automaticamente il testo.
   Esempio di HTML richiamato nel codice Javascript:la stringa in uscita è codificata nella pagina Html
   prima che venga visualizzata nell’etichetta relativa:
   public class StoredXssFixed
   {
   public string foo (Label lblOutput, SqliteConnection connection,
   HttpServerUtility Server, string id)
   {
   SqliteConnection connection = new
   SqliteConnection(connectionString)
   string sql = "select email from CustomerLogin where
   customerNumber = " + id;
   SqliteCommand cmd = new SqliteCommand(sql, connection);
   string output = ( string )cmd.ExecuteScalar();
   lblOutput.Text = String.IsNullOrEmpty(output)? "Customer
   Number does not exist" : Server.HtmlEncode(output);
   }
   }
   ```
   ```
   Esempio Javascript per Client Dom Stored XSS.
   Forma non corretta (routine completa):
   <!DOCTYPE html>
   <html>
   <head>
   <meta charset="utf-8">
   <title>XSS Example</title>
   ```

   ```
   <script
   src="http://ajax.googleapis.com/ajax/libs/jquery/1.6.4/jquery.min.js"></scrip
   t>
   <script>
   $(function() {
   $('#users').each(function() {
   var select = $(this);
   var option = select.children('option').first();
   select.after(option.text());
   select.hide();
   });
   });
   </script>

.. raw:: html

   </head>

.. raw:: html

   <body>

.. raw:: html

   <form method="post">

.. raw:: html

   <p>

 <script>alert(‘xss’);</script>

.. raw:: html

   </p>

< /form>

.. raw:: html

   </body>

.. raw:: html

   </html>

::

Forma corretta (fix relativa alle stringa modificata): // after()
accepts a DOM element so lets create a text node
select.after(document.createTextNode(option.text()));

::

   Per ulteriori informazioni si veda: [http://cwe.mitre.org/data/definitions/97.html,](http://cwe.mitre.org/data/definitions/97.html,)
   CWE-97: Improper Neutralization of Server-Side Includes (SSI) Within a Web Page.

   #### 7.11.4 Client Dom XSS

Come riconoscerla

::

Un utente malintenzionato potrebbe utilizzare metodologie di “social
engineering” (es. falsificazione di siti web di largo accesso con
richiesta di credenziali o dati sensibili) per carpire informazioni
importanti tramite codice manipolato all'interno di pagine web degli
applicativi falsificati. Possono essere prelevate password, dati di
carte di credito etc. Come difendersi

::

 Evitare qualsiasi compilazione dinamica, esecuzione o valutazione del
codice. Nel caso sia necessaria l'esecuzione dinamica, invece di
utilizzare i dati lato client (inclusi i dati precedentemente
memorizzati dall'applicazione stessa), utilizzare solo dati rigidamente
controllati tramite liste prefissate o dati attendibili dal server. 
Occorre verificare sempre l'input, fissando controlli rigidi che
impediscano di immettere caratteri e tipi di dati potenzialmente
dannosi. L'optimum è designare una white list di valori ammessi e
scartare tutto ciò che non vi rientra.  E' necessario quindi codificare
completamente tutti i dati dinamici prima di incorporarli nella pagina
web. La codifica deve essere sensibile al contesto. Per esempio: o Data
type; o Size;

::

o Range; o Format; o Expected values.  La validazione comunque non
sostituisce la codifica. Devono essere completamente codificati tutti i
dati dinamici, indipendentemente dalla sorgente, prima di incorporare
idati stessi in un output. La codifica dovrebbe essere sensibile al
contesto. Per esempio: o Codifica HTML per un contesto di tipo HTML; o
Codifica degli attributi HTML per output degli attributi relativi; o
Codifica Javascript per server-generated di tipo Javascript.  Per
creare HTML dinamico in JavaScript, utilizzare la libreria OWASP
ESAPI4JS:  window.location = ESAPI4JS.encodeForURL(input);  Per creare
dinamicamente URL in JavaScript, utilizzare la libreria OWASP ESAPI4JS:
 window.location = ESAPI4JS.encodeForURL(input);

::

   Per ulteriori informazioni si veda: [http://cwe.mitre.org/data/definitions/97.html,](http://cwe.mitre.org/data/definitions/97.html,)
   CWE-97: Improper Neutralization of Server-Side Includes (SSI) Within a Web Page.

   #### 7.11.5 Client Resource Injection

   **Come riconoscerla**

   Un utente malintenzionato potrebbe aprire un backdoor che consenta all'attaccante di connettersi
   direttamente al server delle applicazioni prendendone il controllo o comunque effettuare attacchi diretti al
   server con effetti pericolosi.

   **Come difendersi**

 Non consentire a un utente di venire in possesso delle informazioni
relative alle definizioni dei parametri di gestione relativi ai “network
sockets”.

::

   #### 7.11.6 Client Second Order Sql Injection.............................................................................................................

   **Come riconoscerla**

   Un utente malintenzionato potrebbe accedere direttamente a tutti i dati del sistema. L'attaccante potrebbe
   rubare qualsiasi informazione riservata memorizzata dal sistema (ad esempio i dati personali dell'utente o
   le carte di credito) e eventualmente modificare o cancellare i dati esistenti.

   **Come difendersi**

 Evitare qualsiasi compilazione dinamica, esecuzione o valutazione del
codice. Nel caso sia necessaria l'esecuzione dinamica, invece di
utilizzare i dati lato client (inclusi i dati precedentemente
memorizzati dall'applicazione stessa), utilizzare solo dati rigidamente
controllati tramite liste prefissate o dati attendibili dal server. 
Occorre verificare sempre l'input, fissando controlli rigidi che
impediscano di immettere caratteri e tipi di dati potenzialmente
dannosi. L'optimum è designare una white list di valori ammessi e
scartare tutto ciò che non vi rientra.  Codificare completamente tutti
i dati dinamici prima di incorporarli nella pagina web. La codifica deve
essere sensibile al contesto. Per esempio: o Data type; o Size; o Range;
o Format; o Expected values;  Invece di concatenare le stringhe:

::

o Utilizzare componenti di database sicuri come le procedure
memorizzate, query parametrizzate e le associazioni degli oggetti (per
comandi e parametri). o Una soluzione ancora migliore è quella di
utilizzare una libreria ORM, come EntityFramework, Hibernate o iBatis. o
Limitare l'accesso agli oggetti e alle funzionalità di database, in base
al principio del minimo privilegio.

::

   Esempio - Javascript per Client Second Order Sql Injection.
   Forma non corretta:

var userId = 5; var query = connection.query(‘SELECT \* FROM users WHERE
id = ?’, [userId], function(err, results) { //query.sql returns SELECT
\* FROM users WHERE id = ‘5’ });

::

   Forma corretta:
   var post = {id: 1, title: 'Hello MySQL'};
   var query = connection.query('INSERT INTO posts SET ?', post, function(err,
   result) {
   //query.sql returns INSERT INTO posts SET `id` = 1, `title` = 'Hello MySQL'
   });

   #### 7.11.7 Client Sql Injection

   **Come riconoscerla**

   Utilizzando questa vulnerabilità utente malintenzionato potrebbe utilizzare i canali di comunicazione tra
   l'applicazione e il suo database inviando una query SQL testuale. L'applicazione viene attaccata con il
   risultato di avere una query modificata di interrogazione al db semplicemente concatenando le stringhe tra
   cui l'input dell'utente. Poiché l'input utente non è stato verificato per la validità del tipo di dati né
   successivamente sanificato, l'input potrebbe contenere comandi SQL che verrebbero interpretati come tali
   dal database.

   **Come difendersi**

 Validare tutti i dati di input, indipendentemente dalla sorgente. La
convalida dovrebbe essere basata su una whitelist (lista prefissata):
dovranno essere accettati solo i dati che rispettano una una struttura
specificata, bloccando i dati che presentano schemi che non rientrano in
queste casistiche. Controllare i seguenti punti:  Codificare
completamente tutti i dati dinamici prima di incorporarli nella pagina
web. La codifica deve essere sensibile al contesto. Per esempio: o Data
type; o Size; o Range; o Format; o Expected values.  Invece di
concatenare le stringhe adottare le seguenti metodologie: o Utilizzare
componenti di database sicuri come le procedure memorizzate, query
parametrizzate e le associazioni degli oggetti (per comandi e
parametri). o Una soluzione ancora migliore è quella di utilizzare una
libreria ORM, come EntityFramework, Hibernate oppure iBatis. o Limitare
l'accesso agli oggetti e alle funzionalità del database, in base alle
regole definite dal “Principle of Least Privilege”. Il principio in
sintesi stabilisce che agli utenti venga attribuito il più

::

basso livello di “diritti” che possano detenere rimanendo comunque in
grado di compiere il proprio lavoro.

::

   Esempio - Javascript per Client SQL Injection
   Forma non corretta:
   var info = {
   userid: message.author.id
   }

connection.query(“SELECT \* FROM table WHERE userid = '” +
message.author.id + “'”, info, function(error) { if (error) throw error;
});

::

   Forma corretta:
   var sql = "SELECT * FROM table WHERE userid = ?";
   var inserts = [message.author.id];
   sql = mysql.format(sql, inserts);

   Per ulteriori informazioni vedere: [http://cwe.mitre.org/data/definitions/89.html,](http://cwe.mitre.org/data/definitions/89.html,)
   CWE-89: Improper Neutralization of Special Elements used in an SQL Command ('SQL Injection').

   #### 7.11.8 Cross-Site Request Forgery (CSRF)

   **Come riconoscerla**

   Il Cross-site request forgery, abbreviato CSRF o anche XSRF, è una vulnerabilità a cui sono esposti i siti web
   dinamici quando sono progettati per ricevere richieste da un client senza meccanismi per controllare se la
   richiesta sia stata inviata intenzionalmente oppure no. Diversamente dal cross-site scripting (XSS), che
   sfrutta la fiducia di un utente in un particolare sito, il CSRF sfrutta la fiducia di un sito nel browser di un
   utente.
   Nelle applicazioni Web 2.0 Ajax comunica con i servizi Web di back-end tramite XML-RPC, SOAP o REST. È
   possibile invocarli tramite interrogazioni di tipo GET e POST che effettuano chiamate cross-site ai servizi
   web. La tecnologia di tipo Cross-Site Request Forgery permette di manipolare queste chiamate indebolendo
   la sicurezza del sistema.
   Un attaccante fa in modo che un utente vittima invii involontariamente una richiesta HTTP dal suo browser
   al sistema web dove è attualmente autenticato. Il sistema, vulnerabile al CSRF, avendo la certezza che la
   richiesta provenga dall'utente già precedentemente autenticato la esegue senza sapere che in realtà dietro
   la richiesta si cela un'azione pensata dall'attaccante come ad esempio un trasferimento di fondi, un
   acquisto di un oggetto, una richiesta di dati o qualsiasi altra funzione offerta dall'applicazione vulnerabile.
   Ci sono innumerevoli modi con i quali un utente può essere ingannato nell'inviare una richiesta pensata da
   un attaccante a un web server. Questo può essere fatto nascondendola ad esempio in un elemento HTML
   di un'immagine, una XMLHttpRequest o un URL.

   **Come difendersi**

 Usare framework, librerie, moduli e in generale codice fidato che
permettano allo sviluppatore di evitare l'introduzione di questa
vulnerabilità.  Nei form che permettono operazioni importanti inserire
un campo hidden nel quale inserire come valore una stringa random. La
stessa stringa, va impostata come variabile di sessione, in questo modo
non è rintracciabile lato client ed è nota solo al server. Una volta
compiuta la submit del form, se il valore della variabile di sessione
corrisponde alla value del sopracitato campo hidden, la richiesta è da
considerarsi valida.

::

 Identificare quelle operazioni che possano risultare pericolose e
quando un utente genera un'operazione di questo tipo inviare una
richiesta addizionale di conferma all'utente, per esempio, la richiesta
di una password, che deve essere verificata prima di eseguire
l'operazione.  Non utilizzare il metodo GET per il passaggio di
parametri da una pagina web all'altra soprattutto per quelle richieste
che comportano un cambiamento di stato come ad esempio la modifica di
dati e controllare il campo di intestazione HTTP referer per vedere se
la richiesta è stata generata da una pagina valida.  Verificare che il
sistema sia esente da vulnerabilità di tipo cross-site scripting poiché
molte delle difese CSRF possono essere evitate usando vulnerabilità di
questo tipo.  Dal lato utente è buona abitudine eseguire sempre il
logout da siti web sensibili prima di visitare altre pagine web.

::

   Per ulteriori informazioni vedere: [http://cwe.mitre.org/data/definitions/352.html,](http://cwe.mitre.org/data/definitions/352.html,)
   CWE-352: Cross-Site Request Forgery (CSRF).

   ### 7.12 GO

   Go è un linguaggio di programmazione open source sviluppato da Google.

   #### 7.12.1 Client Dom Stored XSS

   **Come riconoscerla**

   Cross-site scripting (XSS) è una vulnerabilità che affligge siti web dinamici che impiegano un insufficiente
   controllo dell'input nei form. Un XSS permette ad un Cracker di inserire o eseguire codice lato client al fine
   di attuare un insieme variegato di attacchi quali ad esempio: raccolta, manipolazione e reindirizzamento di
   informazioni riservate, visualizzazione e modifica di dati presenti sui server, alterazione del comportamento
   dinamico delle pagine web ecc.

   GO, proprio come qualsiasi altro linguaggio di programmazione multiuso, è vulnerabile a XSS nonostante la
   documentazione indirizzi chiaramente sull'utilizzo di html/template package.

   In riferimento al seguente frammento di codice:

package main import “net/http”^ import “io” func handler (w
http.ResponseWriter, r \*http.Request) { io.WriteString(w,
r.URL.Query().Get(“param1”)) } func main () {^ http.HandleFunc(“/”,
handler)^ http.ListenAndServe(“:8080”, nil ) }

::

 Questo codice crea e avvia un server HTTP in ascolto sulla porta 8080
(main()) gestendo le richieste sulla root del server (/).  La funzione
handler(), che gestisce le richieste, prevede un parametro query stringa
Param1, il cui valore viene quindi scritto nel flusso di risposta (w): o
Se param1=test, il Content-Type sarà inviato come text/plain:

::


   o Se param1=<h1>, il Content-Type sarà inviato come text/html (ciò rende vulnerabile a XSS):

   Si potrebbe pensare che rendere param1 uguale a qualsiasi tag HTML porti allo stesso
   comportamento, ma non è così: param1=<h2>, param1=<span>, param1=<form> non
   modificano Content-Type in text/html, bensì in plain / text.
   o Se param1=<script>alert(1)</script>, il Content-Type sarà inviato come text/html e il valore
   sarà restituito e quindi facilmente interpretato tramite l’alert (XSS - Cross Site Scripting):


   **Come difendersi**

   ## Sostiruire il text/template package con html/template :

package main

::

   import "net/http"^
   import "html/template"
   func handler(w http.ResponseWriter, r
   *http.Request) { param1 :=
   r.URL.Query().Get("param1")

   tmpl := template.New("hello")^

   tmpl, _ = tmpl.Parse(`{{define "T"}}{{.}}{{end}}`)^

   tmpl.ExecuteTemplate(w, "T" , param1)^
   }

   func main() {^

   http.HandleFunc("/", handler)^

   http.ListenAndServe(":8080", nil )
   }

   Se param1=<h1>, l'intestazione di risposta HTTP Content-Type non verrà inviata come text/plain :

   Param1 è correttamente codificato sul browser:


   #### 7.12.2 SQL Injection

   **Come riconoscerla**

   L’ SQL Injection nasce dalla mancata/non corretta codifica dei dati di input/output. Partendo dalla query di
   esempio riportata di seguito:

   ctx := context.Background()^

   customerId := r.URL.Query().Get("id")^
   query := "SELECT number, expireDate, cvv FROM creditcards WHERE customerId = "
   + customerId
   row, _ := db.QueryContext(ctx, query)

   Quando viene fornito un customerId valido, la query restituisce l’elenco delle carte di credito del cliente.
   Tuttavia, se customerId non è un valore, ma una stringa (concatenazione di diversi valori/simboli) come
   nell’esempio che segue:

SELECT number, expireDate, cvv FROM creditcards WHERE customerId = 1 OR
1=1

::

   La query restituirebbe (a meno di opportune verifiche dei dati immessi in input) tutti i record della tabella
   relativamente a tutti i clienti censiti poiché la condizione 1 = 1 sarà ‘true’ per qualsiasi record.

   **Come difendersi**

   Impostare i placeholder:

   ctx := context.Background()^

   customerId := r.URL.Query().Get("id")^
   query := "SELECT number, expireDate, cvv FROM creditcards WHERE customerId = ?"
   stmt, _ := db.QueryContext(ctx, query, customerId)

   La sintassi è specifica:

   **MySQL**^ **PostgreSQL**^ **Oracle**^

WHERE col =? WHERE col = $1 WHERE col = :col

::

   VALUES(?, ?, ?)^ VALUES($1, $2, $3)^ VALUES(:val1, :val2, :val3)^


   #### 7.12.3 Ulteriori indicazioni per lo sviluppo sicuro

   L'input dell'utente e i relativi dati associati rappresentano un rischio se non vengono attuati opportuni
   controlli di "Input Validation" e "Input Sanitization". Tutte le procedure di convalida dei dati devono essere
   eseguite su sistemi affidabili (ad esempio sul server) e devono essere eseguite ad ogni livello
   dell'applicazione.

   ##### 7.12.3.1 Validazione dell’INPUT .......................................................................................................................................

   I dati dell’input devono essere considerati non sicuri per impostazione predefinita e accettati solo dopo
   aver effettuato i controlli di sicurezza appropriati. Anche le fonti dei dati devono essere identificate come
   attendibili o non affidabili e, in caso di fonti non attendibili, devono essere eseguiti controlli di convalida.

   Se la convalida fallisce, l'input deve essere rifiutato.

   Go dispone di librerie native che includono metodi a supporto del processo di validazione e sanitizzazione
   dei dati:

    strconv per la conversione di stringhe ad altre tipologie di dati:
    Atoi
    ParseBool
    ParseFloat
    ParseInt
    strings per gestire le stringhe e relative proprietà:
   o Trim
   o ToLower
   o ToTitle
   o regexp utilizzabile nelle espressioni regolari per gestire formati personalizzati.
   Altre tecniche per garantire la validità dei dati di input includono:
    _Whitelisting_ – verificare l’input sulla base di una whitelist di caratteri consentiti.
    _Boundary checking_ – verificare la lunghezza dei numeri e dei dati.
    Validazione numerica.
    Verificare i Null Bytes: (%00 )
    Verificare i caratteri di linea: %0d , %0a , \r , \n
    Verificare i caratteri di alterazione del percorso ../ oppure \\..
   **NOTA** : Assicurarsi che le intestazioni di richiesta e risposta HTTP contengano solo caratteri ASCII.


   7.12.3.1.1 Gestione dei File
    Assicurarsi che gli utenti non siano autorizzati a fornire direttamente dati a tutte le funzioni
   dinamiche. In linguaggi come PHP, il passaggio di dati utente a funzioni incluse dinamicamente nel
   codice funzioni è un grave rischio di sicurezza.
    Nel caso di reindirizzamenti dinamici, i dati utente non devono essere passati. Se è richiesto
   dall'applicazione, è necessario adottare ulteriori controlli, che includono ad esempio: l'accettazione
   solo dei dati correttamente convalidati e dei relativi URL. Inoltre, è importante assicurarsi che i
   percorsi a directory e file siano mappati in elenchi di indici di percorsi predefiniti (assicurarsi di
   utilizzare tali indici).
    Non inviare mai il percorso assoluto del file, utilizzare sempre percorsi relativi.
    Per i file e le risorse dell'applicazione, impostare autorizzazioni di sola lettura.
    L’upload dei file sul server dovrebbe essere limitato ai soli utenti autenticati e solo per alcune
   tipologie di file accettati. Questo controllo può essere fatto usando la seguente funzione Go che
   rileva i tipi MIME: func DetectContentType (data[] byte) string. I file caricati dagli utenti non
   devono essere memorizzati nel contesto web dell'applicazione, ma in un server di contenuti o in un
   database. Il percorso su file systm in cui vengono memorizzati tali file non deve avere priviligi di
   esecuzione. Se il file server che ospita i dati caricati dall’utente è basato su *NIX, è necessario
   implementare meccanismi di sicurezza come l'ambiente chrooted o montare la directory del file di

   destinazione come un'unità logica.^

   (^)
   7.12.3.1.2 Sorgenti dati
   Ogni volta che i dati vengono trasmessi da una fonte attendibile a una fonte meno attendibile, è necessario
   eseguire controlli di integrità. Ciò garantisce che i dati non siano stati manomessi e che si stanno ricevendo
   i dati previsti. Altri controlli includono:
    Cross-system consistency checks;
    Hash totals;
    Referential integrity;
    Uniqueness check;
    Table look up check.
   7.12.3.1.3 Azioni di post-validazione (azioni aggiuntive)
    informare l'utente che i dati inseriti non rispettano i requisiti richiesti e pertanto devono essere
   modificati per conformarli alle condizioni richieste;
    modificare i dati inviati dall'utente lato server senza notificare all'utente di tali modifiche.
   7.12.3.1.4 Sanitizzazione
   Dopo aver effettuato i controlli di convalida appropriati, un ulteriore passaggio che viene in genere
   adottato per rafforzare la sicurezza dei dati consiste nel rimuovere o modificare i caratteri ritenuti
   ‘pericolosi’. Le azioni più comuni di sanitizzazione sono i seguenti:
    Escaping. Nel package nativo html ci sono due funzioni usate per la sanitizzazione: una per l'escape
   del testo HTML e un'altra per l'HTML senza escape. La funzione EscapeString(), accetta una stringa
   e restituisce la stessa stringa con i caratteri speciali convertiti. (es. ‘<’ viene sostituito con ‘&lt;’).
   Questa funzione converte solo i seguenti cinque caratteri: <,>, &, ' e ". Viceversa c'è anche la
   funzione UnescapeString () per convertire da entità a caratteri.
    Rimuovere i TAG. Sebbene il package html/template abbia una funzione stripTags (), questa non è
   esportabile. Poiché nessun altro package nativo ha una funzione capace di rimuovere tutti i tag,
   l’alternativa è quella di utilizzare librerie di terze parti o copiare l'intera funzione insieme alle sue
   classi e funzioni private. Alcuni esempi di librerie di terze parti sono:
   o https://github.com/kennygrant/sanitize;
   o https://github.com/maxwells/sanitize;

o https://github.com/microcosm-cc/bluemonday.  Rimuovere le
interruzioni di linea, i Tabs, gli spazi bianchi non necessari. Il
“text/template” e “html/template” includono un modo per rimuovere gli
spazi bianchi dal template, utilizzando un segno meno - all'interno del
delimitatore dell'azione.  URL Request Path. Nel pacchetto “net/http”
c'è un tipo di multiplexer di richiesta HTTP chiamato ServeMux. Questo,
viene utilizzato per far corrispondere la richiesta in arrivo ai pattern
registrati e quindi a invocare il gestore che più si avvicina all' URL
richiesto. Oltre al suo scopo principale, si occupa anche di sanitizzare
il percorso della richiesta URL, reindirizzando qualsiasi richiesta
contenente ‘.’ o ‘..’ o ‘/’ ripetuti a un URL equivalente, ma più
pulito. Di seguito un esempio di Mux: func main() {^ mux :=
http.NewServeMux() rh := http.RedirectHandler(“http://yourDomain.org”,
307) mux.Handle(“/login”, rh) log.Println(“Listening…”)^
http.ListenAndServe(“:3000”, mux)^ }

::

   ##### 7.12.3.2 Gestione Sessione, Controlli Accessi e Crittografia ............................................................................................

   7.12.3.2.1 Sessioni

 La creazione della sessione deve essere eseguita su un sistema
attendibile.  Assicurarsi che gli algoritmi utilizzati per generare
l'identificatore di sessione siano sufficientemente casuali al fine di
prevenire una forzatura bruta di sessione.  Una volta assicurato un
token sufficientemente forte, impostare l'opportuno valore per i cookie:
‘Domain’, ‘Path’, ‘Expires’, ‘HttpOnly’ e ‘Secure’.  Al momento del
login, deve essere sempre generata una nuova sessione. La vecchia
sessione non deve essere mai riutilizzata, anche se questa non è
scaduta. Utilizzare anche il parametro Expire per eseguire la chiusura
periodica della sessione in modo da prevenire il “session hijacking”. Un
altro aspetto importante dei cookie è quello di impedire l'accesso
simultaneo per lo stesso nome utente. Ciò può essere fatto mantenendo un
elenco degli utenti connessi e confrontare il nuovo nome utente di
accesso con tale elenco. Questo elenco di utenti attivi viene di solito
persistito su un database.  Gli identificatori di sessione non devono
mai essere esposti negli URL. Questi dovrebbero essere localizzabili
solo nei cookie presenti nell'intestazione http. Un esempio di cattiva
pratica è quello di passare gli identificatori di sessione come
parametri di GET. I dati della sessione devono inoltre essere protetti
dall'accesso non autorizzato da parte di altri utenti del server.  Per
quanto riguarda le modifiche ai collegamenti da HTTP a HTTPS, si deve
prestare particolare attenzione nel prevenire potenziali attacchi MITM
che fiutano e che possono potenzialmente dirottare la sessione
dell'utente. La pratica migliore per ovviare a questo problema è
utilizzare HTTPS in tutte le richieste (pacchetto “crypto/tls” di Go). 
In caso di operazioni altamente sensibili o critiche, il token deve
essere generato per richiesta invece che per sessione. Accertarsi sempre
che il token sia sufficientemente casuale e abbia una lunghezza
abbastanza sicura da proteggerlo contro possibili attacchi di forza
bruta.  Aspetto da considerare nella gestione delle sessioni è la
funzionalità Logout. L'applicazione deve fornire un modo per
disconnettersi da tutte le pagine che richiedono l'autenticazione,
nonché terminare completamente la sessione e la connessione ad esse
associate. In particolare, quando un utente si disconnette, il cookie
deve essere eliminato dal client. La stessa azione deve essere
intrapresa dalla componente che si occupa della memorizzazione delle
informazioni della sessione utente.

::


   7.12.3.2.2 Controllo Accessi

 Utilizzare solo gli oggetti di sistema attendibili per le decisioni di
autorizzazione all'accesso.  Generare un token di sessione lato server,
quindi memorizzare e utilizzare questo token per convalidare l'utente e
applicare il modello predefinito di controllo degli accessi.  Il
componente utilizzato per l'autorizzazione di accesso deve essere un
unico componente (centralizzazione), utilizzato a livello di sito. Ciò
include quelle funzioni di libreria utilizzate che chiamano servizi di
autorizzazione esterni.  In caso di eccezione, il controllo degli
accessi dovrebbe fallire in modo sicuro. A tale scopo è opportuno
utilizzare la funzione ‘Defer’.  Se l'applicazione non può accedere
alle informazioni di configurazione, ogni accesso all'applicazione deve
essere negato.  I controlli di autorizzazione devono essere applicati
su ogni richiesta, inclusi gli script eseguiti lato server e le
richieste provenienti da tecnologie lato client come AJAX o Flash.  È
importante separare correttamente la logica di gestione dei privilegi
dal resto del codice applicativo.  Altre operazioni importanti in cui i
controlli di accesso devono essere attuati al fine di impedire ad un
utente non autorizzato di accedervi, sono: o File e altre risorse, o
Protezione URL's, o Protezioni Funzioni, o Riferimenti diretti ad
oggetti, o Servizi, o Dati applicativi, o Attributi utente e dati e
informaizoni sulle policy.  Se i dati di stato devono essere
memorizzati lato client, è necessario utilizzare la crittografia ed
effettuare opportuni controlli d'integrità per prevenire possibili
manomissioni.  Il flusso della logica applicativa deve essere conforme
alle regole di business.  Quando si trattano transazioni, il numero di
transazioni che un singolo utente o dispositivo può eseguire in un dato
periodo di tempo deve essere superiore ai requisiti previsti, ma
sufficientemente basso da impedire all'utente di eseguire un attacco di
tipo DoS.  L'impiego della sola intestazione HTTP “referer” è
insufficiente per convalidare l'autorizzazione e deve essere utilizzato
solo come controllo supplementare.  Per le sessioni con autenticazione
a lungo termine, l'applicazione deve riesaminare periodicamente
l'autorizzazione dell'utente per verificare che i permessi di
quest'ultimo non siano cambiati. Se le autorizzazioni sono cambiate, è
necessario scollegare l'utente e costringerlo a riautenticarsi.  Gli
account degli utenti devono essere verificati periodicamente, al fine di
rispettare le procedure di sicurezza. (ad esempio, disabilitando
l'account utente dopo 30 giorni dalla data di scadenza della password).
 L'applicazione deve supportare la possibilità di disabilitare gli
account e la chiusura delle sessioni in caso di revoca
dell'autorizzazione dell'utente. (ad es. cambiamento di ruolo,
situazione occupazionale, ecc.).  In caso di supporto di account di
servizio esterno e account che supportano connessioni da o verso sistemi
esterni, questi account devono essere gestiti in modo tale da avere il
più basso possibile livello di privilegio.

::

   7.12.3.2.3 Crittografia e Hashing
   La crittografia deve essere utilizzata ogni qual volta è necessario comunicare o memorizzare dati sensibili, ai
   quali è necessario accedere in seguito per ulteriori elaborazioni.
    Utilizzare algoritmi sicuri di hashing come l’SHA-256.

 Un caso di utilizzo “semplice” di crittografia è il protocollo HTTPS -
Hyper Text Transfer Protocol Secure. AES è lo standard di fatto per
quanto riguarda la crittografia a chiave simmetrica. Questo algoritmo,
come molte altre cifrature simmetriche, può essere implementato in
diverse modalità.  Utilizzare GCM (Galois Counter Mode) piuttosto che
CBC/ECB. La differenza principale tra GCM e CBC/ECB è il fatto che il
primo è una modalità di cifratura autenticata, il che significa che dopo
la fase di crittografia viene aggiunto un tag di autenticazione al testo
cifrato che sarà quindi convalidato prima della decodifica dei messaggi,
assicurando il messaggio da eventuali manomissioni. Il secondo è una
crittografia a chiave pubblica o una crittografia asimmetrica che
utilizza coppie di chiavi: pubbliche e private. La crittografia a chiave
pubblica è meno performante della crittografia a chiave simmetrica per
la maggior parte dei casi, per cui il suo uso più comune è la
condivisione di una chiave simmetrica tra due parti usando la
crittografia asimmetrica, in modo da poter utilizzare la chiave
simmetrica per scambiare messaggi crittografati con crittografia
simmetrica. A parte AES, che è una tecnologia degli anni' 90, gli autori
di Go hanno iniziato ad implementare e supportare algoritmi di
crittografia simmetrica più moderni che forniscono anche
l'autenticazione, come “chacha20poly1305”.  Un altro package da
considerare in Go, invece dell'uso diretto di AES, è “x/crypto/nacl”. La
“nacl/box” e “nacl/secretbox” in Go sono implementazioni delle
astrazioni di NaCl per l'invio di messaggi crittografati per i due casi
di utilizzo più comuni: o Invio di messaggi autenticati e crittografati
tra due parti utilizzando la crittografia a chiave pubblica (nacl/box).
o Invio di messaggi autenticati e crittografati tra due parti usando la
crittografia simmetrica (a.k.a secret-key).  Si deve stabilire e
utilizzare una politica e un processo per la gestione delle chiavi
crittografiche, in modo tale da proteggere i dati principali più
sensibili dall'accesso non autorizzato. Pertanto, le chiavi
crittografiche non devono assolutamente essere esplicitate e posizionate
nel codice sorgente.  Focalizzare l'attenzione sull'impiego di
algoritmi crittografici più moderni come l'implementazione
“https://godoc.org/golang.org/x/crypto” piuttosto che utilizzare il
pacchetto "crypto/\*“.  Tutti i numeri casuali, nomi di file casuali,
GUID casuali e stringhe casuali generati applicativamente, devono essere
creati utilizzando un generatore di numeri casuali approvato dal modulo
crittografico, soprattutto quando questi valori sono potenzialmente
sensibili e soggetti ad essere indovinati. Utilizzare dunque
la”crypto/rand" che, anche se più lenta della “math/rand”, risulta
essere molto più sicura.

::

   ##### 7.12.3.3 Gestione degli Errori e delle Eccezioni ...............................................................................................................

   La gestione degli errori e il logging rappresentano una parte essenziale nella protezione dell'applicazione e
   dell'infrastruttura. Quando si parla di Gestione degli errori, ci si riferisce all’individuazione di eventuali
   errori nella logica dell'applicazione che potrebbero causare il blocco del sistema a meno che non vengano
   gestiti correttamente.
   In Go esistono funzioni per la gestione degli errori. Queste sono: il panic, recover e il defer. Quando uno
   stato di applicazione è _panic_ , l'esecuzione normale viene interrotta, le dichiarazioni di _defer_ vengono
   eseguite e la funzione torna al suo chiamante. _Recover_ di solito è utilizzato all'interno delle dichiarazioni di
   _defer_ e consente all'applicazione di riacquistare il controllo su una routine di panicking e di tornare alla
   normale esecuzione.
   D'altra parte, il logging dettagliato di tutte le operazioni e delle richieste che si sono verificate nel sistema
   aiuta a determinare quali azioni devono essere adottate per proteggere il sistema. Poiché gli aggressori
   tentano di eliminare tutte le tracce delle loro azioni cancellando i registri, è fondamentale che i registri del
   log siano centralizzati.
   Altre azioni:

 gli sviluppatori devono assicurarsi che non siano divulgate
informazioni sensibili nelle risposte di errore, nonché garantire che
nessun gestore di errori persegua informazioni (ad esempio, il debug o
le informazioni sulle tracce di stack).  Il logging deve essere sempre
gestito dall'applicazione e non deve basarsi sulla configurazione del
server. Tutte le registrazioni devono essere implementate da una routine
master su un sistema affidabile e gli sviluppatori devono inoltre
assicurarsi che i dati sensibili non siano soggetti a logging (ad es.
Password, informazioni sulla sessione, dettagli di sistema, ecc.) né che
ci siano informazioni di tracciamento di debug o stack. Inoltre, la
registrazione dovrebbe coprire sia eventi di successo che di insuccesso
in materia di sicurezza.

::

   Il package nativo di Go che contiene le funzioni di logging non supporta livelli distinti di verbosità, il che
   significa che tale feature deve essere implementata a parte. Un altro problema con il logger nativo è che
   non c'è modo di attivare o disattivare il logging per package. Poiché normalmente sono richieste
   funzionalità di logging adeguate per la manutenzione e la sicurezza, a tal fine, si utilizza una libreria di
   registrazione di terze parti come ad esempio:

   - **Logrus** - https://github.com/Sirupsen/logrus
   - **glog** - https://github.com/golang/glog
   - **loggo** - https://github.com/juju/loggo
   Tra queste librerie, la più usata è “ **Logrus** ”.
   Per garantire la validità e l'integrità dei log, deve essere utilizzata come passo aggiuntivo una funzione di
   hash crittografica al fine di prevenire possibili manomissioni dei log.

   ##### 7.12.3.4 Sicurezza del Database .......................................................................................................................................

 Installazione sicura del server di database: o Modificare / impostare
una password per account di root; o Rimuovere gli accounts “root” che
sono accessibili dall'esterno di localhost; o Rimuovere eventuali
account anonimi; o Rimuovere qualsiasi database di prova esistente; 
Rimuovere eventuali stored procedure non necessarie, pacchetti di
utilità, servizi inutili, contenuti del fornitore (ad es. Schemi di
esempio).  Installare il set minimo di funzionalità e opzioni
necessarie per il database, per funzionare con Go.  Disattivare tutti
gli account predefiniti che non sono richiesti nell'applicazione Web per
connettersi al database.

::



   # LINEE GUIDA PER LA CONFIGURAZIONE PER ADEGUARE LA SICUREZZA DEL SOFTWARE DI BASE

   Trasposizione in markdown delle Linee Guida ufficiali reperibili qui https://www.agid.gov.it/it/sicurezza/cert-pa/linee-guida-sviluppo-del-software-sicuro

   TODO: vanno riportate le immagini.

   ## Sommario



   ###### LISTA DELLE TABELLE

   - 1 INTRODUZIONE
      - 1.1 SCOPO
      - 1.2 STRUTTURA DEL DOCUMENTO
      - 1.3 AMBITO DI APPLICABILITÀ
   - 2 RIFERIMENTI
      - 2.1 DOCUMENTI DI RIFERIMENTO
   - 3 DEFINIZIONI E ACRONIMI
      - 3.1 DEFINIZIONI
      - 3.2 ACRONIMI................................................................................................................................................................
   - 4 MINACCE E TIPOLOGIE DI ATTACCO
      - 4.1 CATALOGO DELLE MINACCE
      - 4.2 CATALOGO DELLE TIPOLOGIE DI ATTACCO
   - 5 BEST PRACTICES PER ADEGUARE E MANTENERE LA SICUREZZA DEL SOFTWARE DI BASE
      - 5.1 COMMON BEST PRACTICE
         - 5.1.1 Utenze
            - Utenze tecniche ......................................................................................................................................................................
            - Terze parti ...............................................................................................................................................................................
         - 5.1.2 Autenticazione
         - 5.1.3 Autorizzazione
         - 5.1.4 Crittografia
         - 5.1.5 Documentazione
         - 5.1.6 Logging
         - 5.1.7 Procedure
            - Change management ..............................................................................................................................................................
            - Maintenance ...........................................................................................................................................................................
            - Patching ..................................................................................................................................................................................
            - Secure testing .........................................................................................................................................................................
            - Disposal ...................................................................................................................................................................................
      - 5.2 SICUREZZA DEI SISTEMI OPERATIVI
         - 5.2.1 Architettura
         - 5.2.2 Hardening
         - 5.2.3 Utenze
         - 5.2.4 Autenticazione
         - 5.2.5 Autorizzazione
         - 5.2.6 Crittografia
         - 5.2.7 Documentazione
         - 5.2.8 Logging
         - 5.2.9 Antivirus
         - 5.2.10 Procedure
      - 5.3 SICUREZZA DEL WEB BROWSER
         - 5.3.1 Architettura
         - 5.3.2 Hardening
         - 5.3.3 Autorizzazione
         - 5.3.4 Crittografia
         - 5.3.5 Procedure
         - 5.3.6 Informazioni addizionali
      - 5.4 SICUREZZA DELLE POSTAZIONI DI LAVORO
         - 5.4.1 Architettura
         - 5.4.2 Hardening
      - 5.4.3 Utenze
      - 5.4.4 Autenticazione
      - 5.4.5 Autorizzazione
      - 5.4.6 Crittografia
      - 5.4.7 Documentazione
      - 5.4.8 Logging
      - 5.4.9 Procedure
   - 5.5 SICUREZZA DEI WEB APPLICATION SERVER
      - 5.5.1 Architettura
      - 5.5.2 Hardening
      - 5.5.3 Utenze
      - 5.5.4 Autenticazione
      - 5.5.5 Autorizzazione
      - 5.5.6 Crittografia
      - 5.5.7 Documentazione
      - 5.5.8 Logging
      - 5.5.9 Sessioni
      - 5.5.10 Procedure
      - 5.5.11 Programmazione e Configurazione
   - 5.6 SICUREZZA DEI DBMS/DATABASE SERVER
      - 5.6.1 Architettura
      - 5.6.2 Hardening
      - 5.6.3 Utenze
      - 5.6.4 Autenticazione
      - 5.6.5 Autorizzazione
      - 5.6.6 Crittografia
      - 5.6.7 Documentazione
      - 5.6.8 Logging
      - 5.6.9 Sessioni
      - 5.6.10 Procedure
      - 5.6.11 Informazioni addizionali
   - 5.7 SICUREZZA DEL MAIL SERVER
      - 5.7.1 Architettura
      - 5.7.2 Utenze
      - 5.7.3 Autenticazione
      - 5.7.4 Autorizzazione
      - 5.7.5 Crittografia
      - 5.7.6 Documentazione
      - 5.7.7 Logging
      - 5.7.8 Anti-Phishing
      - 5.7.9 Anti-Spam
      - 5.7.10 Procedure
   - 5.8 SICUREZZA DEI ENTERPRISE SERVICE BUS (ESB)
      - 5.8.1 Architettura
      - 5.8.2 Hardening
      - 5.8.3 Utenze
      - 5.8.4 Autenticazione
      - 5.8.5 Autorizzazione
      - 5.8.6 Crittografia
      - 5.8.7 Documentazione
      - 5.8.8 Logging
      - 5.8.9 Procedure
      - 5.8.10 Informazioni addizionali
   - 5.9 SICUREZZA DEL PACCHETTO MS OFFICE
      - 5.9.1 Hardening
      - 5.9.2 Autorizzazione
         - 5.9.3 Crittografia
         - 5.9.4 Procedure
         - 5.9.5 References and additional information
      - 5.10 SICUREZZA DEL PACCHETTO OPENOFFICE
         - 5.10.1 Hardening
         - 5.10.2 Autorizzazione
         - 5.10.3 Crittografia
         - 5.10.4 Procedure
   - 6 RIFERIMENTI A ISTRUZIONI OPERATIVE E TOOLS DI HARDENING
      - 6.1 ISTRUZIONI OPERATIVE (BENCHMARKS) DI TERZE PARTI
      - 6.2 TOOLS DI HARDENING E BASELINE DI SICUREZZA FORNITE DAI VENDOR
   - Tabella 2 - Documenti di Riferimento Tabella 1 - Documenti Applicabili Errore. Il segnalibro non è definito.
   - Tabella 3 - Definizioni
   - Tabella 4 - Acronimi
   - Tabella 5 Catalogo delle Minacce
   - Figura 1: Scenario - Sicurezza ad ogni livello (fisico, logico e organizzativo) LISTA DELLE FIGURE


   ## 1 INTRODUZIONE

   ### 1.1 SCOPO

   La sicurezza del software di base ed applicativo richiede di stabilire un processo volto ad identificare rischi e
   contromisure di sicurezza ad ogni livello (fisico, logico e organizzativo) del contesto in cui tali software
   operano e sono utilizzati.

   Pertanto, nel fornire delle linee guida per la configurazione sicura di tali software (nel seguito tale attività
   viene spesso indicata con il termine “hardening”), è necessario considerare vari elementi, quali le
   protezioni perimetrali (fisiche e logiche), le architetture di rete (DMZ, segmentazioni, etc.), le procedure
   organizzative (perché dietro alle tecnologie operano le persone), i programmi formativi di “security
   awareness”, ecc.

   Partendo da questo presupposto, il presente documento si pone l’obiettivo di fornire un insieme di
   indicazioni per affrontare e risolvere correttamente le problematiche legate alla sicurezza del software di
   base e di individuare le misure da adottare per difendere ogni componente da possibili minacce accidentali
   e/o intenzionali.

   ### 1.2 STRUTTURA DEL DOCUMENTO

   I paragrafi a seguire entrano nel dettaglio delle singole componenti (software di base, middleware, office
   automation, ecc.) oggetto di approfondita analisi dal punto di vista delle best practice di sicurezza, e per
   ognuna forniscono un elenco delle misure di sicurezza da adottare a fronte delle principali minacce, in
   modo da diminuire l’esposizione ai rischi per la sicurezza delle informazioni e dei servizi erogati.

   Più nel dettaglio il documento è strutturato come segue:

   - Il par. 4.1 contiene un elenco delle minacce alla sicurezza delle informazioni ritenute applicabili nel
       contesto del presente documento.
   - Il par. 4.2 contiene un catalogo delle principali tipologie di attacco rispetto al software di base, al
       middleware e al software applicativo più comune.
   - Il par. 5.1 fornisce un insieme di raccomandazioni generali ‘trasversali’ che realizzano la base
       comune per affrontare le problematiche di sicurezza delle specifiche componenti.
   - Il par. 6 contiene in una prima tabella l’elenco dei riferimenti alle istruzioni operative di hardening
       (o benchmarks) messe a disposizione da enti/istituzioni preposte ed affermate a livello
       internazionale, operanti con il pieno supporto dei rispettivi vendor, e in una seconda tabella
       l’elenco delle baseline di configurazione e di alcuni strumenti software per l’hardening messi a
       disposizione direttamente dai vendor.

   ### 1.3 AMBITO DI APPLICABILITÀ

   Il presente documento si applica alle principali tipologie di software di base, middleware e applicativo in
   uso presso le pubbliche amministrazioni, ed in particolare:

   - Principali Sistemi Operativi UNIX
   - Sistemi operativi Microsoft Windows Server
   - Sistemi operativi Windows Client
   - Web Browser
   - Postazioni di Lavoro
   - Web Application Server


   - DBMS/Data base server
   - Mail Server
   - Enterprise Service Bus
   - Principali applicativi di Office Automation (Microsoft Office e OpenOffice)


   ## 2 RIFERIMENTI

   ### 2.1 DOCUMENTI DI RIFERIMENTO

   **Rif. Codice Titolo**

   DR-1.

   DR-2.

Tabella 1 - Documenti di Riferimento

::


   ## 3 DEFINIZIONI E ACRONIMI

   ### 3.1 DEFINIZIONI

Vocabolo Titolo

::

Tabella 2 - Definizioni

::

   ### 3.2 ACRONIMI................................................................................................................................................................


   |Codice|Titolo|
   |----|-------|
   |AgID|Agenzia per l'Italia Digitale|
   |ASLR|Address Space Layout Randomization|
   |CAR|Committed Access Rate|
   |CE|Contratto Esecutivo|
   |CMDB|Configuration Management Data Base|
   |COM|Component Object Model|
   |COTS|Commercial Of The Shelf|
   |CQ|Contratto Quadro|
   |CRL|Liste di Revoca dei Certificati|
   |CSRF|Cross-site request forgery|
   |CVE|Common Vulnerabilities Exposures|
   |DEP|Data Execution Prevention|
   |DHA|Directory harvest attack|
   |Dmz|De-militarized zone|
   |DoS|Denial of Service|
   |IDS|Intrusion Detection System|
   |IM|Instant Messaging|
   |IPS|Intrusion Prevention System|
   |KRACK|Key Reinstallation Attacks|
   |LDAP|Lightweight Directory Access Protocol|
   |LLF|Low-level formatting|
   |OCSP|Online Certificate Status Protocol|
   |OSVDB|Open Source Vulnerability DataBase|
   |PDL|Postazione di Lavoro|
   |POODLE|Padding Oracle On Downgraded Legacy Encryption|
   |PT|Penetration Test|


   |Codice|Titolo|
   |----|-------|
   |QoS|Quality of Service|
   |RFI|Remote File Inclusion|
   |RTD|Real Time Data|
   |RTI|Raggruppamento Temporaneo di Impresa|
   |SAML|Language Assertion Markup Language|
   |Spim|Instant Messaging Spam|
   |TLS|Transport Layer Security|
   |VA|Vulnerability Assessment|
   |VSTO|Visual Studio Tools per Office|
   |WAF|Web Application Firewall|
   |WOT|Web of Trust|
   |WPA2|Wi-Fi Protected Access versione 2|
   |XACML|EXtensible Access Control Markup Language|
   |XKMS|XML Key Management Specification|
   |XSS|Cross-site scripting|


Tabella 3 - Acronimi

::


   ## 4 MINACCE E TIPOLOGIE DI ATTACCO

   ### 4.1 CATALOGO DELLE MINACCE

   Nel presente paragrafo viene fornito un possibile catalogo delle minacce rispetto alle informazioni e ai
   servizi erogati. L’elenco è stato costruito seguendo le linee guida dettate dallo standard ISO/IEC 27005:
   “Information technology — Security techniques — Information security risk management”, e più in
   generale lo standard ISO/IEC 27001:2013.

   Le minacce sono state individuate e selezionate in base alla loro effettiva applicabilità nel contesto del
   presente documento, escludendo quindi quelle ritenute non applicabili.

   |Id | Minaccia|
   |--|--|
   |M01|Abuso di privilegi da parte dell'utente.|
   |M02|Abuso di risorse.|
   |M03|Accesso non autorizzato ai sistemi (risorse di sistema, configurazioni, interfacce amministrative, ecc.).
   |M04|Accesso non autorizzato alle informazioni.|
   |M05|Attacchi all’integrità dei sistemi (software e configurazioni).|
   |M06|Attacchi all’integrità delle informazioni.|
   |M07|Cancellazione dei log di accountability e/o ripudio di operazioni effettuate.|
   |M08|Cancellazione o furto di informazioni (accidentale o da attacchi come ad es. il ransomware,ecc.).
   |M09|Compromissione delle comunicazioni.|
   |M10|Crittografia debole o non validata.|
   |M11|Divulgazione di informazioni riservate.|
   |M12|Errori di amministrazione dei sistemi.|
   |M13|Falsificazione di identità.|
   |M14|Furto di credenziali di autenticazione.|
   |M15|Generazione e/o gestione inadeguata delle chiavi crittografiche.|
   |M16|Negazione dei servizi.|
   |M17|Tentativi di frode.|
   |M18|Uso non autorizzato di privilegi.|
   |M19|Violazione della sicurezza, rispetto alle politiche di sicurezza dell’organizzazione (es. malware,ecc.)
   |M20|Violazione di leggi, di regolamenti, di obblighi contrattuali.|
   |M21|Danneggiamento, perdita o furto di un asset fisico.|

Tabella 4 Catalogo delle Minacce

::


   ### 4.2 CATALOGO DELLE TIPOLOGIE DI ATTACCO

   Il presente elenco riporta un esteso catalogo di alcune delle più note tipologie (meccanismi) di attacco
   comunemente usate.

   Si sottolinea che i meccanismi di attacco sono sempre in evoluzione e spesso sfruttano vulnerabilità non
   note (i cosiddetti “zero-day”, descritti brevemente nel seguito), per cui un elenco di questo tipo, per sua
   stessa natura, non può ovviamente essere del tutto esaustivo.

   **ID Tipologia Descrizione**

   A01 BIOS rootkit attack 
    Un attacco di rootkit a livello di BIOS, noto anche come attacco
   persistente del BIOS, è un exploit in cui il BIOS viene aggiornato
   con codice dannoso. Il BIOS rootkit è un programma che risiede
   nella memoria fisica non volatile di un computer (in genera una
   EEPROM) e può consentire anche l'accesso e il monitoraggio del
   sistema da remoto.

   ##### A02 Brute Force Attack Si definisce con il termine "Brute
   Force Attack"tratta di un attacco
   basato sul potere computazionale per decifrare le password o
   altre informazioni sensibili, o per “indovinare” password protette
   da hashing e crittografia.

   ##### A03 Buffer overflow
   Si indica con il termine "Buffer overflow"tratta di una tecnica con
   cui un attaccante riesce ad eseguire uno “sfondamento” della
   memoria nel processo del sistema. Le vulnerabilità di buffer
   overflow possono portare ad attacchi di Denial of Service (DoS) o
   iniezione di codice (Code Injection). Un attacco di Denial of
   Service può causare un crash, uno stop o un rallentamento del
   processo; l'iniezione di codice invece, può modificare l'indirizzo di
   esecuzione del processo per eseguire il codice iniettato
   dall'aggressore.

   ##### A04 Cache poisoning
   Il "cache poisoning", anche detto DNS poisoning o DNS cache
   poisoning, consiste nella compromissione di una tabella di
   sistema che memorizza gli indirizzi IP dei server internet dei nomi
   dei ottenuti dal server di dominio (DNS) Internet, sostituendo un
   indirizzo Internet corretto con quello di un altro indirizzosito
   malevolo. Quando un utente Web cerca la pagina con tale
   indirizzonome host, la richiesta viene reindirizzata dalla
   voceall’indirizzo IP malevolofalsificata presente nella tabella
   verso un indirizzo diverso da quello al posto di quello corretto
   reale. A quel punto è possibile che, un un worm, uno spyware o
   un altro malware venga scaricato nel computer dell'utente
   direttamente dall'indirizzo malevolo, oppure è possibile che un
   sito contraffatto catturi le credenziali utente, eventualmente
   ponendosi come intermediario (man-in-the-middle) verso il sito
   legittimo.

   ##### A05 Clickjacking Il
   Clickjacking (noto anche come reindirizzamento dell'interfaccia
   utente e “IFRAME overlay”) è un exploit in cui viene nascosto del
   codice dannoso nel codice dei pulsanti apparentemente innocui o
   di altri contenuti cliccabili presenti in un sito web.

   ##### A06 Clipboard hijacking
   Il "clipboard hijacking" è un exploit in cui l'aggressore ottiene il


   controllo della clipboard della vittima e sostituisce i contenuti lì
   presenti con i propri dati, ad esempio un collegamento ad un sito
   Web dannoso.

   A07 Code injection È un attacco basato sull’inserimento nel codice dell’applicazione
   web di istruzioni, opportunamente modificate da un
   malintenzionato, finalizzate ad esempio, all'impersonificazione di
   un utente autenticato oppure nel furto di reperimento di
   credenziali di accesso.

   ##### A08 Cold boot attack
   Un "cold boot attack" è un processo utilizzato per ottenere
   accesso non autorizzato alle chiavi di crittografia di un computer
   quando questo viene lasciato fisicamente incustodito. I ricercatori
   dell'Università di Princeton, della Electronic Frontier Foundation e
   Wind River Systems hanno scoperto che è possibile portare un
   attacco di questo tipo, dato che i chip di memoria ad accesso
   casuale dinamico (DRAM) conservano i dati per un breve periodo
   di tempo dopo lo spegnimento del computer su cui sono
   installate. Questa quantità di tempo può aumentare se i chip
   vengono rimossi dalla scheda madre e mantenuti a basse
   temperature. Ciò può essere fatto attraverso un raffreddamento
   con una canna invertita ad aria compressa. I chip possono quindi
   essere reinseriti rapidamente in un computer per poi leggerne il
   contenuto.

   ##### A09 Cracking
   Con cracking si intende la modifica di un software per rimuovere
   la protezione dalla copia, oppure per ottenere accesso ad un'area
   altrimenti riservata. Per cracking si intende anche la violazione di
   sistemi informatici collegati ad Internet o ad un'altra rete, allo
   scopo di danneggiarli, di rubare informazioni oppure di sfruttare i
   servizi telematici della vittima (connessione ad Internet, traffico
   voce, sms, accesso a database etc..) senza la sua autorizzazione
   (thiefing).

   ##### A10 Cross-Frame Scripting (XFS) Si tratta di un attacco che combina un codice
   JavaScript malizioso
   con un iframe che carica una pagina legittima allo scopo di rubare
   dati da un utente inconsapevole.
   In genere funziona in combinazione con il social engineering o il
   phishing.
   A titolo di esempio, un attaccante può convincere un utente a
   navigare su una pagina contenente il codice JavaScript e un
   iframe HTML che punta a un sito legittimo. Quando l’utente
   inserisce le credenziali sul sito legittimo, il codice JavaScript ne
   memorizza i caratteri.

   A11 Cross-site request forgery
   (CSRF)

   Un attacco "cross-site request forgery", detto anche brevemente
   CSRF e talvolta pronunciato "Sea-Surf", consiste nell'abuso della
   fiducia tra l'applicazione e un determinato client (la vittima) al
   fine di eseguire una transazione a livello applicativo, pilotata da
   un attaccante utilizzando l'identità del client. L'attacco è basato
   sull'incorporamento di URL, che rappresentano transazioni
   specifiche dell'applicazione di destinazione, all'interno di una
   pagina controllata dall' attaccante, che è già stata acceduta dalla
   vittima tramite browser dopo aver stabilito una relazione di
   fiducia con l'applicazione di destinazione (ad esempio tramite
   l'autenticazione). Esempi di tali richieste includono il
   trasferimento di fondi monetari e titoli, attività di provisioning,
   amministrazione di applicazioni e perfino operazioni di l’acquisto
   di beni e servizi.

   ##### A12 Cross-site scripting (XSS) Esistono 3 tipi di Cross
   Site Scripting:

   - “Reflected”: Il web server legge i dati dannosi (payload di
       attacco) direttamente dalla richiesta HTTP e li rimanda
       (riflette) indietro nella risposta HTTP (Il meccanismo più
       comune per distribuire i contenuti dannosi è quello di
       includerli come parametro in una URL che viene resa pubblica
       o inviata per e-mail direttamente alla vittima).
   - “Stored”: Il web server memorizza i dati dannosi (payload di
       attacco) in un suo archivio. In un secondo momento, i dati
       dannosi vengono letti e inclusi in una risposta http.
   - “DOM based”: A differenza dei due tipi precedenti, i dati
       dannosi (payload di attacco) non vengono inseriti nella
       risposta (a causa di un difetto lato server). L’attacco mira a
       modificare il DOM “environment” all’interno del browser
       della vittima in modo che uno script che gira lato client
       produca un esito diverso da quello atteso (a causa appunto
       della presenza dei dati dannosi che sono stati iniettati nel
       DOM “environment”). Ad esempio, lo script che gira lato
       client usa il “document.location” –ossia l’url- e l’attaccante
       inserisce opportunamente uno script nell’url.

   ##### A13 CSV Injection Questo attacco, noto anche come
   Formula Injection, avviene
   quando un sito web inserisce input malevoli in dati e formule (o
   anche delle macro maliziose) in un file CSV che viene scaricato
   dagli utenti.
   Quando un programma come Excel (o LibreOffice Calc) apre tale
   foglio CSV, “valuta” le formule presenti nelle celle e contenenti
   valori “maliziosi”. Ci sono tre tipi di attacco di questo tipo:
   - quelli che sfruttano le vulnerabilità del foglio elettronico,
   come quella descritta in CVE-2014-3524;
   - quelli che compromettono il computer dell’utente
   sfruttando la tendenza degli utenti a non effettuare
   controlli antivirus e a ignorare gli avvisi di sicurezza sui
   fogli CSV scaricati;
   - quelli mirati al furto di informazioni da altri fogli
   elettronici aperti dall’utente o da qualsiasi file presente
   sul suo computer.

   ##### A1 4 Denial of
   Service È un attacco mirato a che si perpetra portando al limite delle
   prestazioni il funzionamento di un sistema (ad es., un sito web) al
   limite delle prestazioni,(ad es., un sito web) causando il blocco
   del servizio. La variante distribuita (DDoS) si attua, invece,
   generando un numero molto elevato di richieste simultanee da
   parte di più macchine (a volte decine di migliaia) generalmente
   controllati attraverso un malware specifico,
   contemporaneamente dirette tutte al medesimo server, in modo
   da esaurirne le risorse e renderlo non più in grado di erogare i
   propri servizi. Come conseguenza, il server vittima non risulta più
   raggiungibile dall'esterno.



   ##### A1 5 Dictionary Attack
   Con l'attacco Dictionary, un aggressore utilizza un programma per
   l'iterazione di tutte le parole presenti in un dizionario (o più
   dizionari in diverse lingue) e calcola l'hash per ogni parola. L'hash
   risultante viene confrontato con il valore presente nell'archivio
   delle password. Le password deboli come una squadra preferita o
   un'auto preferita, verranno decifrate rapidamente. Le password
   più forti come ad esempio quelle che combinano sequenze di
   caratteri differenti ("? BiolLNessFiNdMeyePasSWir t!"), sono
   meno probabili da decifrare.

   ##### A1 6 Direct
   Dynamic Code
   Evaluation ('Eval Injection')

   L’attacco colpisce gli script che non validano correttamente
   l’input utente usato nel parametro page.
   Un utente remoto può fornire un input una URL opportunamente
   formata, per passare codice arbitrario a un’istruzione eval().

   ##### A1 7
   Directory harvest attack
   (DHA)

   Un attacco "directory harvest" (DHA) è un tentativo di
   determinare gli indirizzi di posta elettronica validi associati a un
   server di posta elettronica in modo tale da poterli aggiungere a
   un database di spam.
   Attraverso un attacco di brute force (a volte più o meno selettivo
   e mirato a una specifica organizzazione/evoluto nella
   composizione degli usernames) indirizzato verso l'e-mail Mail
   Server, il programma DHA alimenta il database di spam secondo il
   seguente criterio: se l'e-mail Mail Server ritorna restituisce un
   messaggio di replica errore di tipo "Not found" allora l'indirizzo
   provato è inesistente e va scartato, se l'e-mail server invece non
   restituisce nulla allora l'indirizzo provato è valido e va aggiunto al
   database.

   ##### A1 8 Drive-by-Downloads attack
   In un attacco "Drive-by-Download", l'applicazione web viene
   modificata (ad esempio iniettando codice HTML) in modo tale da
   istruire il browser del visitatore a scaricare il malware situato nel
   server controllato da un aggressore.
   Spesso, la manomissione non è visibile ai visitatori, quindi le
   vittime innocenti non sono a conoscenza dell'operazione di
   download che avviene in background.
   Pertanto l'attacco "Drive-by-Download" si svolge su 3 fronti:

   - compromissione di un web server legittimo per hostare il
       contenuto malevolo capace di avviare il download sul
       client della vittima o utilizzare, per lo stesso scopo, un
       _third party service_ (ad es. un banner pubblicitario) che il
       web server legittimo (inconsapevolmente) espone;
   - compromissione del client per avviare il download del
       malware vero e proprio;
   - esecuzione del malware sul client.

   ##### A1 9
   Esecuzione arbitraria di
   codice

   Se un utente malintenzionato riesce a eseguire codice dannoso
   sul server, questo può compromettere le risorse del server o
   installare ulteriore software capace di portare attacchi contro i
   sistemi a valle dell'infrastruttura. I rischi derivanti dall'esecuzione
   arbitraria di codice aumentano se il processo server in cui viene
   eseguito il codice dell'attaccante ha privilegi elevati.
   Le vulnerabilità più comuni che consentono l’esecuzione
   arbitraria di codice sono legate a sistemi server mal configurati
   (privi di hardening) o non aggiornati (privi delle patch di
   sicurezza), oppure alla mancata validazione dell’input utente,
   specie in applicazioni scritte in linguaggi in cui la memoria
   dinamica non è gestita automaticamente e l’accesso diretto alla
   memoria tramite puntatori non è impedire da configurazioni
   deboli dell'application server e da server non patchati che
   consentono l'attraversamento di percorsi non protetti (path
   traversal) e attacchi di buffer overflow, entrambi comunque
   possono portare all'esecuzione di codice arbitrario.
   A 20 Format String Attack Questo attacco si verifica quando i dati forniti in input e copiati in
   una stringa vengono in realtà “valutati” come un comando che
   viene eseguito dall’applicazione.
   In tal modo un attaccante può iniettare codice arbitrario, leggere
   lo stack o causare un “segmentation fault”.

   ##### A2 1 Heap Overflow
   Consiste in un tipo particolare di buffer overflow che avviene
   però nell’area di memoria dello “heap”.
   La memoria nello heap è allocata dinamicamente
   dall’applicazione a run-time e tipicamente contiene le strutture
   dati allocate dinamicamente dal programma.
   L’attacco mira a corrompere queste strutture in vari modi, come
   ad es. sovrascrivendole attraverso i relativi puntatori, usati per
   accedere ad indirizzi che vanno oltre la fine di una determinata
   struttura memorizzata.

   ##### A2 2 Heartbleed
   Si tratta di un attacco che sfrutta un bug della libreria
   crittografica fornita da OpenSSL, usata da innumerevoli
   applicazioni, compresi client e server Web, VPN, LDAP(S),
   IMAP(S), SMTP(S), SFTP, RDBMS, ecc.
   La vulnerabilità è dovuta a una impropria validazione dell’input
   da parte della libreria, in particolare nell’estensione TLS
   heartbeat, che comporta un “buffer over-read” in grado di
   esporre la chiave crittografica del server.
   È descritto in CVE- 2014 - 0160.
   A 23 HTML Injection Ll'HTML injection è una tecnica utilizzata per sfruttare input non
   validati al fine di modificare una pagina web fornita da
   un'applicazione web ai propri utenti. Gli aggressori sfruttano il
   fatto che il contenuto di una pagina web è spesso legato ad una
   precedente interazione con gli utenti. Quando l'applicazione non
   riesce a convalidare i dati forniti dall'utente, un utente
   malintenzionato può inviare un testo HTML opportunamente
   modificato per alterare quei contenuti del sito che vengono poi
   presentati ad altri utenti.
   Una query creata ad-hoc può portare all'inserimento nella pagina
   web di elementi HTML controllati dall'attaccante che modificano
   il modo in cui il contenuto dell'applicazione viene esposto sul
   web.

   ##### A24 HTTP response splitting
   Un attaccante passa dati “maliziosi” a una applicazione che non li
   valida e li include immutati in una HTTP Response Header.
   L’applicazione è vulnerabile se consente l’input di caratteri
   contenenti CR (carriage return, ovvero %0d o \r) ed LF (line feed,
   ovvero %0a o \n) nell’header http e se contemporaneamente la
   piattaforma su cui gira il sistema è a sua volta vulnerabile alla
   injection di tali caratteri.

   Con questo attacco l’aggressore ha la possibilità di controllare le
   successive http response dell’applicazione, incluse l’HEADER e il
   BODY, e inoltre di creare altre response a suo piacimento.

   ##### A25 Infezione da malware
   Compromissione di un sistema di elaborazione causata da un
   software malevolo Si intende il malfunzionamento di un sistema
   di elaborazione causato da software che esegue funzioni "nocive"
   (ad esempio, virus, worm, cavalli di Troia).

   ##### A26 Information gathering
   Si indica con il termine "Information gathering tratta di" una
   tecnica mirata a individuare, identificare e caratterizzare i
   dispositivi di rete possono essere scoperti e profilati. Ciò avviene
   attraverso la scansione delle porte. Dopo aver identificato le
   porte aperte, si rilevano i tipi di periferica e si determinano le
   versioni del sistema operativo e delle applicazioni. Con queste
   informazioni, un aggressore può successivamente attaccare le
   vulnerabilità note che potrebbero non essere state risolte con
   patch di protezione.

   ##### A2 7 Integer Overflow
   Un integer overflow avviene quando un’operazione aritmetica
   cerca di calcolare un valore numerico che supera il range che può
   essere rappresentato con un dato numero di bit.
   In tal modo si ottiene un risultato imprevisto che può
   compromettere la stabilità e l’integrità dell’applicazione, laddove
   l’errore non sia intercettato e gestito.

   ##### A2 8 Keylogging
   Un keylogger è uno strumento hardware o software in grado di
   effettuare lo sniffing della registrazione dei caratteri premuti sulla
   della tastiera di un computer, cioè è in grado di intercettare e
   catturare segretamente tutto ciò che viene digitato sulla tastiera
   senza che l'utente si accorga di essere monitorato.

   ##### A2 9 KRACK L’attacco Key Reinstallation
   AttaCK (KRACK), e un attacco di
   “replay” miralo allo standard Wi-Fi Protected Access protocol
   (WPA / WPA2), che si suppone metta in sicurezza le connessioni
   WiFi.
   L’attacco consiste nel resettare ripetutamente il “nonce”
   trasmesso in una specifica fase dell’handshake WPA2,
   consentendo di analizzare e decifrare gradualmente i pacchetti
   attraverso la comparazione con quelli precedenti, fino a ottenere
   la chiave crittografica utilizzata per cifrare il traffico.
   L’attacco sfrutta una vulnerabilità insita nello standard e non in
   specifici prodotti, e colpisce tutti i principali sistemi operativi
   compresi quelli usati da smartphone e tablet.
   Particolarmente grave è il fatto che sui sistemi linux-based, il
   client wpa-supplicant usato per connettersi alla rete WiFi con il
   WPA2 consente addirittura l’inserimento di una chiave “nulla”.

   ##### A30 LDAP Injection L'LDAP
   Injection è un tipo di attacco portato verso
   un'applicazione web dove gli hacker introducono del codice
   malevolo in un campo di input dell'interfaccia utente nel
   tentativo di ottenere accesso a informazioni non autorizzate.
   L'LDAP Injection utilizza i dati forniti nella richiesta proveniente
   dal client, nella costruzione di istruzioni LDAP (Lightweight
   Directory Access Protocol), quando questi non vengono
   controllati e validati al fine di rimuovere codice potenzialmente
   dannoso. Quando un'applicazione web non applica adeguati


   controlli sull'input fornito dall'utente, gli hacker possono essere
   in grado di modificare la costruzione di un'istruzione LDAP che
   verrà poi eseguita con le stesse autorizzazioni del componente
   destinato all'esecuzione del comando.
   Un LDAP Injection può causare seri problemi di protezione se le
   autorizzazioni consentono di interrogare, modificare o rimuovere
   qualsiasi cosa oggetto presente all'interno dell'albero LDAP.

   A3 1 Man-in-the-browser È un attacco simile al man-in-the-middle, ma agisce all’interno del
   browser utente.
   Generalmente è basato su un “Trojan Horse” che si installa nel
   browser per intercettare e manipolare richieste e risposte http.
   Spesso questa tecnica è usata da malware mirati a specifici siti di
   Home Banking, in grado di rubare denaro modificando “al volo”
   le transazioni finanziarie (es. i bonifici).
   Il malware può insediarsi nei “Browser Helper Objects” di
   Internet Explorer (librerie caricate dinamicamente all’avvio del
   browser), nelle Estensioni dei browser più recenti o attraverso
   “API-Hooking” in un eseguibile o una libreria DLL, o ancora
   tramite Javascript (ad es. attraverso uno “worm” basato su Ajax).

   ##### A3 2 Man-in-the-middle
   Questo attacco consiste nell’intercettare la comunicazione tra
   due sistemi ponendosi in mezzo e fingendo con ciascuno degli
   interlocutori di essere l’altro.
   Ad es. in una connessione http l’attaccante spezza la connessione
   originale in due parti: una connessione dal client a sé stesso
   (fingendosi il server) e una da sé stesso al server (fingendosi il
   client), inoltrando dopo averle intercettate ed eventualmente
   manipolate, le richieste del client al server e le risposte del server
   al client.

   ##### A3 3
   Manipolazione dei campi di
   Form

   I valori dei campi presenti in una form HTML vengono inviati in
   chiaro al server utilizzando il protocollo HTTP POST. Ciò può
   includere campi di form visibili e nascosti. Indipendentemente
   dalla tipologia, questi campi possono essere facilmente modificati
   ignorando le routine di convalida lato client. Di conseguenza, le
   applicazioni che si basano sui valori di input di un campo di una
   form per prendere decisioni di sicurezza lato server sono
   vulnerabili all'attacco in oggetto.

   ##### A34 Manipolazione dei Cookie I cookie sono suscettibili a modifiche da parte del client.
   Ciò è
   vero sia per i cookie persistenti che per quelli che risiedono in
   memoria. Sono disponibili diversi strumenti per supportare un
   aggressore nella modifica del contenuto di un cookie. residente in
   memoria. La manipolazione del cookie è l'attacco che si riferisce
   alla modifica di un cookie, si effettua di solito per ottenere un
   accesso non autorizzato ad un sito Web.

   A35 Manipolazione della Query
   String

   Gli utenti possono facilmente manipolare i valori della stringa di
   query passati tramite HTTP GET da client a server in quanto
   vengono visualizzati nella barra degli indirizzi URL del browser
   Web. Se l'applicazione si basa su valori della stringa di query per
   prendere decisioni di sicurezza o se i valori rappresentano dati
   sensibili o parametri critici di una transazione come importi
   monetari, l'applicazione è vulnerabile all'attacco in oggetto.

   ##### A36 Manipolazione 
   Le headers HTTP passano le informazioni tra il client e il server. Il


   dell'intestazione HTTP client costruisce le headers di richiesta mentre il server costruisce
   le headers di risposta.
   Se l'applicazione si basa sulle headers di richiesta per prendere
   una decisione, questa allora essa è vulnerabile all'attacco in
   oggetto.

   ##### A37 Memory dump attack
   Un attacco di dump di memoria consiste nella cattura e
   nell'utilizzo di contenuti RAM che sono stati scritti su un'unità di
   memorizzazione durante un errore irreversibile (a scopo di
   diagnostica), tipicamente innescato dall'attaccante.

   ##### A38 Path Manipulation 
   Simile alla Resource Injection, salvo che si focalizza sul re-
   indirizzamento verso risorse di file system locali al server,
   forzandolo a caricare risorse diverse da quelle previste.

   ##### A39 Path traversal
   Accesso alla struttura del file system non di pertinenza
   dell'applicativo web. Un aggressore avendo accesso alla gerarchia
   del file system (ad es. mediante la notazione "../") potrebbe
   prelevare informazioni riservate all'interno della struttura di file e
   cartelle esterne all'applicazione.

   ##### A40 Pharming
   Il phishing ed il pharming sono due tecniche utilizzate per
   ottenere l'accesso a informazioni personali o riservate. Nel
   primo caso un utente incauto viene indotto, tramite tecniche di
   social engineering, ad accedere ad un sito web contraffatto in
   modo tale da sembrare ufficiale ed a inserirvi dati personali e/o
   sensibili.
   Nel secondo caso, l'utente viene reindirizzato automaticamente,
   tramite alterazione delle richieste DNS (che possono coinvolgere
   direttamente il DNS server o la PdL vittima tramite l'installazione
   di trojan) al sito web contraffatto anche nel caso in cui digiti nel
   browser l'indirizzo corretto del server autentico.

   ##### A41 Phishing
   Per "phishing" si intende un qualsiasi tentativo (per telefono, e-
   mail, messaggistica immediata o fax) di ottenere informazioni di
   identificazione personale a scopo di furto di identità. Un tipico
   attacco di phishing elettronico comprende due componenti: un
   messaggio e-mail dall’aspetto autentico e una pagina web
   fraudolenta. I collegamenti web inclusi in questi messaggi e-mail
   quasi sempre hanno l’aspetto e il funzionamento dei siti legittimi
   copiati, rendendo la frode quasi impossibile da rilevare.

   ##### A42 POODLE attack 
   Il POODLE (Padding Oracle On Downgraded Legacy Encryption) è
   una vulnerabilità che riguarda la sicurezza di una vecchia versione
   del protocollo SSL, la 3.0., che potrebbe essere sfruttata per
   intercettare i dati in transito fra client e server. La vulnerabilità,
   rivolta al lato client e non a quello server, potrebbe ad esempio
   consentire a un utente malintenzionato di decifrare i cookie che
   corrispondono a servizi come Twitter o Google, per entrare negli
   account degli utenti senza la necessità di conoscere la password
   di accesso.
   Il protocollo SSL 3.0, così come utilizzato in molti prodotti (es.
   OpenSSL 1.0.1i), usa un padding CBC non deterministico che
   consente a un attacco di tipo man-in-the-middle di decifrare
   facilmente i dati trasmessi utilizzando un attacco "padding-
   oracle".
   Il protocollo TLS (Transport Layer Security) ha largamente


   sostituito il protocollo SSL per la comunicazione sicura su
   Internet, ma molti browser tornano ad utilizzare SSL 3.0 quando
   non è disponibile una connessione TLS. Un aggressore che vuole
   sfruttare il POODLE approfitta di questa vulnerabilità inserendosi
   nella sessione di comunicazione e costringendo il browser a
   utilizzare SSL 3.0.

   ##### A4 3
   Privilege horizontal escalation
   attack

   Un attacco di "privilege escalation" è un tipo di intrusione di rete
   che sfrutta gli errori di programmazione o i difetti di
   progettazione per concedere all'attaccante un accesso
   privilegiato alla rete, ai dati e alle applicazioni ad essa associati.
   Nel caso di "horizontal esclation", per "accesso privilegiato" si
   intende un accesso nel quale un utente con certi privilegi accede
   alle funzioni e/o contenuti riservati a un altro utente che gode
   degli stessi privilegi.

   A44 Privilege vertical escalation
   attack

   Un attacco di "privilege escalation" è un tipo di intrusione di rete
   che sfrutta gli errori di programmazione o i difetti di
   progettazione per concedere all'attaccante un accesso
   privilegiato alla rete, ai dati e alle applicazioni ad essa associati.
   Nel caso di "vertical escalation", per "accesso privilegiato" si
   intende un accesso più alto di quello previsto dall'amministratore
   o dallo sviluppatore dell'applicazione.

   ##### A45 Proxy hijacking attack
   Il "proxy hijacking" è una tecnica di attacco in cui unil codice
   malevolo non installa un malware ma configura il browser sul
   sistema dellala macchina vittima per usare un web proxy
   controllato dall'attaccante. Oltre a eseguire il deploy dei proxy
   settings fraudolenti, l'attacco installa un "self-signed root
   certificate" sul sistema in modo che gli attaccanti possano leggere
   il traffico HTTPS che passa attraverso il proxy server fraudolento
   (man-in-the-middleMITN Attack). Tipicamente l'attacco parte da
   spam email con un attachment malevolo che esegue le
   operazioni di cui sopra.

   ##### A46 Remote File Inclusion (RFI)
   Il "Remote File Inclusion (RFI)" è un attacco che punta ad un
   server di computer su cui sono in esecuzione siti e applicazioni
   web. Gli exploit RFI sono spesso attribuiti al linguaggio di
   programmazione PHP utilizzato da molte grandi aziende, tra cui
   Facebook e SugarCRM. Tuttavia, l'RFI può manifestarsi in altri
   ambienti ed è stato infatti introdotto inizialmente come "SHTML
   injection". RFI funziona sfruttando applicazioni che
   dinamicamente fanno riferimento a script esterni indicati da
   input dell'utente, senza adeguati controlli. Di conseguenza,
   l'applicazione può essere istruita per includere uno script ospitato
   su un server remoto e quindi eseguire codice controllato da un
   utente malintenzionato. Gli script eseguiti possono essere
   utilizzati per il furto temporaneo o l’accesso non autorizzato ai
   dati, la loro manipolazione o anche la loro sottrazione, per una
   acquisizione dati a lungo termine.

   ##### A47 Resource Injection
   Questo attacco consiste nel modificare il tipo o l’identificatore di
   una risorsa usato da un’applicazione, attraverso un input non
   validato i cui caratteri sono usati dall’applicazione vulnerabile per
   determinare la risorsa da accedere (es. un nome file su uno share
   remoto, una porta TCP/IP, una URL, ecc.).


   In tal modo l’attaccante forza il server a caricare una risorsa
   arbitraria dalla rete, potenzialmente contenente codice dannoso,
   che in alcuni casi può essere persino memorizzato sul server ed
   essere inviato ad altri utenti.

   ##### A48 SEO poisoning attack
   Il "SEO poisoning", noto anche come "search poisoning", è un
   metodo di attacco in cui i cyber criminali creano siti web dannosi
   e utilizzano tattiche di ottimizzazione dei motori di ricerca per
   renderli prominenti nei risultati della ricerca. Tali siti vengono
   associati a termini presumibilmente utilizzati nella ricerca da un
   numero elevato di persone in un dato momento, ad esempio frasi
   correlate a festività, news e video virali. Secondo i Websense
   Security Labs, in questi casi, fino ad un quarto della prima pagina
   dei risultati della prima pagina della ricerca, questi possono
   essere collegati a siti web dannosi. Gli aggressori creano siti web
   con nomi e descrizioni associate a temi popolari o ad argomenti
   di tendenza. Ad esempio, nelle settimane precedenti a
   Halloween, gli aggressori potrebbero attivare siti che offrono
   modelli gratuiti per i costumi di Halloween. Tuttavia, il vero scopo
   è quello di infettare i visitatori con malware o accedere in modo
   fraudolento a informazioni sensibili da utilizzare poi per il furto di
   identità.

   ##### A49 Sfruttamento delle sessioni
   Ogni applicazione web che si avvale di un meccanismo di login
   autenticazione, basato sul logon gestisce delle sessioni con le
   quali tracciare l’utente, che si attua con l'assegnazione di un
   token (ad es. un cookie, un parametro di sessione) univoco.
   L'attacco si perpetra dopo aver determinato il funzionamento
   dell'algoritmo di generazione del token e, in genere, comporta la
   sostituzione di identità, dando all'aggressore l'opportunità di
   accedere all'applicazione web poiché da essa ritenuto un utente
   accreditato.

   ##### A50 Shellcode
   Uno shellcode è un programma in linguaggio assembly che
   tradizionalmente esegue una shell, come la shell Unix '/bin/sh'
   oppure la shell “command.com” sui sistemi operativi DOS e
   Microsoft Windows. Uno shellcode può essere utilizzato per
   sfruttare un bug mediante un exploit, consentendo ad un hacker
   o un crackemalintenzionator di acquisire l'accesso alla riga di
   comando di un computer, o più in generale di eseguire codice
   arbitrario.

   ##### A51 Spam
   Il termine "spam" descrive una comunicazione non sollecitata
   (inviata per e-mail o messaggi/chat immediata) e destinata al
   lucro commerciale. Il termine spam comprende un’ampia gamma
   di attività, molte delle quali sono dannose (come la distribuzione
   di e-mail di phishing). Una variante di tale attacco è lo spam per
   immagini (spam in cui il messaggio è testo sotto forma di
   immagine, anziché testo effettivo) come mezzo usato per
   evadere il rilevamento.

   A52 Spim
   (Instant Messaging Spam)

Lo Spim è una forma di spam distribuito tramite messaggistica istantanea
(IM) anziché tramite messaggistica di posta elettronica. Anche se meno
diffuso rispetto alla sua controparte di posta elettronica, lo Spim sta
raggiungendo sempre più utenti. l'IM è un canale particolarmente adatto
per gli spammer. Per

::


   prima cosa, l'immediatezza nello scambio di messaggi fornita
   dall'IM rende probabilmente gli utenti meno riflessivi nel cliccare
   sui link. Inoltre, con il fatto che l'IM bypassa il software antivirus e
   i firewall, questo rappresenta un mezzo facile per passare non
   solo messaggi commerciali, ma anche virus e altri malware.

   A53 SQL injection "SQL injection" è una tecnica di hacking che mira a colpire le
   applicazioni web connesse ad un database di tipo SQL. Tale
   attacco sfrutta l'inefficienza dei controlli sui dati ricevuti in input
   ed inserisce codice maligno all'interno di una query SQL. La
   tecnica permette al malintenzionato di autenticarsi con ampi
   privilegi in aree protette dell'applicazione e di visualizzare e/o
   alterare dati sensibili.
   A 54 Stack overflow Lo stack overflow si verifica quando il puntatore di stack di
   chiamata, supera lo spazio di memoria associato allo stack. Lo
   stack delle chiamate può occupare uno spazio di memoria di
   dimensioni ridotte, in genere questa spesso viene determinata
   all'avvio del programma. La dimensione dello stack di chiamata
   dipende da molti fattori, tra cui il linguaggio di programmazione,
   l'architettura della macchina, il multi-threading e la quantità di
   memoria disponibile. Quando un programma tenta di utilizzare
   più spazio di quanto non sia disponibile nello stack di chiamata
   (ovvero quando tenta di accedere alla memoria oltre i limiti dello
   stack di chiamata, che è essenzialmente un buffer overflow), si
   parla di overflow dello stack, che porta al crash del programma.
   Questo si verifica in genere in caso di errori di programmazione
   quali la ricorsione infinita o l’uso di variabili di stack troppo
   grandi.

   ##### A55 XPath Injection
   XPath è un linguaggio di query che consente di accedere a
   qualsiasi parte di un documento XML senza alcuna restrizione nel
   controllo di accesso (chi può accedere a cosa).
   Con un attacco di XPATH Injection, un malintenzionato può
   modificare una query XPATH per eseguire un’azione differente da
   quella prevista.
   La XPath Injection può essere usata per estrarre da
   un’applicazione dati forniti dagli utenti memorizzati in modo non
   sicuro.
   Questo può avvenire se l’applicazione non valida correttamente
   l’input usato per comporre una query XPATH.

   ##### A56 Zero-day exploit
   Un exploit "zero-day" consiste nello sfruttamento di una
   vulnerabilità di sicurezza nello stesso giorno in cui questa
   generalmente diventa nota. Ci sono zero giorni tra il momento
   della scoperta della vulnerabilità e il primo attacco.
   Normalmente, quando qualcuno rileva che un programma
   software contiene un potenziale problema di sicurezza, la
   persona o l'azienda notificano il problema riscontrato alla società
   che ha realizzato il software (e talvolta al mondo in generale) in
   modo da poter intraprendere azioni di correzione. Passa del
   tempo prima che, la società che ha realizzato il software, possa
   correggere il codice e distribuire una patch o un aggiornamento
   software. Anche se potenziali aggressori sono a conoscenza della
   vulnerabilità, potrebbe essere necessario un certo tempo per


   poterla sfruttare a loro vantaggio. Nel frattempo, si spera che la
   soluzione di correzione sia disponibile prima che ciò avvenga.


   ## 5 BEST PRACTICES PER ADEGUARE E MANTENERE LA SICUREZZA DEL SOFTWARE DI BASE

   L’ apertura delle applicazioni verso fornitori, clienti, utenti remoti e mobili ha comportato la scomparsa di
   un perimetro aziendale definito e un’estrema diversificazione delle minacce. In questo nuovo scenario, le
   applicazioni sono diventate il **principale vettore di attacco** ed è sempre più difficile proteggerle. Lo studio
   presentato nel **_Rapporto OAD_**^1 **_2017_** sugli attacchi applicativi in Italia, evidenzia come **principale causa
   degli attacchi** applicativi, sono le **vulnerabilità** delle infrastrutture ICT, del software di base e dei
   middleware usati dalle applicazioni (circa il 37%). Seguono poi le **vulnerabilità intrinseche all'applicativo**
   stesso quali, ad esempio, quelle dei sistemi di identificazione, autenticazione e controllo degli accessi.

Figura 1: Scenario - Sicurezza ad ogni livello (fisico, logico e
organizzativo)

::

   ### 5.1 COMMON BEST PRACTICE

   Si forniscono nel seguito un insieme di raccomandazioni generali ‘trasversali’ che realizzano la base comune
   per affrontare le problematiche di sicurezza delle specifiche componenti.

   Ogni argomento è strutturato in un paragrafo contenente una o più tabelle.

   (^1) Osservatorio Attacchi Digitali –
   https://www.malaboadvisoring.it/index.php?option=com_content&view=article&id=126:rapporto-2017-oad-attacchi-agli-
   applicativi-in -italia-&catid=13:oci-ed-oai-&Itemid=127


   Ciascuna tabella riporta una problematica di sicurezza, le minacce che possono determinarla o comunque
   applicabili, e le contromisure generali suggerite per farvi fronte.

   #### 5.1.1 Utenze

   **Registrazione / Cancellazione utenti
   Minaccia** Abuso di privilegi da parte dell'utente.

   **Contromisure**  Definire, per ogni sistema/piattaforma, un processo di registrazione/cancellazione
   degli utenti ai quali deve essere concesso/revocato un account. Il processo deve
   prevedere almeno:

   - l'uso di User ID individuali in modo che gli utenti possano essere resi responsabili
       delle proprie azioni. L'uso dell'ID di gruppo dovrebbe essere permessa solo per
       esigenze aziendali od operative previa approvazione e produzione della
       documentazione di supporto;
   - la verifica che il livello di accesso richiesto sia in linea con il principio del "need to
       know";
   - l'obbligo di disabilitare o rimuovere immediatamente le UserId degli utenti che
       hanno cessato il rapporto di lavoro;
   - la verifica periodica (almeno trimestrale) dell'assenza di account inconsistenti,
       ridondanti o obsoleti e la loro eliminazione.

   **Assegnazione e revoca dei diritti di accesso degli utenti
   Minaccia** Abuso di privilegi da parte dell'utente.

   **Contromisure**  Definire un processo che disciplini l'assegnazione e la revoca dei diritti di accesso
   dell'utente, identificato con UserId personale. L’accesso a ogni sistema/piattaforma da
   parte di persone fisiche deve essere soggetto a:

   - autenticazione, in modo univoca attraverso un identificativo personale (es.
       username o UserId) e credenziali private (es. password, PIN, token);
   - autorizzazione, nei limiti del principio del need-to-know ovvero attribuire il
       privilegio minimo necessario per svolgere l'attività lavorativa;
   - registrazione di tutti i diritti di accesso assegnati al sistema/piattaforma, in un
       sistema di anagrafica centralizzato. Verificare che il livello di accesso consentito sia
       coerente con le politiche di accesso e con il principio di separazione dei compiti.
   - i profili di accesso devono essere costantemente aggiornati;
   - eventuali deroghe ai criteri di assegnazione/revoca dei diritti di accesso
       dovrebbero essere limitate, registrate e approvate almeno dai responsabili del
       sistema/piattaforma e dai responsabili funzionali.

   **Autorizzazione all'assegnazione dei diritti di accesso privilegiato
   Minaccia** Abuso di privilegi da parte dell'utente.

   **Contromisure**  L’assegnazione dei diritti di accesso privilegiato dovrebbe essere controllata attraverso
   un processo di autorizzazione che preveda:

   - l'identificazione dei diritti di accesso privilegiato relativi al sistema/piattaforma e gli
   utenti a cui è necessario assegnarli; applicazione principio della _segregation of duty_ nel
   processo autorizzativo;
   - una registrazione di tutti i privilegi assegnati;
   - i requisiti per la scadenza dei diritti;
   - riesame regolare delle competenze degli utenti;
   - per le UserId amministrative generiche (da evitare se non indispensabile per

l'esecuzione del servizio), dovrebbe essere mantenuta la riservatezza
delle informazioni segrete di autenticazione quando questa è condivisa.

::

   **Riesame dei diritti di accesso degli utenti
   Minaccia** - Accesso non autorizzato alle informazioni.

   - Abuso di privilegi da parte dell'utente.

   **Contromisure**  I diritti di accesso degli utenti dovrebbero essere riesaminati regolarmente (al massimo
   ogni sei mesi) e dopo ogni cambiamento (es. cessazione del rapporto di lavoro, cambio
   di ruolo, di mansione, all'interno dell'organizzazione). Le autorizzazioni per i diritti di
   accesso privilegiati dovrebbero essere riesaminate ad intervalli più frequenti e gli
   eventuali cambiamenti tracciati. Per ogni cambiamento di privilegi deve esserne
   registrato il richiedente, l’approvatore e la motivazione.
   In caso di cessazione del rapporto di lavoro, sia di personale interno sia esterno, è
   necessario verificare i requisiti per la rimozione, o sospensione dei diritti di accesso al
   sistema/piattaforma. Tali diritti dovrebbero essere ridotti o rimossi prima della
   cessazione o della variazione del rapporto di lavoro, a seconda della valutazione di
   fattori di rischio come:
   - criticità delle informazioni cui si accedeva;
   - ruolo della persona,
   - motivazione della cessazione/cambiamento.

Prevedere controlli o misure di sicurezza per limitare il rischio che:

::

   - in caso di licenziamento o fine contratto, dei dipendenti scontenti o degli utenti di
       terze parti esterne possano deliberatamente corrompere informazioni o
       commettere illeciti;
   - in caso di persone dimissionarie o in uscita, esse possano essere tentate di
       recuperare/copiare informazioni per uso futuro.

   ##### Utenze tecniche ......................................................................................................................................................................

   **Protezione delle informazioni strumentali all'accesso
   Minaccia** - Divulgazione di informazioni riservate.

   - Accesso non autorizzato ai sistemi (risorse di sistema, configurazioni, ecc.).
   - Furto di credenziali di autenticazione.

   **Contromisure**  - Utilizzare ACL forti per proteggere le risorse di sistema.
   - Utilizzare algoritmi standard di crittografia per memorizzare i dati sensibili nei file
   di configurazione (utenze tecniche, non legate a persone fisiche: processi di
   sistema, porzioni di DB, ecc.).
   - Utilizzare algoritmi di comprovata robustezza come, ad esempio, TDES e AES. E
   avere cura che la lunghezza della chiave di cifratura dell'algoritmo adottato (128,
   192 o 256 bit) sia commisurata al livello di riservatezza delle informazioni da
   proteggere.

   ##### Terze parti ...............................................................................................................................................................................

   **Identificazione dei requisiti di sicurezza per l'accesso di fornitori/clienti ad informazioni o beni aziendali
   Minaccia** Violazione della sicurezza, rispetto alle politiche di sicurezza dell’organizzazione, ad
   opera di soggetti esterni.

   **Contromisure**  Devono essere considerati e identificati tutti i requisiti di sicurezza prima di concedere
   ai partners, fornitori/clienti, anche in fase di trattativa, l'accesso a informazioni o beni
   dell'organizzazione ospitati nel sistema/piattaforma. Effettuare un'analisi dei rischi per

valutare l'impatto sul business aziendale (a livello economico,
d'immagine, di continuità operativa, eccetera) nel caso di violazioni
della sicurezza, divulgazione non autorizzata (es. a concorrenti),
illecito trattamento delle informazioni, effettuati da tali soggetti che
accedono ad informazioni.

::

   **Identificazione dei requisiti di sicurezza negli accordi con i fornitori/clienti
   Minaccia** Violazione della sicurezza, rispetto alle politiche di sicurezza dell’organizzazione,
   ad opera di soggetti esterni.

   **Contromisure**  Gli accordi con terze parti che prevedono accesso, elaborazione, comunicazione,
   aggiunte o, in generale, gestione delle informazioni ospitate nel
   sistema/piattaforma dell'organizzazione, devono considerare tutti i requisiti di
   sicurezza pertinenti.
   Prevedere, in particolare, misure preventive per evitare violazioni o illeciti delle
   terze parti nella gestione delle informazioni.
   Definire con precisione le attività, le modalità, le responsabilità e la periodicità, per
   l'esercizio di diritti di audit o comunque di verifiche sull’attività dei fornitori/clienti.
   Gli accessi logici privilegiati da parte di soggetti esterni devono essere subordinati
   alla nomina di tali soggetti ad amministratori di sistema, e tale nomina deve essere
   a sua volta legata ad uno specifico contratto con la ditta di appartenenza
   comprendente accordi di riservatezza e regole per il corretto uso delle risorse
   informatiche vincolanti per il fornitore e per i suoi dipendenti. Ovviamente gli
   accessi logici devono essere monitorati da parte di fornitori devono essere
   completamente monitorati.
   In ogni caso gli accessi privilegiati da parte di soggetti esterni non devono mai
   avvenire da sedi esterne (es. sede fornitore).

   #### 5.1.2 Autenticazione

   **Gestione delle informazioni segrete di autenticazione degli utenti
   Minaccia** Accesso non autorizzato alle informazioni

   **Contromisure**  L'assegnazione agli utenti delle informazioni segrete di autenticazione (es. password)
   deve essere controllata attraverso un processo di gestione. Il processo dovrebbe
   prevedere:

   - l’uso di user ID e password individuali per sostenere il principio di accountability;
   - le modalità di assegnazione temporanea delle informazioni segrete di
       autenticazione, da cambiare al primo uso;
   - procedure per verificare l'identità di un utente, prima di fornire, modificare o
       sostituire nuove informazioni;
   - le modalità per assicurare il rispetto dell'utente della riservatezza delle
       informazioni segrete di autenticazione. Per quest'ultimo punto l'organizzazione
       dovrebbe informare l'utente delle sue responsabilità ed acquisire dallo stesso un
       formale impegno a mantenere riservate le informazioni (ad es. mediante specifica
       lettera da sottoscrivere).

   **Criteri per l'autenticazione mediante password
   Minaccia** - Accesso non autorizzato alle informazioni.

   - Furto di credenziali di autenticazione (ad es. con attacchi in grado di sfruttare
       l’eventuale inadeguatezza delle password).
   - Uso non autorizzato di privilegi (ad es. mediante tecniche di “escalation” verticali


   su un target o orizzontali).

   **Contromisure**  Configurare le funzioni di controllo della qualità delle password per l'accesso ai sistemi,
   affinché la composizione rispetti i criteri di lunghezza, complessità e univocità
   necessari per avere una robustezza elevata. Ovvero, la password:

   - deve essere composta da un numero crescente di caratteri (almeno 8) in funzione
       della criticità delle informazioni da difendere (es. 15 caratteri per utenze
       amministrative);
   - deve contenere caratteri di almeno tre delle quattro categorie seguenti:
       a. lettere maiuscole dell'alfabeto latino (dalla A alla Z);
       b. lettere minuscole dell'alfabeto latino (dalla a alla z);
       c. numeri in base 10 (da 0 a 9);
       d. caratteri speciali non alfanumerici, ad esempio punto esclamativo (!);
   - non si deve riferire a qualcosa che qualcun altro possa facilmente indovinare od
       ottenere utilizzando informazioni relative alla persona (ad esempio: nomi, numeri
       di telefono e date di nascita, etc.);

Inoltre devono essere rispettate le seguenti regole:

::

   - Vietare nomi di account predefiniti e rinominare account standard come, ad
       esempio, l'account amministratore;
   - Non mostrare a video la password (ma neanche PIN, passphrase, ecc., in generale:
       chiavi segrete) quando viene inserita e non dare indicazioni sulla sua lunghezza;
   - La password temporanea deve essere obbligatoriamente cambiata al primo log-on;
   - Deve essere forzato per tutti gli utenti, e particolarmente per gli amministratori, il
       cambiamento periodico della password;
   - La procedura di cambiamento della password deve impedire il riutilizzo di tutte le
       password precedentemente utilizzate e includere una procedura efficace che
       tenga conto di errori di inserimento;
   - Limitare il numero di tentativi consentiti in un determinato periodo di tempo o,
       alternativamente, effettuare il blocco dell'account per l'accesso da parte degli
       utenti finali dopo un determinato numero di tentativi;
   - Non consentire l’accesso fino a quando il processo di log-on sia stato completato
       con successo;
   - Convalidare le informazioni del log-on solo al completamento di tutti i dati di input.
       Se una condizione di errore si presenta, il sistema non deve indicare quale dato è
       corretto o incorretto;
   - Limitare il tempo entro il quale la procedura di log-on deve ultimarsi. In caso di
       eccesso, la procedura deve terminare;
   - Considerare di visualizzare le informazioni seguenti a valle di log-on con successo:
       a. data e ora del precedente log-on di successo;
       b. dettagliare ogni tentativo di log-on di insuccesso dall’ultimo log-on di
          successo;
   - La persistenza e la trasmissione delle password deve avvenire in modo protetto.
       Per quanto concerne la persistenza, la forma “hash salted” rappresenta la best
       practices;
   - Per contrastare la possibilità fornita dalla cache del browser nel consentire
       l'accesso, implementare un criterio che consente all'utente di scegliere di non
       salvare le credenziali o di forzare tale criterio come predefinito;
   - Tracciare sia gli accessi riusciti sia i tentativi di accesso falliti;
   - Eseguire l'Audit degli accessi non andati a buon fine per rilevare tentativi di
       hacking delle password;
   - Controllare e validare sempre l’indirizzo IP sorgente del client usato dall’utente:

a. Se l'applicazione è destinata alla sola intranet, impedire accessi
   provenienti da indirizzi IP esterni alla propria LAN;

b. Se l'applicazione è destinata ad utenti Internet ma la connessione
   arriva da IP esteri, prevedere un livello di controllo maggiore (es.
   una convalida via SMS su un numero di cellulare italiano, oppure più
   in generale per applicazioni critiche l'uso di meccanismi di
   autenticazione a due fattori);

c. Se l'applicazione è destinata ad utenti Internet italiani, quando
   risulti tecnicamente fattibile si dovrebbe rilevare e impedire
   l'eventuale accesso da IP esteri basato su un servizio di Proxy
   Server situato in Italia. Tali requisiti dovrebbero essere
   periodicamente riesaminati per mantenere o rendere più sicura la
   password.

::


   **Altri criteri per l'autenticazione
   Minaccia** Accesso non autorizzato alle informazioni.

   **Contromisure**  La password costituisce la protezione minima obbligatoria per tutti gli accessi logici che
   richiedono l’identificazione dell’utente.
   Forme alternative più robuste di autenticazione quali one-time password o
   autenticazione forte a due fattori detta anche 2FA (pine e token o pin e impronta
   biometrica) o a tre fattori (pin, token e biometria) devono essere utilizzate per gli
   accessi amministrativi e per l’accesso a dati e sistemi critici secondo un approccio
   basato sull’analisi dei rischi.
   Per semplificare l’adozione dei meccanismi di autenticazione forte è possibile adottare
   soluzioni basate su sistemi gatekeepers che permettono di intermediare l'accesso
   privilegiato ai sistemi target senza che su di essi sia necessario alcun intervento.
   Per sistemi isolati o in ambiti IT ristretti, è opportuno preferire l'amministrazione di
   sistema esclusivamente attraverso l’accesso fisico locale al sistema, restringendo la
   possibilità di accesso remoto al minimo.
   In contesti più estesi la gestione remota è in genere indispensabile; in tal caso, a causa
   della sensibilità dei dati passati sulle interfacce amministrative, è necessario utilizzare
   canali crittografati, ad esempio, con tecnologia VPN o SSL, e nel caso del Remote
   Desktop di Windows è necessario abilitare la crittografia del protocollo RDP.
   Per ridurre ulteriormente il rischio, va considerato anche l'impiego di politiche IPSec
   per limitare la gestione remota dei computer collegati nella rete interna.
   In tutti i casi, il numero delle interfacce di amministrazione deve essere ridotto al
   minimo, disabilitando quelle non in uso.

   **Corretto utilizzo delle informazioni segrete di autenticazione
   Minaccia** Accesso non autorizzato alle informazioni

   **Contromisure**  Tutti gli utenti devono essere informati dall'organizzazione sul corretto utilizzo delle
   informazioni segrete di autenticazione. Tutti gli utenti dovrebbero essere avvisati di:

   - evitare di tenere una registrazione (per esempio su carta, documenti software)
       delle informazioni segrete di autenticazione, salvo indicazione di un metodo di
       memorizzazione sicura;
   - modificare le informazioni segrete di autenticazione ogni qualvolta vi sia
       un'indicazione della loro possibile compromissione.
   L'organizzazione dovrebbe definire un processo affinché l'utente "proprietario" o altri
   utenti possano segnalare immediatamente - H24 - eventi/incidenti di sicurezza inerenti
   l'informazione segreta di autenticazione, quali: la divulgazione non autorizzata o la
   perdita di segretezza.


   #### 5.1.3 Autorizzazione

   **Definizione della politica di controllo accesso logico
   Minaccia** Accesso non autorizzato alle informazioni (ad es. causato dal personale utente per
   carenza di una politica per il controllo degli accessi che accoglie i requisiti di sicurezza).

   **Contromisure**  Definire e documentare la politica che regola le autorizzazioni per ciascun utente e
   gruppo di utenti con una granularità che consenta un rigoroso rispetto del principio del
   ''need to know''. Deve essere soddisfatta la regola del ''tutto proibito tranne ciò che è
   espressamente concesso''. La politica deve tenere conto di:

   - requisiti di sicurezza delle applicazioni e dei rischi che le informazioni gestite da tali
       applicazioni possono incontrare;
   - leggi e obblighi contrattuali che riguardano la protezione degli accessi a dati e
       servizi;
   - gestione dei diritti di accesso in un ambiente distribuito e di rete che riconosce
       ogni tipo di connessione disponibile;
   - separazione dei ruoli riguardanti il controllo degli accessi (richiesta di accesso,
       autorizzazione degli accessi, amministrazione degli accessi);
   - rimozione dei diritti di accesso per le credenziali non utilizzate da almeno sei mesi.

   **Separazioni dei compiti e delle responsabilità
   Minaccia** Abuso di risorse.

   **Contromisure**  I compiti e le aree di responsabilità in conflitto tra loro devono essere separati al fine di
   ridurre le possibilità di accedere, modificare o utilizzare asset dell'organizzazione
   impropriamente, senza autorizzazione o misure di controllo.

   **Definizione di regole di trattamento ed etichettatura
   Minaccia** Compromissione della sicurezza dell'informazione per carenza di regole di
   classificazione e trattamento delle informazioni

   **Contromisure**  Definire criteri e procedure per la corretta etichettatura delle informazioni (non solo in
   forma elettronica, ma anche cartacea). Considerare le seguenti etichette:

   1. Confidenziale (Informazione la cui impropria diffusione può provocare danni
       molto gravi, ad esempio: perdite economiche, conseguenze legali,
       conseguenze sul patrimonio, danno di immagine)
   2. Riservata (Informazione la cui impropria diffusione può provocare danni gravi,
       ad esempio: perdita di vantaggio competitivo)
   3. Interna (Informazione la cui diffusione può provocare danno lieve)
   4. Pubblica (Informazione la cui diffusione non può provocare danno)
   Definire procedure che regolino come debba avvenire il trattamento delle informazioni
   ai vari livelli di classifica con riferimento alle attività di elaborazione, diffusione,
   utilizzo, custodia, riclassificazione, distruzione.
   Rendere disponibili le procedure a tutto il personale.

   **Definizione e assegnazione di ruoli e responsabilità
   Contromisura** Compromissione della sicurezza dell'informazione per carenza dell’organizzazione
   interna

   **Contromisure**  Dare la responsabilità delle informazioni (insieme di dati) e delle risorse associate per
   la loro elaborazione (processo di business, gruppo specifico di attività, applicazioni) ad
   una determinata parte dell'organizzazione per assicurare l’appropriata classificazione e

l'applicazione delle politiche di controllo degli accessi a tali
risorse. In particolare: 1) identificare e definire chiaramente i vari
beni (quali i server, le postazioni di lavoro client, gli apparati di
rete e di sicurezza, i sistemi di storage, i dispositivi di stampa, i
sistemi di continuità elettrica, ecc.) e i processi di sicurezza (es.
gestione degli incidenti, gestione delle configurazioni di sistema,
gestione degli aggiornamenti, gestione dei sistemi antivirus, gestione
dei sistemi firewall, gestione delle verifiche tecniche di vulnerability
assessment, gestione delle non conformità e monitoraggio dei rientri,
ecc.). 2) nominare un responsabile della sicurezza di ciascun bene e un
responsabile per ciascun processo di gestione della sicurezza e
documentare in modo dettagliato i processi, definendo in modo chiaro i
ruoli e le responsabilità 3) definire chiaramente i livelli di
autorizzazione per l'accesso o l'utilizzo di ciascun bene.

::

   **Protezione dell'accesso ai dati
   Minaccia** - Abuso di privilegi da parte dell'utente. Accesso non autorizzato ai sistemi (risorse
   di sistema, configurazioni, ecc.).

   - Accesso non autorizzato alle informazioni.
   - Furto di credenziali di autenticazione.

   **Contromisure**  Per quanto riguarda il furto di credenziali di autenticazione e quel che ne consegue
   (accesso non autorizzato a sistemi e informazioni, furto d’identità, ecc.), è necessario
   stabilire meccanismi di autenticazione la cui robustezza sia adeguata alla criticità
   dell’applicazione e ancor più alla sensibilità dei dati che l’applicazione tratta.
   Ad es. per applicazioni critiche o dati particolarmente sensibili è necessario adottare
   meccanismi di autenticazione a due fattori, basati ad es. su SMS inviati su un numero
   di cellulare precedentemente “certificato”, o codici inviati tramite una app per
   smartphone o altri metodi equivalenti.
   Tuttavia qualsiasi misura di sicurezza in tale ambito può risultare inefficace se non
   accompagnata da una appropriata campagna di diffusione della consapevolezza delle
   problematiche di sicurezza (“security awareness”) verso gli utenti che devono essere
   informati e responsabilizzati verso un uso corretto delle credenziali di autenticazione
   con documenti (politiche di sicurezza) ed eventualmente corsi di formazione.
   Per impedire l’accesso non autorizzato ai dati, a riposo e/o in transito, da parte di
   utenti reali (ma non abilitati per i dati in oggetto) e per limitare le possibilità di accesso
   di eventuali utenti che abbiano ottenuto illecitamente delle credenziali valide non di
   propria pertinenza, i dati memorizzati all'interno dei sistemi (file e cartelle) devono
   essere adeguatamente protetti attraverso l’assegnazione di diritti di accesso il più
   possibile granulari e specifici (dal punto di vista delle risorse).
   Qualora i dati siano conservati in archivi elettronici (es. database) accertarsi che
   l'accesso ai dati avvenga mediante un'adeguata profilatura degli utenti e che le
   applicazioni che accedono ai database non utilizzino una singola utenza di “super-
   amministratore” per tutte le operazioni, dato che tale configurazione può essere
   sfruttata da un malintenzionato per prendere pieno possesso dell’archivio.
   L'organizzazione dovrebbe adottare controlli di accesso fisico e/o logico per
   l’isolamento di applicazioni, dati o sistemi critici o sensibili. Per l'accesso ai dati critici o
   sensibili definire requisiti di sicurezza più stringenti applicando tecniche di cifratura o
   altri meccanismi di sicurezza per rafforzare la protezione dell'accesso.
   Infine, per quanto riguarda l’abuso di privilegi da parte degli utenti, questo fenomeno
   può essere contrastato con un approccio basato su più aspetti:


   - Diffondere tra gli utenti un documento di politiche di sicurezza che spieghi qual è
       l’uso corretto delle risorse.
   - Impiegare meccanismi di tracciamento delle operazioni effettuate dagli utenti in
       grado di registrare i tentativi di accesso non riusciti a risorse per le quali non si
       dispone delle necessarie autorizzazioni, nei limiti imposti dalle leggi vigenti.
   - Informare gli utenti attraverso “banner” di accesso (oltre alle citate politiche di
       sicurezza) dell’esistenza di tali meccanismi di tracciamento.
   - Educare gli utenti ad un uso corretto delle risorse attraverso corsi di formazione.

   #### 5.1.4 Crittografia

   **Protezione delle informazioni strumentali all'accesso
   Minaccia** Crittografia debole o non validata.

   **Contromisure**  - Non sviluppare e utilizzare algoritmi di crittografia personalizzati/propri.

   - Utilizzare servizi, funzioni e algoritmi crittografici la cui robustezza sia comprovata
       da certificazioni e standard riconosciuti a livello internazionale, e che risultino
       esenti da vulnerabilità note. A titolo esemplificativo e non esaustivo, per la
       crittografia deve essere usato quanto meno l’algoritmo AES a 128 bit (o meglio a
       256 bit se possibile), per le funzioni di hashing quanto meno lo SHA-256 (MD5 e
       SHA-1 sono deprecati), per le connessioni internet sicure almeno TLS 1.2 (SSL e TLS
       precedenti alla 1.2 sono vulnerabili e deprecate).
   - Per quanto riguarda prodotti di crittografia a titolo esemplificativo devono
       disporre quanto meno di certificazione Common Criteria In genere EAL 4+ (ma a
       seconda dei casi possono essere richiesti livelli minori o anche superiori in base a
       regolamenti e norme di legge).
   - Mantenersi informati sugli algoritmi manomessi e sulle tecniche utilizzate per la
       manomissione, attraverso i bollettini di sicurezza emessi sia dai vendor sia da fonti
       internazionali autorevoli, sia dal CERT della PA.

   **Protezione dei dati di autenticazione (trasmissione)
   Minaccia** Crittografia debole o non validata.

   **Contromisure**  Meccanismi, strumenti, procedure o abilità tecniche atti a prevenire l'accesso non
   autorizzato al sistema e a proteggere i dati di autenticazione quando memorizzati o
   trasmessi.

   **Protezione delle informazioni
   Minaccia** Crittografia debole o non validata.

   **Contromisure**  I controlli crittografici devono essere utilizzati in conformità a tutti gli accordi, leggi e
   regolamenti pertinenti.
   Considerare di adeguarsi alle best practices di crittografia. Di seguito vengono indicate
   le principali:

   - Trasmissione dati: usare TLS 1.1 o 1.2 (viceversa SSL v2 e v3 sono considerate
       insicure).
   - Cifratura dati: usare AES con una chiave a 256 bit (3DES solo per backward
       compatibility, DES è considerato insicuro).
   - Hashing: usare SHA-256 (evitare SHA-1, mentre MD5 è considerato insicuro).
   - 4. RSA: usare chiavi a 2048 bit.


   **Protezione delle informazioni
   Minaccia** - Violazione di leggi, di regolamenti, di obblighi contrattuali.

   - Compromissione delle comunicazioni.
   - Falsificazione di identità.

   **Contromisure**  I controlli crittografici devono essere utilizzati in conformità a tutti gli accordi, leggi e
   regolamenti pertinenti.
   Considerare di adeguarsi alle best practices di crittografia. Di seguito vengono indicate
   le principali:
   - Trasmissione dati: usare TLS 1.1 o 1.2 (viceversa SSL v2 e v3 sono considerate
   insicure).
   - Cifratura dati: usare AES con una chiave a 256 bit (3DES solo per retro-
   compatibilità, DES è considerato insicuro).
   - Hashing: usare SHA-256 (evitare SHA-1, mentre MD5 è considerato insicuro).
   - RSA: usare chiavi almeno a 2048 bit.

   **Protezione delle informazioni strumentali all'accesso
   Minaccia** Generazione e/o gestione inadeguata delle chiavi crittografiche.

   **Contromisure**  Utilizzare routine di crittografia integrate che includono la gestione delle chiavi
   protette. L'interfaccia di programmazione per la protezione dei dati applicativi (DPAPI)
   è un esempio di un servizio di crittografia fornito su sistemi operativi Windows 2000 e
   successivi in cui il sistema operativo gestisce la chiave.
   Se si utilizza un meccanismo di crittografia che richiede di generare o gestire la chiave,
   utilizzare algoritmi di generazione forti delle chiavi casuali e memorizzare la chiave in
   una posizione protetta. Ad esempio, in una chiave del Registro di sistema protetta con
   un ACL restrittivo.
   Crittografare la chiave di crittografia utilizzando DPAPI per una maggiore sicurezza.
   Impostare i limiti temporali di scadenza delle chiavi ad intervalli regolari.

   #### 5.1.5 Documentazione

   **Protezione della documentazione di sistema da accessi non autorizzati
   Minaccia** Accesso non autorizzato alle informazioni.

   **Contromisure**  La documentazione di sistema (ad es. relativa al software del web server/DBMS, della
   piattaforma ospitante il web server/DBMS, ecc.) deve essere protetta da accessi non
   autorizzati e conservata in modo sicuro. In particolare, la documentazione cartacea, se
   non utilizzata, deve essere conservata e custodita all'interno di contenitori (es. armadi,
   cassettiere) chiusi a chiave e accessibile esclusivamente dai soggetti autorizzati. Per la
   documentazione memorizzata su supporto informatico l'accesso dovrebbe essere
   consentito ad una lista ridotta di utenti, mediante l'utilizzo di idonei sistemi di
   autenticazione e autorizzazione informatica.

   #### 5.1.6 Logging

   **Registrazione degli eventi (audit)
   Minaccia** - Abuso di privilegi da parte dell’utente

   - Cancellazione dei log di accountability e/o ripudio di operazioni effettuate..
   - Negazione dei servizi.

   **Contromisure**  I log di audit che registrano le attività dell'utente, le eccezioni e gli eventi di sicurezza
   devono essere prodotti e conservati per essere utilizzati in indagini, come prove da

esibire in caso di dispute, e monitoraggi, come elementi da considerare
nell'identificazione di misure migliorative della sicurezza. Gli eventi
che devono essere registrati includono:

::

   - log-on e log-off e durata dell'accesso dell'utente o applicazione software;
   - tentativi di accesso riusciti e falliti;
   - utilizzo di funzioni amministrative o di gestione;
   - avvio e arresto delle funzioni di audit;
   - errori del software.

La registrazione dell'evento deve riportare almeno i seguenti dati:

::

   - identità dell'utente o l'identificativo del processo che ha scatenato l'evento;
   - indirizzo IP dell’utente nel caso di sessione remota;
   - data e ora dell'evento;
   - tipo dell'evento;
   - oggetti coinvolti dall'evento;
   - eventuali errori prodotti dall’evento..

Conservare i dati relativi agli eventi registrati per un periodo di
tempo di almeno 5 anni.

::

   **Adozione di misure idonee a garantire inalterabilità e integrità dei log registrati
   Minaccia** - Violazione della sicurezza, rispetto alle politiche di sicurezza dell’organizzazione.

   - Abuso di privilegi da parte dell'utente
   - Abuso di risorse.
   - Cancellazione dei log di accountability e/o ripudio di operazioni effettuate..
   - Violazione di leggi, di regolamenti, di obblighi contrattuali.

   **Contromisure**  Le registrazioni (access log) devono avere caratteristiche di completezza, inalterabilità
   e possibilità di verifica della loro integrità adeguate al raggiungimento dello scopo per
   cui sono richieste; tale verifica avviene in conformità alla normativa in materia di
   protezione dei dati personali (Privacy) e dei principi di sicurezza.

Proteggere i file di log utilizzando ACL restrittivi. Attraverso un
processo automatico schedulato a intervalli regolari (ad es. ogni
notte), spostare i file di log fin lì prodotti in una posizione diversa
da quella predefinita e comprimerli. Predisporre un processo automatico
per la raccolta dei log compressi e il loro trasferimento su un server
centralizzato.

::

   **Registrazione e Analisi periodica dei log degli errori
   Minaccia** Accesso non autorizzato alle informazioni

   **Contromisure**  Le segnalazioni di errori (es. di malfunzionamenti, di eventi anomali di sicurezza che
   possono essere segnali di un probabile attacco o palesi tentativi di intrusione) devono
   essere registrate cronologicamente nei file di log del sistema, archiviate centralmente
   su un sistema dedicato e analizzate periodicamente per rilevare prontamente
   eventuali segnali che possono indicare l’insorgenza di un malfunzionamento (che può
   portare a un disservizio) o per rilevare tentativi di attacco.
   I file di log raccolti sul sistema centralizzato devono essere mantenuti per un congruo
   periodi di tempo (in genere sei mesi), allo scopo di consentire analisi anche in tempi
   successivi e per analisi di tipo statistico.
   Si noti che i file di log relativi a transazioni bancarie, dati di traffico telematico e

telefonico, dati personali, sensibili e giudiziari, sono soggetti a
specifiche norme di legge che prescrivono tra l'altro tempi massimi
consentiti di mantenimento, oltre i quali devono essere
obbligatoriamente cancellati.

::

   **Conservazione dei log registrati degli amministratori di sistema
   Minaccia** - Cancellazione dei log di accountability e/o ripudio di operazioni effettuate..

   - Violazione della sicurezza, rispetto alle politiche di sicurezza dell’organizzazione.
   - Violazione di leggi, di regolamenti, di obblighi contrattuali.
   - Abuso di privilegi da parte degli utenti.
   - Abuso di risorse.

   **Contromisure**  - Tracciare eventi chiave come gli eventi di login e logout, i tentativi di login falliti,
   l’uso di privilegi elevati, le transazioni applicative critiche dal punto di vista della
   sicurezza, l’accesso e il tentativo fallito di accesso a oggetti e risorse critiche per la
   sicurezza.
   - Non utilizzare account condivisi o di ruolo poiché non è possibile determinare la
       vera identità dei soggetti. Gli accessi degli amministratori devono essere sempre
       nominativi e i relativi identificativi in caso siano revocati non devono più essere
       riassegnati ad altri utenti neppure in tempi diversi.
   - Salvare i log di accesso amministrativo ai sistemi e quelli di audit (operazioni che
       richiedono l’uso di privilegi) su sistemi di raccolta centralizzati.
   - Le registrazioni dei log degli amministratori devono essere conservate per un
       congruo periodo, non inferiore a sei mesi, in conformità alla normativa in materia
       di protezione dei dati personali (Privacy) e dei principi di sicurezza.
   - Tracciare le operazioni critiche eseguite a livello applicativo.
   - Eseguire un regolare backup dei file di log e analizzarli regolarmente per verificare
       la presenza di attività sospette.

   **Protezione log
   Minaccia** - Abuso di privilegi da parte dell’utente.

   - Negazione dei servizi (ad es. da errori hardware/software non rilevati in maniera
       tempestiva o corretta per carenze di monitoraggio nei sistemi ICT).
   - Accesso non autorizzato alle informazioni.
   - Accesso non autorizzato ai sistemi (risorse di sistema, configurazioni, ecc.).
   - Violazione di leggi, di regolamenti, di obblighi contrattuali.

   **Contromisure**  Controllare che le informazioni contenute nei file di log siano protette da
   manomissioni e accessi non autorizzati e che non ci siano problemi operativi con le
   logging facilities. In particolare, occorre verificare che non vi sia:
   - alterazione delle informazioni tracciate nel file di log;
   - discordanza fra il periodo di conservazione dei log e quanto indicato dalle policy di
   retention o specifiche disposizioni legali;
   - fallimento delle operazioni di registrazione degli eventi causato da un
   raggiungimento della dimensione massima del file di log;
   - sovrascrittura delle informazioni precedentemente tracciate causata da un
   raggiungimento della dimensione massima del file di log, nel caso in cui la scrittura
   dei log sia effettuata in modo ciclico sempre sullo stesso file.

   **Registrazione degli accessi logici da parte degli amministratori di sistema
   Minaccia** - Abuso di privilegi da parte dell'utente;

   - Cancellazione dei log di accountability e/o ripudio di operazioni effettuate.



   **Contromisure**  Devono essere adottati sistemi idonei alla registrazione degli accessi logici
   (autenticazione informatica) al sistema/piattaforma da parte degli amministratori di
   sistema. Le registrazioni devono comprendere i riferimenti temporali e la descrizione
   dell'evento che le ha generate.
   Si tenga presente che il controllo e la registrazione possono essere aggirati da un
   account condiviso (questo vale sia per gli account amministrativi che per gli account
   utente / applicativi / di servizio): pertanto gli account amministrativi non devono
   es sere condivisi.
   In generale, anche per gli account utente non privilegiati e per gli account usati dagli
   applicativi per l’esecuzione dei servizi in uno specifico contesto (es. account httpd per
   un server web in ambito UNIX), devono essere nominativi / specifici per l’utente o
   l’applicativo e non condivisi.

   #### 5.1.7 Procedure

   ##### Change management ..............................................................................................................................................................

   **Gestione dei cambiamenti
   Minaccia** - Accesso non autorizzato ai sistemi (risorse di sistema, configurazioni, ecc.).

   - Accesso non autorizzato alle informazioni.
   - Violazione della sicurezza, rispetto alle politiche di sicurezza dell’organizzazione.
   - Negazione dei servizi.

   **Contromisure**  Deve essere definito un processo di gestione dei cambiamenti (all’interno del ciclo di
   vita dei sistemi, nonché per i processi organizzativi di gestione della sicurezza) che
   tenga in considerazione l'identificazione delle esigenze che determinano il “change”,
   l'analisi e la valutazione degli impatti del “change” (anche in termini di “non
   regressione”), la progettazione e la realizzazione, il testing, l’implementazione, la
   verifica, l’eventuale rollback in caso di errori nell’implementazione.
   La gestione dei cambiamenti può avere come oggetto un servizio, un sistema
   informativo, un’applicazione, un processo organizzativo o un processo di gestione della
   sicurezza, ecc.
   Quando vengono apportate delle modifiche a servizi, sistemi o processi, queste devono
   essere documentate in un registro, riportando informazioni dettagliate sui
   cambiamenti apportati..

   **Procedura di monitoraggio dei cambiamenti
   Minaccia** - Accesso non autorizzato ai sistemi (risorse di sistema, configurazioni, ecc.).

   - Accesso non autorizzato alle informazioni.
   - Violazione della sicurezza, rispetto alle politiche di sicurezza dell’organizzazione.
   - Negazione dei servizi.
   - Attacchi all’integrità dei sistemi (software e configurazioni).

   **Contromisure**  Definire delle formali procedure di controllo dei cambiamenti al fine di garantire
   l’integrità dei sistemi, delle applicazioni e dei prodotti.
   L’introduzione di nuovi sistemi e significativi cambiamenti sui sistemi esistenti
   dovrebbero seguire un processo formale di documentazione, specifica, test, controllo
   di qualità e gestione dell’implementazione.
   I cambiamenti non autorizzati o che comunque non hanno seguito un processo formali
   di “change” devono essere rilevati. Ad es. possono essere utilizzati sistemi cosiddetti
   “Configuration Management Data Base” o CMDB dotati di agent che rilevano le
   configurazioni dei sistemi e possono anche generare alert se tali configurazioni sono

diverse da quelle stabilite. Funzionalità ancora più avanzate che
comprendono la verifica anche su eseguibili e librerie installate nel
sistema e controlli di integrità, possono essere ottenute con sistemi di
controllo della compliance che generano delle “firme” per ciascuna
componente software e le confrontano con quelle definite come “baseline”
in fase di rilascio dell'ultimo “change” autorizzato.

::

   **Riesame tecnico a seguito di cambiamenti
   Minaccia** - Accesso non autorizzato ai sistemi (risorse di sistema, configurazioni, ecc.).

   - Accesso non autorizzato alle informazioni.
   - Violazione della sicurezza, rispetto alle politiche di sicurezza dell’organizzazione.
   - Negazione dei servizi.
   - Attacchi all’integrità dei sistemi (software e configurazioni).

   **Contromisure**  Definire un processo per il riesame tecnico delle applicazioni in seguito a cambiamenti
   apportati nelle piattaforme operative (quest'ultime includono i sistemi di produzione, i
   database e le piattaforme di middleware). Effettuare i necessari test applicativi per
   assicurare che non ci siano impatti negativi sull'operatività o sulla sicurezza
   dell'organizzazione.

   ##### Maintenance ...........................................................................................................................................................................

   **Redigere e applicare le procedure operative
   Minaccia** - Abuso di privilegi da parte dell’utente.

   - Abuso di risorse.
   - Errori di amministrazione dei sistemi.

   **Contromisure**  Le procedure operative concernenti la manutenzione delle strutture di elaborazione
   delle informazioni, quali:
   - installazione e configurazione iniziale dei sistemi;
   - backup e restore;
   - gestione delle vulnerabilità tecniche e aggiornamenti;
   - manutenzione delle apparecchiature;
   - sicurezza fisica delle apparecchiature e procedure per l’accesso fisico del personale
   tecnico addetto alla manutenzione;
   - elenco dei componenti hardware e delle parti di ricambio, dei relativi fornitori, dei
   livelli di servizio per l’assistenza (es. risposta e presa in caricoh24 7x7, con
   risoluzione entro il next business day), dei riferimenti per la richiesta di intervento;
   - procedura per la corretta dismissione del sistema e delle sue componenti;
   devono essere formalmente documentate per iscritto, mantenute attive e aggiornate
   periodicamente al sopraggiungere di ogni cambiamento.
   Ciascuna procedura deve essere distribuita e resa nota ai soggetti interessati
   attraverso un portale documentale interno all’ente/organizzazione.

   **Backup delle informazioni e del software
   Minaccia** - Negazione dei servizi.

   - Cancellazione o furto di informazioni.

   **Contromisure**  Effettuare periodicamente copie di backup delle informazioni e del software, in
   conformità alla politica per il salvataggio dei dati stabilita a livello aziendale. Verificare
   periodicamente, nel rispetto delle leggi, regolamenti, obblighi contrattuali, l'effettiva
   memorizzazione, "leggibilità" e integrità delle informazioni registrate, anche al fine di

assicurare la pronta disponibilità delle stesse in caso di interruzione
dei servizi informativi. Individuare le responsabilità per la gestione
delle copie di backup.

::

   **Account dedicato al gruppo di manutenzione
   Minaccia** Divulgazione di informazioni riservate.
   Abuso di risorse.
   Accesso non autorizzato ai sistemi (risorse di sistema, configurazioni, ecc.).
   Accesso non autorizzato alle informazioni.
   Uso non autorizzato di privilegi.
   Violazione di leggi, di regolamenti, di obblighi contrattuali.

   **Contromisure**  Affidare gli interventi di manutenzione che richiedono un accesso ai sistemi al solo
   personale formalmente autorizzato, appartenente a società fornitrici con le quali sono
   stati stipulati appositi contratti che vincolano il manutentore al corretto uso delle
   risorse informative e alla riservatezza.
   Il manutentore in tali casi dovrà essere munito di un apposito account amministrativo
   nominativo abilitato solo ai compiti stabiliti dal contratto di manutenzione.
   Impedire, se tecnicamente possibile, l'accesso con l’account del manutentore a
   cartelle, file, dati, interfacce applicative di esclusiva pertinenza degli utenti autorizzati.
   Gli interventi di manutenzione che avvengono attraverso un accesso remoto non
   devono mai avvenire dalla sede della società fornitrice, ma sempre dalla rete interna
   dell’ente/organizzazione. In ogni caso le sessioni di amministrazione remota devono
   usare protocolli autenticati e cifrati.

   **Manutenzione periodica dell'asset
   Minaccia** - Negazione dei servizi (per carenze di monitoraggio nei sistemi ICT).

   - Cancellazione o furto di informazioni.
   - Attacchi all’integrità delle informazioni.
   - Violazione di leggi, di regolamenti, di obblighi contrattuali.

   **Contromisure**  Eseguire un'attività di manutenzione, con cadenza almeno semestrale, mediante
   procedure rigorose ed efficaci che prevedano una modulistica di intervento con
   esplicitazione dell'anomalia dichiarata, malfunzionamento accertato, intervento
   effettuato e parti sostituite. Effettuare delle statistiche sulla manutenzione di ogni
   singolo componente al fine di valutarne il livello di obsolescenza e definire un
   programma di manutenzione preventiva.

   **Regolamentazione della manutenzione dei dispositivi ICT
   Minaccia** Divulgazione di informazioni riservate.
   Accesso non autorizzato ai sistemi (risorse di sistema, configurazioni, ecc.).
   Accesso non autorizzato alle informazioni.
   Violazione di leggi, di regolamenti, di obblighi contrattuali

   **Contromisure**  In generale, prima di affidare le apparecchiature a servizi esterni di manutenzione è
   necessario stabilire contrattualmente opportune clausole di riservatezza e di non
   divulgazione delle informazioni e valutare i rischi di sicurezza.
   In alcuni casi è necessario considerare la possibilità di sostituire le apparecchiature
   danneggiate, piuttosto che ripararle, per evitare il rischio di compromissione della
   riservatezza di informazioni particolarmente critiche. In tal caso prima di gettare tali
   apparecchiature è necessario distruggerle fisicamente. Naturalmente questo dipende
   dalla riservatezza dei dati contenuti.
   La regola da osservare è la seguente:

I dispositivi di memorizzazione che contengono informazioni riservate
come ad es. dati personali, sensibili o giudiziari, dati di traffico
telematico e telefonico, dati relativi a transazioni bancarie, specie se
tali dati risultino in chiaro (non cifrati), quando risultino
danneggiati non possono essere inviati a società esterne per la
riparazione, a meno che non sia possibile effettuare una cancellazione
sicura dei dati memorizzati. Negli altri casi, e più in generale ogni
volta che tali dispositivi devono essere dismessi, i dati in essi
contenuti devono essere resi irrecuperabili con sistemi di
smagnetizzazione o attraverso la distruzione fisica.

::

   **Regolamentazione della manutenzione della PdL
   Minaccia** - Negazione dei servizi (per impossibilità di amministrarli o monitorarli da parte del
   personale preposto).

   - Accesso non autorizzato ai sistemi (risorse di sistema, configurazioni, ecc.).
   - Accesso non autorizzato alle informazioni.
   - Divulgazione di informazioni riservate.
   - Violazione di leggi, di regolamenti, di obblighi contrattuali.

   **Contromisure**  Definire una procedura relativamente alla manutenzione delle PdL che preveda:
   - solo il personale autorizzato alla manutenzione dovrebbe svolgere le riparazioni e
   le operazioni di servizio alle apparecchiature;
   - devono essere tenute le registrazioni di tutti i difetti presunti o reali, e di tutti gli
   interventi di manutenzione preventivi e correttivi;
   - devono essere adottati dei controlli appropriati quando si inviano all'esterno le
   apparecchiature in manutenzione, tenendo anche conto se tale manutenzione è
   fatta da personale in sito o all’esterno dell’organizzazione;
   - ove necessario, si dovrebbero eliminare le informazioni critiche
   dall’apparecchiatura oppure il personale di manutenzione dovrebbe essere
   sufficientemente selezionato;

   ##### Patching ..................................................................................................................................................................................

   **Controllo di vulnerabilità tecniche
   Minaccia** - Abuso di risorse.

   - Accesso non autorizzato ai sistemi (risorse di sistema, configurazioni, ecc.).
   - Accesso non autorizzato alle informazioni.
   - Compromissione delle comunicazioni.
   - Crittografia debole o non validata.
   - Divulgazione di informazioni riservate.
   - Negazione dei servizi.
   - Cancellazione o furto di informazioni.
   - Attacchi all’integrità dei sistemi (software e configurazioni).
   - Attacchi all’integrità delle informazioni
   - Violazione della sicurezza, rispetto alle politiche di sicurezza dell’organizzazione.
   - Violazione di leggi, di regolamenti, di obblighi contrattuali.

   **Contromisure**  Ottenere tempestive informazioni sulle vulnerabilità tecniche dei sistemi di
   informazione in uso, valutare l’esposizione dell’azienda a tali vulnerabilità e prendere
   appropriate misure per indicare il rischio associato.
   A tale scopo è necessario mantenere un inventario aggiornato e completo dei beni
   quali il rivenditore del software, il numero della versione, i software installati e i
   sistemi su cui sono installati, e i referenti interni all’azienda responsabili del software.
   In particolare è necessario:
   - definire i ruoli e le responsabilità per la gestione delle vulnerabilità tecniche;


   - definire i mezzi di informazione che saranno usati per identificare le vulnerabilità
       tecniche;
   - identificare i rischi associati e le azioni da intraprendere una volta che una
       potenziale vulnerabilità tecnica è stata identificata;
   - gestire le patch disponibili valutando anche i rischi associati alla loro installazione;
   - controllare il processo di gestione delle vulnerabilità tecniche e valutare la sua
       efficacia ed efficienza.

   **Software Patching
   Minaccia** - Abuso di risorse.

   - Accesso non autorizzato ai sistemi (risorse di sistema, configurazioni, ecc.).
   - Accesso non autorizzato alle informazioni.
   - Compromissione delle comunicazioni.
   - Crittografia debole o non validata.
   - Divulgazione di informazioni riservate.
   - Negazione dei servizi.
   - Cancellazione o furto di informazioni.
   - Attacchi all’integrità dei sistemi (software e configurazioni).
   - Attacchi all’integrità delle informazioni
   - Violazione della sicurezza, rispetto alle politiche di sicurezza dell’organizzazione.
   - Violazione di leggi, di regolamenti, di obblighi contrattuali.

   **Contromisure**  Verificare che sia applicata una procedura di gestione delle patch composto almeno
   dalle fasi di seguito elencate:
   - Rilevamento, avvalersi di strumenti che verifichino l'eventuale mancanza di patch
   di protezione. Il rilevamento deve avvenire in modo automatico ed attivare il
   processo di gestione delle patch;
   - Valutazione, qualora sia riscontrata la mancanza di aggiornamenti utili, valutare la
   gravità delle problematiche risolvibili con l'applicazione delle patch;
   - Acquisizione, nel caso le misure di protezione applicate risultino insufficienti
   all'eliminazione della vulnerabilità, procedere con lo scaricamento della patch per
   sottoporla ad un'approfondita analisi;
   - Verifica, procedere con l'installazione della patch su un sistema di prova al fine di
   verificare l'impatto delle conseguenze dell'aggiornamento sulla configurazione
   dell'ambiente di produzione;
   - Gestione, eseguire la registrazione al servizio di notifica per segnalare eventuali
   vulnerabilità quando individuate;
   - Distribuzione, distribuire la patch sulle macchine interessate; prevedere, inoltre,
   l'adozione di un piano di ripristino o di backup.
   In presenza di “Zero-day exploit”, per i quali non è ancora disponibile la patch,
   massimizzare la difesa perimetrale ed eseguire il patching appena disponibile e testato.

   ##### Secure testing .........................................................................................................................................................................

   **Vulnerability Assessment
   Minaccia** - Accesso non autorizzato ai sistemi (risorse di sistema, configurazioni, interfacce
   amministrative, ecc.).

   - Accesso non autorizzato alle informazioni;
   - Compromissione delle comunicazioni.
   - Divulgazione di informazioni riservate.
   - Negazione dei servizi.


   - Cancellazione o furto di informazioni.
   - Attacchi all’integrità dei sistemi (software e configurazioni).
   - Attacchi all’integrità delle informazioni.
   - Uso non autorizzato di privilegi.
   - Violazione della sicurezza, rispetto alle politiche di sicurezza dell’organizzazione.
   - Violazione di leggi, di regolamenti, di obblighi contrattuali.

   **Contromisure**  Effettuare almeno una volta l'anno un'attività di Vulnerability Assessment (VA) in
   modo da identificare le eventuali vulnerabilità che possono costituire un canale di
   accesso non autorizzato ad informazioni. Il VA deve verificare la corretta
   configurazione delle porte logiche affinché siano attive solo quelle strettamente
   necessarie. Inoltre, l'attività di VA deve essere condotta avendo come riferimento le
   ultime vulnerabilità note, pubblicate nelle banche dati di riferimento in tema di
   sicurezza informatica come, ad esempio, Open Source Vulnerability DataBase (OSVDB)
   e Common Vulnerabilities Exposures (CVE). In seguito all'attività di VA, per mitigare il
   rischio associato alle vulnerabilità identificate è necessario:
   - definire i ruoli e le responsabilità per la gestione delle vulnerabilità tecniche;
   - identificare le azioni da intraprendere (es. disabilitare le funzionalità non utilizzate,
   inclusi protocolli e servizi; rendere più sicure le impostazioni di configurazione
   predefinite, ridurre al minimo il numero delle interfacce di amministrazione, ecc.);
   - revisionare le funzionalità di failover del sistema.

   **Penetration Test
   Minaccia** - Accesso non autorizzato ai sistemi (risorse di sistema, configurazioni, interfacce
   amministrative, ecc.).

   - Accesso non autorizzato alle informazioni;
   - Compromissione delle comunicazioni.
   - Divulgazione di informazioni riservate.
   - Negazione dei servizi.
   - Cancellazione o furto di informazioni.
   - Attacchi all’integrità dei sistemi (software e configurazioni).
   - Attacchi all’integrità delle informazioni.
   - Uso non autorizzato di privilegi.
   - Violazione della sicurezza, rispetto alle politiche di sicurezza dell’organizzazione.
   - Violazione di leggi, di regolamenti, di obblighi contrattuali.

   **Contromisure**  Effettuare, almeno una volta l'anno, un'attività di Penetration Test (PT) sui sistemi più
   critici, simulando dall'esterno un'azione di intrusione al sistema/piattaforma. L'attività
   deve prevedere degli opportuni scenari d'intrusione affinché siano evidenziate la
   presenza di vulnerabilità nel sistema, e la conseguente possibilità di ottenere accessi
   non autorizzati a funzioni ed informazioni riservate.

   **Fuzzing Test
   Minaccia** - Divulgazione di informazioni riservate.

   - Negazione dei servizi.
   - Cancellazione o furto di informazioni.
   - Attacchi all’integrità dei sistemi (software e configurazioni).
   - Attacchi all’integrità delle informazioni.

   **Contromisure**  Eseguire test regolari di tipo fuzzing per rilevare e correggere eventuali
   malfunzionamenti causati da mancata validazione dell’input (es. buffer overflow).


   ##### Disposal ...................................................................................................................................................................................

   **Protezione dei dati personali in caso di reimpiego o riciclo dell'apparecchiatura elettronica
   Minaccia** - Accesso non autorizzato alle informazioni.

   - Divulgazione di informazioni riservate.
   - Violazione di leggi, di regolamenti, di obblighi contrattuali.

   **Contromisure**  Chi procede al reimpiego o al riciclaggio di rifiuti di apparecchiature elettriche ed
   elettroniche o di loro componenti è comunque tenuto ad assicurarsi dell'inesistenza o
   della non intelligibilità di dati personali sui supporti, acquisendo, ove possibile,
   l'autorizzazione a cancellarli o a renderli non intelligibili.

   **Protezione dei dati personali in caso di smaltimento dell'apparecchiatura elettronica
   Minaccia** - Accesso non autorizzato alle informazioni.

   - Divulgazione di informazioni riservate.
   - Violazione di leggi, di regolamenti, di obblighi contrattuali.

   **Contromisure**  In caso di smaltimento di rifiuti elettrici ed elettronici, l'effettiva cancellazione dei dati
   personali dai supporti contenuti nelle apparecchiature elettriche ed elettroniche può
   anche risultare da procedure che, nel rispetto delle normative di settore, comportino
   la distruzione dei supporti di memorizzazione di tipo ottico o magneto-ottico in modo
   da impedire l’acquisizione indebita di dati personali.
   La distruzione dei supporti prevede il ricorso a procedure o strumenti diversi a secondo
   del loro tipo, quali:
   - sistemi di punzonatura o deformazione meccanica;
   - distruzione fisica o di disintegrazione (usata per i supporti ottici come i cd-rom e i
   dvd);
   - demagnetizzazione ad alta intensità.

   ### 5.2 SICUREZZA DEI SISTEMI OPERATIVI

   Di seguito viene fornita una vista delle principali minacce e delle relative contromisure da adottare.

   #### 5.2.1 Architettura

   **Architettura
   Minaccia** Accesso non autorizzato alle informazioni.

   **Contromisure**  - Utilizzare un sistema di protezione del perimetro (Firewall).

   - Segmentare la rete: creare segmenti di rete distinti per le diverse tipologie di
       sistemi dotate di caratteristiche diverse di sensibilità e tipologia. Ad es. creare un
       segmento o layer dati, un layer per i server di front-end, un layer per le postazioni
       di lavoro, un segmento per la rete di amministrazione (da cui gli amministratori
       accedono alle interfacce amministrative dei server e degli apparati di rete e di
       sicurezza).
   - Non usare le VLAN per separare i layer: attestare ogni layer/segmento su una
       diversa interfaccia del firewall.
   - Installare un IDS (intrusion detection system) o IPS (intrusion prevention system)
   - Impiegare VPN terminate sul firewall perimetrale (o su host specifici e dedicati,
       attestati su una apposita DMZ), per la connessione di utenti remoti e di altre reti
       appartenenti a diverse sedi dell’ente/organizzazione.
   - Utilizzare un sistema di controllo accessi alla rete (NAC basato su protocollo 802.1x

e Server RADIUS) per prevenire l'accesso tramite cavo da parte di
sistemi fraudolenti.

::

   - Individuare e rimuovere eventuali punti di accesso wireless non autorizzati e
       utilizzare su quelli leciti il sistema di protezione Wi-Fi Protected Access versione 2
       (WPA2) per la massima protezione dagli attacchi wireless, avendo cura di
       aggiornare il firmware all’ultima versione disponibile (fine Ottobre 2017 o
       successiva), in grado di eliminare la vulnerabilità denominata KRACK (Key
       Reinstallation Attacks) (cfr. https://www.krackattacks.com/).

   **Architettura
   Minaccia** Negazione dei servizi.
   Cancellazione di informazioni (accidentale).

   **Contromisure**  Al fine di garantire la continuità operativa del sistema, configurare i dischi in modalità
   RAID-1 o RAID-5, in modo che i dati presenti su ciascun disco siano replicati.

In questo modo in caso di guasto di un disco, sarà possibile continuare
ad utilizzare il sistema senza perdita di informazione o interruzione di
servizi, procedendo tempestivamente alla sostituzione del disco guasto.
Ciò si applica sia ai dischi locali al sistema, sia a quelli disponibili
in rete attraverso sistemi di Storage Area Networks.

::

   #### 5.2.2 Hardening

   **Hardening del sistema
   Minaccia** Accesso non autorizzato ai sistemi (risorse di sistema, configurazioni, interfacce
   amministrative, ecc.).
   Accesso non autorizzato alle informazioni.
   Furto di credenziali di autenticazione (ad es. con tecniche di brute-force o password
   crackers).
   Negazione dei servizi.
   Cancellazione o furto di informazioni.
   Attacchi all’integrità dei sistemi (BIOS, software di base, configurazioni).
   Attacchi all’integrità delle informazioni
   Violazione della sicurezza, rispetto alle politiche di sicurezza dell’organizzazione.
   Violazione di leggi, di regolamenti, di obblighi contrattuali.

   **Contromisure**  Consolidare la sicurezza di base del sistema implementando dei meccanismi di
   protezione atti a contrastare in maniera più efficace eventuali attacchi e limitarne la
   capacità di azione. I principali interventi da intraprendere sono:

   - attivare una password a protezione del BIOS in modo da prevenire alterazioni alla
       configurazione di avvio del sistema;
   - impedire l’uso di password vuote;
   - configurare il sistema affinché obblighi all’uso di password “robuste” (es. almeno
       una maiuscola, una minuscola, un numero e un carattere speciale, e almeno 8
       caratteri di lunghezza);
   - cambiare le password di default delle utenze di sistema e di quelle applicative in
       uso;
   - disabilitare le utenze di sistema e quelle applicative predefinite e non utilizzate;
   - installare gli aggiornamenti di sicurezza più recenti sia durante la fase di
       installazione iniziale, prima di iniziare ad utilizzare il sistema, sia regolarmente e

periodicamente, quando il sistema è in uso;

::

   - disattivare o rimuovere le funzionalità non utilizzate, inclusi protocolli di
       comunicazione, servizi, software, interfacce di rete, interfacce hardware (es. porte
       seriali e parallele, cd-rom se non usati, porte usb se non permesse, ecc.);
   - assicurarsi che i permessi d'accesso (lettura, scrittura, modifica, etc.) al file system
       siano concessi secondo la profilatura degli utenti accreditati, evitando la presenza
       di condivisioni accessibili indiscriminatamente da tutti gli utenti
       dell’organizzazione, o senza autenticazione, o scrivibili da chiunque;
   - bloccare tutte le porte di comunicazione non utilizzate sul firewall di rete e su
       quelli degli host server (se presenti).

   **Hardening del sistema
   Minaccia** Negazione dei servizi (es. fault per buffer overflows).
   Attacchi all’integrità dei sistemi (BIOS, software di base, configurazioni).

   **Contromisure**  Rendere certe pagine di memoria, come quelle contenenti stack e heap, non eseguibili.
   In generale, utilizzare un meccanismo di Data Execution Prevention (DEP) o l’opzione
   kernel ExecShield per limitare attacchi di iniezione di codice.
   Utilizzare meccanismi di address space layout randomization (ASLR) o l’opzione del
   kernel per il Randomized Virtual Memory Region Placement, nelle modalità più
   restrittive supportata da ciascun sistema operativo.

   **Hardening del protocollo TCP/IP
   Minaccia** Negazione dei servizi (Denial of Service).

   **Contromisure**  Disabilitare l’IP forwarding al fine di impedire che il server in esame possa essere
   utilizzato come “testa di ponte” per attacchi verso ulteriori sistemi nella rete interna.
   Disabilitare il _source routing_ , inibendo la possibilità ad un utente malintenzionato di
   specificare le rotte da percorrere in fase di connessione verso un sistema.

Abilitare i log per i pacchetti di rete ricevuti aventi un indirizzo di
origine non-routable (privo di una rotta in tabella di routing). Questa
contromisura aiuta ad individuare attacchi basati sull'IP spoofing.
Abilitare i TCP SYN cookies per la gestione efficiente dell'handshake
TCP SYN/ACK, in presenza di attacchi DOS specifici. Disattivare la
funzione di risposta alle richieste ICMP via broadcast. Filtrare i
pacchetti IP in modo che siano consentite solo le richieste ICMP
provenienti da indirizzi IP appartenenti al piano d'indirizzamento
aziendale. Attivare la funzione di Quality of Service (QoS) e limitare,
con valori idonei, l'ampiezza della banda di rete destinata al
protocollo ICMP, ad esempio mediante tecniche di Committed Access Rate
(CAR).

::

   **Hardening del sistema
   Minaccia** Accesso non autorizzato alle informazioni (es. da Memory dump attack).

   **Contromisure**  Sui sistemi operativi server è necessario, se possibile tecnicamente e se consentito
   dalle regole del supporto tecnico dei fornitori, disabilitare la generazione dei dump di
   memoria di sistema (“core dump”).
   Laddove ciò non fosse possibile, è necessario configurare i sistemi in modo che i dump
   contengano la minor quantità possibile di informazioni sensibili.

In ogni caso, i dump di memoria possono essere inviati ai fornitori solo
in presenza di un accordo di riservatezza e con modalità di trasmissione
atte a garantirne la riservatezza.

::

   **Hardening del sistema
   Minaccia** Compromissione delle comunicazioni. (es. Cache poisoning)
   Falsificazione di identità.
   Furto di credenziali di autenticazione.
   Negazione dei servizi.
   Violazione della sicurezza, rispetto alle politiche di sicurezza dell’organizzazione (da
   Malware),

   **Contromisure**  - Assicurarsi di utilizzare versioni di software DNS più recenti ed installare tutte le
   patch di sicurezza disponibili;

   - Rimuovere dal server DNS qualsiasi altro servizio e software non necessari al suo
       funzionamento;
   - Proteggere i server DNS con un firewall perimetrale;
   - Configurare i server DNS in modo tale da fare il meno affidamento possibile nei
       rapporti di fiducia con altri server DNS;
   - Configurare il DNS server in modo tale da limitare query ricorsive, memorizzare
       solo i dati relativi a domini richiesti e limitare la risposta al fine di fornire
       informazioni inerenti al solo dominio richiesto. Assicurarsi che non ci siano servizi
       attivi sul DNS che non sono utilizzati;
   - Utilizzare DNSSEC;
   - Utilizzare ARP e tabelle IP statiche sul server DNS;
   - Utilizzare comunicazioni crittografate con SSH per accedere al server DNS.

   **Hardening del sistema
   Minaccia** Perdita di riservatezza delle informazioni sulla rete e sui sistemi.
   Violazione della sicurezza, rispetto alle politiche di sicurezza dell’organizzazione
   (attacchi da Malware).

   **Contromisure**  Configurare i sistemi operativi, in particolare quelli che ospitano il software di rete (ad
   esempio il firewall) o esposti sulla rete, per impedire il footprinting disabilitando i
   protocolli e le porte inutilizzate che possono rivelare informazioni sul sistema, sui
   servizi installati, sulle versioni utilizzate, sul posizionamento dei sistemi e sulla logistica
   degli uffici, ecc.

   **Hardening del sistema
   Minaccia** Negazione dei servizi.

   **Contromisure**  - Configurare le applicazioni, i servizi e il sistema operativo tenendo sempre
   presente le possibili esposizioni ad attacchi DoS.

   - Ad es. è opportuno utilizzare estesamente architetture di tipo “stateless” o
       “RESTful” perché l’esaurimento delle risorse di sistema creando un numero elevato
       di false sessioni su sistemi che memorizzano lo stato di ciascuna di esse è una
       tecnica di attacco molto diffusa.
   - Assicurarsi che i criteri di blocco dell'account predisposti non possano essere
       sfruttati per bloccare service accounts ben noti (quindi il blocco di un account in
       caso di ripetuti tentativi di accesso deve essere temporaneo, e tra un tentativo e
       l’altro deve essere imposto un ritardo dell’ordine dei secondi)..
   - Assicurarsi che il sistema sia in grado di gestire alti volumi di traffico e che le soglie

massime per le risorse siano opportunamente impostate per gestire
carichi anormalmente elevati. A tale scopo è necessario effettuare
periodicamente il monitoraggio del carico sull'applicazione in
condizioni realistiche per verificare il corretto dimensionamento del
sistema in termini di risorse quali memoria RAM e CPU, numero di
sessioni concorrenti gestite e tempi di connessione e di risposta
effettivi in presenza di picchi di carico.

::

   **Hardening del sistema
   Minaccia** Negazione dei servizi (es. fault per buffer overflows).
   Attacchi all’integrità dei sistemi

   **Contromisure**  Disabilitare tutti i protocolli e i servizi legacy non sicuri, quali ad es. Telnet, FTP, r-
   commands, SNMP v1, ecc.

   **Hardening del sistema
   Minaccia** Negazione dei servizi (es. fault per buffer overflows).
   Attacchi all’integrità dei sistemi (software e configurazioni).
   Cancellazione o furto di informazioni (accidentale o da attacchi come ad es. il
   ransomware, ecc.).
   Uso non autorizzato di privilegi.

   **Contromisure**  Assicurarsi che la variabile d’ambiente PATH (usata su UNIX e Windows per accedere
   alle utilità di sistema da una finestra di terminale interattivo), non contenga percorsi
   sospetti né percorsi scrivibili da chiunque, ma solo quelli standard previsti dallo
   specifico sistema operativo. In particolare il PATH non deve mai contenere il percorso
   “.” che rappresenta la directory corrente.
   Su UNIX e Linux in particolare, l’utenza di root deve avere la variabile di ambiente
   PATH definita ad esempio come _PATH=”/usr/bin:/usr/sbin:/sbin”._

   **Disabilitazione delle interfacce di rete inutilizzate
   Minaccia** Negazione dei servizi (es. fault per buffer overflows).
   Attacchi all’integrità dei sistemi.
   Accesso non autorizzato ai sistemi.

   **Contromisure**  Disabilitare le interfacce wireless non necessarie al corretto funzionamento del server.

Ciò include le interfacce WiFi, Bluetooth e di altri protocolli
wireless, ivi compresi quelli proprietari usati da mouse e tastiere
wireless, su sistemi server e su Workstation critiche. Per quanto
riguarda tastiere e mouse wireless sulle postazioni desktop (non server)
è preferibile usare dispositivi bluetooth che consentano di utilizzare
l'autenticazione e la crittografia della comunicazione.

::

   **Anti-spam
   Minaccia** Negazione dei servizi (es. fault per buffer overflows).
   Abuso di risorse.

   **Contromisure**  Sui sistemi Linux e UNIX in genere, i Mail Transfer Agents o MTA (ad es. Sendmail e

Postfix) sono usati per ricevere email in entrata e trasferire I
messaggi all'utente o al mail server di destinazione. Se il sistema non
è un mail server o un SMTP relay, l'MTA deve essere configurato per

::

processare solo le mail generate localmente al sistema (ad es. da
applicative che generano un errore e inviano un messaggio a root per
scopi di diagnostica).

::

   **Hardening del sistema
   Minaccia** Accesso non autorizzato alle informazioni - Cold boot attack
   Accesso non autorizzato ai sistemi.

   **Contromisure**  - Utilizzare meccanismi di crittografia dei dischi di sistema (es. BitLocker);

   - Assicurarsi che tutti i dischi crittografati siano smontati (protetti) quando il
       computer è in una posizione in cui può essere rubato. Tipicamente ciò non è
       possibile con il disco su cui il sistema operativo è in esecuzione;
   - Impiegare un meccanismo di autenticazione a due fattori per l’avvio del sistema,
       ad esempio un PIN di pre-avvio o un dispositivo USB rimovibile contenente una
       chiave di avvio;
   - Assicurarsi che il computer abbia completato la procedura di arresto prima di
       lasciarlo incustodito;
   - Sui sistemi UNIX inserire un controllo di autenticazione per accedere in single user
       mode e disabilitare il boot interattivo (che consente di presentare un prompt
       interattivo di amministratore senza autenticazione);
   - Quando è previsto che il Sistema Operativo passi in modalità di sospensione a
       seguito di un periodo di inutilizzo, configurarlo invece per l’arresto completo;
   - Applicare le patch per kernel Linux quali TRESOR e Loop-Amnesia che modificano il
       kernel del sistema operativo in modo tale da utilizzare i registri della CPU (nel caso
       TRESOR registri di debug x86 e, in caso di Loop-Amnesia, i registri di profilazione
       AMD64 o EMT64) per memorizzare le chiavi di crittografia, piuttosto che
       memorizzarle in RAM;
   - Seguire l'approccio denominato "frozen cache" conosciuto anche come "cache as
       RAM", con il quale si disattiva la cache L1 della CPU per poterla utilizzare come
       supporto di memorizzazione delle chiavi di crittografia. Ovviamente questo
       approccio è oneroso dal punto di vista delle performance, ma si può ovviare a ciò
       utilizzando CPU multicore in cui tale cache viene disattivata per un solo core;
       Impiegare hardware in cui i moduli di memoria RAM sono saldati o incollati nel
       socket della scheda madre.

   **Inibizione dei terminali non in uso
   Minaccia** Accesso non autorizzato ad informazioni, causato dal personale utente per inadeguati
   meccanismi, strumenti, procedure o abilità tecniche atti a prevenire l'accesso non
   autorizzato al sistema.

   **Contromisure**  Tutti gli utenti devono essere sensibilizzati sui requisiti e sulle procedure di sicurezza
   per proteggere le apparecchiature incustodite.
   Le postazioni di lavoro e i sistemi informativi di qualsiasi tipo dotati di un terminale
   video e una tastiera, devono essere configurati in modo da bloccare la sessione di login
   e richiedere la password utente quando il sistema viene lasciato incustodito o inattivo
   per oltre 5 minuti.
   Ciò si applica specialmente ai sistemi server, anche se posizionati in data center o in
   zone ad accesso ristretto.

   **Limitazione del tempo di connessione
   Minaccia** Accesso non autorizzato ad informazioni.
   Abuso di privilegi.



   **Contromisure**  Sui sistemi più critici, laddove sia prevista una durata massima per lo svolgimento di
   determinati compiti, o quando l’uso di tali sistemi sia consentito solamente in certi
   orari, alla scadenza temporale prevista deve essere effettuato un logout automatico.

   **Limitazione dell'uso delle utility/servizi di sistema
   Minaccia** Accesso non autorizzato ad informazioni.
   Abuso di privilegi.
   Errori di amministrazione dei sistemi.
   Uso non autorizzato di privilegi.

   **Contromisure**  Limitare l'uso delle utility/servizi di sistema attraverso:

   - sistemi di identificazione e autenticazione per l'uso delle utility/servizi;
   - separazione delle utility di sistema dalle applicazioni;
   - autorizzazione all'uso delle utility/servizi solo per chi ne ha la reale necessità
       (compreso l'orologio di sistema);
   - tracciamento di ogni operazione privilegiata svolta con l'uso delle utility/servizi;
   - rimozione di tutte le utility/servizi non strettamente necessarie (in particolare i
       servizi di RAS o dial-up, gestione remota, ecc.);
   - di sabilitazione di tutte le porte non necessarie;
   - rimozione di tutti gli strumenti di sviluppo (compilatori e interpreti) su sistemi
       destinati ad ambienti di test, collaudo, certificazione e produzione.

   **Presentazione di messaggi di avvertimento
   Minaccia** Accesso non autorizzato ad informazioni causato dal personale utente per inadeguati
   meccanismi, strumenti, procedure o abilità tecniche atti a prevenire l'accesso non
   autorizzato al sistema o a proteggere i dati di autenticazione quando memorizzati o
   trasmessi.

   **Contromisure**  Includere nella schermata di log-on l'avvertimento che l'accesso è consentito ai soli
   utenti autorizzati.
   Richiamare nella schermata le norme interne o di legge che verrebbero violate in caso
   di accesso non autorizzato e le relative sanzioni.
   Informare chi si accinge ad accedere al sistema che le attività saranno monitorate e
   che ogni accesso non autorizzato ed ogni abuso saranno perseguiti a norma di legge.

   **Sincronizzazione degli orologi
   Minaccia** Accesso non autorizzato al sistema (macchina, configurazione, ecc.).
   Abuso di privilegi da parte degli utenti.

   **Contromisure**  Sincronizzare l'orologio interno di tutti i sistemi e gli apparati di rete attraverso il
   protocollo NTP con un server “fidato” posizionato sulla propria intranet. Laddove
   tecnicamente possibile (sistemi UNIX e apparati di rete evoluti) abilitare
   l’autenticazione verso il server NTP.
   Laddove tecnicamente realizzabile, il server NTP deve a sua volta ottenere l’ora esatta
   attraverso un segnale radio proveniente da stazione terrestre o satellitare (GPS).
   Per le reti di piccole dimensioni, laddove non sia possibile avere un server NTP proprio,
   utilizzare comunque un server NTP “fidato” unico per tutti i sistemi, come ad es. quello
   dell’Istituto Nazionale di Ricerca Metrologica (INRIM) (ex Istituto Elettrotecnico
   Nazionale Galileo Ferraris).


   #### 5.2.3 Utenze

   **Accesso privilegiato nominativo
   Minaccia** Abuso di privilegi da parte degli utenti.
   Abuso di risorse.
   Accesso non autorizzato alle informazioni.
   Cancellazione dei log di accountability e/o ripudio di operazioni effettuate.

   **Contromisure**  Disabilitare la possibilità di accesso ai sistemi (locale o remoto) utilizzando utenze
   amministrative impersonali come “root” o “Administrator”.
   Gli amministratori devono accedere con utenze nominative abilitate ai rispettivi
   compiti (ad es. abilitate all’uso del comando “su” su Unix, o appartenenti al gruppo
   Administrators su Windows).

   Valgono inoltre i principi generali già introdotti nel paragrafo [rif. 5.1.1].

   #### 5.2.4 Autenticazione

   Ai principi generali introdotti nel paragrafo [rif. 5.1.2], si aggiungono le indicazioni, di cui di seguito:

   **Identificazione e autenticazione degli utenti a livello di sistema
   Minaccia** Abuso di privilegi da parte dell’utente.
   Accesso non autorizzato alle informazioni.
   Falsificazione di identità.
   Tentativi di frode.
   Uso non autorizzato di privilegi.

   **Contromisure**  Richiedere l'autenticazione per svolgere qualsiasi tipo di attività di rilievo (compreso lo
   shutdown del sistema).
   Utilizzare tecniche di identificazione e autenticazione a due fattori, ad es. basate su pin
   e token o su pin e impronta biometrica, non solo per l’accesso amministrativo a sistemi
   critici ed apparati di rete e di sicurezza, ma anche per l’accesso ad applicativi che
   trattano dati personali sensibili, dati di traffico telematico e telefonico, dati bancari.

   #### 5.2.5 Autorizzazione

   Ai principi generali introdotti nel paragrafo [rif. 0], si aggiungono le indicazioni, di cui di seguito:

   **Gestione delle informazioni segrete di autenticazione degli utenti
   Minaccia** Perdita di riservatezza delle informazioni.
   Furto di credenziali di autenticazione.
   Falsificazione di identità.

   Contromisure (^) Per i file contenenti le password e altre informazioni riservate relative agli account
   utente, valgono le seguenti restrizioni:

   - Possono essere salvati solo su file system che supportano meccanismi di controllo
       accessi a livello di singolo utente.
   - Devono essere protetti con diritti di accesso il più possibile restrittivi.
   - Devono contenere le password in formato hashed (non invertibile) protetto con un
       codice (“salt”) e non tramite crittografia reversibile. L’hash non deve essere basato
       su MD5, né SHA-1. Preferibilmente deve essere usato l’algoritmo SHA-2 512.
       Questa impostazione ad es. è possibile per il file delle password sui moderni

sistemi operativi UNIX-like e Linux.

::

   **Autorizzazioni basate sui ruoli
   Minaccia** Perdita di riservatezza delle informazioni

   Contromisure (^) Per le informazioni di autorizzazione valgono le seguenti regole:

   - Utilizzare meccanismi autorizzazione di sistema e applicativa basata sui ruoli per
       garantire che solo gli utenti con il livello appropriato di autorizzazione siano
       autorizzati ad accedere a dati sensibili e che tali autorizzazioni discendano da un
       ruolo organizzativo e non da una abilitazione “ad hoc” che è spesso sinonimo di
       eccezione non tracciata e non autorizzata formalmente.
   - Utilizzare la protezione basata sui ruoli con il massimo livello possibile di
       granularità, per distinguere tra utenti che possono creare, visualizzare, aggiornare
       e cancellare dati, distinguendo anche tra le diverse tipologie di dati e di
       funzionalità applicative.
   - A livello di sistema, utilizzare ruoli distinti per diversi compiti amministrativi come
       il backup, l’esecuzione di applicativi, l’avvio di specifici servizi di rete, la
       configurazione dell’audit e la visualizzazione dei log, ecc.

   #### 5.2.6 Crittografia

   Valgono i principi generali introdotti nel paragrafo [rif. 5.1.1.4].

   #### 5.2.7 Documentazione

   Valgono i principi generali introdotti nel paragrafo [rif. 5.1.1.5].

   #### 5.2.8 Logging

   Valgono i principi generali introdotti nel paragrafo [rif. 5.1.1.6].

   #### 5.2.9 Antivirus

   **Prevenzione e individuazione di codice malevolo sul sistema operativo
   Minaccia** - Violazione della sicurezza, rispetto alle politiche di sicurezza dell’organizzazione,
   causata da Malware.

   - Negazione dei servizi causata da Malware.
   - Violazione di leggi, di regolamenti, di obblighi contrattuali.

   **Contromisure**  Su sistemi sia client sia server è necessario installare un software antivirus e
   antimalware di riconosciuta efficacia, in grado di rilevare e rimuovere keylogger,
   spyware, trojans, worms, ransomware ed ogni altro tipo di malware conosciuto.
   I sistemi devono essere configurati in modo che l'antivirus/antimalware:
   - sia eseguito in modo automatico all'avvio della macchina senza possibilità di
   disattivazione da parte di utenti non autorizzati;
   - esegua in automatico l'aggiornamento della lista di definizione dei virus (DAT)
   anche più volte al giorno mediante un'infrastruttura di sistemi dedicati alla
   distribuzione del DAT;
   - esegua una scansione approfondita del disco fisso almeno una volta alla settimana,

in orari che riducano l'impatto sulle attività lavorative (ad es.
durante la pausa pranzo);

::

   - esegua una scansione anche dei file compressi fino a 3 livelli di nidificazione;
   - preveda una gestione remota per la segnalazione di infezioni virali;
   - abbia funzionalità di tipo euristico per la rilevazione dei virus che consenta di
       inserire in "quarantena" tutti i file ritenuti sospetti dal motore euristico;
   - si integri nel sistema operativo al livello di file system e nel software di gestione
       della posta;
   - notifichi, durante la fase di shutdown, se è presente un dispositivo removibile.
   L’amministratore di sistema deve verificare (e se necessario effettuare manualmente)
   l’effettivo aggiornamento dei sistemi anti-virus con cadenza almeno mensile.

   #### 5.2.10 Procedure

   Alle linee guida ‘Procedure generali’ (Change management, Maintenance, Patching,Secure testing,
   Disposal) introdotti nel paragrafo [rif. 5.1.7, 5.1.7], si aggiungono, per l’ambito specifico, le indicazioni di cui
   di seguito:

   **Controlli sulla regolamentazione dell’uso del codice mobile per Sistemi Operativi
   Minaccia** - Violazione della sicurezza, rispetto alle politiche di sicurezza dell’organizzazione,
   causata da Malware.

   - Negazione dei servizi causata da Malware.
   Violazione di leggi, di regolamenti, di obblighi contrattuali.\
   Nel caso in cui si utilizzi “mobile code” (ad es. JavaScript / VBScript scaricati da siti web,
   Java applets, controlli ActiveX, codice Adobe Flash o Shockwave, documenti PDF attivi
   o anche semplici macro VBA trasferite attraverso documenti Microsoft Office), è
   necessario controllare che il “mobile code” non effettui operazioni non autorizzate.
   In particolare è necessario predisporre il maggior numero possibile di controlli tra
   quelli di seguito elencati:
   - esecuzione del mobile code in un ambiente di test isolato logicamente (sistemi di
   malware analysis in grado di analizzare il mobile code);
   - blocco di ogni utilizzo di mobile code sulle postazioni di lavoro e sui server;
   - blocco della ricezione di mobile code da internet (operato dai firewall perimetrali);
   - attivazione delle misure tecniche disponibili sul browser in uso per bloccare o
   quanto meno mettere in sicurezza l’utilizzo del mobile code, ad es. impedendo che
   il mobile code possa eseguire qualsiasi operazione sul sistema operativo, o
   all’esterno di una “sandbox” predisposta dal browser;
   - limitazione delle risorse di sistema che possono essere utilizzate dal mobile code;
   - attivazione di controlli crittografici per autenticare il mobile code (firma digitale del
   codice).

   **Controlli dell'installazione di software sui sistemi in funzione
   Minaccia** Negazione dei servizi.
   Attacchi all’integrità dei sistemi (software e configurazioni).

   **Contromisure**  Devono essere in vigore procedure per controllare l'installazione ed i cambiamenti del
   software sui sistemi di produzione. L’installazione deve essere effettuata seguendo
   scrupolosamente le indicazioni scritte fornite dal produttore e rispettando l’ordine
   delle operazioni da compiere. Nelle procedure devono essere indicate le istruzioni per i
   controlli che possono variare in relazione alla tipologia di ambiente/sistema operativo.


   **Autorizzazione per trasferimento di informazioni, strumenti elettronici e supporti all'esterno
   Minaccia** Accesso non autorizzato alle informazioni.
   Divulgazione di informazioni riservate.
   Uso non autorizzato di privilegi.
   Violazione di leggi, di regolamenti, di obblighi contrattuali.

   **Contromisure**  Il trasferimento all'esterno del sito aziendale o dell'organizzazione di informazioni
   contenute su strumenti o supporti elettronici, oppure in altre tipologie di supporti (es.
   atti e documenti cartacei) deve avvenire mediante preventiva autorizzazione dei
   soggetti responsabili.
   Per il trasferimento di archivi contenenti dati personali presso fornitori esterni
   operanti nell’Unione Europea, è necessaria l’autorizzazione del Titolare e può
   richiedere l’aggiornamento dell’informativa agli utenti laddove necessario. Il fornitore
   esterno deve essere formalmente nominato responsabile del trattamento.
   Il trasferimento di tali archivi all’esterno dell’Unione Europea deve essere impedito.

   **Security awareness: come combattere il phishing/pharming
   Minaccia** Divulgazione di informazioni riservate.
   Violazione della sicurezza, rispetto alle politiche di sicurezza dell’organizzazione.
   Violazione di leggi, di regolamenti, di obblighi contrattuali.

   **Contromisure**  Sensibilizzare il personale sui rischi del phishing/pharming (divulgazione non
   autorizzata a terzi di informazioni riservate o critiche, perdita delle informazioni ad es.
   da ransomware, ecc.).
   Istruire il personale sulle norme di comportamento cui attenersi per diminuire i rischi
   di phishing/pharming. Tali norme dovrebbero, almeno, indicare di:

   - non fare affidamento sull’intuito per distinguere tra richieste legittime e illegali di
       informazioni riservate, ma piuttosto di tentare di comprendere appieno ogni
       richiesta ricevuta prima di effettuare qualsiasi scelta;
   - non consegnare mai informazioni personali o riservate a individui o aziende
       sconosciuti;
   - eliminare messaggi e-mail che richiedono informazioni riservate o l'. Se la richiesta
       appare legittima, verificatene telefonicamente l’autenticità;
   - non disabilitare le protezioni aziendali antivirus, anti-phishing/pharming o altre
       misure di sicurezza (ad esempio quelle del browser);
   - contattate l’assistenza IT nel caso di comunicazioni ricevute per e-mail, telefono,
       fax o messaggistica immediata, che richiedono informazioni aziendali o personali.

   **Security awareness: prevenzione infezioni da malware
   Minaccia** - Violazione della sicurezza, rispetto alle politiche di sicurezza dell’organizzazione.

   - Violazione di leggi, di regolamenti, di obblighi contrattuali.
   - Compromissione delle comunicazioni.
   - Furto di credenziali di autenticazione (es. keylogger).

   **Contromisure**  Verificare il contenuto della clipboard prima di incollarlo su un terminale o sulla barra
   degli indirizzi del browser web o all'interno di un messaggio di posta elettronica;
   Scaricare e installare software solo da siti web riconosciuti e certificati;
   Non aprire file o archivi sospetti;
   Su Windows non aprire file eseguibili (EXE) privi di firma digitale, né file CMD, BAT,
   REG.
   Su sistemi Windows o anche UNIX (dotati di interfaccia grafica tipo KDE o GNOME),

non aprire mai i file con un doppio click in base all'icona
visualizzata: visualizzare e controllare sempre l'estensione del file,
perché un eseguibile contenente un malware può celarsi dietro l'icona
falsificata di un file PDF o altro; Indipendentemente dalla piattaforma
in uso, Linux o Windows, controllare i file di installazione software
attraverso l'uso di programmi capaci di rilevare la presenza di malware.

::

   ### 5.3 SICUREZZA DEL WEB BROWSER

   Di seguito viene fornita una vista delle principali minacce e delle relative contromisure da adottare.

   #### 5.3.1 Architettura

   **Architettura
   Minaccia** Accesso non autorizzato al sistema.
   Violazione della sicurezza, rispetto alle politiche di sicurezza dell’organizzazione.
   Violazione di leggi, di regolamenti, di obblighi contrattuali.

   **Contromisure**  - Utilizzare un sistema di protezione del perimetro (Firewall) in grado di effettuare
   Web Application Firewalling, posizionato tra la rete dei client e tutte le altre.

   - Installare un IDS (intrusion detection system) o IPS (intrusion prevention system) in
       grado di analizzare le richieste Web.
   - Impedire la manipolazione DNS: utilizzare DNS attendibile e protetto.
   - Bloccare i punti di accesso wireless e utilizzare un sistema di protezione come Wi-
       Fi Protected Access 2 e access point non vulnerabili (con firmware aggiornato)
       rispetto all’attacco KRACK precedentemente citato.

Nota Bene. Si tenga presente che i dispositivi portatili personali
possono eludere tali contromisure.

::

   #### 5.3.2 Hardening

   **Hardening del browser
   Minaccia** Accesso non autorizzato al sistema.
   Compromissione delle comunicazioni.
   Furto di credenziali di autenticazione (es. keylogger).
   Violazione della sicurezza, rispetto alle politiche di sicurezza dell’organizzazione.
   Violazione di leggi, di regolamenti, di obblighi contrattuali.

   **Contromisure**  - Utilizzare il browser con un account utente a bassi privilegi (ovvero senza privilegi
   di amministratore) in modo da limitare le possibilità di un attacco (security exploit)
   di compromettere l'intero sistema operativo.

   - Impostare il browser in modo da controllare la validità dei certificati presentati dai
       server, utilizzando le liste di revoca dei certificati (CRL), l'Online Certificate Status
       Protocol (OCSP), o altri meccanismi equivalenti.
   - Limitare/Disabilitare/Condizionare l'uso di:
       - Controlli ActiveX
       - Add-ons
       - Estensioni del browser (plug-ins)
       - JavaScript e Flash
       - Java Applets e applicazioni Silverlight.


   - “Mobile code” in generale.
   Ad esempio, su Internet Explorer esiste la possibilità di esprimere delle white list
   e/o delle black list per controlli ActiveX, add-ons, ed estensioni del browser.
   - Abilitare (se disponibili) meccanismi di sandbox integrati nel browser. Ad esempio
   a partire da IE 7 è disponibile il " _protected mode_ ", una tecnologia che sfrutta i
   meccanismi di sandboxing chiamati “ _Mandatory Integrity Control_ ”. Anche Google
   Chrome fornisce una sandbox che limita l’accesso al sistema operativo da parte
   delle pagine web.
   - Valutare la possibilità di eseguire il browser all’interno di un software di una
   sandbox selezionata e approvata dall’organizzazione.
   - Valutare l’adozione di estensioni e plugin di terze parti create a scopo di hardening
   del browser. A titolo di esempio: - il software “NoScript” che consente l’esecuzione
   di contenuti web basati su JavaScript, Java, Flash, Silverlight e altri plug-in solo se il
   sito è considerato attendibile ossia è stato precedentemente aggiunto a una
   whitelist.
   - Valutare l’adozione del software “MyWOT/WOT” (Web of Trust) che fornisce un
   servizio di reputazione sul livello di trust dei siti web.
   - Considerare di utilizzare il browser all’interno di un LiveCD. I LiveCD, che
   forniscono un sistema operativo da una sorgente non scrivibile e sono tipicamente
   dotati di browser internet. Se l'immagine originale LiveCD è priva di malware, tutto
   il software utilizzato, incluso il browser Internet, verrà caricato malware-free ogni
   volta che viene eseguito il boot dall'immagine LiveCD. Prestare però attenzione ad
   altro genere di pericoli: Qualsiasi traffico web non protetto (ad esempio, non
   utilizzando https) o verso siti web vulnerabili potrebbe ancora essere soggetto ad
   attacchi man-in-the-middle o altre manipolazioni basate sul traffico di rete.

   **Hardening del browser
   Minaccia** Accesso non autorizzato alle informazioni.
   Violazione della sicurezza, rispetto alle politiche di sicurezza dell’organizzazione
   (phishing e malware).
   Violazione di leggi, di regolamenti, di obblighi contrattuali.

   **Contromisure**  - Disabilitare la memorizzazione di password nel browser. Quasi tutti i browser e
   molti siti web in genere offrono la possibilità di ricordare le password per uso
   futuro. L'attivazione di questa funzionalità memorizza le password in un'unica
   posizione sul computer, rendendo più facile per un aggressore scoprirle se il
   sistema venisse compromesso. Se questa funzionalità risulta abilitata, è necessario
   disattivarla e cancellare le password memorizzate.

   - Attivare il blocco dei popup del browser. Le finestre di popup sono una notevole
       tecnica di "phishing". Il blocco dei popup è oggi una funzionalità standard dei
       browser e dovrebbe essere abilitato ogni volta che si naviga sul web. Può essere
       utilizzata anche su siti web specifici e non su altri, dove i popup potrebbero invece
       essere necessari.

   **Privacy durante la navigazione web
   Minaccia** Divulgazione di informazioni riservate.

   **Contromisure**  Adottare le seguenti misure a salvaguardia della privacy degli utenti, rispetto ai siti
   Web che monitorano le attività utente:

   - impostare una routine specifica per eliminare i cookie regolarmente. Alcuni cookie

possono costituire un rischio per la privacy in quanto tengono traccia
dei siti visitati. Non sempre è possibile bloccare i cookie, ma è
opportuno eliminarli (diversamente i cookie possono rimanere memorizzati
nel sistema per settimane o più)

::

   - Attivare funzionalità “Do Not Track”. “ Do Not Track” è un header HTTP che
       comunica ai siti visitati e alle terze parti i cui contenuti sono ospitati in tali siti che
       le proprie attività non devono essere tracciate. **Nota Bene.** L'invio di una richiesta
       “Do Not Track” ai siti non garantisce la protezione della privacy. I siti possono
       scegliere di rispettare la richiesta o continuare a eseguire attività che potrebbero
       essere considerate di monitoraggio anche se è stata espressa questa preferenza.
   - Utilizzare la navigazione anonima. **Nota Bene**. Il livello di protezione è diverso a
       seconda dei browser. In certi casi si tratta fi una difesa da attacchi locali: alcune
       info, come le password, la cronologia di ricerca e la cronologia delle pagine,
       vengono eliminate alla chiusura della scheda. In altri casi si tratta della difesa
       dall’attaccante esterno ossia viene protetto l' **anonimato durante la navigazione**.
   - Disattivare la condivisione della posizione geografica.

   **Hardening del browser: MIME Sniffing
   Minaccia** Attacchi all’integrità dei sistemi.
   Cancellazione o furto di informazioni (accidentale o da attacchi come ad es. il
   ransomware, ecc.).
   Violazione della sicurezza, rispetto alle politiche di sicurezza dell’organizzazione (es.
   malware, ecc.).

   **Contromisure**  Abilitare la barra delle informazioni per consentire all’utente di visualizzare il risultato
   di un’azione (es. cliccare su un link) prima di effettuarla.
   Disabilitare la possibilità per i siti web di iniziare un download senza l’accettazione
   esplicita dell’utente, ad es. da codice (Internet Explorer).
   Abilitare le funzionalità di MIME Sniffing che consentono di “marcare” un file collegato
   a un download attraverso il suo MIME Type, per evitare che un codice eseguibile venga
   visualizzato come testo o altro documento (es. PDF) per invogliare l’utente ad aprirlo.

   **Hardening del browser: segnalazione errori
   Minaccia** Divulgazione di informazioni riservate.

   **Contromisure**  Limitare/Disabilitare i servizi di “segnalazione automatica degli errori”, al fine di evitare
   la divulgazione di dati personali e di altre informazioni riservate.

   **Hardening del sistema operativo che ospita il browser
   Minaccia** Violazione della sicurezza, rispetto alle politiche di sicurezza dell’organizzazione.

   **Contromisure**  Eseguire l’hardening del sistema operativo che ospita il browser. L’hardening del
   sistema operativo è oggetto di un paragrafo specifico [rif. 5.2.2]

   #### 5.3.3 Autorizzazione

   Ai principi generali introdotti nel paragrafo [rif.5.1.3], si aggiungono le indicazioni, di cui di seguito:

   **Autorizzazione
   Minaccia** Accesso non autorizzato al sistema (macchina, configurazione, etc.)

   **Contromisure**  Proteggere i parametri di sicurezza dagli utenti finali: essi devono essere modificabili

solo da un'utenza amministrativa.

::

   #### 5.3.4 Crittografia

   Ai principi generali introdotti nel paragrafo [rif. 5.1.4], si aggiungono le indicazioni, di cui di seguito:

   **Crittografia
   Minaccia** Accesso non autorizzato alle informazioni.
   Divulgazione di informazioni riservate.
   Crittografia debole o non validata.
   Generazione e/o gestione inadeguata delle chiavi crittografiche.

   **Contromisure**  Valgono i principi generali introdotti nel paragrafo [rif. 5.1.4].

   #### 5.3.5 Procedure

   Alle linee guida ‘Procedure generali’ (Change management, Maintenance, Patching, Secure testing,
   Disposal) introdotti nel paragrafo [rif. 5.1.7], si aggiungono, per l’ambito specifico, le indicazioni di cui di
   seguito:

   **Patching
   Minaccia** Accesso non autorizzato ai sistemi (risorse di sistema, configurazioni, interfacce
   amministrative, ecc.).
   Accesso non autorizzato alle informazioni.
   Cancellazione o furto di informazioni (ad es. da ransomware, ecc.).
   Compromissione delle comunicazioni.
   Negazione dei servizi.
   Violazione della sicurezza, rispetto alle politiche di sicurezza dell’organizzazione
   (malware)
   Violazione di leggi, di regolamenti, di obblighi contrattuali.

   **Contromisure**  È necessario controllare periodicamente il sito web del fornitore per gli aggiornamenti.
   A tal fine si fa notare che:

   - Alcuni browser controllano automaticamente gli aggiornamenti disponibili
   - Alcuni fornitori offrono la notifica automatica degli aggiornamenti tramite una
       mailing list.

   **Sensibilizzare il personale sui rischi che la navigazione in Internet via Browser comporta
   Minaccia** Violazione della sicurezza, rispetto alle politiche di sicurezza dell’organizzazione (es.
   malware, ecc.).


   **Contromisure**  Sensibilizzare il personale sui rischi che la navigazione in Internet via Browser
   comporta. Di seguito le principali norme comportamentali da seguire:

   - Non fare clic su collegamenti senza considerare i rischi che ne potrebbero derivare
       (evitare di cliccare su link sospetti presenti nelle pagine).
   - Prestare attenzione al fatto che gli indirizzi di pagine Web potrebbero essere
       mascherati e portare in un sito imprevisto.
   - Considerare che ogni volta che un sito web richiede che vengano abilitate
       determinate funzionalità o installati software e aggiornamenti, si mette a rischio il
       computer. Ad es. non aggiornare mail il Flash Player su richiesta di una pagina web
       ma solo da pannello di controllo.


   - Non riutilizzare la stessa password per siti diversi.
   - Non fornire mai online informazioni personali a meno di non essere certi che il sito
       sia valido e le transazioni sicure: prima di inserire qualsiasi informazione personale,
       controllare la barra degli URL del browser al fine di accertarsi che il sito sia quello
       atteso e che sia presente la dicitura "https:" e un'icona a forma di lucchetto ad
       indicare che la connessione al sito è protetta e che il certificato server è valido.
   - Evitare Wi-Fi pubblici o gratuiti: l’attaccante spesso utilizza sniffers wireless per
       rubare le informazioni degli utenti quando vengono inviate su reti non protette. Il
       modo migliore per proteggersi da questo attacco è evitare di utilizzare queste reti,
       oppure utilizzarle solo con una VPN che incapsuli tutto il traffico in un tunnel
       cifrato.
   - In caso di individuazione di una “falsa” pagina di autenticazione segnalarla al team
       di sicurezza interna all’organizzazione per procedere all’oscuramento della
       medesima e possibilmente all’individuazione dei responsabili.

   #### 5.3.6 Informazioni addizionali

   **Riferimenti CERT
   CERT/CC** - Technical Trends in Phishing Attacks,
   [http://www.cert.org/archive/pdf/Phishing_trends.pdf](http://www.cert.org/archive/pdf/Phishing_trends.pdf)

   - Spyware, [http://www.cert.org/archive/pdf/spyware2005.pdf](http://www.cert.org/archive/pdf/spyware2005.pdf)
   **US-CERT** - Evaluating Your Web Browser's Security Settings, [http://www.us-](http://www.us-)
   cert.gov/ncas/tips/st05-001
   - Browsing Safely: Understanding Active Content and Cookies, [http://www.us-](http://www.us-)
       cert.gov/ncas/tips/st04-012
   - Understanding Website Certificates, [http://www.us-cert.gov/ncas/tips/st05-010](http://www.us-cert.gov/ncas/tips/st05-010)
   - Understanding Internationalized Domain Names, [http://www.us-](http://www.us-)
       cert.gov/ncas/tips/st05-016
   - Avoiding Social Engineering, [http://www.us-cert.gov/ncas/tips/st04-](http://www.us-cert.gov/ncas/tips/st04-) 014

   **Riferimenti Prodotti
   Microsoft
   Internet Explorer**

   Microsoft Internet Explorer (IE) è un browser web integrato nel sistema
   operativo Microsoft Windows. Per informazioni aggiornate sulle impostazioni di
   protezione e privacy per Internet Explorer, visitare il sito:
   [http://windows.microsoft.com/en-us/internet-explorer/ie-security-privacy-](http://windows.microsoft.com/en-us/internet-explorer/ie-security-privacy-)
   settings.
   **Mozilla Firefox** Mozilla Firefox è un popolare browser di terze parti per Windows, Mac e Linux.
   Per informazioni su come mantenere le informazioni protette e sicure con la
   navigazione privata di Firefox, le funzioni di password e altre impostazioni di
   protezione, visitare il sito:
   https://support.mozilla.org/en-US/products/firefox/privacy-and-security.
   **Apple Safari** Per informazioni visitare la pagina (selezionare "Privacy e sicurezza" nel menu):
   [http://help.apple.com/safari/mac/8.0/](http://help.apple.com/safari/mac/8.0/)
   **Google Chrome** Per ulteriori informazioni sulla sicurezza di Chrome (caratteristiche e
   funzionalità) si rinvia alla pagina (selezionare le opzioni visualizzate
   nell'argomento):
   https://support.google.com/chrome#topic=3421433.

   Opera (^) - Security badges,
   [http://help.opera.com/opera/Windows/1857/en/private.html#badges](http://help.opera.com/opera/Windows/1857/en/private.html#badges)

   - Web preferences,

http://help.opera.com/opera/Windows/1857/en/controlPages.html#conten t

::

   Chromium (^) Security information, https://www.chromium.org/Home/chromium-security

   ### 5.4 SICUREZZA DELLE POSTAZIONI DI LAVORO

   #### 5.4.1 Architettura

   **Protezione reti extranet (ad es., Internet)
   Minaccia** Furto di credenziali di autenticazione

   **Contromisure**  Provvedere ad un'adeguata protezione dell'infrastruttura di rete nella quale è
   operativa la PdL, mediante la configurazione di uno o più dispositivi (firewall, proxy
   server, etc.) di protezione dalle reti esterne (Internet e reti di partner e fornitori).
   Prevedere inoltre una segmentazione della rete interna che isoli tramite firewall le PdL
   in una apposita sezione di rete.

   **Continuità elettrica delle PdL
   Minaccia** Negazione dei servizi - Black out elettrico o mancanza improvvisa di energia elettrica

   **Contromisure**  Verificare che sia garantita l'alimentazione delle PdL in caso di interruzione della
   corrente elettrica, tramite l'utilizzo di dispositivi UPS che garantiscano anche la
   protezione dalle sovratensioni, prevedendo uno shutdown automatico allo scadere del
   periodo di autonomia dell’UPS. Effettuare un monitoraggio delle batterie degli UPS e
   prevederne la sostituzione qualora si ravvisi un degrado della loro capacità.

   **Protezione fisica dei dispositivi (fissi e mobili)
   Minaccia** Cancellazione o furto di informazioni.
   Danneggiamento, perdita o furto di un asset fisico..
   Negazione dei servizi.
   Violazione della sicurezza, rispetto alle politiche di sicurezza dell’organizzazione.

   **Contromisure**  Assicurare un cavo di acciaio galvanizzato, non meno di 3,5 mm di spessore, munito di
   chiusura a chiave o a combinazione al computer da proteggere o, in alternativa,
   utilizzare delle gabbie di sicurezza facilmente ancorabili, in cui riporre i dispositivi.
   Accertare che il cavo sia assicurato ad un elemento fisso non smontabile, facendone
   passare un’estremità nell’occhiello posto ad un capo del cavo ed inserire il lucchetto di
   sicurezza nell’apposito foro presente nel computer.

   #### 5.4.2 Hardening

   **Hardening del sistema operativo che gira sulla PDL
   Minaccia** Accesso non autorizzato ai sistemi (risorse di sistema, configurazioni, interfacce
   amministrative, ecc.).
   Accesso non autorizzato alle informazioni.
   Cancellazione o furto di informazioni (accidentale o da attacchi come ad es. il
   ransomware, ecc.).
   Violazione della sicurezza, rispetto alle politiche di sicurezza dell’organizzazione
   (malware).

   **Contromisure**  Eseguire l’hardening del sistema operativo che gira sulla PDL [rif. 5.2.2].


   **Hardening del/i web browser/s che gira/no sulla PDL
   Minaccia** Accesso non autorizzato alle informazioni.
   Cancellazione o furto di informazioni (accidentale o da attacchi come ad es. il
   ransomware, ecc.).
   Violazione della sicurezza, rispetto alle politiche di sicurezza dell’organizzazione
   (malware)

   **Contromisure**  I principi per la sicurezza del web browser sono oggetto di un paragrafo precedente.
   Effettuare controlli periodici al fine di verificare che i browser installati sulle PdL siano
   effettivamente quelli autorizzati e con le configurazioni di sicurezza previste (es.
   funzionalità di blocco dei popup, degli script, ecc.).

   **Hardening del sistema
   Minaccia** Negazione dei servizi (per spam su sistemi di messaggistica).

   **Contromisure**  Se è autorizzato l’uso di sistemi di messaggistica immediata, dotarsi di strumenti
   specifici "IM spam blockers".

   ### 5.4.3 Utenze

   Valgono i principi generali già introdotti nel paragrafo [rif. 5.1.1].

   ### 5.4.4 Autenticazione

   Valgono i principi generali già introdotti nel paragrafo [rif. 5.1.2].

   ### 5.4.5 Autorizzazione

   Valgono i principi generali già introdotti nel paragrafo [rif.5.1.3].

   ### 5.4.6 Crittografia

   Ai principi generali introdotti nel paragrafo [rif. 5.1.1.4 ], si aggiungono le indicazioni, di cui di seguito:

   **Crittografia
   Minaccia** Accesso non autorizzato alle informazioni

   **Contromisure**  Per l'accesso ai dati critici o sensibili definire requisiti di sicurezza più stringenti
   applicando tecniche di cifratura o altri meccanismi di sicurezza per rafforzare la
   protezione dagli accessi non autorizzati.

   ### 5.4.7 Documentazione

   Valgono i principi generali già introdotti nel paragrafo [rif. 5.1.1.5].

   ### 5.4.8 Logging

   Valgono i principi generali già introdotti nel paragrafo [rif. 5.1.1.6].


   ### 5.4.9 Procedure

   Ai principi generali introdotti nel paragrafo [rif. 5.1.7], si aggiungono le indicazioni, di cui di seguito:

   **Politica per la gestione delle postazioni di lavoro
   Minaccia** Abuso di privilegi da parte dell'utente.
   Abuso di risorse.
   Accesso non autorizzato ai sistemi (risorse di sistema, configurazioni, interfacce
   amministrative, ecc.).
   Accesso non autorizzato alle informazioni.
   Danneggiamento, perdita o furto di un asset fisico.
   Uso non autorizzato di privilegi.
   Violazione della sicurezza, rispetto alle politiche di sicurezza dell’organizzazione (es.
   malware, ecc.)
   Violazione di leggi, di regolamenti, di obblighi contrattuali.

   **Contromisure**  Verificare l'esistenza e l'applicazione di una formale politica di sicurezza che specifichi
   dei principi e delle linee guida per il corretto utilizzo delle postazioni di lavoro
   (workstation, desktop, notebook) da parte degli utenti, al fine di garantire la
   salvaguardia dell’informazione aziendale. Tale politica di sicurezza deve, nel rispetto
   della politica di sicurezza generale dell'azienda, specificare:

   - i requisiti di sicurezza fisica da soddisfare durante l'utilizzo dei dispositivi (ad
       esempio, il corretto posizionamento delle PdL);
   - i requisiti relativi alla corretta gestione della password, al backup, alla protezione
       contro i virus, alla configurazione del sistema operativo e delle applicazioni;
   - gli utilizzi non consentiti, estranei agli incarichi lavorativi, della propria postazione
       di lavoro;
   - i requisiti relativi al riutilizzo o alla rottamazione della PdL;
   - i requisiti relativi alla restituzione della PdL in caso di cessazione del rapporto di
       lavoro e/o cambio mansione.
   Eseguire delle attività di controllo e degli audit periodici sull'utilizzo della PdL da parte
   degli utenti, anche tramite tecnologie di controllo compatibili con quanto disposto
   dalle norme di legge.

   **Misure tecniche di garanzia di effettiva cancellazione dei dati o di loro non intellegibilità in caso di
   reimpiego o riciclo dell'apparecchiatura elettronica
   Minaccia** Accesso non autorizzato alle informazioni / ai dati personali contenuti in
   apparecchiature elettroniche dismesse.

   **Contromisure**  Adottare misure tecniche che garantiscano la non intellegibilità dei dati o l'effettiva
   cancellazione. Le prime possono consistere, tra l'altro, nella cifratura di singoli file o
   gruppi di file, di volta in volta protetti con parole-chiave riservate, note al solo utente
   proprietario dei dati, che può con queste procedere alla successiva decifratura.
   La cancellazione sicura delle informazioni, è ottenibile mediante misure tecniche
   consistenti in:

   - utilizzo di programmi informatici (quali wiping program o file shredder);
   - demagnetizzazione (degaussing) dei dispositivi di memoria basati su supporti
       magnetici o magneto-ottici (dischi rigidi, floppy-disk, nastri magnetici);
   - distruzione fisica dei dispositivi di memoria dismessi.

   **Politica di protezione da accesso fisico non autorizzato
   Minaccia** Accesso non autorizzato alle informazioni.


   Danneggiamento, perdita o furto di un asset fisico.
   Violazione della sicurezza (riservatezza, integrità, disponibilità) delle informazioni.

   **Contromisure**  Deve essere adottata una politica di sospensione della sessione per inattività su PC e
   notebook che preveda almeno che i terminali:

   - non debbano essere lasciati incustoditi durante e fuori orario di lavoro;
   - siano protetti da accessi non autorizzati con la sospensione della sessione
       mediante un salva-schermo che richieda l’autenticazione per continuare..
   Le informazioni critiche, riportate su carta o su supporti informatici e i dispositivi critici
   quando non utilizzati, dovrebbero essere chiusi a chiave (in cassaforte o armadio o altri
   mobili con caratteristiche di sicurezza) soprattutto quando l’ufficio è vuoto.
   Devono essere adottate regole e accorgimenti per evitare il danneggiamento/
   distruzione delle apparecchiature.

   **Sensibilizzazione del personale sui rischi di divulgazione di informazioni riservate
   Minaccia** Divulgazione di informazioni riservate (codici di accesso).
   Furto di credenziali di autenticazione.

   **Contromisure**  Effettuare opere di sensibilizzazione nei confronti del personale perché non divulghi a
   terze parti informazioni riservate o critiche quali, ad esempio, dati personali e
   password.

   ## 5.5 SICUREZZA DEI WEB APPLICATION SERVER

   Il componente estende l’analisi sulla sicurezza dei sistemi informativi che adottano tecnologia web based.

   ### 5.5.1 Architettura

   **Isolamento dei sistemi critici
   Minaccia** Accesso non autorizzato alle informazioni

   **Contromisure**  I sistemi critici come i Web Server devono avere un ambiente di elaborazione dedicato,
   strettamente controllato e monitorato.
   Tipicamente è necessaria una protezione perimetrale fisica (CED) e logica (firewall). Il
   web Server va collocato in un segmento di rete di front-end isolato tramite regole
   firewall dagli altri segmenti interni.

   **Failover
   Minaccia** Negazione dei servizi.

   **Contromisure**  Prevedere meccanismi di failover del sistema.
   Ad es. alimentatori, ventole, schede di rete e hard disk devono essere in
   configurazione ridondata.
   I sistemi middleware più critici dal punto di vista della disponibilità devono utilizzare
   meccanismi di clustering applicativo.
   I sistemi di front-end web più critici per la disponibilità o particolarmente impegnati
   per un elevato numero di connessioni devono usare meccanismi di clustering
   applicativo oppure devono essere posti alle spalle di sistemi di bilanciamento del
   carico.
   In tutti i casi, in presenza di un fault di un sistema, deve essere presente un processo di
   controllo (watchdog) in grado di rilevare il fault, generare un alert verso i sistemi di

monitoraggio e gestire il carico esistente attraverso gli altri sistemi,
eventualmente attivando sistemi di riserva configurati in modalità
“hot-standby”.

::

   **Protezione dei servizi web
   Minaccia** Attacchi all’integrità dei sistemi (software e configurazioni).

   **Contromisure**  Laddove sia necessario pubblicare in front-end web una serie di servizi che risiedono su
   molteplici server della rete interna, anziché esporre tutti questi server verso l’esterno è
   necessario invece installare un unico sistema di front-end opportunamente
   hardenizzato e posizionato su un segmento di rete dedicato, protetto dal firewall
   perimetrale e controllato da una sonda di intrusion detection.
   Tale sistema conterrà un servizio di “reverse proxy” o “portale” in grado di presentare
   in un’unica interfaccia l’insieme dei vari servizi interni, in modo controllato.
   Su tale sistema è necessario definire opportune politiche di controllo accessi e di
   autorizzazione, per consentire l’accesso alle varie sezioni del sito (corrispondenti ai
   diversi servizi interni) ai soli utenti autorizzati.

   **Sicurezza nelle connessioni nei sistemi web
   Minaccia** Accesso non autorizzato alle informazioni.
   Accesso non autorizzato al sistema.
   Attacchi all’integrità dei sistemi (software e configurazioni).
   Attacchi all’integrità delle informazioni.

   **Contromisure**  L’eventuale reverse proxy o portale di front-end deve essere configurato in modo da
   concentrare l’accesso solo a determinati server interni senza consentire ad es. la
   manipolazione delle URL o dei parametri di una richiesta http POST in modo tale da
   ottenere una connessione verso un indirizzo arbitrario della intranet.
   In conformità al principio della defense-in-depth, il firewall che protegge tale sistema
   deve essere configurato in maniera puntuale per consentire unicamente le connessioni
   previste da internet verso il server e dal server verso gli altri server interni (indirizzi ip e
   porte dei soli server effettivamente previsti).
   In tal modo l’accesso al portale non deve permettere accessi non autorizzati a reti a cui
   il sistema è inter-connesso.

   **Controllo del traffico dati
   Minaccia** Accesso non autorizzato alle informazioni.
   Attacchi all’integrità delle informazioni.
   (esempi: Zero-day exploit, Remote File Inclusion)

   **Contromisure**  Impiegare un Web Application Firewall (WAF):

   - Il web application firewall consente il controllo di tutti i tipi di richiesta HTTP (URL,
       form, cookie, query string, hidden field e parametri).
   - L'impiego di una blacklist di URL referenziate consente al WAF di bloccare exploit
       basati su vulnerabilità applicative "zero-day" (portate lo stesso giorno in cui la
       vulnerabilità diventa nota).

   **Controllo del traffico dati
   Minaccia** Accesso non autorizzato alle informazioni - HTML Injection

   **Contromisure**  Utilizzare un Web Application Firewall capace di monitorare la comunicazione tra gli
   utenti e l'applicazione e creare profili di interazioni HTML consentite.


   **Controllo del traffico dati
   Minaccia** Furto di credenziali di autenticazione
   Negazione del servizio

   **Contromisure**  Attivare, a livello perimetrale, un dispositivo di sicurezza intelligente di tipo IDS
   (Intrusion Detection System) o IPS (Intrusion Prevention System) per individuare (IDS)
   la presenza di codice malevolo e bloccare (IPS) le intrusioni.

   **Comunicazioni sicure tra differenti Application Server
   Minaccia** Accesso non autorizzato alle informazioni.
   Attacchi all’integrità delle informazioni.

   **Contromisure**  Quando un servizio web utilizza un’architettura distribuita, composta da server web di
   front-end e application server, ciascun server deve essere dotato di un certificato
   digitale e deve comunicare con gli altri in HTTPS attraverso TLS 1.2 o successivo.
   Sui sistemi maggiormente critici ed esposti come front-end su Internet, o usati per
   transazioni commerciali, la chiave privata deve essere custodita su un dispositivo
   hardware esterno (HSM).

   ### 5.5.2 Hardening

   **Hardening della piattaforma web
   Minaccia** Abuso di privilegi
   Abuso di risorse
   Accesso non autorizzato alle informazioni
   Accesso non autorizzato al sistema (macchina, configurazione, ecc.)

   **Contromisure**  Concedere al Web Server i privilegi minimi necessari per completare le operazioni
   richieste. In particolare dovrà utilizzare un account nominativo diverso da “root” o
   “administrator”.
   Disabilitare gli script, le applicazioni d'esempio, i servizi, le utility non strettamente
   necessari ed ogni altra funzionalità non pertinente agli scopi della piattaforma web,
   proposti dalle configurazioni di base del web server.
   Limitare l'accesso al file system da parte del web server separando la root directory e
   le directory virtuali dal resto del file system, facendole puntare su partizioni / mount
   dedicate.
   Disattivare sul web server la possibilità di navigazione del file system.
   Disabilitare il “Directory Listing”.
   Proteggere con opportune ACL su file system, i file di configurazione e le directory
   contenenti i siti web i log del server, i suoi eseguibili e i suoi file tempranei.
   Modificare i messaggi di sistema eliminando tutte le informazioni atte ad identificare il
   tipo di server, la versione e la build.
   Isolare il servizio web dal sistema che lo ospita e da altri servizi web utilizzando
   tecniche di “jail” o “chroot”, oppure containers Docker o altre tecniche di
   virtualizzazione in grado di fornire un efficace isolamento.
   Se l’application server lo consente, eseguirlo attraverso una sandbox per proteggere il
   codice da errori, trojans e codice malizioso (es. eseguire Apache Tomcat attraverso il
   Security Manager).
   Proteggere l’accesso all’interfaccia di amministrazione dell’application server
   attraverso un firewall o una VPN, in modo da restringere tale accesso ai soli indirizzi IP
   e utenti autorizzati. Forzare inoltre l’interfaccia amministrativa all’utilizzo di TLS 1.2 o
   successivi escludendo il semplice http.


   **Hardening della piattaforma web
   Minaccia** Accesso non autorizzato alle informazioni - Path traversal
   Violazione della sicurezza, rispetto alle politiche di sicurezza dell’organizzazione -
   esecuzione arbitraria di codice

   **Contromisure**  - Configurare l'application server in modo tale da rifiutare le URL con sequenze "../",
   al fine di impedire l'attraversamento di percorsi non protetti.

   - Bloccare i comandi e le utility di sistema con ACL restrittive.

   **Hardening della piattaforma web
   Minaccia** Negazione dei servizi.

   **Contromisure**  - Configurare le applicazioni, i servizi e il sistema operativo tenendo sempre
   presente le possibili esposizioni ad attacchi DoS.

   - Assicurarsi che i criteri di blocco dell'account predisposti non possano essere
       sfruttati per bloccare service accounts ben noti.
   - Assicurarsi che il sistema sia in grado di gestire alti volumi di traffico e che le soglie
       siano opportunamente impostate per gestire carichi anormalmente elevati.
   - Configurare il sistema operativo e il server web in modo da evitare il rischio di
       esaurimento di risorse in presenza di un elevato numero di connessioni non
       completate (es. TCP SYN COOKIES su kernel Linux/Unix e configurazione opportuna
       dei timeout sul server web).
   - Su server web soggetti ad un elevatissimo numero di connessioni, utilizzare
       applicativi con logica RESTful di tipo connectionless, o affidare l’onere di gestire i
       parametri della sessione al client attraverso l’inclusione dei parametri di sessione
       in cookies cifrati e non predicibili né manipolabili lato client.
   - Alcuni Application Server e Web Server espongono semplici interfacce
       amministrative per lo shutdown remoto che devono essere disabilitate (es. Apache
       Tomcat sulla porta TCP 8005).

   **Hardening della piattaforma web
   Minaccia** Accesso non autorizzato alle informazioni.
   Compromissione delle comunicazioni.
   Falsificazione di identità.
   Violazione della sicurezza, rispetto alle politiche di sicurezza dell’organizzazione (Cross-
   site scripting, Clickjacking, Hijacking, ecc.).

   **Contromisure**  Configurare sempre una dimensione massima accettabile per l’Header http.

Inoltre, considerare l'adozione di http security headers. Di seguito i
principali:

::

   - HttpOnly: istruisce il browser ad impedire che i cookies siano acceduti lato client a
       mezzo di script;
   - strict-transport-security: forza il browser a comunicare solo su HTTPS ;
   - cache-control impostato a "no-cache, no-store, must-revalidate" (laddove sono in
       gioco dati sensibili) ;
   - expires impostato a 0 (laddove sono in gioco dati sensibili) ;
   - content-security-policy: definisce quali sono le sorgenti attendibili dei contenuti
       (script) e quindi caricabili dal browser;
   - x-xss-protection: abilita un filtro sul browser che previene i XSS di tipo reflected;
   - x-frame-options: mette al riparo da un particolare tipo di attacco: il “clickjacking”.
       Di fatto impedisce agli iframes di caricare il sito;


   - public-key-pins: istruisce il browser di associare una opportuna public key con un
       certo web server. Ciò mette al riparo:
          o da Man-In-The-Middle attack (tentato con un certificate falso) o
          o dall’eventualità in cui la certification authority fosse compromessa.
   - x-content-type impostato a nosniff: mette al riparo da un particolare tipo di
       attacco: il “mime based attacks”. Di fatto impone al browser di attenersi
       rigorosamente al content type specificato (es. se il server imposta il content come
       text/html, il browser ne farà il rendering come text/html).

NB. Non tutti i browser supportano gli http security headers di cui
sopra. Anche la scelta del browser è importante.

::

   **Hardening della piattaforma web
   Minaccia** Accesso non autorizzato alle informazioni - Remote File Inclusion (RFI)

   **Contromisure**  L'utilizzo di blacklist di IP costruiti sulla base di osservazioni eseguite su avvenuti
   attacchi (es. di tipo RFI), potrebbero essere usati per bloccare altri tipi di attacchi
   portati dalla stessa origine.
   Ove possibile, limitare gli accessi a indirizzi IP o Reti specifiche.

   **Hardening della piattaforma web
   Minaccia** Crittografia debole o non validata.

   **Contromisure**  Non consentire il fallback a SSL (qualsiasi versione) né a TLS 1.1 o versioni inferiori.
   Deve essere richiesto l’uso obbligatorio almeno di TLS 1.2.

   **Hardening della piattaforma web
   Minaccia** Divulgazione di informazioni riservate.

   **Contromisure**  Rimuovere HTTP Response Headers che espongono informazioni sul web server. A
   titolo di esempio, in ambiente Microsoft, rimuovere:

   - Server– Specifica la versione del web server version.
   - X-Powered-By- Indica che il website è "powered by ASP.NET."
   - X-AspNet-Version- Specifica la versione di ASP.NET usata.

Disabilitare il metodo HTTP TRACE. A titolo di esempio:

::

   - in ambiente Microsoft, impostare la chiave di registro “EnableTraceMethod” (sotto
       HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\W3SVC\Parameters)
       a 0 (zero)
   - in ambiente Apache, configurare “TraceEnable off” in http.conf.
   - In Apache Tomcat disabilitare l’attributo allowTrace per ogni connettore.
   Su Apache Tomcat disabilitare inoltre lo Stack Tracing sul client.

   **Hardening della piattaforma web
   Minaccia** Negazione dei servizi (Buffer overflows).

   **Contromisure**  - Utilizzare linguaggi di programmazione che forniscono controlli automatici sulla
   dimensione dei buffer di memoria (o a tempo di compilazione o a runtime) come
   Java, Python o Perl.

   - Utilizzare le safe libraries (ad es. in C e C++), ovvero librerie di funzioni che
       implementano protezioni contro il buffer overflow quando tale protezione non è
       nativamente supportata dal linguaggio di programmazione.


   - Prevedere che sia il compilatore ad inserire le verifiche sulla dimensione di tutti i
       buffer nel codice compilato senza richiedere alcuna modifica al codice sorgente (a
       titolo di esempio, utilizzare il flag /GS per compilare codice sviluppato con
       Microsoft Visual C ++ ®. Il flag / GS fa sì che il compilatore inietti controlli di
       sicurezza nel codice compilato).

   **Integrità del software e dei dati nei sistemi web
   Minaccia** Attacchi all’integrità dei sistemi (software e configurazioni).

   **Contromisure**  Il web server deve proteggere il software, i dati e le informazioni memorizzate sul
   sistema con meccanismi appropriati per garantire un alto livello di integrità attraverso
   l’uso di firma digitale o MAC (message authentication codes).

   **Hardening del sistema operativo che ospita la piattaforma web
   Minaccia** Accesso non autorizzato al sistema.
   Compromissione delle comunicazioni.
   Furto di credenziali di autenticazione (es. keylogger).
   Violazione della sicurezza, rispetto alle politiche di sicurezza dell’organizzazione.
   Violazione di leggi, di regolamenti, di obblighi contrattuali.

   **Contromisure**  Eseguire l’hardening del sistema operativo che ospita il Web Server [rif. 5.2.2].

   ### 5.5.3 Utenze

   Valgono i principi generali già introdotti nel paragrafo [rif. 5.1.1].

   ### 5.5.4 Autenticazione

   Valgono i principi generali già introdotti nel paragrafo [rif. 5.1.2].

   ### 5.5.5 Autorizzazione

   A i principi generali già introdotti nel paragrafo [rif. 5.1.3], si aggiungono le seguenti indicazioni per il
   contesto specifico:

   **Autorizzazione
   Minaccia** Accesso non autorizzato ai sistemi (macchina, configurazione, ecc.).
   Accesso non autorizzato alle informazioni.

   **Contromisure**  Utilizzare e configurare opportunamente i meccanismi di controllo di accesso alle
   risorse esposte dal web server (a titolo di esempio l’autorizzazione di accesso a livello
   di specifiche URL fornita dal Framework .NET).

   ### 5.5.6 Crittografia

   Valgono i principi generali già introdotti nel paragrafo [rif. 5.1.4].


   ### 5.5.7 Documentazione

   Valgono i principi generali già introdotti nel paragrafo [rif. 5.1.5].

   ### 5.5.8 Logging

   Valgono i principi generali già introdotti nel paragrafo [rif. 5.1.6].

   ### 5.5.9 Sessioni

   **Contrasto delle riproduzioni di sessione
   Minaccia** Accesso non autorizzato alle informazioni.
   Compromissione delle comunicazioni.
   Falsificazione di identità.
   Uso non autorizzato di privilegi.

   **Contromisure**  Verificare che siano adottate le seguenti best practices:

   - Utilizzare token di sessione (ad es. cookie o sessionID) difficilmente predicibili
       (ossia random)
   - Configurare l'applicativo web in modo che venga verificata la validità e l'integrità di
       ciascun token di sessione (ad es. cookie o sessionID) associato ad una richiesta di
       accesso.
   - Generare un nuovo identificativo di sessione dopo il login (per evitare il session
       fixation ossia che il session ID sia forzato dall'esterno).
   - Limitare il periodo di scadenza del token di sessione in modo da limitare il tempo
       disponibile per sferrare un attacco.
   - Utilizzare un protocollo di comunicazione cifrato (TLS 1.2 o successivo) per la
       creazione di un canale di comunicazione protetto, e configurare il protocollo in
       modo che i cookie di autenticazione transitino solo mediante connessione HTTPS;
   - Configurare il client web (browser) in modo da consentire di non archiviare i dati di
       sessione sulla postazione di lavoro;
   - Prevedere un meccanismo che imponga di terminare una sessione qualora ne
       venga avviata una nuova con le medesime credenziali di autenticazione della
       precedente.
   - Attivare un meccanismo per la disconnessione automatica delle sessioni di lavoro
       dopo un periodo di inattività inferiore ai 5 minuti.

   **Gestione delle informazioni segrete di autenticazione degli utenti
   Minaccia** Accesso non autorizzato alle informazioni.
   Crittografia debole o non validata.
   Falsificazione di identità.
   Uso non autorizzato di privilegi.

   **Contromisure**  Mentre l’SSL/TLS protegge i cookie in rete, non impedisce loro di essere modificati nel
   computer del client. Per contrastare la minaccia di manipolazione dei cookie,
   crittografare i cookie utilizzando un HMAC.

   ### 5.5.10 Procedure

   A i principi generali già introdotti nel paragrafo [rif. 5.1.7], si aggiungono le seguenti indicazioni per il
   contesto specifico:


   **Controlli sulla regolamentazione dell’uso del codice mobile per Web Server
   Minaccia** Negazione dei servizi.
   Violazione della sicurezza, rispetto alle politiche di sicurezza dell’organizzazione.

   **Contromisure**  Controllare che nel caso in cui si sia concesso l’utilizzo del mobile code (codice, come
   Java Applet, che è trasmesso via rete e eseguito su una macchina remota, “a fianco” di
   altro mobile code, potenzialmente malevolo) non siano effettuate operazioni non
   autorizzate rispetto alla politica definita per l’utilizzo del codice mobile. In particolare,
   controllare il rispetto delle politiche riguardanti:

   - esecuzione del mobile code in un ambiente isolato logicamente;
   - blocco di ogni utilizzo di mobile code;
   - blocco della ricezione di mobile code dall’esterno;
   - attivazione di controlli crittografici per autenticare univocamente il mobile code.
   - rispetto delle security guidelines di programmazione sicura per il per mobile code.

   **Inventario piattaforma web
   Minaccia** Attacchi all’integrità dei sistemi (software e configurazioni).
   Errori di amministrazione dei sistemi.
   Negazione dei servizi.

   **Contromisure**  Mantenere un inventario aggiornato che evidenzi:

   - Le date di pubblicazione dei dati forniti dal servizio web;
   - La release software del servizio web con l'indicazione, nelle Release Notes, di tutte
       le modifiche introdotte (come nuove funzionalità, plug-in, etc.);
   - I sistemi su cui è implementato il servizio web;
   - L’owner o funzione responsabile dei servizi web e dei relativi sistemi.

   **Collaudo del servizio web
   Minaccia** Accesso non autorizzato alle informazioni.
   Uso non autorizzato di privilegi.
   Negazione dei servizi.

   **Contromisure**  Effettuare un collaudo del servizio web prima di renderlo operativo, a tal proposito:

   - Svolgere il test in un ambiente diverso da quello dello sviluppo;
   - Considerare, nelle specifiche di collaudo, le tipologie di browser maggiormente
       diffuse e le versioni più recenti;
   - Assicurarsi che durante la fase di testing siano predisposte verifiche mirate non
       solo alla componente funzionale ma si attui anche una mirata attività dedicata alle
       eventuali falle di sicurezza. A questo riguardo:
          - Utilizzare specifici software per il controllo della qualità del codice (analisi
             statica) che tenga conto dei princìpi di sicurezza della programmazione
             (SAST).
          - Utilizzare specifici software per l’analisi dinamica del codice (DAST).

   **Procedura di monitoraggio sull'uso del web server
   Minaccia** Accesso non autorizzato ai sistemi (risorse di sistema, configurazioni, interfacce
   amministrative, ecc.).
   Accesso non autorizzato alle informazioni.
   Attacchi all’integrità dei sistemi (software e configurazioni).
   Negazione dei servizi.

   **Contromisure**  Definire procedure che specifichino le modalità con cui monitorare il web server per
   garantirne la funzionalità e l'uso corretto. La procedura deve specificare cosa

monitorare (ambito del monitoraggio) e quando eseguire l'audit rimanendo
conformi ai requisiti di legge e alle policy in vigore
nell'organizzazione. Gli aspetti da considerare sono:

::

   - accessi autorizzati, includendo dettagli quali:
       - user ID;
       - indirizzo IP del client;
       - data e ora degli eventi chiave;
       - i tipi di eventi;
       - indirizzo delle risorse accedute;
   - tutte le operazioni privilegiate, come:
       - l'uso di account privilegiati (supervisor, root, administrator);
       - avvio e arresto del sistema;
       - collegamento e scollegamento di dispositivi di input/output;
   - tentativi di accesso non autorizzato, come:
       - azioni degli utenti falliti o rifiutati;
       - azioni fallite o rifiutate che coinvolgono dati o altre risorse;
       - violazioni della policy di accesso e notifiche generate da gateway e firewall;
       - alert da sistemi di intrusion detection;
   - alert o avaria dei sistemi come:
       - alert o messaggi inviati alle console di amministrazione;
       - eccezioni dei log dei sistemi;
       - allarmi provenienti da sistemi di gestione della rete;
       - allarmi generati dai sistemi di controllo degli accessi;
   - cambiamenti o tentativi di cambiamento delle configurazioni di sicurezza del
       sistema.

La procedura deve specificare la frequenza con cui effettuare l'audit
ogni qual volta sussista la necessità e comunque non oltre il termine di
1 mese.

::

   **Rimozione delle vulnerabilità nei sistemi web
   Minaccia** Accesso non autorizzato ai sistemi (risorse di sistema, configurazioni, interfacce
   amministrative, ecc.).
   Accesso non autorizzato alle informazioni.
   Negazione dei servizi.

   **Contromisure**  - Il web server deve essere accuratamente testato prima che le informazioni siano
   rese disponibili affinché vulnerabilità e malfunzionamenti siano rimossi.

   - Aggiornamenti o patch rilevanti la sicurezza devono essere installati dove ritenuto
       necessario. Se aggiornamenti o patch sono indisponibili, devono essere adottate
       contromisure addizionali per la riduzione della vulnerabilità (massimizzare la difesa
       perimetrale)
   - Il web server deve essere soggetto ad una analisi delle vulnerabilità tramite
       strumenti automatici di vulnerability assessment e le vulnerabilità specifiche per la
       sicurezza ritenute critiche e riscontrate devono essere rimosse.
   - L’analisi delle vulnerabilità deve essere eseguita ogni qual volta sussista la
       necessità e comunque non oltre il termine di 1 mese.

   **Accordi con i fornitori di servizi internet per scoprire l'attacco
   Minaccia** Negazione dei servizi.

Violazione della sicurezza, rispetto alle politiche di sicurezza
dell'organizzazione.

::


   **Contromisure**  Prevedere accordi contrattuali con il proprio Provider di servizi internet (Internet
   Service Provider "ISP") perché, soprattutto in fase di attacco in corso, sia possibile
   effettuare un'attività di tracciamento degli indirizzi di rete (IP) per tentare di
   individuare l'aggressore mediante un percorso a ritroso e provare a fermare l'attacco.

   ### 5.5.11 Programmazione e Configurazione

   **Convalida dell'input
   Minaccia** Accesso non autorizzato alle informazioni.

   **Contromisure**  - Evitare di utilizzare parametri nella stringa di query che contengono dati sensibili o
   dati che possono in qualche modo influenzare la logica di protezione sul server.
   Utilizzare invece un identificativo di sessione per identificare il client e
   memorizzare sul server gli elementi sensibili nell'archivio di sessione.

   - Preferire l'utilizzo di HTTP POST piuttosto che HTTP GET per inviare form di dati.
   - Adottare un processo di serializzazione (anche noto come deflating o marshalling)
       in modo da convertire i dati in una sequenza di bit da trasmettere sulla rete
   - Crittografare i parametri passati nella query string.
   - Validare tutti i parametri di input al fine di garantire la conformità allo standard
       adottato in termini di lunghezza minima e massima consentita, range di valori
       numerici consentiti, sequenze di caratteri e patterns ammessi e se e quando sono
       consentiti valori nulli.
   - Utilizzare un meccanismo di Whitelisting nella validazione dei parametri di query.

   **Convalida dell'input
   Minaccia** Compromissione delle comunicazioni - Cross-site request forgery (CSRF)

   **Contromisure**  Aggiungere a ciascuna transazione un valore numerico casuale di lunghezza elevata (da
   usare come token). Tale valore allegato alla richiesta viene convalidato rispetto al
   valore dato per quella specifica sessione utente. Pertanto, un aggressore non potrà
   incorporare una URL che rappresenta una transazione valida nella pagina controllata
   dall'attaccante.
   Richiedere un'interazione umana aggiuntiva per le transazioni sensibili in forma di
   autenticazione ripetuta o risposta a CAPTCHA.

   **Convalida dell'input
   Minaccia** Compromissione delle comunicazioni - Manipolazione dell'intestazione HTTP

   **Contromisure**  Non basare le decisioni di sicurezza sulle intestazioni HTTP. Ad esempio, non fidarsi di
   quanto riportato nell'intestazione "HTTP Referer" per determinare la provenienza di
   una richiesta in quanto facilmente falsificabile.

   **Convalida dell'input
   Minaccia** Accesso non autorizzato alle informazioni.
   Attacchi all’integrità dei sistemi
   Negazione dei servizi.
   (Ad es. per attacchi di injection ed esecuzione arbitraria di codice).


   **Contromisure**  Configurare il web service in modo da garantire l'attuazione di specifici controlli dei
   dati in ingresso. In particolare determinare:

   - Il set di caratteri consentito;


   - La lunghezza minima e massima dei dati;
   - L'intervallo numerico (range) dei dati;
   - Quali valori sono ammessi;
   - Se è previsto il tipo "NULL";
   - Se sono consentiti duplicati;
   - Il formato consentito dei nomi dei file, nel caso siano accettati come input, e
       verificarne la presenza nella gerarchia di directory dell'applicazione.

   **Convalida dell'input
   Minaccia** Accesso non autorizzato alle informazioni.
   Attacchi all’integrità dei sistemi
   Negazione dei servizi.
   (Ad es. con Cross-site scripting - XSS).

   **Contromisure**  Eseguire una convalida completa dell'input. Il sistema deve garantire che l'input da
   query strings, i campi delle form e i cookie siano validi. Considerare tutti gli input da
   parte degli utenti come potenzialmente dannosi, pertanto è necessario filtrare o
   sanitizzare l'input lato server. Validare tutti gli input per valori validi noti e quindi
   rifiutare tutti gli altri input. Utilizzare espressioni regolari per convalidare i dati di input
   ricevuti tramite i campi di form HTML, cookie e query strings.
   Utilizzare le funzioni HTMLEncode e URLEncode per codificare qualsiasi output che
   contiene l'input dell'utente. Questo converte gli script eseguibili in HTML innocuo.

   **Convalida dell'input
   Minaccia** Negazione dei Servizi (Buffer overflows)

   **Contromisure**  Eseguire una convalida completa dell'input. Questa è la prima linea di difesa contro il
   buffer overflow. Sebbene possa esistere un bug nel processo che consente all'input
   atteso di sconfinare le aree di memoria allocate, gli input inattesi sono in genere la
   causa principale di questa vulnerabilità. Filtrare l'input convalidandolo per tipo,
   lunghezza, formato e range.
   Quando possibile, limitare l'utilizzo di codice unmanaged (es. C, C++) da parte
   dell'applicazione e verificare accuratamente le API che usano codice unmanaged per
   garantire che l'input venga correttamente convalidato.
   Esaminare i casi in cui il codice managed chiama API che usano codice unmanaged al
   fine di assicurare che solo parametri appropriati possano essere passati come
   parametri all'API.
   Utilizzare specifici flag di compilazione del codice sorgente per verificare staticamente
   le formattazioni di stringhe e produrre eventuali avvisi di pericolo o di sospetto.

   **Convalida dell'input
   Minaccia** Accesso non autorizzato alle informazioni.
   Attacchi all’integrità dei sistemi
   Negazione dei servizi.
   (Ad es. da esecuzione arbitraria di codice).


   **Contromisure**   Evitate di utilizzare i nomi dei file come input dove possibile e utilizzare invece percorsi
   di file assoluti che non possono essere modificati dall'utente finale.
   Assicurarsi che i nomi dei file seguano gli standard di formato consentiti dal file system
   (se si deve accettare i nomi dei file come input) e convalidarli nel contesto
   dell'applicazione. Ad esempio, verificare che siano all'interno della gerarchia di
   directory dell'applicazione.

Assicurarsi che la codifica dei caratteri sia impostata correttamente
per limitare il modo in cui l'input può essere rappresentato
(canonicalizzazione).

::

   **Convalida dell'input
   Minaccia** Accesso non autorizzato alle informazioni (anipolazione dei campi di un Form).

   **Contromisure**  Invece di utilizzare i campi nascosti di una form, utilizzare gli identificativi di sessione
   allo stato di riferimento mantenuto nell'archivio di stato lato server.
   Validate tutti i campi di input al fine di garantire la conformità allo standard adottato in
   termini di lunghezza minima e massima consentita, range di valori numerici consentiti,
   sequenze di caratteri e patterns ammessi e se e quando sono consentiti valori nulli.
   Utilizzare un meccanismo di Whitelisting nella validazione dei campi di input.
   Usare e configurare in modo appropriato un firewall per l'applicazione web in uso.

   **Convalida dell'input
   Minaccia** Accesso non autorizzato alle informazioni (HTML Injection).

   **Contromisure**  Validare gli elementi HTML nel flusso HTTP in entrata che contiene i dati forniti
   dall'utente. Impiegando una convalida nativa dell'input dell'utente è possibile
   rimuovere qualsiasi sottostringa di sintassi HTML (come tag e link) dai contenuti
   testuali forniti dall'utente stesso.

   **Convalida dell'input
   Minaccia** Accesso non autorizzato alle informazioni (Path traversal).

   **Contromisure**  Validare l'input proveniente dal browser web attraverso l'uso di white list.
   Verificare che non esistano file documentali facilmente raggiungibili o il cui percorso
   sia intuitivo (ad es., solo digitando l'url corretto). Mascherare il percorso dei file
   documentali memorizzati nelle applicazioni web (ad esempio, con la conversione in
   hash dei nomi dei file o la visualizzazione del percorso con sequenze di lettere e
   numeri) provvedendo ad inserirli all’interno di specifici repository, utilizzando percorsi
   di tipo semantico complessi non facilmente riproducibili nell’ url.

   **Convalida dell'input
   Minaccia** Negazione dei servizi.

   **Contromisure**  Validare l'input proveniente dal browser web attraverso l'uso di white list.
   Valutare accuratamente tutti i dati di input sul server.
   Gestire le eccezioni nel codice dell'applicazione.

   **Personalizzazione dei messaggi di errore del web server
   Minaccia** Divulgazione di informazioni riservate (Attacchi che rivelano dettagli implementativi).

   **Contromisure**  Gestire le eccezioni nel codice dell'applicazione.
   Codificare e registrare le eccezioni che possono essere propagate all'esterno
   dell'applicazione.
   In caso di eccezione, restituire al client messaggi di errore generici (ad es., 404 Not
   Found, 408 Request Timeout) e/o codificati che non rivelino dettagli interni del
   sistema.

   **Password in memoria RAM
   Minaccia** Divulgazione di informazioni riservate (Memory dump attack).



   **Contromisure**  Il Web Server deve utilizzare le password hash invece di memorizzare il testo delle
   password in chiaro.
   Il Web Server può utilizzare la Tokenizzazione in modo che solo i dati rappresentativi
   saranno in memoria mentre i dati sensibili vengono memorizzati altrove;
   I Web Server basati su .NET e su Java possono utilizzare il tipo SecureString per limitare
   il tempo in cui le password non crittografate sono disponibili in memoria.

   ## 5.6 SICUREZZA DEI DBMS/DATABASE SERVER

   ### 5.6.1 Architettura

   **Isolamento dei sistemi critici
   Minaccia** Accesso non autorizzato alle informazioni

   **Contromisure**  I sistemi critici come i DBMS devono avere un ambiente di elaborazione dedicato,
   strettamente controllato e monitorato.
   Per tali sistemi vale quanto segue:

   - Devono essere posti su un sistema dedicato che ospita solo il DB (e non ad es. un
       Web Server, un Application Server, un Directory Server e o altri servizi importanti).
   - Devono essere posti su un “layer dati” (segmento) di rete diverso da quello dei
       sistemi di front-end e da quello delle postazioni di lavoro client.
   - I diversi layer di rete devono essere posti su interfacce diverse di un firewall
   - Il firewall deve consentire unicamente le comunicazioni strettamente necessarie
       da e per i DB rispetto agli altri sistemi (Web Server, Application Server, client
       interni).
   - Non deve essere consentita dai firewall nessuna connessione diretta da internet o
       altre reti esterne all’organizzazione, verso il layer dati che ospita i DBMS.

   **Failover
   Minaccia** Negazione dei servizi.

   **Contromisure**  Prevedere meccanismi di failover del sistema DB per i database più critici dal punto di
   vista della disponibilità del servizio.
   In tali casi, è necessario utilizzare architetture DBMS in cluster applicativi, scegliendo
   se possibile i sistemi di clustering nativi dello specifico prodotto piuttosto che soluzioni
   di terze parti.
   Quando un DBMS del cluster va in fault, un processo di controllo (watchdog) deve
   rilevare il problema, generare un alert verso i sistemi di monitoraggio e ripartire il
   carico di lavoro sui sistemi restanti, eventualmente attivando sistemi di riserva posti in
   configurazione “hot-standby”.
   Il cluster deve essere in grado di salvaguardare l’integrità dei dati dal punto di vista
   delle transazioni, attraverso opportuni meccanismi di replica in grado di avere i dati
   sempre coerenti rispetto all’ultima operazione di “commit” eseguita.

   **Controllo del traffico dati
   Minaccia** Accesso non autorizzato ai sistemi.
   Negazione dei servizi.

   **Contromisure**  Attivare, a livello perimetrale, un dispositivo di sicurezza intelligente di tipo IDS
   (Intrusion Detection System) o IPS (Intrusion Prevention System) per individuare (IDS)
   la presenza di codice malevolo e bloccare (IPS) le intrusioni.


   ### 5.6.2 Hardening

   **Hardening della piattaforma DBMS
   Minaccia** Accesso non autorizzato alle informazioni.
   Accesso non autorizzato ai sistemi.
   Negazione dei servizi.
   Uso non autorizzato di privilegi.

   **Contromisure**  Concedere al DBMS i privilegi minimi necessari per completare le operazioni richieste.
   In particolare i processi del DB devono essere eseguiti sul sistema nel contesto di una
   utenza non privilegiata (diversa da root/Administrator e dotata dei privilegi minimi
   necessari).
   Disinstallare o disabilitare tutte le componenti opzionali / aggiuntive del DBMS non
   strettamente necessarie (es. Reporting Services, Debugging, interfacce amministrative,
   servizi di replica o backup, servizi di ricerca Full Text, interfacce web o Web Services,
   ecc.). Prestare particolare attenzione a quelle componenti aggiuntive che espongono
   servizi o interfacce amministrative su specifiche porte TCP/IP.
   Rimuovere gli “schema” e i DB di default presenti al termine dell’installazione standard
   e non utilizzati.
   Dopo la creazione del database, rimuovere gli eventuali script utilizzati per la creazione
   o, come minimo, spostarli su un repository “sicuro” (quanto meno dotato di controllo
   accessi) ed esterno al sistema.
   Quando si avviano processi o tools legati al DBMS, evitare di fornire a linea di comando
   informazioni sensibili quali ad es. username e password o chiavi crittografiche, perché
   tali parametri possono essere visualizzati da tutti gli utenti del sistema, anche in
   remoto, esaminando l’elenco dei processi in esecuzione. Analogamente, tali
   informazioni non devono essere memorizzate neppure in variabili d’ambiente né come
   testo in chiaro in file batch, ma piuttosto fornite a mano dall’operatore, o memorizzate
   in file di configurazione crittografati o come minimo offuscati.

   **Hardening della piattaforma DBMS
   Minaccia** Abuso di risorse.

   **Contromisure**  Disabilitare gli script, le applicazioni d'esempio, le utility non strettamente necessari ed
   ogni altra funzionalità non pertinente agli scopi della piattaforma DBMS, proposti dalle
   configurazioni di base del DBMS.

   **Protezione delle informazioni strumentali all'accesso
   Minaccia** Accesso non autorizzato ai sistemi.

   **Contromisure**  Non utilizzare nomi di account predefiniti e rinominare account standard come
   l'account amministratore del DB.
   Eseguire l'Audit degli accessi non andati a buon fine per intercettare tentativi di
   indovinare le password.

   **Accesso a dati sensibili su memoria di massa
   Minaccia** Accesso non autorizzato alle informazioni.

   **Contromisure**  Utilizzare ACL restrittive per tutti i data stores e in particolare per quelli che
   contengono dati sensibili.
   Memorizzare i data store che contengono dati sensibili o comunque riservati su file
   system crittografati.


   **Hardening della piattaforma DBMS
   Minaccia** Negazione dei servizi.

   **Contromisure**  Configurare le applicazioni, i servizi e il sistema operativo che compongono / ospitano
   il DBMS, tenendo sempre presente le possibili esposizioni ad attacchi DoS.
   Assicurarsi che i criteri di blocco dell'account predisposti non possano essere sfruttati
   per bloccare account di servizio ben noti.
   Assicurarsi che il DBMS sia in grado di gestire alti volumi di traffico e che le soglie siano
   opportunamente impostate per gestire carichi anormalmente elevati.

   **Hardening del sistema operativo che ospita il DBMS
   Minaccia** Accesso non autorizzato al sistema.
   Compromissione delle comunicazioni.
   Furto di credenziali di autenticazione (es. keylogger).
   Violazione della sicurezza, rispetto alle politiche di sicurezza dell’organizzazione.

   **Contromisure**  Eseguire l’hardening del sistema operativo che ospita il DBMS. L’hardening del sistema
   operativo è oggetto di un paragrafo specifico [rif. 5.2.2].

   **Patching del DBMS
   Minaccia** Accesso non autorizzato al sistema.
   Accesso non autorizzato alle informazioni.
   Compromissione delle comunicazioni.
   Violazione della sicurezza, rispetto alle politiche di sicurezza dell’organizzazione.

   **Contromisure**  Eseguire il patching iniziale (prima di mettere in uso i sistemi DBMS) e successivamente
   in maniera regolare e periodica, installando tutti gli aggiornamenti suggeriti e di
   sicurezza rilasciati dal produttore.

   **Disabilitazione delle interazioni con il sistema operativo
   Minaccia** Accesso non autorizzato al sistema.
   Attacchi all’integrità dei sistemi (software e configurazioni).
   Compromissione delle comunicazioni.
   Violazione della sicurezza, rispetto alle politiche di sicurezza dell’organizzazione.

   **Contromisure**  Molti DBMS, tra cui Microsoft SQL Server (attraverso alcune Extended Stored
   Procedure come _xp_cmdshell_ , _xp_dirtree_ , _xp_servicecontrol_ , ecc.) e Oracle (con altri
   meccanismi) consentono di interagire in modo molto stretto con il sistema operativo,
   ad es. richiamando eseguibili sul sistema, navigando sul file system,
   avviando/arrestando servizi o eseguendo altre operazioni anche privilegiate.
   Tali meccanismi, quando non effettivamente necessari, devono essere disabilitati.

   ### 5.6.3 Utenze

   Valgono i principi generali già introdotti nel paragrafo [rif. 5.1.15.1.1].

   ### 5.6.4 Autenticazione

   Valgono i principi generali già introdotti nel paragrafo [rif. 5.1.2].


   ### 5.6.5 Autorizzazione

   A i principi generali già introdotti nel paragrafo [rif. 0], si aggiungono le seguenti indicazioni per il contesto
   specifico:

   **Autorizzazione
   Minaccia** Accesso non autorizzato alle informazioni.

   **Contromisure**  Utilizzare e configurare opportunamente i meccanismi di controllo di accesso alle
   risorse (tabelle, viste, procedure, ecc.) gestite dal DBMS (a titolo di esempio
   l’istruzione “grant” fornita da Oracle), fornendo a ciascun utente o utenza applicativa i
   minimi diritti effettivamente necessari al corretto funzionamento, secondo il principio
   del _least privilege_.
   Ad es., evitare l’accesso di un application server al DBMS con utenza di amministratore
   globale del database, anche quando un utente non privilegiato deve effettuare compiti
   di ordinaria operatività.

   ### 5.6.6 Crittografia

   Ai principi generali già introdotti nel paragrafo [rif. 5.1.4], si aggiungono le seguenti indicazioni per il
   contesto specifico:

   **Protezione delle informazioni riservate
   Minaccia** Crittografia debole o non validata.
   Accesso non autorizzato alle informazioni.

   **Contromisure**  - Per la protezione delle informazioni riservate custodite nel database, all’interno di
   campi specifici di tabelle specifiche, utilizzare tecniche di crittografia dei dati a
   livello di colonna fornite nativamente dallo specifico DBMS, evitando l’uso di
   soluzioni custom o di terze parti, evitando così tutta una serie di problemi che
   possono sorgere (ad es. quando la colonna cifrata è parte di un indice: in tal caso
   solitamente si indicizza il valore cifrato anziché quello in chiaro);

   - Per la protezione delle informazioni riservate custodite nel database, all’interno di
       righe specifiche di una tabella, utilizzare tecniche di crittografia dei dati a livello di
       riga fornite nativamente dallo specifico DBMS, evitando l’uso di soluzioni custom o
       di terze parti;
   - In presenza di dati particolarmente sensibili, valutare se vi sia davvero la necessità
       di custodirli all’interno del DBMS, e in caso contrario, evitare la loro
       memorizzazione permanente;
   - I dati sensibili presenti sui DBMS di produzione non devono mai essere trasferiti su
       sistemi di sviluppo, test e collaudo, se non dopo essere stati sottoposti ad un
       processo di “anonimizzazione” o “tokenizzazione”.

   **Protezione delle informazioni strumentali all'accesso
   Minaccia** Crittografia debole o non validata.
   Accesso non autorizzato alle informazioni.

   **Contromisure**  Per la memorizzazione sicura delle chiavi applicative di accesso e/o di cifratura
   utilizzare funzionalità o prodotti di tipo “wallet” native o aggiuntive ma comunque

certificate dal vendor dello specifico database.

::

   ### 5.6.7 Documentazione

   Valgono i principi generali già introdotti nel paragrafo [rif. 5.1.5].

   ### 5.6.8 Logging

   Valgono i principi generali già introdotti nel paragrafo [rif. 5.1.6].

   ### 5.6.9 Sessioni

   **Protezione delle sessioni di lavoro
   Minaccia** Accesso non autorizzato alle informazioni.

   **Contromisure**  Attivare un meccanismo per la disconnessione automatica delle sessioni di lavoro dopo
   un periodo di inattività inferiore ai 5 minuti

   ### 5.6.10 Procedure

   Ai principi generali già introdotti nel paragrafo [rif. 5.1.7], si aggiungono le seguenti indicazioni per il
   contesto specifico:

   **Limitare e controllare l'uso dei programmi di utilità
   Minaccia** Accesso non autorizzato ai sistemi.

   **Contromisure**  Limitare e tenere sotto controllo l'uso di programmi di utilità, considerando le seguenti
   linee guida:

   - utilizzo di procedure di identificazione, autenticazione e autorizzazione per i
       programmi di utilità;
   - limitazione della disponibilità e tracciamento di tutti gli utilizzi dei programmi di
       utilità;
   - rimozione o disabilitazione di tutti i programmi di utilità non necessari.

   **Tecniche di programmazione SQL sicura e protezione degli accessi
   Minaccia** Accesso non autorizzato alle informazioni.
   Cancellazione o furto di informazioni.

   **Contromisure**  Alcuni prodotti di mercato (es. Oracle Database 12c) forniscono un “database firewall”
   specializzato per monitorare le istruzioni SQL dirette al DBMS. Ciò corrobora le best
   practices di programmazione sicura, difendendo il DBMS da vari tipi di attacchi.

   ### 5.6.11 Informazioni addizionali

   **Riferimenti
   Oracle Database
   12c**

   Per informazioni aggiornate sulle impostazioni di protezione e privacy per Oracle
   Database 12c, scaricare il documento:
   [http://www.oracle.com/us/products/database/securing-oracle-database-primer-](http://www.oracle.com/us/products/database/securing-oracle-database-primer-)
   2522965.pdf.
   **Microsoft SQL
   Server 2012**

Per informazioni aggiornate sulle impostazioni di protezione e privacy
per Microsoft SQL Server 2012, visitare il sito:

::

https://docs.microsoft.com/en-us/sql/relational-databases/security/securing-sql-
server.

::

   ## 5.7 SICUREZZA DEL MAIL SERVER

   ### 5.7.1 Architettura

   **Isolamento dei sistemi critici
   Minaccia** Accesso non autorizzato alle informazioni

   **Contromisure**  I sistemi critici come il Mail Server devono avere un ambiente di elaborazione
   dedicato, strettamente controllato e monitorato.
   Tipicamente è necessaria una protezione perimetrale fisica (CED) e logica (firewall).
   Occorrono in linea di principio:

   - un SMTP server hardenizzato collocato in DMZ che si limita ad accettare le
       connessioni in ingresso provenienti da Internet, con funzione di “relay”;
   - uno o più mail server interni anch’essi opportunamente messi in sicurezza (vedi
       best practices successive) a cui l’SMTP server in DMZ inoltra (relay) le mail ricevute
       dall’esterno e da cui riceve quelle provenienti dall’interno.
   Inoltre si può considerare di installare un Application Layer inspection firewall a
   protezione del server SMTP in DMZ.
   Si consideri, a titolo di esempio, il seguente schema (con 2 firewall) in ambiente
   Microsoft:

[Fonte: https://msdn.microsoft.com/en-us/library/cc505927.aspx]

::

   **Failover
   Minaccia** Negazione dei servizi.

   **Contromisure**  Prevedere meccanismi di failover dei sistemi di posta elettronica.


   **Controllo del traffico dati
   Minaccia** Accesso non autorizzato alle informazioni.
   Compromissione delle comunicazioni.
   Negazione dei servizi.

   **Contromisure**  Attivare, a livello perimetrale, un dispositivo di sicurezza intelligente di tipo IDS
   (Intrusion Detection System) o IPS (Intrusion Prevention System) per individuare (IDS)
   la presenza di codice malevolo e bloccare (IPS) le intrusioni.

   **Hardening del MailServer
   Minaccia** Accesso non autorizzato alle informazioni.
   Accesso non autorizzato ai sistemi.
   Negazione dei servizi.

   **Contromisure**  Concedere al Mail Server i privilegi minimi necessari per completare le operazioni
   richieste. In particolare i processi del server devono essere eseguiti nel contesto di una
   utenza non privilegiata.

   **Hardening del MailServer
   Minaccia** Accesso non autorizzato ai sistemi.
   Compromissione delle comunicazioni.

   **Contromisure**  Customizzare opportunamente le configurazioni di base del mail server. In particolare,
   cambiare i nomi degli account di default e degli alias pre-definiti.

   **Hardening del MailServer
   Minaccia** Negazione dei servizi.

   **Contromisure**  Configurare le applicazioni, i servizi e il sistema operativo tenendo sempre presente le
   possibili esposizioni ad attacchi DoS.
   Assicurarsi che i criteri di blocco dell'account predisposti non possano essere sfruttati
   per bloccare service accounts ben noti.
   Assicurarsi che il sistema sia in grado di gestire alti volumi di traffico e che le soglie
   siano opportunamente impostate per gestire carichi anormalmente elevati.

   **Hardening del MailServer
   Minaccia** Compromissione delle comunicazioni.
   Negazione dei servizi.

   **Contromisure**  L'utilizzo di black-list di IP/indirizzi mail costruite sulla base di osservazioni su attacchi
   avvenuti in passato, può ridurre notevolmente i rischi derivanti da attacchi di vario tipo
   (es. spam). Tali liste sono disponibili in internet oppure sono incluse in prodotti
   commerciali di protezione dei mail server.
   Ove possibile, limitare gli accessi a indirizzi IP/indirizzi mail presenti in queste black-list.

   **Hardening del MailServer
   Minaccia** Divulgazione di informazioni riservate.

   **Contromisure**  Configurare opportunamente i messaggi prodotti dal mail server (messaggi di Hello,
   risposte automatiche ad es. per i messaggi non consegnabili, messaggi di errore,
   funzionalità diagnostiche, ecc.) in modo da non rivelare nessuna informazione ad un
   eventuale aggressore, quali ad es. indirizzi email degli amministratori o di altri utenti o

di caselle di risposta automatica, versione del software, ecc. Infatti
un malintenzionato potrebbe indurre il sistema in errore per ottenere
indirizzi email validi da usare ad es. in una campagna di phishing o
spamming.

::

   **Hardening del MailServer
   Minaccia** Accesso non autorizzato ai sistemi (risorse di sistema, configurazioni, interfacce
   amministrative, ecc.).
   Attacchi all’integrità dei sistemi (software e configurazioni).
   Furto di credenziali di autenticazione (es. keylogger).
   Negazione dei servizi.
   Tentativi di frode.
   Violazione della sicurezza, rispetto alle politiche di sicurezza dell’organizzazione (es.
   malware, ecc.).
   Violazione di leggi, di regolamenti, di obblighi contrattuali.

   **Contromisure**  Filtrare gli Attachments. Installare un software antivirus e implementare filtri per
   bloccare attachment sospetti o potenzialmente pericolosi.

   **Hardening del MailServer
   Minaccia** Accesso non autorizzato alle informazioni.
   Compromissione delle comunicazioni.

   **Contromisure**  Utilizzare solo protocolli sicuri per l’accesso alla posta elettronica:

   - Client POP3: Solo se si utilizza con SSL/TLS, altrimenti usare IMAP4.
   - Client IMAP4: Configurare sempre l’uso di SSL/TLS.
   - Server SMTP: Configurare sempre l’uso di SSL/TLS.
   Utilizzare solo TLS 1.2, evitando SSL e le versioni precedenti di TLS, in quanto
   vulnerabili a diverse tipologie di attacchi.

   **Hardening del MailServer
   Minaccia** Accesso non autorizzato alle informazioni.
   Compromissione delle comunicazioni.

   **Contromisure**  Webmail Access. Se il MailServer supporta la Webmail, è necessario adottare tutte le
   misure di sicurezza previste nel presente documento per i server web.
   In particolare però il server di webmail deve obbligatoriamente utilizzare HTTPS con
   TLS 1.2 o superiore, per l’intera durata della sessione.

   **Hardening del MailServer
   Minaccia** Negazione dei servizi.

   **Contromisure**  Limitare sempre la dimensione massima dei messaggi e degli attachments sia per i
   messaggi in ingresso sia per quelli in uscita, utilizzando valori considerati accettabili per
   l’organizzazione. Ciò protegge da situazioni potenzialmente pericolose (degrado
   prestazioni, crash, esaurimento disco, SPAM e attacchi DOS verso terzi) in cui messaggi
   con allegati di grandi dimensioni sono inviati a molteplici destinatari.
   Configurare anche un numero massimo ragionevole di destinatari per i messaggi in
   uscita o in fase di relay.
   Configurare una dimensione massima ragionevole per le mailbox degli utenti e per le
   cartelle pubbliche / condivise.


   **Hardening del MailServer
   Minaccia** Divulgazione di informazioni riservate.
   Negazione dei servizi (Spam).

   **Contromisure**  Disabilitare il comando “VRFY” (che consente di verificare se un account di email esiste
   sul server).

   **Hardening del MailServer
   Minaccia** Negazione dei servizi.

   **Contromisure**  Limitare il numero di messaggi di posta elettronica per minuto o per ora che un server
   può ricevere, legittimare o altro.

   **Hardening del MailServer
   Minaccia** Attacchi all’integrità dei sistemi.
   Negazione dei servizi.

   **Contromisure**  Il mobile code può essere scaricato ed eseguito su PC utente anche via email. Oltre al
   download via attachment (ad esempio: macro in un file Word), si consideri anche il
   caso di body HTML della mail (ad esempio: JavaScript). In generale, a livello di mail
   client occorre:

   - Assicurarsi che il “reading pane”, se presente, non attivi script e/o apra attachment
       automaticamente;
   - Bloccare contentuti esterni in HTML (es. immagini o altri elementi multimediali).

   **Hardening del sistema operativo che ospita il Mail Server
   Minaccia** Accesso non autorizzato alle informazioni.
   Accesso non autorizzato al sistema.
   Compromissione delle comunicazioni.
   Furto di credenziali di autenticazione (es. keylogger).
   Violazione della sicurezza, rispetto alle politiche di sicurezza dell’organizzazione.
   Violazione di leggi, di regolamenti, di obblighi contrattuali.

   **Contromisure**  Eseguire l’hardening del sistema operativo che ospita il Mail Server [rif. 5.2.2].

   ### 5.7.2 Utenze

   Valgono i principi generali già introdotti nel paragrafo [rif. 5.1.1].

   ### 5.7.3 Autenticazione

   Valgono i principi generali già introdotti nel paragrafo [rif. 5.1.2].

   ### 5.7.4 Autorizzazione

   A i principi generali già introdotti nel paragrafo [rif. 5.1.3], si aggiungono le seguenti indicazioni per il
   contesto specifico:

   **Autorizzazione
   Minaccia** Negazione dei servizi.


   **Contromisure**  - Attivare la “Relaying Protection” in modo che solo gli utenti identificati ed
   autorizzati possano collegarsi per l’invio di email. Disabilitare il funzionamento

come “open relay”.

::

   - Configurare inoltre il server in modo da accettare (in ingresso) o effettuare il relay
       (in uscita) solo per le email rispetto alle quali è autoritativo (per il dominio) e solo
       da e per caselle di posta effettivamente esistenti all’interno dell’organizzazione.
   - Infine quando il server è un relay host (il cui compito è di inoltrare i messaggi ad un
       altro SMTP server), utilizzare sempre l’autenticazione per la connessione tra i
       diversi server SMTP dell’architettura, utilizzando su ogni host il TLS 1.2 o
       successivo.

   ### 5.7.5 Crittografia

   Ai principi generali già introdotti nel paragrafo [rif. 5.1.4], si aggiungono le seguenti indicazioni per il
   contesto specifico:

   **Protezione delle informazioni strumentali all'accesso
   Minaccia** Attacchi all’integrità delle informazioni.^
   Compromissione delle comunicazioni.
   Divulgazione di informazioni riservate.
   Falsificazione di identità.

   **Contromisure**  A livello di client mail, si tengano presenti:

   - L’utilizzo di meccanismi per la protezione dell'integrità e dell’autenticità delle
       informazioni trasmesse e/o ricevute via e-mail che prevedano utilizzo di strumenti
       crittografici, quali ad esempio la firma digitale.
   - L’utilizzo di meccanismi per la protezione della confidenzialità delle informazioni
       trasmesse e/o ricevute via e-mail eseguendo la cifratura dei messaggi end-to-end
       (cioè a livello dei client), con strumenti idonei ammessi dalla politica aziendale.

   ### 5.7.6 Documentazione

   Valgono i principi generali già introdotti nel paragrafo [rif. 5.1.5].

   ### 5.7.7 Logging

   Valgono i principi generali già introdotti nel paragrafo [rif. 5.1.6].

   ### 5.7.8 Anti-Phishing

   **Software anti-phishing
   Minaccia** Attacchi all’integrità dei sistemi.
   Furto di credenziali di autenticazione.
   Negazione dei servizi.

   **Contromisure**  Mail Server: Installare sul Mail Server un modulo aggiuntivo anti-phishing che aggiorni
   il proprio database delle “firme” (pattern riconosciuti come pericolosi) almeno una
   volta al giorno.
   Mail Client: Prevedere per i client di posta aziendali, come Microsoft Outlook, un
   modulo aggiuntivo con il quale possano essere rilevati i collegamenti sospetti di un e-
   mail.
   Webmail: Utilizzare un browser recente e aggiornato, dotato di funzionalità di filtro
   anti-phishing native, o in alternativa utilizzare un software anti-malware dotato di
   estensioni anti-phishing per i browser adottati dall’organizzazione.


   ### 5.7.9 Anti-Spam

   **Software anti-Spam
   Minaccia** Negazione dei servizi.

   **Contromisure**  Installare sul Mail Server un software anti-spam che aggiorni il proprio database delle
   “firme” almeno una volta al giorno. Il software deve avere la funzione di auto-
   apprendimento in modo da incrementare l'accuratezza del filtraggio, e deve eseguire il
   filtraggio dei messaggi sospetti mediante analisi di tipo:

   - Semantico, ovvero la rilevazione in base a parole chiavi (ad es. Viagra, sesso, Prozac,
   etc.);
   - Euristico, ovvero individuare la posta ricevuta con comportamento anomalo (ad
   esempio con un numero insolitamente elevato di destinatari, con l'assenza
   dell'indirizzo del mittente o con l'indirizzo del mittente identico a quello del
   destinatario).
   Inoltre il software deve usare una specifica tecnica di blocco dei messaggi sospetti in
   base al mail server di provenienza come, ad esempio, la tecnica DNSBL (DNS-based
   Blackhole Lists) che si avvale dell'ausilio di una lista pubblicata su internet, che viene
   manutenuta costantemente da terze parti ed in cui sono elencati i servers che
   favoriscono lo spam (ad es. server SMTP Open Relay, server che emettono spam, ISP
   che supportano lo spam, etc.).

   ### 5.7.10 Procedure

   A i principi generali già introdotti nel paragrafo [rif. 5.1.7] (i principi generali si applicano sia ai MailServer
   quanto che ai Mail Client), si aggiungono le seguenti indicazioni per il contesto specifico:

   **Uso corretto della posta elettronica
   Minaccia** Abuso di risorse.
   Attacchi all’integrità dei sistemi.
   Compromissione delle comunicazioni.
   Furto di credenziali di autenticazione.

   **Contromisure**  - Evitare l'uso dell'e-mail a fini diversi da quelli strettamente aziendali (ad esempio,
   per iscriversi a mailing list, forum, chat, blog, etc.) che non siano attinenti alla
   funzione svolta.

   - Non cliccare mai direttamente su un link presente in una e-mail per accedere a un
       sito web contenente informazioni sensibili. Copiare e incollare il testo del
       collegamento in una nuova finestra del browser e verificare l'URL per assicurarsi
       che la sessione inizi dall'indirizzo autentico conosciuto del sito, senza che vengano
       aggiunti altri caratteri.
   - Controllare che la pagina web del sito dell’eventuale istituto creditizio a cui
       conduce un link presente in una e-mail, disponga di un certificato digitale
       attendibile, ovvero appartenente al legittimo proprietario, e che tale certificato sia
       ancora valido. Ad esempio, nelle versioni più recenti di Internet Explorer e in
       diversi altri browser comunemente disponibili è sufficiente cliccare con il pulsante
       destro del mouse in un punto qualsiasi della finestra del browser e selezionare
       “Proprietà” dal menu a comparsa, dopo aver visualizzato la finestra "Proprietà",
       occorre cliccare su “Certificati” per controllarne la validità ed attendibilità.


   **Sensibilizzazione del personale sui rischi di infezione da malware
   Minaccia** Attacchi all’integrità dei sistemi.
   Furto di credenziali di autenticazione.
   Violazione della sicurezza, rispetto alle politiche di sicurezza dell’organizzazione
   (malware).

   **Contromisure**  Sensibilizzare il personale sui rischi di infezione da malware. Ad esempio, informare sui
   rischi derivanti dal phishing/pharming (divulgazione a terze parti d'informazioni
   riservate o critiche quali, ad esempio, dati personali, password, numeri di conto o carta
   di credito) sui sintomi di infezione e sulla protezione di PC e dispositivi portatili.
   Istruire il personale sulle norme di comportamento cui attenersi per diminuire i rischi
   di phishing/pharming. Tali norme dovrebbero, almeno, indicare di:

   - non fare affidamento sull’intuito per distinguere tra richieste legittime e illegali di
       informazioni riservate;
   - non consegnare mai informazioni personali o riservate a individui o aziende
       sconosciuti;
       eliminare messaggi e-mail che richiedono informazioni riservate. Se la richiesta
       appare legittima, verificatene telefonicamente l’autenticità;
   - non disabilitare le protezioni aziendali antivirus, anti-phishing/pharming o altre
       misure di sicurezza (ad esempio quelle del browser);
   - contattate l’assistenza IT nel caso di comunicazioni ricevute per e-mail, telefono,
       fax o messaggistica immediata, che richiedono informazioni aziendali o personali.

   **Procedura di monitoraggio sull'uso del mail server
   Minaccia** Abuso di risorse.
   Negazione dei servizi.

   **Contromisure**  Definire procedure che specifichino le modalità con cui monitorare il mail server per
   garantirne la funzionalità e l'uso corretto. La procedura deve specificare cosa
   monitorare (ambito del monitoraggio) e quando eseguire l'audit rimanendo conformi
   ai requisiti di legge e alle politiche aziendali.
   Un monitoraggio di base dovrebbe considerare i carichi medi del traffico email e delle
   risorse del sistema: analizzando in tempo reale tali parametri e le loro deviazioni
   rispetto ai valori attesi, si possono trovare indizi di problemi e attacchi.
   La procedura deve specificare la frequenza con cui effettuare i controlli ogni qual volta
   sussista la necessità (non meno di una volta al giorno).

   **Accordi con i Service Provider
   Minaccia** Negazione dei servizi.

   **Contromisure**  Considerare le seguenti linee guida per i contratti con i service provider di posta
   elettronica:

   - stabilire livelli di servizio garantiti, accettabili per l’organizzazione;
   - ottenere la garanzia di ottenere dal provider il massimo supporto in caso di
       attacco, per individuare gli indirizzi di rete (IP) degli aggressori mediante un
       percorso a ritroso, e per bloccare l’attacco.

   ## 5.8 SICUREZZA DEI ENTERPRISE SERVICE BUS (ESB)

   ### 5.8.1 Architettura

   **Isolamento dei sistemi critici**


   **Minaccia** Accesso non autorizzato alle informazioni.
   Negazione dei servizi.

   **Contromisure**  I sistemi critici come l’ESB devono avere un ambiente di elaborazione dedicato,
   strettamente controllato e monitorato.
   Tipicamente è necessaria una protezione perimetrale fisica (CED) e logica (firewall).
   Occorrono in linea di principio:

   - un “external ESB” collocato in DMZ che agisce come Security Gateway (Security
       Enforcement Point – es. gestione identità) e un “internal ESB” opportunamente
       messo in sicurezza (vedi best practices successive) a cui l’“external ESB” passa le
       chiamate esterne e da cui riceve le risposte (ed eventuali chiamate verso
       l’esterno). Oltre al routing dei messaggi, è qui che avviene la conversione dei
       messaggi ed è qui che risiedono i business workflow.
   - Un “Security Decision Service”, interno (ossia non in DMZ), cui i 2 ESB si riferiscono
       come repository unico delle security policies.

   ### 5.8.2 Hardening

   **Hardening del sistema operativo che ospita l’ESB
   Minaccia** Accesso non autorizzato al sistema.
   Compromissione delle comunicazioni.
   Furto di credenziali di autenticazione (es. keylogger).
   Violazione della sicurezza, rispetto alle politiche di sicurezza dell’organizzazione.
   Violazione di leggi, di regolamenti, di obblighi contrattuali.

   **Contromisure**  Eseguire l’hardening del sistema operativo che ospita l’ESB [rif. 5.2.2].
   Tipicamente è necessaria una protezione perimetrale fisica (CED) e logica (firewall).

   **Hardening della piattaforma web che ospita l’ESB
   Minaccia** Accesso non autorizzato al sistema.
   Compromissione delle comunicazioni.
   Furto di credenziali di autenticazione (es. keylogger).
   Violazione della sicurezza, rispetto alle politiche di sicurezza dell’organizzazione.
   Violazione di leggi, di regolamenti, di obblighi contrattuali.

   **Contromisure**  Siccome SOA sfrutta e si basa sulle tecnologie Web, le vulnerabilità associate a tali
   tecnologie influenzano anche SOA. Pertanto, deve essere eseguito l’hardening della
   piattaforma web che ospita l’ESB [rif. 5.3.2].

   **Hardening del Web Services Layer
   Minaccia** Accesso non autorizzato alle informazioni.
   Divulgazione di informazioni riservate.

   **Contromisure**  Utilizzare adeguati meccanismi di controllo dell'accesso per separare “operazioni
   interne” da “operazioni esterne” come:

   - un firewall XML che “tagli” le operazioni interne o
   - spostare le operazioni interne su servizi Web privati e ospitarle sui server Web
       interni.
   Il WSDL di un Web Service pubblica le sue operazioni, i parametri e le associazioni di
   rete. Alcune di queste (operazioni interne) devono essere utilizzate solo dal fornitore di
   servizi, tipicamente le operazioni amministrative. Il resto delle operazioni (operazioni
   esterne) può essere richiamato dal consumatore di servizi. Ora un attaccante può
   tentare di indovinare le operazioni interne e invocarle tramite l'endpoint (che è

disponibile nel WSDL). Tale attacco è chiamato scansione WSDL.

::

   **Hardening del Web Services Layer
   Minaccia** Compromissione delle comunicazioni.

   **Contromisure**  Verificare l'autenticità dei metadati del servizio Web (si tenga presente che non
   esistono meccanismi standard per verificare l'autenticità dei metadati).
   Un attaccante che, ad esempio, riesca a modificare l'endpoint del servizio può mettere
   in atto un man-in-the-middle attack per l'intercettazione o la modifica dei dati del
   servizio Web.

   **Hardening del Web Services Layer
   Minaccia** Violazione della sicurezza, rispetto alle politiche di sicurezza dell’organizzazione.

   **Contromisure**  La validazione dello schema del contenuto cifrato va eseguita dopo la decifratura e non
   prima.
   Gli standard di XML Encryption e XML Signature, utilizzati per fornire servizi di
   crittografia e firma digitale sui messaggi scambiati via Web Services (ad esempio
   SOAP), possono essere utilizzati da un attaccante per nascondere codice malevolo che
   va in esecuzione durante la decifratura (Attack obfuscation).

   **Hardening del Web Services Layer
   Minaccia** Negazione dei servizi.

   **Contromisure**  Le richieste dei service consumer devono essere elaborate solo se gli elementi del
   security header del messaggio SOAP in entrata corrispondono esattamente ai requisiti
   imposti dallo schema della security policy. Diversamente vanno scartati.
   Lo standard WS-Security non impone restrizioni né su quali parti del security header di
   un messaggio SOAP possono essere crittografate né sulla dimensione massima di un
   messaggio crittografato. Ciò significa che un attaccante è in grado di provocare un
   denial of service inviando a un servizio Web dei security headers crittografati di grandi
   dimensioni. Le operazioni di decifratura causano un carico elevato sulla CPU del server
   che ospita il Web Service, carico che a sua volta crea problemi di disponibilità.

   **Hardening del Business Processes Layer
   Minaccia** Accesso non autorizzato alle informazioni.
   Divulgazione di informazioni riservate.

   **Contromisure**  Estendere i meccanismi di controllo dell'accesso per separare “operazioni interne” da
   “operazioni esterne” a livello BPEL.
   Un WS-BPEL (BPEL) di un processo di business può essere sottoposto ad un attacco di
   "BPEL scanning" analogo al “WSDL scanning” (ma portato su un layer diverso).

   **Hardening del Business Processes Layer
   Minaccia** Compromissione delle comunicazioni. - Metadata spoofing

   **Contromisure**  Verificare l'autenticità dei metadati a livello BPEL.
   Un attaccante, ad esempio, potrebbe modificare a suo vantaggio i riferimenti di
   endpoint del processo aziendale nella dichiarazione BPEL.

   **BPEL state deviation
   Minaccia** Negazione dei servizi. - Metadata spoofing



   **Contromisure**  Un attaccante può inondare (flood) il motore BPEL con molti messaggi BPEL che sono
   conformi allo schema ma non hanno alcun contenuto significativo. Le risorse
   computazionali del motore BPEL potrebbero esaurirsi producendo un attacco di denial
   of service.
   Per rifiutare i messaggi non validi, l’approccio migliore è quello di utilizzare un
   application level firewall.

   **Hardening del Business Processes Layer
   Minaccia** Negazione dei servizi - Instantiation flooding (diretto e indiretto)

   **Contromisure**  I motori BPEL istanziano un nuovo processo quando ricevono un “receive message”
   (che istanzia un processo BPEL). Quando viene ricevuto un “receive message”, il
   motore BPEL sospende l'esecuzione corrente finché il messaggio entrante è
   completamente ricevuto. Un attaccante può sfruttare questo comportamento dei
   motori BPEL inondandoli di “receive message” non validi, producendo un attacco di
   denial of service.
   L'attacco può avvenire anche in modo indiretto: si colpisce un motore BPEL per
   attaccarne un altro che interagisce con il primo.
   La protezione dei motori BPEL contro questa tipologia di attacchi di flooding è
   complessa: occorrerebbe un’analisi semantica per individuare i messaggi non validi. E
   ciò esula dalle possibilità di un application level firewall.
   In caso di attacco occorre intervenire a livello di difesa perimetrale in modo mirato.

   **Hardening del Business Processes Layer
   Minaccia** Compromissione delle comunicazioni - WS-Addressing spoofing

   **Contromisure**  Verificare la validità degli endpoint prima che il processo venga eseguito dal motore
   BPEL (caso di endpoint non validi o pericolosi)
   La specifica WS-Addressing descrive come indirizzare in modo standard gli endpoint di
   un web service o di un business process.
   Un attaccante può modificare gli header WS-Addressing facendo puntare il motore
   BPEL agli endpoint di servizi o di processi non validi o pericolosi.

   **Hardening del Business Processes Layer
   Minaccia** Negazione dei servizi - Workflow engine hijacking

   **Contromisure**  Verificare la validità degli endpoint prima che il processo venga eseguito dal motore
   BPEL (caso di endpoint a un sistema di destinazione esistente, che fornisce un servizio
   reale all'URL specificato).
   In caso contrario, un attaccante può utilizzare il WS-Addressing spoofing per provocare
   il denial of service di un servizio legittimo attraverso un attacco di flooding.
   L'endpoint di cui l'attaccante esegue lo spoofing è quello di un servizio legittimo (il
   target dell'attacco).
   Il sistema attaccato tenta di elaborare una grande quantità di messaggi che gli
   pervengono come risultato del WS-Addressing spoofing e, se non ci riesce, i suoi utenti
   legittimi subiscono un Denial of Service.

   **Hardening del protocollo SOAP
   Minaccia** Attacchi all’integrità dei sistemi - Harmful SOAP attachments

   **Contromisure**  I messaggi SOAP possono contenere allegati di dimensione arbitraria. Pertanto un
   attaccante può allegare un virus a un messaggio SOAP e inviarlo per l'elaborazione al

sistema di destinazione. Gestire gli allegati SOAP secondo le seguenti
modalità:

::

   - bloccarli se non previsti o sospetti;
   - filtrarli in base al MIME-type;
   - analizzarli con un anti-malware.

   **Hardening del protocollo SOAP
   Minaccia** Accesso non autorizzato alle informazioni.
   Attacchi all’integrità delle informazioni.
   Negazione dei servizi.
   (SOAPAction spoofing ).

   **Contromisure**  Verificare rigorosamente se l'azione specificata nel SOAP body corrisponde all'azione
   specificata nell’HTTP header. Se non corrispondono, il messaggio in arrivo deve essere
   rifiutato.
   Non utilizzare mai il campo SOAPAction nell'intestazione HTTP come identificativo
   dell'operazione del servizio. Un malintenzionato potrebbe facilmente modificare
   l'elemento "SOAPAction" nell'intestazione HTTP per eseguire un'azione diversa da
   quella specificata nel SOAP body.

   **Hardening dei documenti XML
   Minaccia** Accesso non autorizzato alle informazioni.
   Attacchi all’integrità delle informazioni.
   (XPath injection).

   **Contromisure**  È necessario utilizzare un'interfaccia XPath parametrizzata (se disponibile) oppure
   eseguire la sanitizzazione dell'input utente prima di includerlo in una query costruita
   dinamicamente (in analogia con le tecniche per evitare la SQL Injection).
   La specifica XPath viene utilizzata per navigare nel contenuto di un documento XML.
   Un attacco di XPath injection (simile all'attacco SQL injection) inietta un'espressione
   XPath all’interno di quella predisposta dal programmatore al fine di accedere a
   informazioni non autorizzate in un documento XML.

   **Hardening dei documenti XML
   Minaccia** Negazione dei servizi.

   **Contromisure**  Limitare la dimensione dei messaggi SOAP in arrivo per contrastare un attacco di
   payload di grandi dimensioni.
   Si tenga presente che l'approccio Document Object Model (DOM) per l'analisi e
   l'elaborazione di XML consuma una grande quantità di memoria. Ciò è dovuto al fatto
   che è necessaria una rappresentazione in memoria ad oggetti dell'intero documento
   XML, che richiede molto più spazio di memoria rispetto al documento XML stesso.
   Payload di grandi dimensioni possono essere ottenuti ad esempio:

   - Abusando della proprietà di nesting di elementi, inserendo a piacimento molteplici
       elementi nel documento.
   - Abusando della funzionalità di DTD (Document Type Definitions) per creare
       ricorsivamente entità all’interno del documento fino a farlo “esplodere”.

   **Hardening dei documenti XML
   Minaccia** Negazione dei servizi.

   **Contromisure**  Considerare l’impiego di session tokens univoci nei messaggi SOAP come i nonces

(ossia numeri univoci usati una sola volta). Messaggi XML completamente
validi possono essere usati per causare un attacco DoS chiamato “replay
attack”. Un attaccante può inviare messaggi SOAP ripetitivi contenenti
payload XML validi e richieste ben formate reèòicando messaggi
precedentemente osservati, per portare un attacco DoS.

::

   **Hardening dei documenti XML
   Minaccia** Negazione dei servizi (es. Coercive parsing).

   **Contromisure**  Verificare che l’input XML sia sempre validato attraverso il corrispondente schema
   XML.

   **Hardening dei documenti XML
   Minaccia** Negazione dei servizi - Schema poisoning

   **Contromisure**  Proteggere gli schemi XML contro modifiche non autorizzate.
   Un attaccante può intercettare uno schema XML prima di raggiungere un service
   consumer e modificarlo con uno “Schema poisoning”. In tal modo, AD ESEMPIO, è
   possibile compromettere, lato web service, l’elaborazione dell’XML parser (che può
   andare in hang, crash o in uno stato inconsistente), producendo un denial of service.

   ### 5.8.3 Utenze

   Ai principi generali già introdotti nel paragrafo [rif. 5.1.1], si aggiungono le seguenti indicazioni per il
   contesto specifico:

   **Utenze
   Minaccia** Accesso non autorizzato alle informazioni.
   Attacchi all’integrità delle informazioni.
   Divulgazione di informazioni riservate.

   **Contromisure**  Nel contesto ESB, sistemi e utenze applicative (non assegnate a persone fisiche)
   dovranno essere chiaramente identificati e autenticati.

   ### 5.8.4 Autenticazione

   Ai principi generali già introdotti nel paragrafo [rif. 5.1.2], si aggiungono le seguenti indicazioni per il
   contesto specifico:

   **Autenticazione
   Minaccia** Abuso di privilegi da parte dell’utente.
   Accesso non autorizzato alle informazioni.

   **Contromisure**  Lo standard SAML è una specifica di protezione basata su XML per scambiare
   informazioni di autenticazione e autorizzazione su un utente o un soggetto. Definisce
   uno XML schema e le asserzioni di sicurezza. Le asserzioni sono di tre tipi e riguardano:

   - l'autenticazione
   - gli attributi relativi alla sicurezza per il soggetto
   - le decisioni di autorizzazione adottate.
   Laddove si debbano realizzare applicazioni interoperabili (tra differenti application
   server) o web services richiamabili da molteplici operazioni (si pensi ad es. ad un
   servizio di CRM che espone i suoi metodi tramite web services ad un gran numero di

altre applicazioni interne), è necessario utilizzare SAML per la
gestione delle autorizzazioni applicative del soggetto che richiede i
servizi in base agli attributi di sicurezza di cui dispone.

::

   ### 5.8.5 Autorizzazione

   Ai principi generali già introdotti nel paragrafo [rif. 5.1.3], si aggiungono le seguenti indicazioni per il
   contesto specifico:

   **Autorizzazione
   Minaccia** Accesso non autorizzato alle informazioni.
   Uso non autorizzato di privilegi.
   Crittografia debole o non validata.
   Falsificazione di identità.

   **Contromisure**  Si considerino i seguenti standard:

   - XML Signature: definisce la sintassi della firma digitale nell’ambito dei documenti
       XML e le regole per il suo processing.
   - XML Encryption: si avvale di una tecnologia a chiave condivisa. Il motivo per cui è
       richiesta la crittografia a livello XML (al di sopra di quella di trasporto, ad esempio
       SSL) è che la riservatezza dei messaggi deve essere mantenuta quando un
       messaggio attraversa più nodi nel suo percorso verso la destinazione. Inoltre XML
       Encryption conserva anche la riservatezza dei messaggi a riposo (quando cioè un
       messaggio XML viene memorizzato sulla destinazione finale).
   - XML Key Management Specification (XKMS): completa gli standard XML Signature
       e XML Encryption, specificando i protocolli per la distribuzione e la registrazione di
       chiavi pubbliche (crittografia a chiave pubblica) che possono essere utilizzate con
       XML Signature e XML Encryption.
   - WS-Security: definisce le estensioni per il protocollo SOAP per realizzare
       messaggistica sicura ovvero tale da garantire l'integrità, la riservatezza,
       l'autenticazione dei messaggi. È un meccanismo di uso generale per associare i
       token di sicurezza ai messaggi SOAP. Si basa su XML Signature e XML Encryption.
   Le funzionalità descritte, laddove richieste da un’applicazione, non devono essere
   implementate autonomamente partendo da zero c con librerie generiche, ma devono
   necessariamente utilizzare gli standard sopra elencati.

   ### 5.8.6 Crittografia

   Ai principi generali già introdotti nel paragrafo [rif. 5.1.1], si aggiungono le seguenti indicazioni per il
   contesto specifico:

   **Utenti
   Minaccia** Accesso non autorizzato ai sistemi.
   Accesso non autorizzato alle informazioni.

   **Contromisure**  Per la definizione delle politiche di controllo di accesso e per valutare le richieste di
   autorizzazione, utilizzare lo standard XACML o eXtensible Access Control Markup
   Language, basato su XML.

   ### 5.8.7 Documentazione

   Valgono i principi generali già introdotti nel paragrafo [rif. 5.1.5].


   ### 5.8.8 Logging

   Valgono i principi generali già introdotti nel paragrafo [rif. 5.1.6].

   ### 5.8.9 Procedure

   Valgono i principi generali già introdotti nel paragrafo [rif. 5.1.7].

   ### 5.8.10 Informazioni addizionali

   Gli standard citati per mettere in sicurezza l’ESB (Security Assertion Markup Language (SAML), WS-Security,
   eXtensible Access Control Markup Language (XACML), ecc.) sono implementati e resi fruibili da soluzioni
   COTS (Commercial Of The Shelf), la cui adozione indirizza molte delle best practices descritte.

   **Riferimenti
   SAML, XACML, etc** Gli standard citati per mettere in sicurezza l’ESB (SAML - Security Assertion
   Markup Language, WS-Security, XACML - eXtensible Access Control Markup
   Language, ecc.) sono implementati e resi fruibili da soluzioni **COTS** (Commercial
   Of The Shelf), la cui adozione indirizza molte delle best practices descritte nei
   paragrafi precedenti.
   **Web Services** Per informazioni sulle problematiche di sicurezza relative alla tecnologia dei Web
   Services, visitare il sito:
   https://www.us-cert.gov/bsi/articles/best-practices/assembly-integration-and-
   evolution--security-concept-challenge-and-design-considerations-web-services-
   integration.

   ## 5.9 SICUREZZA DEL PACCHETTO MS OFFICE

   ### 5.9.1 Hardening

   **Hardening della suite Office
   Minaccia** Accesso non autorizzato alle informazioni.
   Attacchi all’integrità dei sistemi.
   Violazione della sicurezza, rispetto alle politiche di sicurezza dell’organizzazione
   (malware).

   **Contromisure**  Limitare/Disabilitare/Condizionare l'uso di contenuti attivi.
   Per contenuti attivi si intendono:

   - i controlli ActiveX,
   - i componenti aggiuntivi quali, ad esempio:
       - Componenti aggiuntivi COM (Component Object Model)
       - Componenti aggiuntivi Visual Studio Tools per Office (VSTO)
       - Componenti aggiuntivi di automazione
       - Server RTD (RealTimeData)
       - Componenti aggiuntivi di applicazioni, ad esempio file con estensioni wll, xll e
          xlam
       - Pacchetti di espansione XML
       - Fogli di stile XML


   ### • Macro VBA

   **Riferimenti** - Pianificare le impostazioni di sicurezza per i controlli ActiveX in Office 2013,
   https://technet.microsoft.com/it-it/library/cc179076.aspx

   - Pianificare le impostazioni di protezione per i componenti aggiuntivi per Office
       2013, https://technet.microsoft.com/it-it/library/ee857086.aspx
   - Pianificare le impostazioni di protezione per le macro VBA per Office 2013,
       https://technet.microsoft.com/it-it/library/ee857085.aspx

   **Hardening della suite Office
   Minaccia** Accesso non autorizzato alle informazioni.
   Attacchi all’integrità dei sistemi.
   Violazione della sicurezza, rispetto alle politiche di sicurezza dell’organizzazione
   (malware).

   **Contromisure**  Bloccare i contenuti esterni, come: Immagini, elementi multimediali, Hyperlinks,
   Connessioni dati, Templates, etc.
   I contenuti esterni possono nascondere Web beacons (che minano la privacy) o
   malware (con svariati esiti).
   **Riferimenti** - Blocco o sblocco di contenuti esterni in documenti di Office,
   https://support.office.com/en-us/article/Block-or-unblock-external-content-in-
   Office-documents-10204ae0-0621-411f-b0d6-
   575b0847a795?CorrelationId=2589076c-bc38-4c1e-bac5-317c19aed229&ui=en-
   US&rs=en-US&ad=US&ocmsassetID=HA010065176

   **Hardening della suite Office
   Minaccia** Divulgazione di informazioni riservate.

   **Contromisure**  I documenti possono contenere grandi quantità di informazioni nascoste:

   - Nome utente, organizzazione
   - Storia delle modifiche, aggiunte, cancellazioni
   - Note, Commenti
   - Testo nascosto
   - Un intero foglio di calcolo “dietro” a un semplice diagramma (con cifre
       confidenziali!)
   - A volte anche blocchi casuali di memoria
   - Proprietà del server di documenti (se il documento fosse stato salvato in un server
       di gestione dei documenti, che ad esempio si basa su Microsoft Windows
       SharePoint Services, il documento potrebbe contenere informazioni aggiuntive
       relative a quel server).
   Per rimuovere tali informazioni, utilizzare lo strumento di Office denominato
   “Document Inspector”.

   **Riferimenti** - Remove hidden data and personal information by inspecting documents,
   https://support.office.com/en-us/article/Remove-hidden-data-and-personal-
   information-by-inspecting-documents-356b7b5d-77af-44fe-a07f-9aa4d085966f

   - Using the document inspector, https://msdn.microsoft.com/en-us/vba/office-
       shared-vba/articles/using-the-document-inspector

   **Hardening della suite Office
   Minaccia** Accesso non autorizzato alle informazioni.
   Attacchi all’integrità dei sistemi.


   Violazione della sicurezza, rispetto alle politiche di sicurezza dell’organizzazione.
   (Zero-day-exploits).

   **Contromisure**  - Bloccare (in via temporanea) l’apertura e/o il salvataggio di certi di tipi di file. Ciò
   attenua il rischio di attacchi alla sicurezza di tipo zero-day, impedendo
   temporaneamente agli utenti di aprire tipi di file specifici, nell’attesa di
   aggiornamento software o un Service Pack.

   - Attivare la funzionalità “Convalida file di Office”. Tale funzionalità consente di
       individuare e prevenire un tipo di exploit noto come “file format attack” o “file
       fuzzing attack” (la struttura del file viene modificata al fine di aggiungere malware).
       In pratica se “Convalida file di Office” determina che la struttura di un file (prima
       ancora di essere aperto) non è conforme a tutte le regole descritte nello schema, il
       file non supera la convalida.
   **Riferimenti** - Pianificare le impostazioni di blocco dei file per Office,
   https://technet.microsoft.com/it-it/library/cc179230.aspx

   **Hardening della suite Office
   Minaccia** Accesso non autorizzato alle informazioni.
   Attacchi all’integrità dei sistemi.
   Violazione della sicurezza, rispetto alle politiche di sicurezza dell’organizzazione
   (malware).

   **Contromisure**  - Limitare/Disabilitare i servizi, basati su Internet, che contribuiscono a proteggere e
   migliorare le applicazioni di Office (ad esempio quelli che inviano le informazioni
   dei messaggi di errore a Microsoft), al fine di controllare la divulgazione di
   informazioni private (privacy).

   - Attivare la funzionalità di “Visualizzazione protetta”. La “Visualizzazione protetta”
       protegge da diversi tipi di exploit poiché apre i documenti in una sandbox (un
       ambiente isolato da dove risulta difficile sferrare attacchi). In Visualizzazione
       protetta:
       - i contenuti attivi non sono abilitati
       - gli utenti possono visualizzare il contenuto di un file ma non possono eseguire
          operazioni di modifica, salvataggio o stampa, né visualizzare le eventuali firme
          digitali del file.
   - Limitare/Disabilitare l’uso dei meccanismi:
       - Trusted Documents
       - Trusted Locations
       - Trusted Publishers
   Tali meccanismi infatti by-passano molti controlli di sicurezza. In particolare tutti i
   contenuti di un “trusted document” o di un documento preso da una “trusted
   location”, o firmati da un “Trusted Publisher” sono immediatamente attivi all’apertura
   del documento.
   **References** - Pianificare le impostazioni di Visualizzazione protetta per Office 2013,
   https://technet.microsoft.com/it-it/library/ee857087.aspx
   - Trusted documents, https://support.office.com/en-us/article/Trusted-documents-
       cf872bd8-47ec-4c02-baa5-1fdba1a11b53
   - Pianificare e configurare le impostazioni di Percorsi attendibili per Office 2013,
       https://technet.microsoft.com/it-it/library/cc179039.aspx

   **Hardening del sistema operativo che ospita la suite
   Minaccia** Accesso non autorizzato alle informazioni.
   Attacchi all’integrità dei sistemi.


   Violazione della sicurezza, rispetto alle politiche di sicurezza dell’organizzazione
   (malware).

   **Contromisure**  Eseguire l’hardening del sistema operativo che ospita la suite Office. L’hardening del
   sistema operativo è oggetto di un paragrafo specifico [rif. 5.2.2].
   Installare sul sistema software anti-malware in grado di:

   - analizzare i “contenuti attivi” presenti nei documenti Office rilevando la presenza
       di malware;
   - rimuovere dai documenti di Office i “contenuti attivi” in base a specifiche politiche
       configurabili, ad es. In base alla tipologia (macro, scripts, oggetti “embedded”,
       applets, etc.), e altre caratteristiche.

   ### 5.9.2 Autorizzazione

   A i principi generali già introdotti nel paragrafo [rif. 5.1.3], si aggiungono le seguenti indicazioni per il
   contesto specifico:

   **Autorizzazione
   Minaccia** Attacchi all’integrità dei sistemi.
   Violazione della sicurezza, rispetto alle politiche di sicurezza dell’organizzazione
   (malware).

   **Contromisure**  Proteggere i parametri di sicurezza e la definizione delle “trusted location” da
   eventuali cambiamenti apportati dagli utenti finali.
   Tali configurazioni devono essere impostabili solo da un’utenza amministrativa.

   #### 5.9.3 Crittografia

   A i principi generali già introdotti nel paragrafo [rif. 5.1.4], si aggiungono le seguenti indicazioni per il
   contesto specifico:

   **Crittografia
   Minaccia** Accesso non autorizzato alle informazioni
   Attacchi all’integrità delle informazioni.
   Falsificazione di identità.

   **Contromisure**  Si tengano presenti i seguenti strumenti integrati in Office:

   - L’utilizzo di firma digitale per la protezione dell'integrità dei documenti prodotti
       (Gli utenti possono firmare digitalmente un documento di Excel, PowerPoint o
       Word);
   - L’utilizzo di meccanismi per la protezione della confidenzialità dei documenti
       prodotti eseguendone la cifratura. Sono disponibili impostazioni che consentono di
       imporre l'utilizzo di password complesse, ad esempio regole relative alla
       complessità e alla lunghezza.
   **References** - Pianificare le impostazioni della firma digitale per Office 2013,
   https://technet.microsoft.com/it-it/library/cc545900.aspx
   - Pianificare le impostazioni di complessità delle password per Office 2013,
       https://technet.microsoft.com/it-it/library/ff657853.aspx

   **Crittografia
   Minaccia** Disponibilità dei servizi.

   **Contromisure**  Valutare l’adozione dello strumento DocRecrypt che funziona sul principio del Key
   escrow, ovvero un accordo in cui le chiavi necessarie per decifrare i dati crittografati
   sono detenuti in un “deposito” (escrow) in modo che, in determinate circostanze, una

terza parte autorizzata, ad esempio un apposito incaricato appartenente
alla Security dell'organizzazione, possa accedere a tali chiavi.

::

   - Pro: si può recuperare il contenuto di un file cifrato anche nell’eventualità che il
       detentore della password la smarrisca o lasci l'organizzazione.
   - Contro: occorre affidarsi a un soggetto fidato.
   **References** - Rimuovere o reimpostare le password dei file in Office,
   https://technet.microsoft.com/it-it/library/jj923033.aspx

   #### 5.9.4 Procedure

   A i principi generali già introdotti nel paragrafo [rif. 5.1.7], si aggiungono le seguenti indicazioni per il
   contesto specifico:

   **Patching
   Minaccia** Accesso non autorizzato alle informazioni.
   Attacchi all’integrità dei sistemi.
   Violazione della sicurezza, rispetto alle politiche di sicurezza dell’organizzazione
   (malware).
   Violazione di leggi, di regolamenti, di obblighi contrattuali.

   **Contromisure**  Per quanto concerne il Patching, il Microsoft Security Response Center rilascia
   mensilmente dei bollettini sulla sicurezza che descrivono gli aggiornamenti di sicurezza
   pubblicati nel mese corrente. Essi risolvono le vulnerabilità legate alla sicurezza del
   software Microsoft, i relativi rimedi e forniscono i collegamenti agli aggiornamenti
   applicabili per il software interessato.
   **References** - Security Bulletins, https://technet.microsoft.com/en-
   us/library/security/dn631937.aspx

   **Procedura
   Minaccia** Accesso non autorizzato alle informazioni.
   Attacchi all’integrità dei sistemi.
   Violazione della sicurezza, rispetto alle politiche di sicurezza dell’organizzazione
   (malware).

   **Contromisure**  Visto che:
   A partire da Office 2013 si distinguono 2 tipi di documenti: “normal” e “macro-
   enabled”:

   - Normal (default): .doc **x** , .xls **x** e .ppt **x**
   - Macro-enabled: .doc **m** , .xls **m** , .ppt **m**
   I documenti “normal” (‘ **x** ’) non hanno macro abilitate, mentre i documenti “macro-
   enabled” hanno le macro abilitate
   La regola più sicura è che si dovrebbe usare sempre documenti di tipo “normal” (‘ **x** ’
   finale), evitando di aprire quelli contenenti macro.

   #### 5.9.5 References and additional information

   I riferimenti sono già stati riportati all’interno delle singole best practices.


   ### 5.10 SICUREZZA DEL PACCHETTO OPENOFFICE

   #### 5.10.1 Hardening

   **Hardening della suite OpenOffice
   Minaccia** Accesso non autorizzato alle informazioni.
   Attacchi all’integrità dei sistemi.
   Violazione della sicurezza, rispetto alle politiche di sicurezza dell’organizzazione
   (malware).

   **Contromisure**  Limitare/Disabilitare/Condizionare l'uso di contenuti attivi. Per contenuti attivi si
   intendono:

   - EXE, COM, PIF, SCR, etc.: Binary code;
   - BAT, CMD, VBS, JS, etc.: Commands, Scripts;
   - HTML, XML, XHTML: Scripts;
   - PDF : Scripts, Embedded files, Commands
   - Word, Excel, PowerPoint, Access, ... : Macros, OLE objects, Embedded files,
       Commands;
   - URLs.
   OpenOffice offre una certa difesa a livello di:
   - esecuzione delle macro (4 modalità -low, medium, high, very high- e possibilità di
       definizione di “trusted sources”);
   - navigazione degli hyperlinks (attraverso Ctrl-click).
   **References** - Security options,
   https://wiki.openoffice.org/wiki/Documentation/OOo3_User_Guides/Getting_Start
   ed/Choosing_options_for_all_of_OOo_-_Security_options

   **Hardening della suite OpenOffice
   Minaccia** Divulgazione di informazioni riservate.

   **Contromisure**  I documenti possono contenere grandi quantità di informazioni nascoste:

   - Nome utente, organizzazione;
   - Storia delle modifiche, aggiunte, cancellazioni;
   - Note, Commenti;
   - Testo nascosto;
   - Un intero foglio di calcolo “dietro” a un semplice diagramma (con cifre aziendali
       confidenziali!) ;
   - A volte anche blocchi casuali di memoria.
   Se si registrano le modifiche al documento o si includono informazioni o commenti
   nascosti nei documenti, per evitare la diffusione incontrollata di tali informazioni
   utilizzare i meccanismi messi a disposizione da OpenOffice che consentono di:
   - impostare warnings per ricordare (in fase di firma, esportazione PDF e salvataggio)
       di rimuovere tali informazioni oppure;
   - rimuovere automaticamente alcune informazioni.
   **References** - Security options and warnings,
   https://wiki.openoffice.org/wiki/Documentation/OOo3_User_Guides/Getting_Start
   ed/Choosing_options_for_all_of_OOo_-_Security_options

   **Hardening del sistema operativo che ospita la suite OpenOffice
   Minaccia** Accesso non autorizzato alle informazioni.
   Attacchi all’integrità dei sistemi.


   Violazione della sicurezza, rispetto alle politiche di sicurezza dell’organizzazione
   (malware).

   **Contromisure**  Eseguire l’hardening del sistema operativo che ospita la suite [rif. 5.2.2].
   Installare sul sistema software anti-malware in grado di:

   - analizzare i “contenuti attivi” presenti nei documenti OpenOffice rilevando la
       presenza di malware;
   - rimuovere dai documenti OpenOffice i “contenuti attivi” in base a specifiche
       politiche configurabili, ad es. In base alla tipologia (macro, scripts, oggetti
       “embedded”, applets, etc.), e altre caratteristiche.

   #### 5.10.2 Autorizzazione

   Ai principi generali già introdotti nel paragrafo [rif. 5.1.3], si aggiungono le seguenti indicazioni per il
   contesto specifico:

   **Autorizzazione
   Minaccia** Attacchi all’integrità dei sistemi.
   Violazione della sicurezza, rispetto alle politiche di sicurezza dell’organizzazione
   (malware).

   **Contromisure**  Proteggere i parametri di sicurezza e la definizione delle “trusted location” da
   eventuali cambiamenti apportati dagli utenti finali.
   Tali configurazioni devono essere impostabili solo da un’utenza amministrativa.

   #### 5.10.3 Crittografia

   Ai principi generali già introdotti nel paragrafo [rif.5.1.4], si aggiungono le seguenti indicazioni per il
   contesto specifico:

   **Crittografia
   Minaccia** Accesso non autorizzato alle informazioni
   Attacchi all’integrità delle informazioni.
   Falsificazione di identità.


   **Contromisure**  Si tengano presenti i seguenti strumenti integrati in OpenOffice:

   - L’utilizzo di firma digitale per la protezione dell'integrità dei documenti prodotti
       (attraverso l’azione “File  Digital Signatures”);
   - L’utilizzo di meccanismi per la protezione della confidenzialità dei documenti
       prodotti eseguendone la cifratura (attraverso l’azione "Save With Password").

   #### 5.10.4 Procedure

   Ai principi generali già introdotti nel paragrafo [rif. 5.1.7], si aggiungono le seguenti indicazioni per il
   contesto specifico:

   **Patching
   Minaccia** Accesso non autorizzato alle informazioni.
   Attacchi all’integrità dei sistemi.
   Violazione della sicurezza, rispetto alle politiche di sicurezza dell’organizzazione
   (malware).
   Violazione di leggi, di regolamenti, di obblighi contrattuali.


   **Contromisure**  Dalla versione 2.1, OpenOffice ha incluso una funzionalità che segnala se è disponibile


   una nuova versione. Per attivare questa opzione: _Tools_  _Options_  _Online Update_ 
   _Check for updates automatically_
   È possibile ricevere alerts via email su vulnerabilità di sicurezza risolte (vedi references:
   [1]);
   È possibile ricevere informazioni complete sugli alert per tutte le vulnerabilità di
   sicurezza risolte (vedi references: [2]).
   Tutte le patch di sicurezza devono essere installate prontamente.
   **References** - [1] Security Alerts, https://www.openoffice.org/security/alerts.html

   - [2] Security Bulletin, https://www.openoffice.org/security/bulletin.html

   **Limitare e controllare l'uso di open source “spurio”
   Minaccia** Violazione della sicurezza, rispetto alle politiche di sicurezza dell’organizzazione
   (malware).

   **Contromisure**  Poiché l'open source rende il codice sorgente disponibile a chiunque, un attaccante
   potrebbe:

   - progettare e distribuire alcuni malware incorporando codice dannoso nella
       distribuzione originale open source (al fine di lasciare backdoor o eseguire l’upload
       di dati sensibili o informazioni aziendali)
   - mostrare alcune caratteristiche interessanti della distribuzione malevola attirando
       così alcuni utenti finali.
   L'organizzazione deve definire una chiara politica di sicurezza sull'utilizzo di open
   source, per evitare che vengano scaricate e installate customizzazioni di software open
   source da fonti non attendibili, considerando le seguenti linee guida:
   - utilizzo di procedure di identificazione, autenticazione e autorizzazione per il
       software open source;
   - limitazione della disponibilità e tracciamento di tutti gli utilizzi di software open
       source;
   - rimozione o disabilitazione di tutti i programmi open source non necessari e non
       ammessi.

   **Minaccia** Accesso non autorizzato alle informazioni.
   Attacchi all’integrità dei sistemi.
   Violazione della sicurezza, rispetto alle politiche di sicurezza dell’organizzazione
   (malware).

   **Contromisure**  Assicurarsi che la copia di OpenOffice sia genuina:

   - scaricata da un sito attendibile (https://www.openoffice.org/download/);
   - acquisita da uno distributore ufficiale.
   Verificare il checksum per assicurarsi che la copia non sia stata danneggiata prima di
   installarla.

   **Minaccia** Accesso non autorizzato alle informazioni.
   Attacchi all’integrità dei sistemi.
   Falsificazione di identità.
   Violazione della sicurezza, rispetto alle politiche di sicurezza dell’organizzazione
   (malware).

   **Contromisure**  Una macro può essere collegata a qualsiasi file OpenOffice (documento, foglio di

lavoro, ecc.). Ogni volta che OpenOffice rileva le macro in un documento
aperto, gestirà/eseguirà la macro come impostato a livello di “Security
options Macro security”, che offre una protezione limitata.

::

La regola più sicura è di non aprire alcun file OpenOffice a meno che
non si abbia sicurezza della provenienza e fiducia del mittente, tanto
più se contiene delle macro. Pertanto, se è necessario scambiare
regolarmente documenti con soggetti ben individuati, si consiglia l'uso
di firme digitali per certificare l'autenticità e l'integrità del
documento.

::

   **Minaccia** Divulgazione di informazioni riservate.

   **Contromisure**  Definire la modalità di segnalazione di eventuali vulnerabilità sospette o errori di
   OpenOffice al team di Sicurezza dell’organizzazione o dell’eventuale provider (in caso
   di servizi di sicurezza gestita) o a fornitori che erogano servizi di supporto tecnico, al
   fine di impedire la divulgazione di informazioni riservate. Occorre definire:

   - Quali informazioni si possono fornire.
   - Gli accordi di riservatezza.


   ## 6 RIFERIMENTI A ISTRUZIONI OPERATIVE E TOOLS DI HARDENING

   ### 6.1 ISTRUZIONI OPERATIVE (BENCHMARKS) DI TERZE PARTI

   Si riporta nel seguito l’elenco completo dei riferimenti alle istruzioni operative di hardening (o benchmarks)
   delle varie componenti (sistemi operativi, middleware, office automation, ecc.) che sono state oggetto di
   analisi nei capitoli precedenti.

Fonte Categoria Famiglia Target Titolo

::

   CIS
   Benchmarks

Sistemi Operativi

::

Linux Ubuntu Securing Ubuntu Linux - An objective, consensus-driven
security guideline for the Ubuntu Linux Operating Systems.
https://www.cisecurity.org/benchmark/ubuntu_linux/

::

   CIS
   Benchmarks

Sistemi Operativi

::

Linux CentOS Securing CentOS Linux - An objective, consensus-driven
security guideline for the CentOS Linux Operating Systems.
https://www.cisecurity.org/benchmark/centos_linux/

::

   CIS
   Benchmarks

Sistemi Operativi

::

Linux Red Hat Securing Red Hat Linux - An objective, consensus-driven
security guideline for the Red Hat Linux Operating Systems.
https://www.cisecurity.org/benchmark/red_hat_linux/

::

   CIS
   Benchmarks

Sistemi Operativi

::

Linux Debian Securing Debian Linux - An objective, consensus-driven
security guideline for the Debian Linux Operating Systems.
https://www.cisecurity.org/benchmark/debian_linux/

::

   CIS
   Benchmarks

Sistemi Operativi

::

Linux Oracle Linux

::

Securing Oracle Linux - An objective, consensus-driven security
guideline for the Oracle Linux Operating Systems.
https://www.cisecurity.org/benchmark/oracle_linux/

::

   CIS
   Benchmarks

Sistemi Operativi

::

Linux SUSE Securing SUSE Linux - An objective, consensus-driven security
guideline for the SUSE Linux Operating Systems.
https://www.cisecurity.org/benchmark/suse_linux/

::

   CIS
   Benchmarks

Sistemi Operativi

::

UNIX AIX 7.1 CIS IBM AIX 7.1 Benchmark
https://www.cisecurity.org/benchmark/ibm_aix

::

   CIS
   Benchmarks

Sistemi Operativi

::

UNIX Solaris 11.1

::

CIS Oracle Solaris 11.1 Benchmark
https://www.cisecurity.org/benchmark/oracle_solaris

::

   CIS
   Benchmarks

Sistemi Operativi

::

UNIX Solaris 11

::

CIS Oracle Solaris 11 Benchmark
https://www.cisecurity.org/benchmark/oracle_solaris

::

   CIS
   Benchmarks

Sistemi Operativi

::

UNIX Solaris 10

::

CIS Oracle Solaris 10 Benchmark
https://www.cisecurity.org/benchmark/oracle_solaris

::

   CIS
   Benchmarks

Sistemi Operativi

::

Windows Desktop

::

Windows 10

::

CIS Benchmarks for CIS Microsoft Windows 10 Enterprise: Securing
Microsoft Windows Desktop - An objective, consensus-driven security
guideline for the Microsoft Windows Desktop Operating Systems - For
Microsoft Windows Desktop 10
https://www.cisecurity.org/benchmark/microsoft_windows_desktop/

::

   CIS
   Benchmarks

Sistemi Operativi

::

Windows Desktop

::

Windows 8.1

::

CIS Microsoft Windows 8.1 Workstation Benchmark
https://www.cisecurity.org/benchmark/microsoft_windows_desktop/

::

   CIS
   Benchmarks

Sistemi Operativi

::

Windows Desktop

::

Windows 8

::

CIS Microsoft Windows 8 Benchmark
https://www.cisecurity.org/benchmark/microsoft_windows_desktop/

::


   CIS
   Benchmarks

Sistemi Operativi

::

Windows Desktop

::

Windows 7

::

CIS Microsoft Windows 7 Workstation Benchmark
https://www.cisecurity.org/benchmark/microsoft_windows_desktop/

::

   CIS
   Benchmarks

Sistemi Operativi

::

Windows Desktop

::

Windows XP

::

CIS Microsoft Windows XP Benchmark
https://www.cisecurity.org/benchmark/microsoft_windows_desktop/

::

   CIS
   Benchmarks

Sistemi Operativi

::

Windows Server

::

2016 CIS Microsoft Windows Server 2016 RTM Benchmark
https://www.cisecurity.org/benchmark/microsoft_windows_server/

::

   CIS
   Benchmarks

Sistemi Operativi

::

Windows Server

::

2012 R2 CIS Microsoft Windows Server 2012 R2 Benchmark
https://www.cisecurity.org/benchmark/microsoft_windows_server/

::

   CIS
   Benchmarks

Sistemi Operativi

::

Windows Server

::

2012 CIS Microsoft Windows Server 2012 (non-R2) Benchmark
https://www.cisecurity.org/benchmark/microsoft_windows_server/

::

   CIS
   Benchmarks

Sistemi Operativi

::

Windows Server

::

2008 R2 CIS Microsoft Windows Server 2008 R2 Benchmark
https://www.cisecurity.org/benchmark/microsoft_windows_server/

::

   CIS
   Benchmarks

Sistemi Operativi

::

Windows Server

::

2008 CIS Microsoft Windows Server 2008 (non-R2) Benchmark
https://www.cisecurity.org/benchmark/microsoft_windows_server/

::

   CIS
   Benchmarks

Sistemi Operativi

::

Windows Server

::

2003 CIS Microsoft Windows Server 2003 Benchmark
https://www.cisecurity.org/benchmark/microsoft_windows_server/

::

   CIS
   Benchmarks

Collaboration Server

::

Microsoft SharePoint

::

2016 CIS Microsoft SharePoint 2016 Benchmark
https://www.cisecurity.org/benchmark/microsoft_sharepoint/

::

   CIS
   Benchmarks

Web / Application Server

::

Microsoft IIS

::

IIS 10 CIS Microsoft IIS 10 Benchmark
https://www.cisecurity.org/benchmark/microsoft_iis/

::

   CIS
   Benchmarks

Web / Application Server

::

Microsoft IIS

::

IIS 8 CIS Microsoft IIS 8 Benchmark
https://www.cisecurity.org/benchmark/microsoft_iis/

::

   CIS
   Benchmarks

Web / Application Server

::

Microsoft IIS

::

IIS 7 CIS Microsoft IIS 7 Benchmark
https://www.cisecurity.org/benchmark/microsoft_iis/

::

   CIS
   Benchmarks

Web / Application Server

::

Apache HTTP

::

2.4 CIS Apache HTTP Server 2.4 Benchmark
https://www.cisecurity.org/benchmark/apache_http_server/

::

   CIS
   Benchmarks

Web / Application Server

::

Apache HTTP

::

2.2 CIS Apache HTTP Server 2.2 Benchmark
https://www.cisecurity.org/benchmark/apache_http_server/

::

   CIS
   Benchmarks

Web / Application Server

::

Apache Tomcat

::

8 CIS Apache Tomcat 8 Benchmark
https://www.cisecurity.org/benchmark/apache_tomcat/

::

   CIS
   Benchmarks

Web / Application Server

::

Apache Tomcat

::

7 CIS Apache Tomcat 7 Benchmark
https://www.cisecurity.org/benchmark/apache_tomcat/

::

   CIS
   Benchmarks

DBMS Microsoft SQL Server

::

2016 CIS Microsoft SQL Server 2016 Benchmark
https://www.cisecurity.org/benchmark/microsoft_sql_server/

::

   CIS
   Benchmarks

DBMS Microsoft SQL Server

::

2014 CIS Microsoft SQL Server 2014 Benchmark
https://www.cisecurity.org/benchmark/microsoft_sql_server/

::


   CIS
   Benchmarks

DBMS Microsoft SQL Server

::

2012 CIS Microsoft SQL Server 2012 Benchmark
https://www.cisecurity.org/benchmark/microsoft_sql_server/

::

   CIS
   Benchmarks

DBMS Microsoft SQL Server

::

2008 R2 CIS Microsoft SQL Server 2008 R2 Benchmark
https://www.cisecurity.org/benchmark/microsoft_sql_server/

::

   CIS
   Benchmarks

DBMS Oracle DB 12c CIS Oracle Database 12c Benchmark
https://www.cisecurity.org/benchmark/oracle_database/

::

   CIS
   Benchmarks

DBMS Oracle DB 11g R2 CIS Oracle Database 11g R2 Benchmark
https://www.cisecurity.org/benchmark/oracle_database/

::

   CIS
   Benchmarks

DBMS Oracle DB 11 – 11g CIS Oracle Database Server 11 - 11g Benchmark
https://www.cisecurity.org/benchmark/oracle_database/

::

   CIS
   Benchmarks

DBMS Oracle MySQL

::

5.7 EE CIS Oracle MySQL Enterprise Edition 5.7 BenchmarK
https://www.cisecurity.org/benchmark/oracle_mysql/

::

   CIS
   Benchmarks

DBMS Oracle MySQL

::

5.7 CE CIS Oracle MySQL Community Server 5.7 Benchmark
https://www.cisecurity.org/benchmark/oracle_mysql/

::

   CIS
   Benchmarks

DBMS Oracle MySQL

::

5.6 EE CIS Oracle MySQL Enterprise Edition 5.6 Benchmark
https://www.cisecurity.org/benchmark/oracle_mysql/

::

   CIS
   Benchmarks

DBMS Oracle MySQL

::

5.6 CE CIS Oracle MySQL Community Server 5.6 Benchmark
https://www.cisecurity.org/benchmark/oracle_mysql/

::

   CIS
   Benchmarks

DBMS IBM DB2 10 CIS IBM DB2 10 Benchmark
https://www.cisecurity.org/benchmark/ibm_db2/

::

   CIS
   Benchmarks

DBMS IBM DB2 9 CIS IBM DB2 9 Benchmark
https://www.cisecurity.org/benchmark/ibm_db2/

::

   CIS
   Benchmarks

DBMS IBM DB2 8 CIS IBM DB2 Benchmark
https://www.cisecurity.org/benchmark/ibm_db2/

::

   CIS
   Benchmarks

DNS Server BIND 9.9 CIS ISC BIND DNS Server 9.9 Benchmark

::

   CIS
   Benchmarks

Mail Server Microsoft Exchange Server

::

2016 CIS Microsoft Exchange Server 2016 Benchmark
https://www.cisecurity.org/benchmark/microsoft_exchange_server/

::

   CIS
   Benchmarks

Mail Server Microsoft Exchange Server

::

2013 CIS Microsoft Exchange Server 2013 Benchmark
https://www.cisecurity.org/benchmark/microsoft_exchange_server/

::

   CIS
   Benchmarks

Mail Server Microsoft Exchange Server

::

2010 CIS Microsoft Exchange Server 2010 BenchmarK
https://www.cisecurity.org/benchmark/microsoft_exchange_server/

::


   CIS
   Benchmarks

Office Automation

::

Microsoft Office

::

2016 2013

::

CIS Microsoft Office 2016 Benchmark CIS Microsoft Office Word 2016
Benchmark CIS Microsoft Office Excel 2016 Benchmark CIS Microsoft Office
PowerPoint 2016 Benchmark CIS Microsoft Office Access 2016 Benchmark CIS
Microsoft Office Outlook 2016 Benchmark CIS Microsoft Office 2013
Benchmark CIS Microsoft Office Word 2013 Benchmark CIS Microsoft Office
Excel 2013 Benchmark CIS Microsoft Office PowerPoint 2013 Benchmark CIS
Microsoft Office Access 2013 Benchmark CIS Microsoft Office Outlook 2013
Benchmark https://www.cisecurity.org/benchmark/microsoft_office/

::

   CIS
   Benchmarks

Web Browser

::

Internet Explorer

::

11 CIS Microsoft Internet Explorer 11 Benchmark
https://www.cisecurity.org/benchmark/microsoft_internet_explorer/

::

   CIS
   Benchmarks

Web Browser

::

Internet Explorer

::

10 CIS Microsoft Internet Explorer 10 Benchmark
https://www.cisecurity.org/benchmark/microsoft_internet_explorer/

::

   CIS
   Benchmarks

Web Browser

::

Mozilla Firefox

::

CIS Mozilla Firefox 38 ESR Benchmark
https://www.cisecurity.org/benchmark/mozilla_firefox/

::

   CIS
   Benchmarks

Web Browser

::

Mozilla Firefox

::

CIS Mozilla Firefox 24 ESR Benchmark
https://www.cisecurity.org/benchmark/mozilla_firefox/

::

   CIS
   Benchmarks

Web Browser

::

Google Chrome

::

CIS Google Chrome Benchmark
https://www.cisecurity.org/benchmark/google_chrome/

::

   CIS
   Benchmarks

Networking Cisco IOS IOS 15 CIS Cisco IOS 15 Benchmark
https://www.cisecurity.org/benchmark/cisco/

::

   CIS
   Benchmarks

Networking Cisco IOS IOS 12 CIS Cisco IOS 12 Benchmark
https://www.cisecurity.org/benchmark/cisco/

::

   ### 6.2 TOOLS DI HARDENING E BASELINE DI SICUREZZA FORNITE DAI VENDOR

   Si riporta nel seguito un elenco di strumenti software (laddove disponibili) e baseline di sicurezza, per la
   configurazione sicura (hardening) dei principali sistemi target.


   **Fonte Categoria Famiglia Target Titolo**

   Microsoft Sistemi
   Operativi

Windows Windows Server & Client

::

Microsoft Security Compliance Manager (SCM) È uno strumento gratuito di
Microsoft che consente di gestire correttamente e agilmente la sicurezza
dell'infrastruttura IT e delle applicazioni, analizzando la propria
infrastruttura e configurandola seguendo le raccomandazioni di
Microsoft. Consente una gestione centralizzata dell'insieme delle
baseline di sicurezza, con la possibilità di gestire specifiche
personalizzazioni in base a specifiche esigenze di certi sistemi.
Consente inoltre di esportare le configurazioni in vari formati tra cui
XLS (Excel) e GPO (Group Policy Objects). Supporta i sistemi operativi
Windows Server e Windows Client. https://technet.microsoft.com/en-
us/solutionaccelerators/cc835245.aspx

::

   Microsoft Web Server IIS 8 Security Best Practices for IIS 8

https://technet.microsoft.com/en- us/library/jj635855(v=ws.11).aspx

::

   Microsoft DBMS SQL Server 20108 -
   2016

Non è disponibile ad oggi un tool specific ma esiste una pagina di
riferimento di Microsoft aggiornata che contiene oppotyune indicazioni
per la configurazione sicura di SQL Server:
https://docs.microsoft.com/en-us/sql/relational-
databases/security/securing-sql-server#sql-server-security-
tools-utilities-views-and-functions Esiste inoltre una pagina ulteriore
di supporto per specifici task di configurazione sicura che riguardano
non solo SQL Server ma più in generale l'accesso ai dati: Security
Checklists for the Database Engine:

::

   - Checklist: Database Engine Security Configuration
   - Checklist: Enhancing the Security of Database Engine
       Connections
   - Checklist: Limiting Access to Data
   - Checklist: Encrypting Sensitive Data
   https://technet.microsoft.com/en-
   us/library/ff848778(v=sql.105).aspx

   Bastille Sistemi
   Operativi

Linux (RedHat, SUSE, Debian, Ubuntu) e HP- UX

::

Vari Bastille Linux è un tool gratuito per l'hardening di vari sistemi
operative Linux (RedHat, Debian, SUSE, ecc.) e HP-UX. Sulla maggior
parte dei sistemi operativi supportati fa parte della distribuzione
standard ed è quindi immediatamente disponibile per l'uso.
http://bastille-linux.sourceforge.net/

::

   Apache
   Software
   Foundation

Web Server Apache HTTP 2.4 Security Tips - Apache HTTP Server Version
2.4 https://httpd.apache.org/docs/2.4/misc/security_tips.html

::

   Apache
   Software
   Foundation

Web Server Tomcat 8 Apache Tomcat 8 Security Considerations
https://tomcat.apache.org/tomcat-8.0-doc/security-howto.html

::


   Oracle DBMS Oracle
   Database

12c 11g

::

Oracle Database 12c Security and Compliance
https://www.oracle.com/webfolder/s/delivery_production/doc
s/FY15h1/doc6/security-compliance-wp.pdf Cost Effective Security and
Compliance with Oracle Database 11g
http://www.oracle.com/technetwork/database/security/owp-
security-database-11gr2-134651.pdf L'elenco del software Oracle legato
alla sicurezza del prodotto Oracle Database è disponibile a questo
indirizzo: Oracle Database Security Products
https://www.oracle.com/database/security/products.html

::

   Oracle Database Oracle MySQL 5.7 MySQL Security Guide, parte di MySQL Reference Manual

Un estratto è disponibile a questo link:
https://dev.mysql.com/doc/mysql-security-excerpt/5.7/en/

::

   McAfee Database Oracle MySQL Varie McAfee MySQL Database Security Tool (gratuito):

https://www.mcafee.com/ca/products/database- security/mysql-plug-in.aspx

::

   Microsoft Mail Server Exchange
   Server

2016 2013 2010

::

Offline Assessment for Exchange Server Security
http://download.microsoft.com/download/1/C/1/1C15BA51- 840E-498D-86C6-
4BD35D33C79E/Prerequisites_Offline_EXCHSec.pdf

::




   # LINEE GUIDA PER LA MODELLAZIONE DELLE MINACCE ED INDIVIDUAZIONE DELLE AZIONI DI MITIGAZIONE CONFORMI AI PRINCIPI DEL SECURE/PRIVACY BY DESIGN

   Trasposizione in markdown delle Linee Guida ufficiali reperibili qui https://www.agid.gov.it/it/sicurezza/cert-pa/linee-guida-sviluppo-del-software-sicuro

   TODO: vanno riportate le immagini.



   ## Linee Guida per la modellazione delle minacce ed individuazione delle azioni di mitigazione conformi ai principi del Secure/Privacy


   ###### LISTA DELLE TABELLE

   Tabella 1 - Documenti Applicabili ............................................................................... **Errore. Il segnalibro non è definito.**

Figura 5 - Diagramma del sistema
………………………………………………………………………………………………………………………. Figura 6 - Aggiunta dei
“Trust boundaries” al diagramma ……………………………………………………………………………………….

::

   - 1 INTRODUZIONE SOMMARIO
      - 1.1 SCOPO
      - 1.2 AMBITO DI APPLICABILITÀ
      - 1.3 STRUTTURA DEL DOCUMENTO
   - 2 DEFINIZIONI E ACRONIMI
      - 2.1 DEFINIZIONI
      - 2.2 ACRONIMI................................................................................................................................................................
   - 3 ESIGENZE ED AMBITI DI APPLICAZIONE
   - 4 PROGETTAZIONE DEL SOFTWARE SECURE/PRIVACY BY DESIGN
      - 4.1 PROCESSI DI SVILUPPO DEL SOFTWARE SICURO
         - 4.1.1 Open Software Assurance Maturity Model (SAMM)
         - 4.1.2 Building Security in Maturity Model (BSIMM)
         - 4.1.3 Comprehensive, Light-weight Application Security Process (CLASP)
         - 4.1.4 Microsoft’s Security Development Lifecycle (SDL)
      - 4.2 MODELLAZIONE E INDIVIDUAZIONE DELLE MINACCE: THREAT MODELLING
         - 4.2.1 Introduzione e concetti base
         - 4.2.2 Motivazioni nell’uso del Threat Model
            - 4.2.2.1 Ricerca preventiva dei bug di sicurezza
            - 4.2.2.2 Comprensione dei requisiti di sicurezza .................................................................................................................
            - 4.2.2.3 Ingegnerizzazione e rilascio di prodotti più sicuri ...................................................................................................
         - 4.2.3 Processo di modellazione del sistema da proteggere
            - 4.2.3.1 Diagrammi DFD .......................................................................................................................................................
         - 4.2.4 Tecniche di modellazione e individuazione delle minacce
            - 4.2.4.1 Microsoft SDL – STRIDE ..........................................................................................................................................
            - 4.2.4.2 Attack tree ..............................................................................................................................................................
            - 4.2.4.3 TRIKE .......................................................................................................................................................................
            - 4.2.4.4 P.A.S.T.A (Process for Attack Simulation and Threat Analysis) ...............................................................................
            - 4.2.4.5 AS/NZS 31000:2009 Risk Management ..................................................................................................................
            - 4.2.4.6 Best practices di carattere generale .......................................................................................................................
      - 4.3 INDIRIZZAMENTO DELLE MINACCE
      - 4.4 VALUTAZIONE DEL RISCHIO: TECNICHE DI RISK RANKING
         - 4.4.1 DREAD
         - 4.4.2 Security Bulletin Severity Rating System (S.B.S.R.S)
         - 4.4.3 Altri processi di valutazione del rischio........................................................................................................
      - 4.5 PRIVACY BY DESIGN
         - 4.5.1 Introduzione e concetti base
            - 4.5.1.1 Proprietà
            - 4.5.1.2 Principi ....................................................................................................................................................................
            - 4.5.1.3 Riferimenti normativi .............................................................................................................................................
         - 4.5.2 Best practices per il trattamento dei dati personali
         - 4.5.3 Tecniche di modellazione e individuazione delle minacce
            - 4.5.3.1 LINDDUN
            - 4.5.3.2 PRoPAN ...................................................................................................................................................................
            - 4.5.3.3 PriS ..........................................................................................................................................................................
            - 4.5.3.4 FPFSD ......................................................................................................................................................................
            - 4.5.3.5 MPRA ......................................................................................................................................................................
            - 4.5.3.6 Privacy in the Cloud ................................................................................................................................................
            - 4.5.3.7 Adaptive privacy .....................................................................................................................................................
            - 4.5.3.8 STRAP ......................................................................................................................................................................
            - 4.5.3.9 Microsoft privacy guidelines ...................................................................................................................................
            - 4.5.3.10 PRET ......................................................................................................................................................................
   - 5 LINEE GUIDA PER L’INDIVIDUAZIONE E LA RIVISITAZIONE DEI REQUISITI DI SICUREZZA E DI PRIVACY APPLICATIVI
      - 5.1 LINEE GUIDA PER LA MODELLAZIONE DELLE MINACCE Linee Guida per la modellazione delle minacce ed individuazione delle azioni di mitigazione conformi ai principi del Secure/Privacy
         - 5.1.1 Identificazione degli obiettivi di sicurezza
         - 5.1.2 Creazione di un disegno ad alto livello dell’applicazione
            - 5.1.2.1 Identificazione dei Ruoli .........................................................................................................................................
            - 5.1.2.2 Identificare gli Scenari d’Uso Chiave .......................................................................................................................
            - 5.1.2.3 Identificare le Tecnologie .......................................................................................................................................
            - 5.1.2.4 Identificare Meccanismi di Sicurezza Applicativa ...................................................................................................
         - 5.1.3 Scomposizione dell’applicazione
            - 5.1.3.1 Confini di fiducia (Trust boundaries) ......................................................................................................................
            - 5.1.3.2 Flussi di Dati ............................................................................................................................................................
            - 5.1.3.3 Punti d’Ingresso (Entry Points) ...............................................................................................................................
            - 5.1.3.4 Punti di Uscita (Exit Points) .....................................................................................................................................
         - 5.1.4 Identificazione delle minacce
            - 5.1.4.1 Identificazione delle minacce e attacchi comuni ....................................................................................................
            - 5.1.4.2 Identificazione delle potenziali minacce annidate nei casi d’uso ...........................................................................
            - 5.1.4.3 Identificazione delle potenziali minacce annidate nei flussi di dati ........................................................................
            - 5.1.4.4 Esplorare minacce ulteriori usando gli alberi delle minacce/attacchi ....................................................................
         - 5.1.5 Identificazione delle vulnerabilità................................................................................................................
      - 5.2 IDENTIFICAZIONE DEL PROCESSO DI SVILUPPO DEL SOFTWARE SICURO
      - 5.3 MODELLAZIONE E INDIVIDUAZIONE DELLE MINACCE CON STRIDE
      - 5.4 VALUTAZIONE DEL RISCHIO DERIVANTE DALLE MINACCE INDIVIDUATE CON DREAD
      - 5.5 MODELLAZIONE E INDIVIDUAZIONE DELLE MINACCE DI PRIVACY CON LINDUN
   - 6 UN ESEMPIO APPLICATIVO: CASO D’USO “EASY WEB SITE”
      - 6.1 DIAGRAMMA: USE CASE
      - 6.2 INTERAZIONE: DA BROWSER CLIENT A WEB SERVER
         - 6.2.1 Assunzioni
         - 6.2.2 Accesso a internet non valido
         - 6.2.3 Mancanza di convalida dell'input da parte del "Web Server"
         - 6.2.4 Cross Site Scripting
         - 6.2.5 Ripudio di dati da parte del 'Browser Client'
         - 6.2.6 Crash o fermo del processo 'Web Server'
         - 6.2.7 Interruzione del flusso dati HTTPS (o inaccessibilità da parte del 'Web Server')
         - 6.2.8 Elevazione di privilegi attraverso l’esecuzione remota di codice da parte del 'Web Server'
         - 6.2.9 Elevazione dei privilegi attraverso il cambiamento del flusso di esecuzione nel codice del 'Web Server'
         - 6.2.10 Cross Site Request Forgery
      - 6.3 INTERAZIONE: DA WEB SERVER A BROWSER CLIENT
         - 6.3.1 Assunzioni
         - 6.3.2 Analisi delle minacce e mitigazioni
      - 6.4 INTERAZIONE: DA WEB SERVER A SQL DATABASE
         - 6.4.1 Assunzioni
         - 6.4.2 Vulnerabilità di SQL Injection nel 'SQL Database'
         - 6.4.3 Possibile corruzione del 'SQL Database'
         - 6.4.4 Consumo eccessivo di risorse da parte del 'Web Server' o del 'SQL Database'
      - 6.5 INTERAZIONE: DA SQL DATABASE A WEB SERVER
         - 6.5.1 Assunzioni
         - 6.5.2 Persistent Cross Site Scripting
         - 6.5.3 Controllo accesso debole per una risorsa
   - 7 BIBLIOGRAFIA
   - Tabella 3 - Definizioni Tabella 2 - Documenti di Riferimento Errore. Il segnalibro non è definito.
   - Tabella 4 - Acronimi
   - Tabella 5 - Vulnerabilità dovute a errori
   - Tabella 6 - Caratteristiche degli elementi DFD Linee Guida per la modellazione delle minacce ed individuazione delle azioni di mitigazione conformi ai principi del Secure/Privacy
   - Tabella 7 - STRIDE per elemento DFD
   - Tabella 8 - STRIDE proprietà violate
   - Tabella 9 - Tecniche di mitigazione
   - Tabella 10 - STRIDE: Indirizzamento dello Spoofing
   - Tabella 11 - STRIDE: Indirizzamento del Tampering
   - Tabella 12 - STRIDE: Indirizzamento della repudiation
   - Tabella 13 - STRIDE: Indirizzamento dell'Information disclosure
   - Tabella 14 - STRIDE: Indirizzamento del Denial of Service
   - Tabella 15 - STRIDE: Indirizzamento dell'Elevation of privilege
   - Tabella 16 - Modello DREAD
   - Tabella 17 - Sistema di classificazione del S.B.S.R.S.
   - Tabella 18 - Concetti alla base della Privacy
   - Tabella 19 - Minacce LINDDUN per elemento DFD
   - Tabella 20 - obiettivi di privacy basati sule varie tipologie di minaccia previste in LINDDDUN........................................
   - Tabella 21 - LINDDUN Hard & Soft privacy
   - Tabella 22 - Mappatura tra obiettivi e tecniche di miglioramento della privacy..............................................................
   - Figura 1 - Processo del ciclo di sviluppo sicuro di Microsoft LISTA DELLE FIGURE
   - Figura 2 - SDL: Passi nella modellazione delle minacce
   - Figura 4 - Simbolismo nel Threat Modelling Figura 3 - I quattro step del Framework
   - Figura 8 - Esempio di disegno architetturale di una applicazione Figura 7 - Numerazione degli elementi del diagramma
   - Figura 9 - Diagramma dello use case
   - Figura 10 - Interazione tra Browser Client e Web Server
   - Figura 11 - Interazione tra Web Server e Browser Client
   - Figura 12 - Interazione tra Web Server e SQL Database
   - Figura 13 - Interazione tra SQL Database e Web Server


   Linee Guida per la modellazione delle minacce ed individuazione delle azioni di mitigazione conformi ai principi del Secure/Privacy

   ## 1 INTRODUZIONE SOMMARIO

   ### 1.1 SCOPO

   Gli obiettivi degli attacchi sono spesso vulnerabilità che si celano all’interno delle applicazioni software. La
   comunità OWASP (www.owasp.org) sottolinea la necessità di accrescere la consapevolezza sulla sicurezza
   delle applicazioni in quanto il software non sicuro mette a repentaglio le infrastrutture finanziarie,

   ### sanitarie, difensive, etc.

   Questo documento vuole analizzare il contesto (processi, metodi e modelli) della Progettazione di
   Applicazioni Sicure con l’obiettivo di fornire le linee guida per la modellazione delle minacce e conseguente
   individuazione di azioni di mitigazione, in conformità con i principi “Secure/privacy by Design”. Ciò
   costituisce una fase importante nel processo di individuazione preventiva dei requisiti di sicurezza e
   privacy.

   ### 1.2 AMBITO DI APPLICABILITÀ

   Il presente documento si applica al contesto tecnologico dell’Agenzia per l’Italia Digitale (in seguito AgID)
   nell’ambito dei servizi previsti dal Contratto Esecutivo in [DA-8 ].

   ### 1.3 STRUTTURA DEL DOCUMENTO

   Il presente documento è articolato come segue:

   - Il **Capitolo 5** , introduce i concetti base di security e privacy by design, analizza gli strumenti e i
       modelli a supporto della fase di progettazione del software sicuro, in essere e in divenire;
   - Il **Capitolo 6** , definisce le linee guida per l’identificazione preventiva delle possibili minacce, delle
       relative azioni di mitigazione e per la valutazione e prioritizzazione delle minacce stesse;
   - Il **Capitolo 7** , fornisce un caso d’uso applicativo in cui vengono impiegate le metodologie e gli
       strumenti di sicurezza indicati nel Capitolo 5 (Linee Guida).


   Linee Guida per la modellazione delle minacce ed individuazione delle azioni di mitigazione conformi ai principi del Secure/Privacy

   ## 2 DEFINIZIONI E ACRONIMI

   ### 2.1 DEFINIZIONI

   Vocabolo Descrizione

   Ambiente di produzione Agglomerato di sistemi, dispositivi hardware ed applicazioni in cui il software
   viene installato nella sua forma definitiva al fine di soddisfare le richieste
   dell’operatore o dell’utente finale.

   Ambiente di sviluppo Agglomerato di sistemi, dispositivi hardware ed applicazioni in cui il software
   viene progettato e creato.

   Ambiente di test Agglomerato di sistemi, dispositivi hardware ed applicazioni in cui il software
   creato viene testato.

   Autenticazione

Processo attraverso il quale un sistema, un utente o un programma tenta
di confermare la sua identità ad un altro sistema o applicazione.

::

   Autorizzazione

Processo di definizione dei privilegi, ruoli e permessi di un utente su
un sistema o un'applicazione.

::

   Batch Job Processo di scambio dati o informazioni che intercorre automaticamente, in
   periodi temporali prestabiliti, tra due sistemi, applicazioni o componenti.

   Dati critici

Dati che hanno una rilevanza preponderante per l'immagine e l'operato
aziendale (esempio cartellini di traffico telefonico).

::

   Dati personali Come da decreto legislativo 196/03: “qualunque informazione relativa a persona
   fisica, persona giuridica, ente od associazione, identificati o identificabili, anche
   indirettamente, mediante riferimento a qualsiasi altra informazione, ivi
   compreso un numero di identificazione personale”.

   Dati sensibili Come da decreto legislativo 196/03: “Dati personali idonei a rivelare l'origine
   razziale ed etnica, le convinzioni religiose, filosofiche o di altro genere, le
   opinioni politiche, l'adesione a partiti, sindacati, associazioni od organizzazioni a
   carattere religioso, filosofico, politico o sindacale, nonché i dati personali idonei
   a rivelare lo stato di salute e la vita sessuale”.

   Eccezione Occorrenza di una circostanza che altera o mira ad alterare il corso previsto o il
   normale operato di un sistema, di un’applicazione o di una sua componente.

   Evento Situazione riconducibile ad un’attività svolta o ad un’eccezione causata
   dall’utente, rilevante ai fini della sicurezza del sistema e dell’Information
   Security.

   Identificazione Meccanismo di convalida preventiva di un’azione.

   Information Gathering &
   Disclosure

Processo relativo alla fuga di dati o informazioni, causato da bug o
errori nel software.

::

   Information Security Insieme di controlli, policy, processi e procedure mirate a garantire la sicurezza
   delle informazioni in azienda.

   Offuscatore Software che converte il codice sorgente in forma difficilmente interpretabile o
   non interpretabile del tutto al fine di inibire l’utilizzo di tecniche di reverse
   engineering.


   Linee Guida per la modellazione delle minacce ed individuazione delle azioni di mitigazione conformi ai principi del Secure/Privacy

   Vocabolo Descrizione

   Organizzazione Ente locale o centrale della Pubblica Amministrazione

   Reverse Engineering Processo mirato a scoprire i principi tecnologici di un’applicazione attraverso la
   sua analisi strutturale.

   Token Valore generato per identificare univocamente una sessione interattiva.

Tabella 1 - Definizioni

::

   ### 2.2 ACRONIMI................................................................................................................................................................

Codice Titolo

::

   ACLs Access Control List

   AgID Agenzia per l'Italia Digitale

   API Application Programming Interface^

   ASLR Address Space Layout Randomization^

   BSIMM Building Security in Maturity Model^

   CLASP Comprehensive and Lightweight Application Security Process^

   CVSS Common Vulnerability Scoring System^

   DFD Data Flow Diagram^

   DPD Data Protection Directive^

   DPIA Data Protection Impact Analysis^

   DPO Data Protection Officer^

   DREAD Damage Potential, Reproducibility, Exploitability, Affected users, Discoverability^

   DS Data Store^

   E Entity^

   FIPP Fair Information Practice Principles^

   FIPPs Fair Information Practice Principles^

   FPFSD framework for Privacy-Friendly System Design

   GDPR General Data Protection Regulation^

   HAZOP Hazardous Operations^

   IOI Item^ of Interest^

   IPSec IP Security^

   LINDDUN Linkability, Identifiability, Non Repudiation, Detectability, Disclosure of information, Content
   Unawareness e Policy and consent Non-compliance

   MIC Mandatory Integrity Control^

   MITM Man In The Midle^

   MPRA Multilateral Privacy Requirements Analysis^

   MS –SDL Microsoft’s Security Development Lifecycle^


   Linee Guida per la modellazione delle minacce ed individuazione delle azioni di mitigazione conformi ai principi del Secure/Privacy

Codice Titolo

::

   NIST National Institute of Standards and Technology^

   OCSE Organizzazione per la Cooperazione e lo Sviluppo Economico^

   OWASP Open Web Application Security Project^

   P Process^

   P.A.S.T.A Process for Attack Simulation and Threat Analysis^

   PAR Privacy Awareness Requirements^

   PbD Privacy by Design^

   PE Privacy Engineering^

   PETs Privacy-Enhancing Technologies^

   PI Personal Informations^

   PII Personale Indentifiable Information^

   PRET Privacy Requirements Elicitation Technique^

   PriS Incorporating Privacy Requirements into the System Design Process^

   ProPAn Problem-based Privacy Analysis^^

   ROI Return On Investment

   S.B.S.R.S. Security Bulletin Severity Rating System^

   SAMM Software Assurance Maturity Model^

   SDL Security Development Lifecycle^

   SDLC Software Development Life Cycle^

   SSDLC Secure Software Development Life Cycle^

   STRIDE Spoofing, Tampering, Repudiation, Information disclosure, Denial of service, Elevation of^
   privilege

   SW Software^

   TCP Trasmission Control Protocol^

   UML Linguaggio di modellazione Unificata^

   XSS Cross-site scripting^

Tabella 2 - Acronimi

::


   Linee Guida per la modellazione delle minacce ed individuazione delle azioni di mitigazione conformi ai principi del Secure/Privacy

   ## 3 ESIGENZE ED AMBITI DI APPLICAZIONE

   Secondo la fonte Gartner^1 , anche in considerazione delle contromisure adottate negli ultimi anni per il
   controllo degli accessi alle infrastrutture e la messa in protezione dei dati, negli ultimi tempi, oltre il 75%
   degli attacchi sono stati indirizzati direttamente verso le applicazioni software, causando gravi danni di
   immagine e pesanti perdite finanziarie. Gli obiettivi degli attacchi sono le vulnerabilità che si celano
   all’interno di tale applicazioni. Le vulnerabilità applicative sono quasi sempre presenti poiché, fino ad ora, le
   politiche di qualità del software ed i relativi investimenti si sono concentrate soprattutto sulla correzione
   delle difettosità funzionali e sulle performance delle logiche applicative, trascurando l’attuazione di
   pratiche di progettazione e programmazione che garantiscono l’opportuna sicurezza.

   Le vulnerabilità applicative vengono continuamente introdotte dagli stessi team di sviluppo interni alle
   organizzazioni, dai fornitori, dalle soluzioni open-source: alcuni analisti affermano che il 64% degli
   sviluppatori non sono confidenti di poter scrivere applicazioni sicure (fonte: Microsoft Developer
   Research^2 );

   A titolo esplicativo, la seguente matrice riporta un indice quantitativo di effort in termini di costi necessario
   nella risoluzione delle problematiche di sicurezza applicativa:

   ###### PROBLEMATICHE DI SICUREZZA (VULNERABILITA’)

Scoperte in fase di progettazione e disegno

::

Scoperte in fase di sviluppo

::

Scoperte in fase di integrazione

::

Scoperte in fase di collaudo

::

Scoperte in fase di esercizio

::

   ###### DOVUTE A

   ###### ERRORI

Architetturali^ 1X^ 5X^ 10X^ 20X^ 30X^ Di codifica 1X 10X 20X 30X

::

Di integrazione 1X 10X 15X Tabella 3 - Vulnerabilità dovute a errori

::

   Il National Institute of Standards and Technology (NIST^3 ) ha stimato che il costo del “code fixing” eseguito
   dopo il rilascio in produzione può risultare 30 volte il costo che si avrebbe in fase di progettazione.

   Il numero delle tipologie di attacchi cresce in maniera esponenziale: dalle circa 2500 identificate nel 2000, si
   è passati ad oltre 50000 nel 2009 e continuamente se ne scoprono delle nuove (fonte: CERT^4 ). Da qui
   l’inizio della diffusione delle prime e fondamentali best practices in materia di sicurezza applicativa, le
   prime tra tutte riconducibili ad una buona ingegnerizzazione del software, una piena comprensione delle
   minacce più comuni, compresi i difetti propri dei linguaggi di programmazione, ma soprattutto una
   considerazione della problematica fin dalle prime fasi del ciclo di sviluppo.

   I costi aggiuntivi possono portare ad una perdita significativa di produttività e fiducia da parte degli utenti.
   L'adozione di un ciclo di vita sicuro del software (SSDLC) - **_Linee guida per l'adozione di un ciclo di sviluppo
   software sicuro - D01.Fase1.SP2_** [DR-1 ] - aiuta sistematicamente a considerare ed implementare
   opportune attività/metodologie di sicurezza nel corso di tutte le sue fasi: analisi, progettazione, sviluppo,

   (^1) https://www.gartner.com
   (^2) https://developer.microsoft.com/it-it/windows
   (^3) https://www.nist.gov/
   (^4) https://www.certnazionale.it/


   Linee Guida per la modellazione delle minacce ed individuazione delle azioni di mitigazione conformi ai principi del Secure/Privacy

   test e manutenzione, assicurando che le vulnerabilità siano più facilmente individuabili e misurate prima
   della distribuzione dell'applicazione, riducendo così il costo totale dello sviluppo del software.

   Esistono diversi modelli e metodologie di ciclo di vita di sviluppo del software, ma ciascuna di queste in
   generale consiste di una serie di step o fasi predefinite. Indipendentemente dal modello SDLC scelto, è
   necessario integrare il concetto di sicurezza al fine di garantire una appropriata protezione del sistema e
   delle informazioni che dovrà trasmettere, elaborare e memorizzare.

   La progettazione di applicazioni software sicure può essere complessa e difficile, ma una buona strategia da
   adottare è quella di scomporre l’applicativo in piccole parti in modo da renderlo più facilmente analizzabile.
   Esistono importanti motivazioni che giustificano la necessità di realizzare un modello delle minacce, primo
   tra tutti la ricerca preventiva di difetti di sicurezza e a seguire, la finalizzazione dei requisiti di sicurezza nella
   progettazione di applicazioni più sicure.


   Linee Guida per la modellazione delle minacce ed individuazione delle azioni di mitigazione conformi ai principi del Secure/Privacy

   ## 4 PROGETTAZIONE DEL SOFTWARE SECURE/PRIVACY BY DESIGN

   ### 4.1 PROCESSI DI SVILUPPO DEL SOFTWARE SICURO

   Questo capitolo illustra alcuni dei framework di processo di riferimento nello sviluppo sicuro delle
   applicazioni software, quali: il Software Assurance Maturity Model (SAMMM), il Building Security in
   Maturity Model (BSIMM), il Comprehensive and Lightweight Application Security Process (CLASP) e il ciclo
   di vita di sviluppo sicuro (SDL) di Microsoft (MS-SDL).

   Lo scopo nel presentare diversi framework di sviluppo è quello di ottenere una migliore comprensione delle
   tecniche di Threat Modeling e di come questo si adatta alle fasi del ciclo di sviluppo del software.

   #### 4.1.1 Open Software Assurance Maturity Model (SAMM)

   OpenSAAM^5 è un framework supportato da OWASP^6 (Open Web Application Security Project) che si basa
   su un insieme di procedure di sicurezza legate a quattro importanti funzioni di business critiche, coinvolte
   nello sviluppo del software, vale a dire Governance, Costruzione, Verifica e Distribuzione. Ciascuna funzione
   di business adotta tre pratiche di sicurezza e ciascuna di esse è suddivisa in tre livelli di maturità. La
   valutazione delle minacce è la prima pratica di sicurezza adottata durante la funzione di business
   “Costruzione”. Questa utilizza il Threat modeling per identificare i potenziali rischi. OpenSAAM non si lega
   ad alcun approccio di modellazione delle minacce e raccomanda l'uso di STRIDE della Microsoft o TRIKE
   come possibili opzioni.

   #### 4.1.2 Building Security in Maturity Model (BSIMM)

   L' iniziativa di sicurezza BSIMM^7 è stata progettata per aiutare i team di sviluppo software a comprendere e
   pianificare la sicurezza in un ciclo di vita di sviluppo delle applicazioni, studiando le pratiche di cinquantuno
   importanti iniziative di sicurezza software. Aziende come Google, Adobe, Intel, Visa, Nokia, Sony e
   Microsoft hanno partecipato alla ricerca guidata da Gary McGraw (leader esperto di settore nella sicurezza
   del software, vicepresidente della Security Technology presso la Synopsys Inc. SNPS, autorità riconosciuta a
   livello mondiale per la sicurezza del software e autore di otto libri tra i più venduti su questa tematica). La
   metodologia risultante ha unito le migliori pratiche (parere del team BSIMM) in un'unica iniziativa. Si tratta
   di dodici pratiche raggruppate in quattro domini, Governance, Intelligence, SSDL Touchpoint (pratiche
   associate all'analisi e alla garanzia di particolari manufatti e processi di sviluppo del software. Tutte le
   metodologie di sicurezza del software includono l’analisi dell’architettura, la revisione del codice e i test di
   sicurezza) e Deployment, utilizzate per organizzare le attività del framework di sicurezza del software. La
   prima pratica all'interno del dominio “Intelligence” è costituita dai modelli di attacco. Il Threat modelling
   viene utilizzato durante questa fase per modellare gli attacchi e per creare una base di conoscenza relativa
   all'applicazione.

   BSIMM non è un approccio innovativo per lo sviluppo sicuro del software. Questo framework ha raccolto
   dati su attività effettivamente svolte dai leader dell'industria promuovendo poi quelle migliori e più
   utilizzate. Per tradizione, le società di software erano riluttanti a divulgare informazioni riguardo le pratiche
   interne. L’impiego della metodologia BSIMM sarebbe vantaggiosa per un'organizzazione che intende
   adottare un'iniziativa di sicurezza o migliorare/maturare le pratiche esistenti. Tuttavia, BSIMM non fornisce
   sufficienti informazioni di dettaglio riguardo il Threat Modeling.

   (^5) [http://www.opensamm.org/](http://www.opensamm.org/)
   (^6) https://www.owasp.org/images/6/6f/SAMM_Core_V1-5_FINAL.pdf
   (^7) https://www.bsimm.com/


   Linee Guida per la modellazione delle minacce ed individuazione delle azioni di mitigazione conformi ai principi del Secure/Privacy

   #### 4.1.3 Comprehensive, Light-weight Application Security Process (CLASP)

   Il CLASP^8 , è un altro framework di sicurezza supportato dall' OWASP che contiene best practices
   formalizzate per attuare la sicurezza, in modo strutturato e ripetibile, nei cicli di vita di sviluppo di software
   in essere o in divenire. Il framework esiste dal 2005, ma non sono stati registrati recenti aggiornamenti del
   progetto. È stato originariamente sviluppato dalla Secure Software Inc. e successivamente donato a OWASP
   che lo ha rilasciato come soluzione completa di sicurezza a favore delle organizzazioni. Insieme all'SDL di
   Microsoft, CLASP è stato riconosciuto come uno dei processi originali di alto profilo per lo sviluppo di
   software sicuro. CLASP, si basa su sette best practices che sono alla base di tutte le attività connesse alla
   sicurezza. La valutazione dell’applicazione è una di queste pratiche, che promuove un'analisi dei requisiti di
   sicurezza e la progettazione del sistema basata su l’utilizzo del Threat Modeling.

   Il CLASP non è legato ad alcun metodo di modellizzazione specifico e non ha sviluppato un proprio
   approccio. Al fine di proporre un'iniziativa di sicurezza, a causa di una mancata evoluzione di questo
   progetto, è preferibile prendere in considerazione un framework più innovativo.

   #### 4.1.4 Microsoft’s Security Development Lifecycle (SDL)

   Il ciclo di vita di sviluppo sicuro (SDL^9 ) è una metodologia introdotta dall'iniziativa "Trustworthy Computing"
   di Microsoft. SDL mira a ridurre i costi di manutenzione del software e ad aumentare l'affidabilità
   implementando la sicurezza in ciascuna fase del ciclo di vita dello sviluppo.

   Il processo consiste in pratiche di sicurezza, raggruppate in sette fasi distinte: formazione, requisitazione,
   progettazione, implementazione, verifica, rilascio e monitoraggio/manutenzione.

   Uno degli aspetti chiave dell'SDL è l'introduzione del Threat Modeling nella fase di progettazione, che
   promuove l’individuazione preventiva delle vulnerabilità presenti nelle applicazioni e alcune volte persino i
   potenziali difetti di progettazione. Queste informazioni vengono poi utilizzate per attuare eventuali piani di
   mitigazione o modifiche progettuali.

Figura 1 - Processo del ciclo di sviluppo sicuro di Microsoft

::

   Sono disponibili diversi strumenti, non solo per il Threat Modeling ma per ciascun aspetto dell'SDL, tutorial
   online, documentazione, forum e blog di supporto. Il processo può essere utilizzato anche con le
   metodologie di sviluppo Waterfall e Agile e può essere applicato a qualsiasi piattaforma e implementato da
   qualsiasi organizzazione indipendentemente dalla sua dimensione.

   L'obiettivo che tutte le metodologie di modellazione delle minacce condividono è lo sviluppo di un processo
   a passi iterativi che un team di sviluppo può facilmente seguire durante la valutazione di un sistema
   software.

   (^8) https://www.owasp.org/index.php/CLASP_Concepts
   (^9) https://www.microsoft.com/en-us/sdl/default.aspx


   Linee Guida per la modellazione delle minacce ed individuazione delle azioni di mitigazione conformi ai principi del Secure/Privacy

   Microsoft ha sviluppato e pubblicato una propria metodologia di modellazione delle minacce denominata
   STRIDE (Spoofing, Tampering, Repudiation, Information disclosure, Denial of service, Elevation of privilege)
   e diversi approcci per l’analisi dei rischi, tra cui la DREAD (Damage potential, Reproducibility, Exploitability,
   Affected users, Discoverability). Hussain, Erwin e Dunne hanno indicato la STRIDE come la metodologia di
   Threat modeling più ampiamente utilizzata [1].

   Al termine dell'attività STRIDE, viene prodotto un elenco di vulnerabilità. Tali vulnerabilità vengono poi
   classificate secondo un indice di priorità (basso/medio/alto) utilizzando una tecnica di prioritizzazione delle
   contromisure attraverso la DREAD. Inoltre il prodotto finale dell’analisi STRIDE/DREAD può indirizzare
   anche in una fase successiva un eventuale Penetration Test (sulla base delle vulnerabilità riscontrate è
   possibile delimitare il perimetro che sarà poi oggetto di PT).

   La Figura che segue illustra le fasi principali nella preparazione e nell'esecuzione di una modellazione delle
   minacce.

   ## Figura 2 - SDL: Passi nella modellazione delle minacce

   I processi riguardanti le diverse metodologie di Threat Modelling possono differire fra loro, ma
   hanno tutti in comune la raccolta delle informazioni sull'applicazione, sul suo ambiente, su come questa
   viene utilizzata e distribuita, come le vulnerabilità vengono identificate e come i rischi vengono valutati.

   La tabella che segue riassume le caratteristiche principali di un processo di modellazione delle minacce:

   **Caratteristica/ambito Descrizione**
   Ambito e vincoli La modellazione delle minacce può essere un processo che richiede tempo,
   soprattutto se si modella un’applicazione di scala enterprise. Avere chiari gli
   obiettivi, aiuta a focalizzare l'attività di modellazione delle minacce. L’obiettivo del
   modello dovrebbe essere ben definito fin dall'inizio. Nel caso di sistemi più grandi,
   il processo può dare in modo più rapido maggior valore, riuscendo a limitare il
   campo di azione solo ad aree specifiche.
   Nella fase iniziale del processo di Threat Modelling, quando l’ambito e i vincoli
   sono ben definiti, informazioni aggiuntive come scenari d'uso, dipendenze e note
   di sicurezza forniscono supporto a una migliore comprensione del sistema stesso.
   Scenari d’uso Viene creato un elenco di possibili scenari di utilizzo o di trascorsi che dimostrano
   l'uso previsto dell'applicazione. Ciò può aiutare nell'identificazione di potenziali


   Linee Guida per la modellazione delle minacce ed individuazione delle azioni di mitigazione conformi ai principi del Secure/Privacy

   aree di abuso presenti nel sistema.
   Dipendenze
   esterne/interne

   Le applicazioni software spesso dipendono da altri sistemi o componenti. Questi
   possono avere un impatto diretto sulla sicurezza del sistema in oggetto. È
   importante elencare tali dipendenze e individuare l'impatto che questi possono
   avere sul sistema stesso. Alcuni esempi posso essere l’utilizzo di: Antivirus,
   Firewalls, librerie di terze parti e sistemi di autenticazione.
   Note di sicurezza Vengono registrati dettagli come le informazioni già conosciute relative agli
   aspetti di sicurezza di un sistema, eventuali ipotesi fatte sull'applicazione, o trade-
   off a livello di disegno. Queste note di sicurezza possono aiutare il processo
   decisionale.
   Asset Vengono elencati gli asset che potrebbero essere di interesse per un potenziale
   avversario. Questi possono essere di tipo fisico o logico. Potenziali esempi di asset
   sono: le credenziali di accesso, i dettagli di una carta di credito, le chiavi di
   crittografia o i dettagli dell’utente.
   Punti di
   Ingresso/Uscita

   I punti di ingresso/uscita sono quei punti del sistema dove i dati entrano o escono.
   Questi vengono talvolta indicati come “punti di attacco” poiché soggetti ad uno o
   più potenziali attacchi. Ciascuno di questi, corrisponde ad una parte del sistema
   per la quale dovrebbero essere implementate opportune misure di sicurezza.
   Livelli di Fiducia o di
   Trust

Un livello di trust viene utilizzato per definire i privilegi che
un'entità esterna deve avere per accedere al sistema. Questi possono
essere classificati in base ai privilegi assegnati o alle credenziali
fornite e fanno riferimento a punti di ingresso/uscita di risorse
protette. Possibili esempi sono l'utente anonimo del sistema, l'utente
autenticato del sistema e l'amministratore. I livelli di trust vengono
applicati ad ogni punto di entrata/uscita.

::

   ### 4.2 MODELLAZIONE E INDIVIDUAZIONE DELLE MINACCE: THREAT MODELLING

   I processi di sviluppo sicuro del software, analizzati nel capitolo precedente, prevedono la modellazione
   delle minacce e suggeriscono l'inclusione dell’attività di modellazione delle minacce nella metodologia, al
   fine di migliorare la pratica dell’identificazione delle vulnerabilità in materia di sicurezza del Software.

   #### 4.2.1 Introduzione e concetti base

   Nella sua forma più elementare la modellazione delle minacce è un approccio strutturato che identifica
   potenziali minacce alla sicurezza, valutandone il rischio e fornendo le necessarie contromisure.

   La modellazione delle minacce comporta l'identificazione degli asset in un processo strutturato,
   individuando le potenziali minacce su cui insistono, categorizzandole e determinando le opportune
   strategie di mitigazione.

   Quando si approccia con la modellizzazione delle minacce, è importante avere una corretta comprensione
   della terminologia di base:

   - **Asset** , è qualcosa di valore su cui un avversario pone particolare interesse. I dati presenti in un
       database sono un esempio di Asset.
   - **Minaccia** (threat), è un evento che può o non essere dannoso all’origine ma che può danneggiare o
       compromettere un'attività a seguito di un attacco.
   - **Vulnerabilità** , è un difetto nella sicurezza di una o più parti di un sistema che rende possibile una
       minaccia.
   - **Attacco** , è un tentativo da parte di un avversario di sfruttare una vulnerabilità.
   - **Rischio** , è la probabilità di essere bersaglio di un attacco.
   - **Contromisura** , è un'azione o uno strumento che contrasta una minaccia e mitiga il rischio.


   Linee Guida per la modellazione delle minacce ed individuazione delle azioni di mitigazione conformi ai principi del Secure/Privacy

   La modellazione delle minacce può essere definita come la "revisione sistematica delle caratteristiche e
   dell'architettura dell’applicazione da un punto di vista della sicurezza”. Il processo fornisce un approccio
   strutturato per identificare e classificare le minacce basate sui componenti del software, sui flussi di dati e
   sui confini di fiducia (confini entro i quali esistono dei criteri di sicurezza).

   La modellazione delle minacce è una parte importante del ciclo di vita del software che identifica le
   minacce che potrebbero non essere riconosciute nelle tradizionali sessioni di brainstorming sulla sicurezza.

   A differenza delle tecniche di test del software come il penetration testing o fuzzing, la modellazione delle
   minacce può essere eseguita durante la fase di progettazione del sistema rendendola indipendente dallo
   sviluppo del codice. Introdotto nel ciclo di vita dello sviluppo del software, il Threat Modelling può
   contribuire a garantire la sicurezza già nella fase di progettazione e disegno di un'applicazione, riducendo i
   costi e minimizzando le necessarie successive correzioni di sicurezza nel progetto. Anche i sistemi in essere
   possono beneficiare di tale processo. Possono essere identificati nel sistema i problemi di sicurezza
   sconosciuti o non risolti e può essere applicata una classificazione del rischio alle vulnerabilità individuate. Il
   processo può anche essere adattato alle pratiche di sviluppo quali Agile.

   #### 4.2.2 Motivazioni nell’uso del Threat Model

   ##### 4.2.2.1 Ricerca preventiva dei bug di sicurezza

   Si pensi alla costruzione di una casa; le decisioni prese all’inizio del progetto impatteranno drasticamente
   sulla sicurezza del prodotto finale. La scelta di pareti in legno e un consistente numero di finestre al piano
   terra, espongono la casa a maggiori rischi rispetto ad una costruzione fatta in mattoni e con poche finestre.
   A seconda di dove si sta costruendo e di altri fattori, potrebbe anche essere una scelta ragionevole.
   Comunque, una volta effettuata la scelta, possibili futuri cambiamenti avrebbero sicuramente un impatto
   significativo sui costi. Certo, si possono sempre mettere delle inferiate sulle finestre, ma non sarebbe
   meglio concepire una soluzione più efficace e appropriata sin dall'inizio? È possibile applicare gli stessi tipi
   di compromessi alla tecnologia. La modellazione delle minacce aiuta a trovare problematiche di
   progettazione anche prima della stesura del codice e questa fase risulta essere il momento migliore per
   scoprire tali problemi.

   ##### 4.2.2.2 Comprensione dei requisiti di sicurezza .................................................................................................................

   Individuare le minacce e decidere come si intende procedere, rende chiari i requisiti. Con i requisiti più
   chiari, è possibile dedicare maggior energia ad un insieme consistente di funzionalità e proprietà di
   sicurezza. Esiste un'importante interazione tra requisiti, minacce e mitigazioni. Durante la fase di
   modellazione delle minacce, è possibile scoprire ad esempio, che alcune minacce non sono conformi ai
   requisiti aziendali e come tali potrebbero non essere prese in considerazione. Altresì i requisiti di sicurezza
   potrebbero dover tener conto di ulteriori minacce la cui risoluzione potrebbe però, essere troppo
   complessa e dispendiosa, pertanto, si dovrà scegliere tra l'indirizzare parzialmente tali minacce o accettarle
   comunicando che non è possibile affrontarle.

   ##### 4.2.2.3 Ingegnerizzazione e rilascio di prodotti più sicuri ...................................................................................................

   Considerando i requisiti e la progettazione effettuati all'inizio del processo, è possibile ridurre
   drasticamente le probabilità di dover ri-progettare o ricostruire il sistema, o manutenere un flusso costante
   di bug di sicurezza. L’effort risparmiato in tal senso potrebbe andare a favore di un processo di costruzione
   di un prodotto migliore, più veloce, più economico o più sicuro, lasciando spazio ad una maggiore
   concentrazione nella fase realizzativa dei requisiti funzionali.


   Linee Guida per la modellazione delle minacce ed individuazione delle azioni di mitigazione conformi ai principi del Secure/Privacy

   #### 4.2.3 Processo di modellazione del sistema da proteggere

   Il processo di modellazione delle minacce s’identifica in un insieme di passi che realizzano dei sotto-
   obiettivi, piuttosto che come una singola attività. Essenzialmente, le domande da porsi al fine di identificare
   i sotto-obiettivi, sono:

   - Cosa si sta realizzando?
   - Cosa potrebbe andare storto una volta realizzato?
   - Cosa è necessario fare per contrastare eventuali problemi?
   - È stato svolto un lavoro di analisi accettabile?

   Queste domane indirizzano puntualmente i quattro step del processo illustrato graficamente nella figura
   che segue e che possono essere così riassunti:

   - Modellare il sistema che si sta costruendo, rilasciando o modificando.
   - Identificare le minacce usando il modello e gli approcci descritti nel Paragrafo 5.2.4.
   - Indirizzare le minacce utilizzando gli approcci descritti nel Paragrafo 5.3.
   - Convalidare il lavoro per completezza ed efficacia sulla base delle best practices riportate nel
       Paragrafo 5.2.4.6.

   Il framework si concretizza come una modalità strutturata per modellare le minacce.

   ##### 4.2.3.1 Diagrammi DFD .......................................................................................................................................................

   I diagrammi sono un buon metodo per rappresentare ciò che si sta realizzando. Questi sono il modo più
   efficace per pensare a ciò che si sta costruendo. Ci sono diversi modi per diagrammare il software, e si può
   iniziare con un diagramma disegnato su una lavagna che rappresenta i flussi di dati e come questi
   attraversano il sistema.

   La modellazione delle minacce si concentra sui dati, su come questi vengono fruiti (flussi) e su come si
   muovono tra i vari componenti del sistema. I diagrammi di modellazione forniscono una rappresentazione
   visiva del modo in cui i singoli sottosistemi operano e lavorano insieme. I diagrammi di flusso di dati (DFD)

Modellazione del sistema

::

Individuazione delle minacce

::

Indirizzamento delle minacce

::

Validazione

::

   ## Figura 4 - Simbolismo nel Threat Modelling Figura 3 - I quattro step del Framework


   Linee Guida per la modellazione delle minacce ed individuazione delle azioni di mitigazione conformi ai principi del Secure/Privacy

   vengono normalmente utilizzati in molti processi di modellazione delle minacce. Questi forniscono un
   modo coerente e compatto per modellare i flussi di dati presenti in un'applicazione attraverso l'utilizzo di
   sei forme distinte che rappresentano: il processo, i processi multipli, l’entità esterna, l’archivio dati, il flusso
   di dati e il perimetro privilegiato (Figura sottostante).

Figura 4 - Simbolismo nel Threat Modelling

::

   I Trust boundaries (confini di fiducia) vengono identificati da una linea tratteggiata rossa, i Process
   Boundary (confini di processo) vengono invece identificati da una linea tratteggiata marrone, i Machine
   Boundary (confini della macchina) vengono identificati da una linea tratteggiata blu mentre gli altri confini
   vengono identificati da una linea tratteggiata verde.

   L'utilizzo del colore consente ai team di riconoscere facilmente durante la valutazione del DFD del sistema
   quale tipo di confine il flusso di dati attraversa. Qui alcuni esempi di elementi che costituisco il DFD:

   - Processo o Processi multipli
       o File di libreria dinamica
       o File eseguibile
       o Componente SW/FW
       o Web Service
       o Assemblies
       o Etc.
   - Interazione o Entità esterna
       o Persona
       o Altro sistema
       o Sito web
       o Etc.
   - Archivio dati
       o Database
       o File
       o Registro
       o Memoria condivisa
       o Code e Stack
       o Etc.
   - Flusso dati
       o Chiamata a funzione


   Linee Guida per la modellazione delle minacce ed individuazione delle azioni di mitigazione conformi ai principi del Secure/Privacy

o Traffico di rete o Etc.

::

   - Trust boundaries
       o Perimetro del processo
       o File system
       o Etc.

   Segue una tabella riepilogativa in cui, per ciascun elemento DFD viene riportato l’aspetto che assume nel
   diagramma, il significato ed alcuni brevi esempi:

ELEMENTO DFD ASPETTO SIGNIFICATO ESEMPIO

::

   **Processo** Rettangolo arrotondato ,
   cerchio o cerchio
   concentrico

Qualunque codice in esecuzione

::

Codice scritto in C, C#, Python o PHP, etc.

::

   **Flusso dati** Freccia Comunicazione tra
   processi o tra processi e
   archivi di dati

Connessioni di rete, HTTP, RPC, LPC, etc.

::

   **Archivio dati** Due linee parallele con
   etichetta nel mezzo

Supporti di memorizzazione dati

::

File, database, registro di Windows, segmenti di memoria condivisi.

::

   **Entità esterna** Rettangolo con angoli
   retti

Persone o codice al di fuori del nostro controllo

::

Un utente, un sito web esterno. Tabella 4 - Caratteristiche degli
elementi DFD

::

   L’impiego di diverse tipologie di diagramma concepiti come diversi blocchi di costruzione aiutano a
   modellare ciò che si sta realizzando.

   Nell’esempio che segue, viene rappresentato un modello di una semplice applicazione web che implementa
   una su logica di business che interagisce con un browser web, con un server web e con un database (vedi
   figura a seguire).

   Un modo semplice per migliorare il diagramma consiste nel delineare i confini per dare evidenza di “chi
   controlla cosa”. Si può facilmente comprendere che le minacce che attraversano questi confini sono
   probabilmente le più importanti e possono essere un buon punto di partenza nel processo di
   identificazione. Questi confini prendono il nome di “trust boundaries” (confini di fiducia) e dovrebbero
   essere sicuramente disegnati ovunque esiste un controllo da parte di persone. Alcuni esempi significativi:

Figura 5 - Diagramma del sistema

::


   Linee Guida per la modellazione delle minacce ed individuazione delle azioni di mitigazione conformi ai principi del Secure/Privacy

   - Account (User ID sui sistemi Unix o i Security Identifiers su sistemi Microsoft Windows);
   - Interfacce di rete;
   - Macchine fisiche;
   - Macchine virtuali;
   - Perimetri organizzativi;
   - Ovunque possa essere messa in discussione la diversificazione dei privilegi.

   Nel diagramma riportato nella Figura che segue, si aggiungono i “trust boundaries” (rappresentati da
   rettangoli tratteggiati) e la descrizione di ciò che il perimetro contiene:

   Quando il diagramma diventa più grande e più complesso, può essere molto utile numerare ogni processo,
   flusso dati e archivio dati presenti nel diagramma, come mostra la figura che segue (Ciascun “trust
   boundary” dovrebbe avere un identificativo univoco in rappresentanza del suo contenuto):

   Si deve pensare al diagramma del modello come parte integrante del processo di sviluppo, quindi deve
   essere messo sotto il controllo di versionamento così come tutto il resto del materiale relativo al progetto.
   A partire da questo modello, si procede con l’individuazione delle minacce sulla base delle metodologie e
   delle tecniche descritte nel paragrafo successivo.

Figura 6 - Aggiunta dei “Trust boundaries” al diagramma

::

   ## Figura 8 - Esempio di disegno architetturale di una applicazione Figura 7 - Numerazione degli elementi del diagramma


   Linee Guida per la modellazione delle minacce ed individuazione delle azioni di mitigazione conformi ai principi del Secure/Privacy

   #### 4.2.4 Tecniche di modellazione e individuazione delle minacce

   L'obiettivo che tutte le metodologie di modellazione delle minacce condividono è lo sviluppo di un processo
   di passi iterativi che un team può facilmente seguire durante la valutazione di un sistema software.

   ##### 4.2.4.1 Microsoft SDL – STRIDE ..........................................................................................................................................

   La STRIDE è un processo metodologico che aiuta ad individuare le minacce di sicurezza in un sistema
   complesso. L’elemento mnemonico STRIDE è acronimo di Spoofing, Tampering, Repudiation, Information
   disclosure, Denial of service e Elevation of privilege.

   Si riporta a seguire la descrizione delle classi di minacce previste:

   - **Spoofing** (falsificazione di identità): è la pretesa di essere qualcos’altro o qualcun altro che non si è.
       Classifica l’insieme delle minacce che permettono ad un attaccante di interagire con il sistema
       utilizzando un’altra identità. Per esempio, un server di phising che pretende di essere il server della
       nostra banca.
   - **Tampering** (alterazione dei dati): è l’alterazione di qualcosa che si presuppone non sia oggetto di
       modifica. Ciò può includere pacchetti di rete (sia fissa che mobile), dati persistiti su supporto di
       massa o in memoria nonché il codice applicativo. Classifica l’insieme delle minacce che permettono
       di modificare in modo fraudolento, dati e codice delle applicazioni. Per esempio, un attaccante
       sfruttando un bug software riesce a cambiare il codice di un’applicazione per aprire una back-door
       nel sistema.
   - **Repudiation** (ripudio di una azione): significa dichiarare di non aver fatto qualcosa
       (indipendentemente dal fatto che sia stato fatto o meno). Classifica l’insieme delle minacce che
       permettono ad un attaccante di negare di aver compiuto un’azione sul sistema. Per esempio, un
       utente compie un’azione illegale sul sistema e il sistema non è in grado di rilevare l'azione o
       identificare l’utente.
   - **Information Disclosure** (divulgazione di informazioni): riguarda l’esposizione delle informazioni a
       persone non autorizzate alla loro visione. Classifica l’insieme delle minacce che provocano
       l’esposizione di informazioni ad utenti/individui a cui non è consentito l’accesso in lettura/scrittura.
       Per esempio, un utente legge un file per il quale non ha ricevuto i diritti di lettura oppure un
       attaccante legge i dati in transito sulla rete.
   - **Denial of Service** (diniego di servizio): sono attacchi designati all’interruzione del servizio da parte
       dei sistemi. Questi includono come effetto il crashing, il rallentamento che porta alla non usabilità
       del sistema e il riempimento degli storage. Classifica l’insieme delle minacce che permettono di
       negare o degradare la fornitura di un servizio. Per esempio, un attaccante invia molti pacchetti al
       fine di intasare la banda di rete di un server il quale non potrà a sua volta essere contattato e/o
       fornire i suoi servizi agli utenti.
   - **Elevation of Privilege** (elevazione dei privilegi): avviene quando un programma o un utente è
       tecnicamente abilitato a fare cose che si presuppone non debba fare. Classifica l’insieme delle
       minacce che permettono ad un utente di ottenere privilegi non previsti per il suo ruolo. Per
       esempio, un utente anonimo sfrutta un bug software per ottenere i privilegi di amministratore.

   Partendo dal diagramma (Figura 7):

   - Come si fa a sapere se il browser web verrà utilizzato solo dalle persone che ci si aspetta?
   - Cosa accade se qualcuno altera i dati presenti nel database?
   - È corretto far transitare i dati da una componente all’atra del sistema senza che questi vengano
       cifrati?

   Questi sono esattamente e rispettivamente esempi di spoofing, tampering e information disclosure che
   possono essere facilmente individuati con l’ausilio della STRIDE. Con una scarsa conoscenza della sicurezza,


   Linee Guida per la modellazione delle minacce ed individuazione delle azioni di mitigazione conformi ai principi del Secure/Privacy

   ma con l’impiego delle giuste tecniche, è possibile trovare le minacce più importanti in modo veloce e con
   maggiore affidabilità. Se si sta impiegando un processo di modellizzazione delle minacce, la
   documentazione prodotta da tale processo, può aumentare il livello di fiducia nel realizzare un software più
   sicuro.

   Per ciascuna minaccia vengono evidenziati gli elementi del diagramma su cui impattano (normalmente si ha
   maggiore impatto sul software, sui flussi dati o gli storage piuttosto che sui trust boundary).

   La lista che segue fornisce alcuni esempi di minacce per ciascuna categoria (l’elenco non vuole essere
   esaustivo):

   ###### SPOOFING

Qualcuno potrebbe fingere di essere un altro utente del nostro sistema,
quindi serve un modo per autenticare tutti gli utenti.

::

Qualcuno potrebbe fingere di essere il nostro sito web, quindi è
necessario assicurarsi di avere un certificato SSL e di utilizzare un
singolo dominio per tutte le nostre pagine (per aiutare quel
sottoinsieme di utenti che leggono gli URL per vedere se sono nel posto
giusto).

::

Qualcuno potrebbe mettere un collegamento nascosto in una delle nostre
pagine, ad esempio logout.html o placeorder.aspx. Dobbiamo controllare
il campo HTTP “Referer” prima di intraprendere qualsiasi azione. Non è
una soluzione definitiva per contrastare il CSRF (Cross Site Request
Forgery), ma è un inizio.

::

   ###### TAMPERING

Qualcuno potrebbe manomettere i dati del back-end.

::

Qualcuno potrebbe manomettere i dati in transito tra il data center e il
consumer.

::

Chi sviluppa potrebbe rilasciare il codice del front-end
dell'applicazione senza verificarlo, pensando che sia in fase di
caricamento nell'area di staging. Ciò consentirebbe ad uno sviluppatore
malintenzionato di aggiungere codice malevolo.

::

   ###### REPUDIATION

Le azioni precedenti potrebbero richiedere una attenta analisi per
comprendere ciò che è accaduto. E' necessario porsi delle domande quali:
Esistono i log di sistema? Nel log di sistema vengono registrate le
giuste informazioni? Il log di sistema è protetto dal tampering?

::

   ###### INFORMATION

   ###### DISCLOSURE

Cosa accade se qualcuno legge i dati presenti nel database? E' possibile
che qualcuno possa connettersi al database per leggere o scrivere
informazioni?

::

   ###### DENIAL OF SERVICE

Cosa accade se migliaia di utenti si connettono contemporaneamente alla
nostra applicazione? E se il sistema va giù?

::

   ###### ELEVATION OF

   ###### PRIVILEGE

Magari il front-end è l'unico punto di accesso al nostro sito da parte
degli utenti, ma cosa lo impone? Cosa previene l'accesso diretto da
parte degli utenti alla logica di business in esecuzione sul server o al
caricamento di un nuovo codice? Se è presente un firewall, questo è
stato correttamente configurato? Chi controlla l'accesso al database, o
cosa accade se un impiegato commette un

::


   Linee Guida per la modellazione delle minacce ed individuazione delle azioni di mitigazione conformi ai principi del Secure/Privacy

errore o premeditatamente modifica i file a livello di configurazione?

::

   Microsoft ha inizialmente previsto l’applicabilità della STRIDE solo per i punti di ingresso/uscita del sistema
   in analisi. Tale approccio è stato poi affinato applicando la STRIDE a tutti gli elementi DFD del modello.

   Segue una tabella che indica l’esposizione in termini di vulnerabilità secondo la STRIDE rispetto agli
   elementi DFD utilizzati nel processo di modellazione:

Elemento DFD S T R I D E

::

   **Entità Esterna X X**

   **Flusso Dati X X X**

   **Archivio Dati X * X X**

   **Processo X X X X X X**

   X – possibile classe di minaccia per l’elemento indicato

   * – applicabile solo se l’archivio dati contiene dati di logging o di auditing

Tabella 5 - STRIDE per elemento DFD

::

   Le minacce STRIDE sono esattamente l'opposto di alcune delle proprietà che il nostro sistema dovrebbe
   avere, ovvero: autenticità, integrità, non ripudio, riservatezza, disponibilità e autorizzazione. La seguente
   tabella, mostra la correlazione tra la categoria di minacce STRIDE, la corrispettiva proprietà che si desidera
   mantenere, e gli elementi del sistema che sono tipicamente esposti alla classe di minacce indicata.

   ###### MINACCIA

   ###### PROPRIETA’ VIOLATA

(requisito o controllo di sicurezza)

::

   ###### TIPICA VITTIMA

Spoofing Autenticazione Processo Entità esterna

::

Persona

::

Tampering Integrità e Privacy (*) Processo Archivio dati Flusso dati

::

Repudiation Non ripudio (*) Processo

::

Information Disclosure Confidenzialità e Privacy (*) Processo

::

Archivio dati Flusso dati

::

Denial of Service Disponibilità e Privacy (*) Processo Archivio dati

::

Flusso dati

::

Elevation of Privilege Autorizzazione Processo

::


   Linee Guida per la modellazione delle minacce ed individuazione delle azioni di mitigazione conformi ai principi del Secure/Privacy

Tabella 6 - STRIDE proprietà violate

::

   (*) Articoli 25 e 32 del GDPR.

   Ad esempio, alcuni elementi quali un flusso di dati tra due componenti, un processo o un archivio di dati; in
   base alla classificazione STRIDE sono potenzialmente vulnerabili a manomissioni, divulgazione di
   informazioni e negazione del servizio. Il processo di modellazione delle minacce prende in considerazione
   ogni minaccia per elemento e valuta se esistono tecniche di mitigazione adeguate per quel tipo di minaccia.
   Analizzando ciascun elemento del sistema come identificato nei DFD, viene creato un profilo di minaccia
   dell'applicazione.

   4.2.4.1.1 Tecniche di mitigazione

   Ogni minaccia viene mitigata o accettata. Per i non esperti di sicurezza, la STRIDE fornisce per ogni tipo di
   potenziale minaccia identificata una o più classificazioni delle tecniche di mitigazione da mettere in campo
   (vedi tabella che segue).

Tipo Minaccia Tecnica di mitigazione o controlli di sicurezza

::

   **Spoofing Autenticazione**

   **Tampering Integrità**

   **Repudiation Servizi di non ripudio**

   **Information disclosure Confidenzialità**

   **Denial of Service Disponibilità**

   **Elevation of Privilege Autorizzazione**

Tabella 7 - Tecniche di mitigazione

::

   ###### AUTENTICAZIONE – TECNICHE DI MITIGAZIONE DELLO SPOOFING

   Le tecnologie per l'autenticazione di computer (o account di computer) includono quanto segue:

   - IPSec,
   - DNSSEC,
   - SSH host keys,
   - Kerberos authentication,
   - HTTP Digest o Basic authentication,
   - “Windows authentication” (NTLM),
   - Sistemi PKI, come SSL o TLS con certificati.

   Le tecnologie per l'autenticazione dei flussi a livello di bit (file, messaggi, ecc.) includono quanto segue:

   - Digital signatures,
   - Hashes.

   I metodi per l'autenticazione delle persone possono coinvolgere uno qualsiasi dei seguenti elementi:

   - Qualcosa che sai, come ad esempio una password,
   - Qualcosa che hai, come una card di accesso,
   - Qualcosa che sei, come ad esempio un dispositivo biometrico, comprese le fotografie,


   Linee Guida per la modellazione delle minacce ed individuazione delle azioni di mitigazione conformi ai principi del Secure/Privacy

   - Qualcuno che conosci e che può autenticarti.

   Le tecnologie per mantenere l'autenticazione tra le connessioni includono quanto segue:

   - Cookies.

   ###### INTEGRITA’ – TECNICHE DI MITIGAZIONE DEL TAMPERING

   Le tecnologie per la protezione degli asset includono:

   - ACLs o permissions,
   - Digital signatures,
   - Hashes,
   - Windows Mandatory Integrity Control (MIC) feature,
   - Unix immutable bits.

   Le tecnologie per la protezione del traffico di rete:

   - SSL,
   - SSH,
   - IPSec,
   - Digital signatures.

   ###### NON RIPUDIO – TECNICHE DI MITIGAZIONE DELLA REPUDIATION

   Le tecnologie che è possibile utilizzare per affrontare il problema del ripudio includono:

   - Logging,
   - Log analysis tools,
   - Secured log storage,
   - Digital signatures,
   - Secure time stamps,
   - Trusted third parties,
   - Hash trees,
   - Strumenti per la prevenzione delle frodi.

   ###### CONFIDENZIALITA’ – TECNICHE DI MITIGAZIONE DELLA INFORMATION DISCLOSURE

   Le tecnologie per la riservatezza includono:

   - Protezione dei files:
       o ACLs/permissions,
       o Encryption,
       o Appropriata gestione delle keys.
   - Protezione dei dati di rete:
       o Encryption,
       o Appropriata gestione delle keys.
   - Protezione della comunicazione e delle headers di comunicazione:
       o Mix networks,
       o Onion routing,
       o Steganography.


   Linee Guida per la modellazione delle minacce ed individuazione delle azioni di mitigazione conformi ai principi del Secure/Privacy

   ###### DISPONIBILITA’ – TECNICHE DI MITIGAZIONE DEL DENIAL OF SERVICE

   Le tecnologie per la protezione degli asset includono:

   - ACLs,
   - Filters,
   - Quotas (rate limiting, thresholding, throttling),
   - High-availability design,
   - Extra bandwidth (rate limiting, throttling),
   - Cloud services.

   ###### AUTORIZZAZIONE – TECNICHE DI MITIGAZIONE DELL’ELEVATION OF PRIVILEGE

   Le tecnologie per migliorare l'autorizzazione includono:

   - ACLs,
   - Group or role membership,
   - Role based access control,
   - Claims-based access control,
   - Windows privileges (runas),
   - Unix sudo,
   - Chroot, AppArmor o altre unix sandboxes,
   - The “MOICE” Windows sandbox pattern,
   - Convalida degli input per uno scopo definito.

   _4.2.4.1.1.1 Indirizzamento dello Spoofing_

   La Tabella seguente elenca gli obiettivi di spoofing, le strategie di mitigazione per indirizzare lo spoofing e le
   tecniche per attuare tali mitigazioni:

   ###### OBIETTIVO DELLA

   ###### MINACCIA

   ###### STRATEGIA DI MITIGAZIONE TECNICA DI MITIGAZIONE

   **Spoofing di una persona** Identificazione e
   autenticazione (username e
   qualcosa che
   conosci/hai/sei)

Username, nomi reali, identificativi:

::

   - Password;
   - Token;
   - Biometria.
   Registrazione/Manutenzione/Scadenza.

   **Spoofing di un file su disco** Sfruttare il Sistema
   Operativo

   - Percorsi assoluti;
   - Controllo ACL;
   - Assicurarsi che le pipes vengano
       create correttamente.
   Autenticatori crittografici Firme digitali o autenticatori.

   **Spoofing di un indirizzo di
   rete**

   Crittografia (^) • DNSSEC;

   - HTTPS/SSL;
   - IPsec.
   **Spoofing di un programma
   in memoria**

Sfruttare il Sistema Operativo

::

Molti sistemi operativi moderni hanno una qualche forma attuabile di
identificazione dell'applicazione.

::


   Linee Guida per la modellazione delle minacce ed individuazione delle azioni di mitigazione conformi ai principi del Secure/Privacy

Tabella 8 - STRIDE: Indirizzamento dello Spoofing

::

   **Spoofing di una persona**. Per evitare lo spoofing di una persona, è necessario che sia stato implementato
   un meccanismo di autenticazione e che a questa persona sia stato associato un nome utente univoco.

   **Spoofing di un file su disco**. Quando si accede ad un file presente sul disco, non bisogna aprirlo utilizzando
   un percorso relativo come _open(file)_. Utilizzare il percorso assoluto _open(/percorso/assoluto/del/file)_. Se il
   file contiene dati sensibili, dopo averlo aperto, è necessario attuare un controllo di sicurezza sugli elementi
   del descrittore del file stesso (come il fully resolved name, i permessi e l’owner). Si potrebbe anche voler
   controllare il descrittore del file per evitare eventuali _race conditions._ Ciò vale doppiamente quando il file è
   un eseguibile, ma il controllo dopo l'apertura potrebbe essere complicato. Ciò, può aiutare a garantire che
   le autorizzazioni sull'eseguibile non possano essere modificate da parte di un utente malintenzionato. In
   ogni caso, è quasi sempre sconsigliabile invocare _exec()_ con il parametro file specificato in modo relativo
   _./file_.

   **Spoofing di un indirizzo di rete.** Nel caso di spoofing di un indirizzo di rete, è consigliabile l’impiego di
   protocolli come DNSSEC, SSL, IPsec o una combinazione di questi per assicurarsi di colloquiare con la
   controparte attesa.

   **Spoofing di un programma in memoria.** Si tratta di programmi che si nascondono mostrandosi come
   programmi legittimi ma con l’intento di fare danni o trafugare informazioni. Questi sono un tipo di Trojan, i
   quali duplicano le azioni di processi esistenti che vengono poi eseguite inconsapevolmente dall'utente. E’
   necessario tenere sempre aggiornato il software come il sistema operativo e il browser web. Mantenere la
   connessione a Internet il più sicura possibile, tenendo sempre attivo un firewall. Sia i firewall hardware che
   software sono eccellenti strumenti per controllare il traffico Internet dannoso. E’ opportuno installare
   inoltre un software antivirus o un Trojan remover.

   _4.2.4.1.1.2 Indirizzamento del Tampering_

   La Tabella seguente mostra in elenco gli obiettivi di tampering, le strategie di mitigazione per indirizzare il
   tampering e le tecniche per attuare tali mitigazioni.

OBIETTIVO DELLA MINACCIA

::

   ###### STRATEGIA DI MITIGAZIONE TECNICA DI MITIGAZIONE

   **Tampering di un file** Sfruttare il Sistema
   Operativo

ACLs.

::

Crittografia • Firme digitali;

::

   - Keyed MAC.
   **Concorrenza nella
   creazione di un file
   (tampering del file system)**

Utilizzo di una directory protetta da manipolazione arbitraria di un
utente

::

   - ACLs;
   - Utilizzo di strutture private di
       directory;
   - La randomizzare dei nomi dei file
       contrasta l’esecuzione di possibili
       attacchi.
   **Tampering dei pacchetti di
   rete**

   Crittografia (^) • HTTPS/SSL;

   - IPsec.
   Anti-pattern Isolamento della rete.
   **_Tabella 9 - STRIDE: Indirizzamento del Tampering_**

   **Tampering di un file.** Se un attaccante possiede un account su una macchina, questo può facilmente
   portare un attacco di tampering su di un file che risiede sulla stessa macchina, oppure quando questo
   transita sulla rete per essere ricevuto.


   Linee Guida per la modellazione delle minacce ed individuazione delle azioni di mitigazione conformi ai principi del Secure/Privacy

   **Tampering della memoria.** Ciò avviene quando un processo con privilegi minimi di trust o non, altera in
   qualche modo la memoria fisica della macchina. Per esempio, se si stanno prendendo dati da un segmento
   di memoria condivisa, esistono delle ACL tali da consentirne agli altri processi la sola lettura? Per le
   applicazioni web che acquisiscono dati tramite AJAX, assicurarsi di validare tali dati prima di darli in pasto
   alla logica di business.

   **Tampering del traffico di rete.** La prevenzione del traffico di rete richiede una gestione sia dello spoofing
   che del tampering. Diversamente, qualunque intenzionato ad alterare i dati in transito potrebbe
   semplicemente far finta di essere all’altra estremità, portando invece un attacco di tipo MITM (Man In The
   Midle). La soluzione più comune per contrastare questo problema è utilizzare il protocollo SSL o l’IPsec (IP
   Security) come infrastruttura di comunicazione. Entrambi, SSL e IPsec indirizzano le problematiche legate
   alla confidenzialità e all’alterazione di informazioni e possono anche aiutare ad indirizzare lo spoofing.

   **Tampering del traffico di rete attraverso l’anti-pattern.** L’ isolamento della rete non assicura la protezione
   dalle minacce di tampering poiché generalmente non si riesce a mantenere la rete costantemente isolata.

   _4.2.4.1.1.3 Indirizzamento della repudiation_

   Indirizzare la repudiation in genere significa garantire che il sistema venga progettato prevedendo il
   tracciamento e la registrazione delle operazioni svolte (logging), garantendo inoltre che, tali registrazioni
   vengano protette e preservate. Alcuni di questi registri possono essere gestiti utilizzando un trasporto
   affidabile specifico. In questo senso, il syslog su UDP presenta forti lacune in termini di sicurezza; il syslog su
   TCP / SSL invece è notevolmente migliore.

   La Tabella seguente mostra in elenco gli obiettivi di repudiation, le strategie di mitigazione per indirizzare la
   repudiation e le tecniche per attuare tali mitigazioni:

OBIETTIVO DELLA MINACCIA

::

   ###### STRATEGIA DI MITIGAZIONE TECNICA DI MITIGAZIONE

   **Non utilizzare un
   meccanismo di log vuol
   dire non poter provare
   nulla.**

Log Assicurarsi di tracciare tutte le informazioni rilevanti dal punto
di vista della sicurezza.

::

   **Esposizione dei Logs a
   eventuali attacchi**

Proteggere i logs • syslog su TCP / SSL;

::

   - ACL.

   **Il Log come canale di
   attacco**

Informazioni dettagliate sul log

::

Documentare la progettazione del log sin dall'inizio del processo di
sviluppo. Tabella 10 - STRIDE: Indirizzamento della repudiation

::

   **Non avere un log significa non poter provare nulla.** Prevedere e mantenere i log, significa, poter
   investigare su quanto accaduto, al fine di acquisire un valido riscontro, nel momento in cui qualcuno nega
   di aver ottenuto o fatto qualcosa.

   **Esposizione del log a possibili attacchi.** Eventuali aggressori faranno del tutto per invalidare le informazioni
   contenute nel log, contrastando a volte l’operazione stessa di scrittura o forzando il “roll over” del registro,
   con il fine di rendere difficile l'individuazione dell'attacco. Questi inoltre, possono agire in modo tale da
   disattivare gli allarmi, facendo sì che, il vero attacco non venga alla luce.

   **Il log come canale di attacco.** Da progettazione, è possibile che vengono raccolti dati provenienti da
   sorgenti ‘malevoli’ fuori dal nostro controllo, fornendo poi gli stessi dati a persone o sistemi che hanno dei
   privilegi di sicurezza. Un esempio di questa tipologia di attacco potrebbe essere l’invio di una e-mail
   indirizzata a “</html> destinatario@dominio.com”, che causa problemi a quegli strumenti web-based che
   non prevedono l’HTML inline.


   Linee Guida per la modellazione delle minacce ed individuazione delle azioni di mitigazione conformi ai principi del Secure/Privacy

   È possibile rendere il tutto più semplice scrivendo codice sicuro nell’elaborazione dei dati di log, dando
   chiara evidenza di ciò che questi non possono contenere, ad esempio "I dati di log sono tutti in chiaro, ed
   eventuali aggressori potrebbero inserire ciò che vogliono" oppure "I campi da 1 a 5 del tracciato del log
   sono sotto stretto controllo da parte del nostro software, mentre i campi da 6 a 9 sono facilmente
   iniettabili. Il campo 1 è un campo time GMT. I campi 2 e 3 sono indirizzi IP (v4 o v6) ... ".

   _4.2.4.1.1.4 Indirizzamento dell’information disclosure_

   La Tabella seguente mostra in elenco gli obiettivi dell’information disclosure, le strategie di mitigazione per
   indirizzare l’information disclosure e le tecniche per attuare tali mitigazioni:

OBIETTIVO DELLA MINACCIA

::

   ###### STRATEGIA DI MITIGAZIONE TECNICA DI MITIGAZIONE

   **Monitoraggio della rete** Crittografia • HTTPS/SSL;

   - IPsec.
   **Directory o nomi di file (per
   esempio “lettere-di -
   licenziamento/” o
   “NomeCognome.docx”)**

Sfruttare il Sistema Operativo

::

ACLs.

::

   **Contenuti di un file** Sfruttare il Sistema
   Operativo

ACLs.

::

Crittografia Crittografia dei file come PGP, crittografia del disco
(FileVault, BitLocker).

::

   **API information disclosure** Progettazione Attento controllo nella progettazione,
   considerando il passaggio dei parametri
   per indirizzo o valore.
   **_Tabella 11 - STRIDE: Indirizzamento dell'Information disclosure_**

   **Monitoraggio della rete.** Il processo di monitoraggio della rete, si avvale dell'architettura adottata nel
   realizzare la maggior parte delle reti, per monitorarne il traffico (In particolare, la maggior parte delle reti
   attuali inviano i pacchetti sulla rete e ciascun listener presente su ogni end-point deve decidere se il
   pacchetto è per lui importante o meno). Quando le reti vengono progettate in modi diversi, esistono
   svariate tecniche per tracciare il traffico che va verso o attraversa la stazione di monitoraggio. Se non viene
   indirizzato lo spoofing, così come il tampering, un attaccante può mettersi nel mezzo attuando lo spoofing
   su ciascun end-point. La mitigazione dell’information disclosure sulla rete richiede la gestione delle minacce
   di spoofing e di tampering. Se non si indirizza il tampering, ci sono diversi modi intelligenti per ottenere
   informazioni. Quindi di nuovo, l’SSL e l’IPSec sono le migliori scelte da mettere in campo.

   **Nomi che rivelano informazioni.** Quando il nome di una directory o di un file di per se forniscono
   informazioni utili ad un possibile attaccante, il modo migliore per proteggersi è creare una directory padre
   con un nome innocuo e utilizzare le ACLs o i permessi del sistema operativo per proteggerle.

   **Contenuti sensibili nei file.** Quando il contenuto di un file necessita di protezione, utilizzare le ACLs o la
   crittografia. Nel caso in cui la macchina (computer) dovesse cadere in mani non autorizzate, è necessario
   preventivamente utilizzare la crittografia al fine di proteggere tutti i dati. Le modalità di protezione
   crittografica che prevedono l’inserimento di una chiave o parola chiave da parte di una persona, sono più
   sicure ma meno convenienti. Esistono tecniche crittografiche per i file, filesystem e database, dipende da
   ciò che si deve proteggere.

   **API (Interfaccia di programmazione di una applicazione).** Quando si progetta un'API, o diversamente si
   trasmettono informazioni oltre un confine di fiducia, è importante fare attenzione a quali informazioni si
   divulgano. È necessario partire dal presupposto che le informazioni fornite vengono passate ad altri, quindi


   Linee Guida per la modellazione delle minacce ed individuazione delle azioni di mitigazione conformi ai principi del Secure/Privacy

   bisogna essere molto cauti e selettivi su ciò che viene fornito. Situazioni di errore generate da un sito web
   che mostrano il nome utente e la password di un database sono un esempio comune di questo problema.

   _4.2.4.1.1.5 Indirizzamento del denial of service_

   La Tabella seguente mostra in elenco gli obiettivi del Denial Of Service, le strategie di mitigazione per
   indirizzare il Denial Of Service e le tecniche per attuare tali mitigazioni:

OBIETTIVO DELLA MINACCIA

::

   ###### STRATEGIA DI MITIGAZIONE TECNICA DI MITIGAZIONE

   **Saturazione della rete**

   **(Network flooding)**

   Verificare le risorse esauribili (^) • Risorse flessibili (Elastic
   resources);

   - Progettare pensando che il
       consumo di risorse da parte di un
       futuro utilizzatore
       malintenzionato possa essere alto
       o comunque superiore a quello
       presunto.
   ACLs di rete.

   **Risorse utilizzate da un
   programma**

Progettazione attenta e cautelativa

::

Gestione di risorse flessibili.

::

Evitare i moltiplicatori (fattori moltiplicativi)

::

Analizzare i punti in cui un eventuale attacco portato con uno sforzo
minimo, potrebbe produrre una moltiplicazione nel consumo di CPU.
Intervenire in modo tale da rendere più arduo il lavoro dell'attaccante
abilitandone l'identificazione, come i client che applicano la
crittografia o il login prima di procedere con il vero lavoro
(ovviamente ciò non vuol dire che gli accessi non debbano essere
crittografati).

::

   **Risorse di sistema** Sfruttare il Sistema
   Operativo

Usare le impostazioni del sistema operativo. Tabella 12 - STRIDE:
Indirizzamento del Denial of Service

::

   **Saturazione della rete.** Se si dispone di strutture statiche di connessioni, cosa accade se queste si saturano?
   L’utilizzo di firewall può fornire un livello di protezione basato su ACLs per controllare l’accettazione (o
   l’invio) di dati e possono essere utili per mitigare gli attacchi di negazione di servizio di rete.

   **Individuazione delle risorse esauribili.** Si possono identificare tre tipologie distinte di risorse esauribili: la
   prima è quella relativa alle risorse di rete; la seconda è quella relativa a quelle risorse direttamente gestite
   lato codice; la terza è quella relativa alle risorse gestite dal sistema operativo. In ogni caso, le risorse
   flessibili (elastic resources) risultano sempre essere una tecnica preziosa. Ad esempio, negli anni 90 alcuni
   stack TCP avevano un limite hardcoded di cinque connessioni TCP semiaperte (una connessione semiaperta
   è una connessione che viene aperta nel processo di avvio. Non bisogna preoccuparsi del fatto che ciò
   potrebbe non avere un senso, piuttosto bisognerebbe chiedersi il motivo per cui questo limite fu impostato
   a cinque). Oggi è spesso possibile ottenere risorse flessibili dai vari tipi di cloud provider.

   **Risorse di sistema.** I sistemi operativi tendono ad avere limiti o quote per controllare il consumo di risorse a
   livello di codice utente. Considerare le risorse gestite dal sistema operativo, come la memoria o l'utilizzo del
   disco. Se il nostro codice viene eseguito su server dedicati, può essere ragionevole consentirgli di utilizzare


   Linee Guida per la modellazione delle minacce ed individuazione delle azioni di mitigazione conformi ai principi del Secure/Privacy

   tutte le risorse di cui quel server dispone. Prestare attenzione a porre gli opportuni limiti al codice e
   assicurarsi di documentare ciò che si sta facendo.

   **Risorse del programma.** Acquisire consapevolezza circa le limitazioni che si potrebbero avere nella gestione
   delle risorse applicative. Ad esempio, un attaccante potrebbe portarci ad un dispendio di lavoro e risorse
   inviando un flusso dati che richiedono costose operazioni crittografiche che potrebbero esporci a
   vulnerabilità di “Denial Of service”.

   _4.2.4.1.1.6 Indirizzamento dell’elevation of privilege_

   La Tabella seguente mostra in elenco gli obiettivi dell’Elevation Of Privilege, le strategie di mitigazione per
   indirizzare l’Elevation Of Privilege e le tecniche per attuare tali mitigazioni.

OBIETTIVO DELLA MINACCIA

::

   ###### STRATEGIA DI MITIGAZIONE TECNICA DI MITIGAZIONE

   **Confusione tra dati/codice** Usa strumenti e architetture
   che separano dati dal codice.

   - Prepared Statement o Stored
       procedure per l’SQL;
   - Separatori chiari con forme canoniche;
   - Validare i dati prima di passarli al
       consumer.
   **Attacchi di corruzione del
   flusso di controllo e della
   memoria**

Utilizzare un linguaggio di programmazione sicuro

::

Utilizzare un linguaggio di programmazione sicura nella stesura del
codice ci protegge da intere classi di attacco.

::

Sfruttare il sistema operativo per la protezione della memoria.

::

I sistemi operativi di ultima generazione possiedono meccanismi
intrinsechi di protezione della memoria.

::

   Utilizzare il sandboxing (^) • I sistemi operativi moderni
   supportano il sandboxing in vari modi
   (AppArmor su Linux, AppContainer o il
   modello MOICE su Windows,
   Sandboxlib su Mac OS).

   - Non utilizzare per l’esecuzione
       l'account "nobody", crearne uno
       nuovo per ogni applicazione. Postfix e
       QMail sono buoni esempi del modello
       di un account per funzione.
   **Attacchi di command-
   injection**

Fare attenzione Validare l'input in termini di forma e dimensione
attesi. Non sanitizzare. Tracciare l'input nel log e scartarlo se non
viene riconosciuto. Tabella 13 - STRIDE: Indirizzamento dell'Elevation
of privilege

::

   **Confusione tra dati/codice.** Accade spesso che i dati vengono trattati come codice. Attacchi come gli XSS
   sfruttano l’unione tra codice HTML e dati (un file html che contiene sia codice, come Javascript, che dati,
   come il testo da visualizzare e talvolta anche istruzioni di formattazione per il testo stesso). Esistono alcune
   strategie per affrontare questo problema. Il primo consiste nell’adottare modalità/strumenti che aiutano a
   mantenere separati codice e dati (a d esempio, i prepared statement in SQL indicano al database quali
   dichiarazioni aspettarsi e dove saranno posizionati i dati). Un’altra strategia è validare i dati prima di
   passarli. Ad esempio, se si stanno inviando dati ad una pagina web, è necessario assicurarsi che questi non
   contengano caratteri come <, >, # o & e quant'altro.


   Linee Guida per la modellazione delle minacce ed individuazione delle azioni di mitigazione conformi ai principi del Secure/Privacy

   **Attacchi di corruzione del flusso di controllo e/o della memoria.** Questo insieme di attacchi generalmente
   sfrutta il “weak typing” e le strutture statiche presenti nei linguaggi simili al C per consentire ad un
   aggressore di introdurre del codice per poi eseguirlo. Se si utilizza un linguaggio sicuro, come Java o C#,
   molti di questi attacchi sono più difficili da portare. I sistemi operativi più moderni tendono a incorporare
   funzioni di protezione della memoria e di randomizzazione, come ad esempio l’Address Space Layout
   Randomization (ASLR). A volte queste funzioni sono opzionali e richiedono un compilatore o un linker
   switch. In molti casi, queste funzioni possono essere utilizzate gratuitamente e pertanto dovrebbero essere
   utilizzate. Ciò non è del tutto indolore, potrebbe essere necessario ricompilare, testare o fare altri piccoli
   interventi. L'ultima serie di controlli per contrastare la corruzione della memoria sono le sandbox. Le
   Sandbox sono funzioni del sistema operativo progettate per proteggere da un programma danneggiato il
   sistema operativo stesso e il resto dei programmi dell’utente in esecuzione su di esso.

   **Attacchi di command-injection.** Gli attacchi di command-injection (iniezione di comando) sfruttano i dati di
   input come vettore di attacco (un aggressore fornisce un carattere di controllo, seguito da una serie di
   comandi). Per esempio, nella SQL injection, un apice chiude spesso un'istruzione dinamica SQL e quando si
   tratta di script shell unix, la shell può interpretare un punto e virgola come la fine dell'input, prendendo
   come comando qualsiasi cosa viene dopo.

   ##### 4.2.4.2 Attack tree ..............................................................................................................................................................

   L’attack tree rappresenta un’ulteriore metodologia per raccogliere e documentare i potenziali attacchi in
   modo strutturato e gerarchico.

   Un attack tree è modellato attraverso una struttura ad albero i cui elementi base sono:

   - Il nodo radice che rappresenta _l'obiettivo finale_ dell’attaccante,
   - I nodi figli che rappresentano i _sotto-goals_ che concorrono al raggiungimento dell’ _obiettivo finale_ ,
   - Le foglie che rappresentano gli _attacchi_.

   La modellazione segue la seguente logica di base:

   - I “nodi OR” indicano le alternative, ossia modi indipendenti, per raggiungere un goal/sotto-goal.
   - I “nodi AND” indicano i passi che concorrono al raggiungimento dello stesso goal/sotto-goal.

   **PASSO 1 – Modellazione degli attacchi**

   Si modellano quindi, tanti attack tree quanti sono gli obiettivi di un attaccante. In questa fase l’analista
   deve identificare i possibili obiettivi di attacco e, per ciascuno di essi, i passi attraverso cui realizzarli (la
   capacità di identificazione degli obiettivi e dei passi è quindi assolutamente soggettiva).

   Si riporta di seguito, un esempio di modellazione di attack tree:


   Linee Guida per la modellazione delle minacce ed individuazione delle azioni di mitigazione conformi ai principi del Secure/Privacy

   Nell’esempio in figura:

   - Il nodo radice rappresenta l’obiettivo finale dell’attaccante che consiste nell’ “Ottenere le
       credenziali di autenticazione”,
   - L’ obiettivo finale può essere raggiunto in vari modi (“OR”):

1.1 - “Usare tecniche di social engineering”, 1.2 - “Usare tecniche di
sniffing di rete”,

::

1.3 - “Usare tecniche di brute force”, ecc.

::

   - Sulla base della modalità di Livello-1 scelta, saranno diversi gli elementi (nodi foglie) che
       concorreranno al raggiungimento dell’obiettivo radice. Ad esempio, nel caso si scelga il percorso
       1.2 - “Usare tecniche di sniffing di rete” l’obiettivo si raggiunge (sub-goal) attraverso 2 step correlati
       (“ AND”) :
          1.2.1 - “ARP spoof attack”;
          1.2.2 - “L’attaccante ottiene l’accesso alla LAN”.

   Lo stesso attack tree può anche essere rappresentato in forma testuale:

   _Obiettivo 1 - Ottenere le credenziali di autenticazione_

1.1 - Usare tecniche di social engineering OR …

::

1.2 - Usare tecniche di sniffing di rete OR 1.2.1 - ARP spoof attack AND
1.2.2 - L'attaccante ottiene l'accesso alla LAN

::

1.3 - Usare tecniche di brute force OR …

::

…

::

   **PASSO 2 – Analisi degli attributi di sicurezza**

   Dopo aver modellato i possibili attacchi al sistema, è necessario analizzare gli attributi di sicurezza del
   sistema quali, ad esempio:


   Linee Guida per la modellazione delle minacce ed individuazione delle azioni di mitigazione conformi ai principi del Secure/Privacy

   1. la possibilità o l’impossibilità dell’attacco (P=Possibile, I=Impossibile)
   2. il costo dell’attacco (valore in euro, es. 10K)
   3. gli strumenti necessari per realizzare l’attacco (AS=Attrezzature Specifiche, SAS=Senza Attrezzature
       Specifiche)

   Per determinare il costo di un attacco:

   1. si determina il valore per ciascun nodo foglia.
   2. si determina il valore dei nodi non foglia. Questo è ricavato a partire dal valore dei loro figli.

   L'analista dovrà avere la capacità di attribuire dei “buoni” valori per i nodi foglia (anche in questa fase la
   capacità di identificazione dei valori è assolutamente soggettiva).

   **PASSO 3 – Analisi dei risultati**

   L’analisi è volta a determinare:

   1. il costo dell'attacco più economico (si analizzano i valori degli attributi a livello del nodo radice);
   2. gli attacchi il cui costo non supera una certa soglia (si analizzano i sotto-alberi i cui nodi
       rappresentano una determinata proprietà/soglia);
   3. l'attacco più economico che non utilizza attrezzature speciali (si analizzano i sotto-alberi i cui nodi
       rappresentano un determinato insieme di proprietà).

   L’analisi dei risultati deve tenere conto delle caratteristiche del potenziale attaccante in quanto queste
   determinano quali parti dell’attack tree devono essere prese in considerazione. Attaccanti diversi hanno
   diversi livelli di abilità, accesso, avversione al rischio, soldi e così via. Se il potenziale attaccante è la
   criminalità organizzata, occorre considerare la possibilità di attacchi costosi e “mezzi illeciti” (corruzione,
   ricatto, ecc.) che espongono l’attaccante fino al rischio di andare in prigione. Se il potenziale attaccante è
   un terrorista, occorre considerare “mezzi illeciti” che espongono l’attaccante fino al rischio di morire per
   raggiungere l’obiettivo. Se l’attaccante è un casual hacker si esclude la possibilità di attacchi costosi e
   “mezzi illeciti” (corruzione, ricatto, ecc.).

   **PASSO 4 – Analisi What-if**

   L’analisi "what if" è costruita a partire dalle diverse ipotesi di adozione delle contromisure. Introducendo
   contromisure, cambiano i valori attribuiti nel secondo step della metodologia e quindi cambiano i risultati
   dell’analisi.

   In conclusione, una delle caratteristiche di valore degli attack tree è che sono riutilizzabili. Tornando
   all’esempio inziale, una volta completato l'albero di attacco relativo a “Ottenere le credenziali di
   autenticazione”, è possibile utilizzarlo in qualsiasi situazione in cui sia interesse dell’attaccante
   l’acquisizione delle credenziali di autenticazione. L’attack tree relativo a “Ottenere le credenziali di
   autenticazione” può inoltre diventare parte di un attack tree più grande.

   ##### 4.2.4.3 TRIKE .......................................................................................................................................................................

   TRIKE è un framework open-source per l'auditing della sicurezza da un punto di vista di risk management
   basato sulla generazione di modelli di minacce in modo affidabile e ripetibile. Il progetto ebbe inizio nel
   2005 come tentativo di migliorare l'efficienza e l'efficacia delle esistenti metodologie di modellazione delle
   minacce e da allora viene attivamente aggiornato e utilizzato. I creatori di TRIKE hanno anche sviluppato
   strumenti a supporto di questa metodologia come il foglio di calcolo TRIKE. Questo strumento si focalizza
   sull'automazione della generazione delle minacce e non prevede alcun brainstorming. I team di sicurezza
   non hanno la necessità di individuare le possibili minacce in quanto tali minacce sono già predefinite. TRIKE
   può essere utilizzato anche da uno sviluppatore di sicurezza inesperto per trovare le vulnerabilità di
   sicurezza in modo efficace ed affidabile. Il team TRIKE ha adottato l'analisi HAZOP (Hazardous Operations),


   Linee Guida per la modellazione delle minacce ed individuazione delle azioni di mitigazione conformi ai principi del Secure/Privacy

   ovvero, un metodo sistematico per identificare quali variazioni di processo devono essere mitigate. Questo
   framework può sostituire gli alberi di minaccia e d'attacco (attack tree).

   TRIKE utilizza un approccio basato sul rischio con distinte implementazioni dei modelli di minacce e rischi.
   Approccia al Threat Modeling assumendo una posizione difensiva rispetto a quella di un attaccante. TRIKE
   ha anche proposto il concatenamento delle minacce, un'alternativa agli alberi delle minacce, nel tentativo
   di ridurre la natura ripetitiva di quest’ultimi.

   ##### 4.2.4.4 P.A.S.T.A (Process for Attack Simulation and Threat Analysis) ...............................................................................

   Si tratta di un processo agnostico rispetto alla piattaforma, suddiviso in sette fasi distinte e applicabile alla
   maggior parte delle metodologie di sviluppo. Il suo obiettivo principale è quello di affrontare le minacce più
   gravi per un determinato obiettivo applicativo. Di seguito in elenco le fasi di cui sopra:

   - Definizione degli obiettivi di business;
   - Definizione dell'ambito tecnico;
   - Scomposizione del sistema;
   - Analisi delle minacce;
   - Rilevamento della vulnerabilità;
   - Enumerazione degli attacchi;
   - Analisi del rischio/impatto.

   Il processo è una combinazione di diversi approcci di modellizzazione delle minacce, definisce gli obiettivi di
   business, i requisiti di sicurezza e conformità e l'analisi dell'impatto sul business. Similmente al processo
   adottato da Microsoft, nella rappresentazione del sistema, l'applicazione viene ridotta in componenti
   discreti attraverso l’utilizzo di casi d' uso e DFD. Durante l'analisi delle minacce e delle vulnerabilità vengono
   utilizzati anche gli alberi delle minacce e i casi di abuso. Si calcola quindi l'impatto sul rischio e sul business
   e vengono individuate le necessarie contromisure.

   ##### 4.2.4.5 AS/NZS 31000:2009 Risk Management ..................................................................................................................

   L'AS/NZS 31000:2009^10 , pubblicato nel novembre 2009, è stato concepito sulla base dello standard
   australiano/Nuova Zelanda AS/NZS 4360:2004^11 , il primo standard formale al mondo per la
   documentazione e la gestione dei rischi che fornisce linee guida generiche sulla gestione del rischio.
   L' approccio standard è semplice, flessibile e iterativo. Questo non vincola le organizzazioni ad adottare una
   particolare metodologia di gestione del rischio, a condizione che la metodologia adottata soddisfi le cinque
   fasi del processo AS/NZS 4360, ovvero:

   - Stabilire il contesto: stabilire il dominio di rischio, definendo quali asset/sistemi sono importanti.
   - Identificare i rischi: nell'ambito del rischio, quali specifici rischi sono in evidenza?
   - Analisi dei rischi: esamina i rischi e determina se esistono controlli a supporto.
   - Valutazione del rischio: determina il rischio residuo.
   - Trattamento del rischio: descrive le modalità di trattamento dei rischi in modo da mitigare i rischi di
       business indicati.

   La gestione del rischio AS/NZS 31000:2009 può essere utilizzata per classificare i rischi ai fini dei controlli di
   sicurezza. Tuttavia, per quanto riguarda l'enumerazione delle minacce manca di metodi strutturati, e
   pertanto potrebbe essere ritenuto inadeguato.

   (^10) https://infostore.saiglobal.com/preview/as/as30000/31000/31000-2009.pdf?sku=1378670
   (^11) [http://www.fanarco.net/books/risk/AS-NZS_4360-2004_Risk_Management.pdf](http://www.fanarco.net/books/risk/AS-NZS_4360-2004_Risk_Management.pdf)


   Linee Guida per la modellazione delle minacce ed individuazione delle azioni di mitigazione conformi ai principi del Secure/Privacy

   ##### 4.2.4.6 Best practices di carattere generale .......................................................................................................................

   - VALIDARE E NON SANITIZZARE - Dobbiamo sapere cosa e quanto ci aspettiamo di ricevere e
       dobbiamo convalidare ciò che riceviamo. Se si riceve qualcos'altro rispetto al previsto, è necessario
       scartarlo restituendo un messaggio di errore. A meno che il nostro codice non sia perfetto,
       eventuali errori di sanitizzazione potrebbero produrre ancor più danno, in quanto, dopo aver scritto
       la funzione di sanitizzazione dell’input si farebbe affidamento su di essa.
   - AFFIDARSI AL SISTEMA OPERATIVO - Affidarsi al sistema operativo è una buona pratica per i
       seguenti motivi:
          o Il sistema operativo mette a disposizione funzionalità di sicurezza che consentono di
             concentrarsi sui propri obiettivi.
          o Il sistema operativo funziona con privilegi che probabilmente non sono disponibili per il
             programma o l'aggressore.
          o Se l'aggressore controlla il sistema operativo, è probabile che abbiamo problemi ben più
             gravi, indipendentemente da ciò che il codice tenta di fare.

Con tutti questi consigli sul fidarsi del sistema operativo, ci si
potrebbe chiedere “quale bisogno c'è di modellare le minacce? Perché non
affidarsi solo al sistema operativo?”. Ebbene, sta a noi verificare di
non impostare le autorizzazioni su un file a 777, o impostare gli ACL in
modo tale da consentire la scrittura agli account “guest”. Sta a noi
scrivere codice che funzioni bene con i permessi di un utente normale
piuttosto che con i permessi di un utente sandboxed.

::

   - FILE BUGS - È bene includere le minacce tra i bugs e contrassegnarle come bug di sicurezza. Bisogna
       inoltre dare una priorità a questi bugs. I bugs di tipo “Elevation-of-privilege” sono quasi sempre
       riconducibili alla categoria di più alta priorità poiché, quando vengono sfruttati causano molti
       danni. I bugs di tipo “Denial of service” spesso vanno considerati per ultimi.
   - VERIFICA DEL LAVORO SVOLTO - La convalida del modello è l'ultima cosa da fare come parte della
       modellazione delle minacce. Ci sono alcune attività da svolgere prima, ed è bene mantenerle
       allineate con l'ordine in cui è stato svolto il lavoro precedente. Pertanto, le attività di validazione
       includono il controllo del modello, la verifica di ciascuna minaccia e il controllo dei test.
       Probabilmente si desidera convalidare il modello anche una seconda volta, ovvero quando ci si
       avvicina al rilascio o all'installazione.
   - CONTROLLO DEL MODELLO - È necessario assicurarsi che il modello finale corrisponda a quello
       costruito. Se così non fosse, come potremmo sapere se le minacce trovate sono giuste e rilevanti?
       Per fare ciò, è opportuno organizzare degli incontri durante i quali tutti, osservando e analizzando il
       diagramma, rispondano alle seguenti domande:
          o il diagramma è completo?
          o il diagramma è accurato?
          o il diagramma copre tutti le decisioni intraprese in termini di sicurezza?
          o è possibile procedere con la versione successiva del diagramma senza apportare
             modifiche?

Una risposta affermativa a tutte le domande di cui sopra, indica che il
diagramma è sufficientemente aggiornato e maturo per poter procedere.
Diversamente sarà necessario apportare gli opportuni cambiamenti.

::

   - DETTAGLI DEL DIAGRAMMA - Non disegnare mai un diagramma ad occhio, con un livello di
       dettaglio tale da rappresentare l’intero comportamento del sistema. Utilizzare un sotto diagramma
       che mostri il solo dettaglio di una particolare area del sistema stesso. Si deve cercare di filtrare ciò
       che non ha senso per il progetto. Per esempio, se si è davanti ad un processo molto complesso,
       forse tutto ciò che è in quel processo dovrebbe essere trattato in un diagramma, e tutto ciò che è al
       di fuori di esso in un altro. Se si ha un dispatcher o un sistema di code, questi sono un buon punto
       di suddivisione, e lo sono anche i database o i sistemi di fail-over. Forse ci sono ancora alcuni


   Linee Guida per la modellazione delle minacce ed individuazione delle azioni di mitigazione conformi ai principi del Secure/Privacy

elementi che devono essere maggiormente dettagliati? Bene, questi vanno
filtrati. La cosa importante da ricordare è che il diagramma ha lo scopo
di aiutare a comprendere e discutere il sistema.

::

   ### 4.3 INDIRIZZAMENTO DELLE MINACCE

   Una volta raccolte le minacce individuate in una o più liste, il passo successivo nel processo di modellazione
   è quello di scorrere l’elenco o gli elenchi indirizzando ciascuna minaccia. Ci sono quattro tipologie di azioni
   che si possono intraprendere per contrastare tali minacce:

   - **Mitigazione** delle minacce - Si concretizza nel fare qualcosa per rendere più difficile la possibilità di
       poter essere sfruttate. Richiedere una password per controllare chi accede al sistema, mitiga la
       minaccia di spoofing. Aggiungere un controllo password che ne rafforza la complessità o la
       scadenza, riduce la probabilità che una password venga scoperta o venga utilizzata se rubata.
   - **Eliminazione** delle minacce - Avviene quasi sempre eliminandone le caratteristiche. Se si presenta
       una minaccia in cui qualcuno ha accesso ad una funzione amministrativa di un sito web entrando in
       “/admin/URL”, è possibile mitigarla impiegando delle password o altre tecniche di autenticazione,
       ma comunque, questa non verrà risolta. È possibile rendere più complessa la URL in modo da
       rendere meno probabile la possibilità che questa venga trovata, ma anche in questo caso la
       minaccia non verrà risolta. La si può eliminare rimuovendo l’interfaccia amministrativa, e gestendo
       l’attività di amministrazione tramite linea di comando. In questo caso esisterebbero comunque
       altre minacce associabili a come l’utente amministratore dovrebbe loggarsi per poter procedere
       con l’attività di amministrazione da linea di comando. Lo spostamento dell’interfaccia dall’http a
       linea di comando rende facile la mitigazione della minaccia controllando la superficie di attacco.
   - **Spostamento** delle minacce - Consiste nel lasciare che qualcuno o qualcos'altro gestisca il rischio.
       Per esempio, potremmo demandare la gestione delle minacce relative all’autenticazione al sistema
       operativo, oppure rinforzare il perimetro di fiducia con un firewall. È anche possibile trasferire il
       rischio direttamente all’utente utilizzatore, chiedendogli di navigare attraverso una moltitudine di
       finestre di dialogo incomprensibili prima che questo possa effettivamente utilizzare il sistema.
       Ovviamente questa non vuole essere assolutamente una tra le migliori soluzioni, ma in alcuni casi
       esiste da parte degli utilizzatori una conoscenza tale da poterli rendere partecipi per convenire ad
       un compromesso di sicurezza. Se si pensa che esistano i presupposti per una soluzione del genere,
       si dovrebbe aiutare chi usa il sistema a prendere una decisione in tal senso.
   - **Accettazione** della minaccia - È l’ultimo approccio per indirizzare le minacce. In alcuni casi, il costo
       nell’impedire a qualcuno di inserire una back-door nella scheda madre di un hardware aziendale
       potrebbe risultare elevato, quindi in questi casi si potrebbe scegliere di accettare il rischio. Una
       volta che questo viene accettato, non c’è più bisogno di preoccuparsene. A volte la preoccupazione
       indica che il rischio non è stato pienamente accettato o che l'accettazione del rischio non sia
       appropriata.

   ### 4.4 VALUTAZIONE DEL RISCHIO: TECNICHE DI RISK RANKING

   #### 4.4.1 DREAD

   Microsoft ha sviluppato la metodologia DREAD (tabella che segue) per valutare ciascun rischio individuato
   durante l'attività STRIDE. Ad ogni rischio viene assegnato un punteggio DREAD da parte del team di
   sicurezza/sviluppo i quali realizzano e applicano il modello delle minacce.

   Esistono diverse varianti del sistema di valutazione e prioritizzazione del rischio:

DREAD DESCRIZIONE

::

   **Damage potential** Classifica l'estensione del danno che si verifica se si sfrutta la vulnerabilità individuata.

   **Reproducibility** (^) Classifica quanto spesso un tentativo di sfruttamento della vulnerabilità individuata


   Linee Guida per la modellazione delle minacce ed individuazione delle azioni di mitigazione conformi ai principi del Secure/Privacy

funziona.

::

   **Exploitability** Assegna un valore numerico allo sforzo necessario per sfruttare la vulnerabilità
   individuata. Inoltre, la possibilità di sfruttamento considera come condizioni
   preliminari che l'utente deve essere autenticato.

   **Affected Users** Assegna un valore numerico che rappresenta la razione di istanze installate del
   sistema che potrebbero essere interessate se un exploit divenisse ampiamente
   disponibile.

   **Discoverability** Misura la probabilità che una vulnerabilità possa essere trovata da ricercatori esterni
   della sicurezza e/o dagli hacker, se questa non viene risolta tramite patch.
   **_Tabella 14 - Modello DREAD_**

   Nella valutazione del rischio ad ogni componente DREAD viene assegnato un punteggio. I punteggi dei
   singoli componenti vengono quindi calcolati per dare un 'punteggio DREAD' totale.

   Il rischio viene quindi determinato in base al valore che il punteggio "DREAD" assume rispetto ad intervalli
   di valori predefiniti. Il risultato finale è un elenco di vulnerabilità classificate per rischio.

   Il processo di applicazione della metodologia DREAD è estremamente soggettivo e richiede le necessarie
   competenze. È consigliabile avere almeno un membro del team che abbia competenze sulla sicurezza per
   dare il necessario supporto nell’assegnazione dei punteggi DREAD.

   Come fase finale del processo di modellazione delle minacce, viene attuata una valutazione del **rischio** ( _risk
   assessment_ ), per dare una priorità a ciascuna vulnerabilità indentificata.

   In generale, in termini quantitativi, il rischio è definito come il prodotto tra la probabilità di accadimento
   dell’evento e l’impatto:

Rischio = Probabilità x Impatto

::

   In effetti, se almeno uno dei due termini del prodotto tende a zero, percepiamo il rischio come basso.
   Viceversa percepiamo un rischio grave quando ambedue i termini sono elevati.

   Nella metodologia DREAD il concetto di “impatto” viene declinato in termini di:

   1. danno (Damage)
   2. utenti interessati (Affected Users)

   mentre il concetto di “probabilità” viene declinato in termini di:

   3. riproducibilità (Reproducibility),
   4. sfruttabilità (Exploitability)
   5. rilevabilità (Discoverability).

   DREAD è appunto l’acronimo che “fattorizza” il rischio rispetto a queste 5 distinte categorie che
   caratterizzano la minaccia:

   1. **Damage potential** : Quanto sarebbe rilevante il danno in caso di concretizzazione della minaccia^12?
   2. **Reproducibility** : Quanto è facile che la minaccia possa ripetersi?
   3. **Exploitability** : Quanto tempo, sforzo e conoscenza è necessaria per concretizzare con successo la
       minaccia?
   4. **Affected Users** : Nel caso in cui la minaccia si concretizzi, quale percentuale di utenti sarebbe
       coinvolta?

   (^12) Si ricordi che la minaccia è un evento potenziale, accidentale o deliberato. Se deliberato, la minaccia si configura come attacco.


   Linee Guida per la modellazione delle minacce ed individuazione delle azioni di mitigazione conformi ai principi del Secure/Privacy

   5. **Discoverability** : Quanto è facile per un attaccante scoprire la minaccia?

   A ciascuna categoria viene attribuito un peso. Il “DREAD score” è la media dei 5 pesi, ossia:

DREAD Score= (Damage + Reproducibility + Exploitability + Affected Users
+ Discoverability) / 5

::

   Occorre quindi valutare e dare un peso numerico alle cinque categorie della tabella sopra mostrata. A
   seconda del dominio considerato, ci si può riferire o a una scala (semplificata) di tre soli valori o a una scala
   (più granulare) a dieci valori. I valori crescono rispettivamente al crescere del danno, della facilità di
   riproduzione, della facilità di sfruttamento, del numero di utenze coinvolte, della facilità di rilevamento.

   A titolo di esempio, si consideri la categoria “Exploitability”:

   - nel caso si voglia adottare una scala a 3 valori si potrebbero voler considerare e pesare in modo
       diverso i seguenti casi (Quanto è difficile sfruttare la vulnerabilità?):

o 1= L'attacco richiede una figura senior e una conoscenza profonda del
sistema attaccato; un'utenza con diritti di amministrazione; dispendio
di parecchie risorse per organizzare l'attacco (es. impiego di custom
tool); o 2 = L'attacco richiede una figura senior; un'utenza autenticata
con abilità non amministrative; tool di attacco disponibili in rete; o 3
= L'attacco è alla portata di una figura junior; senza autenticazione;
con web browser.

::

   - nel caso si voglia adottare una scala a 10 valori si potrebbero voler considerare e pesare in modo
       diverso i seguenti casi (Quanto è difficile sfruttare la vulnerabilità?):

o 1 = Anche con conoscenza approfondita della vulnerabilità non si
individua un percorso di attacco valido per l'exploit; o 2 = Sono
richieste tecniche avanzate e tool custom. Sfruttabile solo dagli utenti
autenticati; o 5 = La possibilità di exploit esiste, alla portata di
skill medie da un'utenza autenticata; o 7 = La possibilità di exploit
esiste, alla portata di un'utenza non autenticata; o 10 = Banale: basta
un web browser.

::

   Nel primo caso il calcolo del DREAD score:

   DREAD Score= (Damage + Reproducibility + Exploitability + Affected Users + Discoverability) / 5

   ricade in un numero compreso tra 1 e 3. Nel secondo caso ricade in un numero compreso tra 1 e 10.

   Il risultato finale è, in entrambi i casi, come desiderato, un elenco di vulnerabilità classificate per rischio
   ossia ordinate per priorità di intervento (a valori bassi corrisponde priorità bassa, a valori alti priorità alta).

   #### 4.4.2 Security Bulletin Severity Rating System (S.B.S.R.S)

   Come alternativa alla metodologia di analisi DREAD, Microsoft si avvale anche del "Security Bulletin Severity
   Rating System" per valutare le vulnerabilità nei prodotti Microsoft. Il sistema di classificazione raggruppa le
   vulnerabilità in una delle quattro categorie sotto riportate. Microsoft utilizza questo sistema per valutare la
   necessità di patch di sicurezza per i propri prodotti.

CLASSIFICAZIONE DEFINIZIONE

::

   **CRITICA** Una vulnerabilità il cui sfruttamento potrebbe consentire
   l'esecuzione di codice senza alcuna interazione da parte
   dell’utente.


   Linee Guida per la modellazione delle minacce ed individuazione delle azioni di mitigazione conformi ai principi del Secure/Privacy

   **IMPORTANTE** Una vulnerabilità il cui sfruttamento potrebbe compromettere la
   riservatezza, l'integrità o la disponibilità dei dati degli utenti o
   l'integrità o la disponibilità delle risorse necessarie all’
   elaborazione.

   **MODERATA** L'impatto della vulnerabilità è mitigato in misura significativa da
   fattori quali i requisiti di autenticazione o l'applicabilità solo alle
   configurazioni non predefinite.

   **BASSA** L'impatto della vulnerabilità è ampiamente mitigato dalle
   caratteristiche del componente interessato. Microsoft raccomanda
   ai clienti di valutare se applicare l'aggiornamento di sicurezza ai
   sistemi interessati.
   **_Tabella 15 - Sistema di classificazione del S.B.S.R.S._**

   Questo sistema di rating può anche essere adattato per classificare le vulnerabilità identificate dalla STRIDE.
   L' obiettivo finale è quello di produrre un elenco di prioritizzazione delle vulnerabilità a supporto del
   processo decisionale. Sebbene Microsoft non utilizzi più l’analisi DREAD, le motivazioni potrebbero essere
   giustificate dal fatto che si tratta di un processo di valutazione del rischio più adatto ai non esperti di
   sicurezza o a team novizi nella modellazione delle minacce rispetto al Security Bulletin Severity Rating
   System. L’analisi DREAD prevede un calcolo basato sulla valutazione di diversi aspetti della vulnerabilità,
   quali il danno potenziale o la riproducibilità. Il Security Bulletin Severity Rating System classifica le
   vulnerabilità in una di quattro categorie. Entrambi si basano sul parere del singolo individuo/team che
   effettua la valutazione del rischio. La DREAD ha perfezionato il suo sistema di valutazione del punteggio
   riducendo la probabilità di variazione dei risultati ed offre un approccio strutturato che i team possono
   adottare. Il processo è inoltre ben documentato e relativamente facile da attuare. Questa è una delle
   possibili motivazioni per cui scegliere l’analisi DREAD rispetto a S. B. S. R. S.

   #### 4.4.3 Altri processi di valutazione del rischio........................................................................................................

   Esistono altre opzioni disponibili per la valutazione del rischio, come l'US-CERT Vulnerability Metric, che
   utilizza una metrica quantitativa e valuta la gravità di una vulnerabilità assegnandole un valore compreso
   tra 0 e 180. Il Common Vulnerability Scoring System (CVSS) mira a fornire un framework open per misurare
   l' impatto delle vulnerabilità IT, mentre la scala SANS Critical Vulnerability Analysis classifica le vulnerabilità
   utilizzando diversi fattori chiave e variando il grado di peso. Il processo di valutazione del rischio da
   adottare dipende essenzialmente dalla scelta individuale del team che realizza il Threat Model.

   ### 4.5 PRIVACY BY DESIGN

   #### 4.5.1 Introduzione e concetti base

   La garanzia di sicurezza di un'organizzazione rappresenta la base per la protezione della privacy degli
   individui. La privacy può essere compromessa a causa di un errore nella sicurezza, tuttavia, la privacy si
   riferisce all'utilizzo improprio e non, delle informazioni da parte di utenti autorizzati. La privacy è una
   politica di gestione delle informazioni più che una politica di controllo accesso. Insieme, privacy e sicurezza,
   rappresentano la base per creare un rapporto di fiducia. Una sicurezza solida è la base della protezione
   della privacy. La privacy richiede una sicurezza effettiva, ma quest'ultima da sola, non garantisce una
   privacy effettiva. La sicurezza garantisce ad esempio il controllo accessi alle risorse di un'organizzazione
   attraverso un'istruzione di controllo accessi come: all'entità X è consentito eseguire l'operazione Y sulla
   risorsa Z che tradotta in un esempio pratico, potrebbe essere: "Il personale del settore finanziario può
   interrogare la base dati della contabilità".


   Linee Guida per la modellazione delle minacce ed individuazione delle azioni di mitigazione conformi ai principi del Secure/Privacy

   La privacy si riferisce alla relazione tra un'organizzazione che raccoglie informazioni e il proprietario delle
   informazioni raccolte. Per stabilire e gestire questa relazione, è necessario creare una politica di
   riservatezza formata da diverse istruzioni. Un'istruzione della politica di riservatezza definisce:

   - I tipi di informazioni raccolte e quelle accessibili;
   - Chi può accedere alle informazioni raccolte;
   - Per quali scopi è possibile accedere alle informazioni.

   Tale istruzione può assumere la seguente forma: all'entità X è consentito eseguire l'operazione Y sulla
   risorsa protetta Z del proprietario A per lo scopo B solo se il proprietario A esprime il proprio consenso
   esplicito. Una possibile traduzione di tale concetto in un esempio pratico, potrebbe essere: "I membri del
   settore di ricerca e sviluppo possono consultare i dati del modello di utilizzo di un singolo individuo per lo
   sviluppo di un nuovo prodotto se la persona in questione ha espresso esplicitamente il proprio consenso a
   rilasciare i propri dati su tale modello". Da notare che questa istruzione comprende la scelta da parte del
   proprietario delle informazioni di stabilire come utilizzare le sue informazioni. È possibile, inoltre, applicare
   anche altre dipendenze per l'accesso alle informazioni personali. Ad esempio, una norma può imporre
   alcune restrizioni sull'utilizzo delle informazioni raccolte.

   La privacy by Design è emersa come un approccio proattivo, integrativo e creativo per rafforzare i requisiti
   di privacy nelle prime fasi della progettazione applicativa. Tra le sfide legate all'ingegneria della privacy by
   design vi è la mancanza di metodologie olistiche, sistematiche e integrative che affrontino la complessità e
   la variabilità della privacy e sostengano la traduzione dei suoi principi fondamentali nelle attività di
   ingegneria. Per certi versi questo è comprensibile poiché l'approccio è stato sviluppato per tener conto di
   una serie di fonti e standard. Tuttavia, ne consegue che i suoi principi fondanti sono dati ad un alto livello di
   astrazione senza fornire a corredo metodologie e linee guida per ottenere requisiti concreti in materia di
   privacy. I principi fondamentali della Privacy by Design si basano sui Fair Information Practice Principles
   (FIPP) e fungono da framework universale per l'integrazione della privacy in tre principali aree di
   applicazione: tecnologie dell'informazione e della comunicazione, aree di business, progetti fisici e
   infrastrutturali.

   La Privacy Engineering si è affermata come una nuova disciplina che mira ad applicare principi e processi di
   ingegneria nello sviluppo, nell’implementazione e manutenzione dei sistemi, in modo sistematico e
   ripetibile, per raggiungere un livello accettabile di protezione della privacy. Per distinguere questi concetti;
   la Privacy by Design (PbD) intende spiegare "Cosa fare" per raggiungere un livello adeguato di protezione
   della privacy, mentre la Privacy Engineering (PE) intende spiegare "Come farlo" definendo la privacy come
   un attributo di qualità nell'ingegneria dei sistemi. In altre parole, la PE si concentra sullo sviluppo e la
   valutazione di metodi, tecniche e strumenti che identificano e affrontano in modo sistematico le
   problematiche legate alla privacy durante il processo di sviluppo dei sistemi.

   La tabella che segue, sintetizza i ‘concetti’ alla base della Privacy:

Concetto di Privacy Descrizione

::

   Personal Identifiable Information (PII) Informazioni che possono essere ricondotte ad un individuo.

   Data Subject Individuo collegato alla PII.

   Item of Interest (IOI) Informazioni relative ad un individuo (ad esempio soggetti,
   messaggi, azioni, ecc.).

   Unlinkability Non essere in grado di distinguere se due IOI sono correlati.

   Anonymity Non essere in grado di identificare il soggetto all'interno di un
   gruppo di soggetti.

   Plausible deniability Essere in grado di negare di aver eseguito un'azione.


   Linee Guida per la modellazione delle minacce ed individuazione delle azioni di mitigazione conformi ai principi del Secure/Privacy

   Undetectability Non essere in grado di distinguere se esiste un IOI.

   Unobservability Impossibilità nell’essere rintracciabili da tutti i soggetti
   coinvolti.

   Confidentiality Restrizioni autorizzate all'accesso e alla divulgazione delle
   informazioni.

   Awareness Essere consapevoli delle conseguenze della condivisione delle
   informazioni personali (PI).

   Compliance Aderenza alle normative e alle politiche interne di una
   organizzazione.
   **_Tabella 16 - Concetti alla base della Privacy_**

   Similmente alla miriade di normative sulla privacy disponibili, ci sono stati diversi tentativi di strutturare e
   classificare i concetti di privacy. Di seguito si riportano alcuni esempi di tassonomie basate su due approcci
   distinti:

   - Classificazione dei concetti di privacy da un punto di vista giuridico;
   - Classificazione dei concetti di privacy da un punto di vista di ingegneria del software.

   **Tassonomia di Solove.** Presenta una tassonomia delle violazioni della privacy da un punto di vista legale.
   Anche se questa non tratta la privacy digitale, ma descrive la privacy in generale, fornisce comunque alcune
   informazioni utili in materia. Solove^13 opera una distinzione tra quattro gruppi di attività di base dannose:

   - Raccolta dei dati. Include due tipi di violazioni della privacy: il controllo inteso come "osservazione,
       ascolto o registrazione delle attività di un individuo", e, l’investigazione che consiste in varie forme
       di sondaggio per ottenere informazioni.
   - Trattamento dei dati. Include cinque tipi di violazioni dei dati raccolti al punto precedente:
       aggregazione (ovvero combinazione di dati relativi a un individuo), identificazione (ovvero
       collegamento dei dati per identificare un individuo), negligenza (poca attenzione nella protezione
       dei dati memorizzati), uso secondario (ovvero utilizzo dei dati per scopi diversi da quelli per i quali
       sono stati raccolti) ed esclusione (ovvero quando l'interessato non è a conoscenza dei dati che gli
       altri hanno su di esso).
   - Diffusione dei dati. Include sette categorie di violazioni: violazione della riservatezza (ovvero non
       mantenere riservate le informazioni di una persona), divulgazione (cioè rivelare informazioni
       "sensibili" veritiere su una persona), esposizione (cioè rivelare le nudità, il dolore o le
       caratteristiche fisiche di una persona), maggiore accessibilità (cioè amplificare l'accessibilità dei
       dati), appropriazione (cioè l'uso della propria identità per perseguire un'altra finalità).
   - Invasione. A differenza dei gruppi precedenti, non riguarda necessariamente le informazioni
       personali, ma degli elementi che limitano la sfera personale e decisionale (ad esempio atti invasivi
       che violano la tranquillità di una persona e atti invasivi che impattano sulle decisioni private di una
       persona).

   **Linee guida FIPPs (Fair Information Practice Principles).** La Privacy and Personal Information Protection
   raccoglie un insieme di indicazioni proposte dalla Federal Trade Commission degli Stati Uniti. Queste
   possono essere considerate come il fondamento di tutta la legislazione vigente negli Stati Uniti, in materia
   di protezione dei dati. Sono state utilizzate per la definizione delle linee guida dell'OCSE (Organizzazione per

   (^13) https://en.wikipedia.org/wiki/Daniel_J._Solove


   Linee Guida per la modellazione delle minacce ed individuazione delle azioni di mitigazione conformi ai principi del Secure/Privacy

   la Cooperazione e lo Sviluppo Economico) e per la direttiva europea sulla protezione dei dati. I principi si
   basano su cinque distinte categorie:

   - Avviso/Consapevolezza. I consumatori dovrebbero essere adeguatamente informati prima di
       procedere nella raccolta delle informazioni personali.
   - Scelta/Consenso. I consumatori devono essere in grado di scegliere come devono essere utilizzati i
       propri dati personali. In particolare laddove si fa un uso secondario dei dati (ad esempio,
       registrazione ad una mailing list o trasferimento di informazioni a terzi).
   - Accesso/Partecipazione. Una persona dovrebbe essere in grado di accedere ai dati che la
       riguardano e di contestarne l'accuratezza e la completezza.
   - Integrità/Sicurezza. I dati devono essere accurati e sicuri.
   - Enforcement/Redress. Dovrebbero essere messe in atto misure di enforcement per garantire il
       rispetto dei FIPP.

   Le FIPP sono utilizzate anche per definire altre tassonomie di privacy. Se ne cita qualcuna a titolo di
   esempio:

   - linee guida Microsoft per la privacy;
   - tassonomia definita da Anton et al.[13]. Questa tassonomia però, non contiene solo i cinque FIPP
       come obiettivi di protezione della privacy, ma include anche una serie di obiettivi di vulnerabilità
       alla privacy che sono correlati alle minacce esistenti. Questi obiettivi di vulnerabilità includono il
       monitoraggio delle informazioni, l'aggregazione, la memorizzazione, il trasferimento di
       informazioni, la raccolta e la personalizzazione.

   **European Data Protection Legislation.** La legislazione è una questione complessa, spesso vaga e formulata
   in modo ambiguo; il che la rende molto difficile da attuare. La privacy non richiede solo misure
   tecnologiche, ma anche misure organizzative. Inoltre, è difficile prevedere tutti i potenziali domini e
   contesti (e le relative normative) in cui un prodotto software verrà poi utilizzato. Tuttavia, alcune
   disposizioni legislative in materia di protezione dei dati possono, con un minimo sforzo, essere integrate
   nella progettazione del sistema.

   Guarda e Zannone [2] riassumono la Direttiva Europea sulla Protezione dei Dati nei seguenti nove principi:

   - Elaborazione corretta e lecita. La raccolta e il trattamento dei dati personali non devono interferire
       in modo irragionevole con la privacy delle persone interessate né interferire in modo irragionevole
       con la loro autonomia e integrità e devono essere conformi al quadro giuridico generale.
   - Consenso. I dati personali devono essere raccolti e trattati solo previo esplicito consenso al loro
       trattamento da parte degli interessati.
   - Finalità. I dati personali devono essere raccolti per finalità specifiche, lecite e legittime e non
       devono essere trattati per finalità non compatibili con quelle per cui sono stati raccolti.
   - Minimalità. La raccolta e il trattamento dei dati personali sono limitati al minimo necessario per il
       raggiungimento delle finalità specifiche. Ciò include che i dati personali vengono conservati solo per
       il tempo necessario a raggiungere lo scopo specifico.
   - Informazione minima. La divulgazione di dati personali a terzi è limitata e avviene solo a
       determinate condizioni.
   - Qualità dell'informazione. I dati personali devono essere accurati, pertinenti e completi rispetto alle
       finalità per le quali sono raccolti e trattati.
   - Controllo dell'interessato. L'interessato deve essere in grado di controllare e condizionare il
       trattamento dei suoi dati personali.
   - Sensibilità. Nel trattamento dei dati personali è necessario applicare misure di protezione più
       rigorose sui dati ritenuti particolarmente sensibili per il soggetto interessato.
   - Sicurezza delle informazioni. I dati personali devono essere trattati in modo da garantire un livello
       di sicurezza adeguato ai rischi connessi al trattamento e alla natura dei dati stessi.


   Linee Guida per la modellazione delle minacce ed individuazione delle azioni di mitigazione conformi ai principi del Secure/Privacy

   Poiché il DPD è stato creato in un momento in cui Internet era ancora agli inizi, nel 2012 è stata elaborata
   una proposta di riforma della legislazione attuale per rafforzare i diritti della privacy online. Questa riforma
   indirizza:

   - il "diritto all'oblio" ovvero, l'obbligo di fornire esplicitamente il consenso necessario al trattamento
       dei dati;
   - il "diritto di portabilità dei dati" che consente un accesso più facile ai propri dati e una maggiore
       trasparenza sul modo in cui questi vengono gestiti.

   Anche la responsabilità di coloro che trattano i dati personali è accresciuta dall'attuazione di principi quali
   "Privacy by Design".

   La direttiva relativa alla privacy e alle comunicazioni elettroniche è stata promulgata nel 2002 e completa la
   direttiva DPD in quanto si concentra sulla protezione dei dati nell'era digitale. Essa disciplina il settore delle
   comunicazioni elettroniche ed è stata modificata nel 2009. È principalmente nota per la richiesta di
   consenso da parte dell'utente nella memorizzazione dei cookie, ed è quindi spesso indicata come la
   "direttiva sui cookie". Inoltre, la direttiva disciplina lo spam online imponendo un regime di “opt-in”, in base
   al quale le e-mail indesiderate possono essere inviate solo previo accordo del destinatario. La direttiva
   comprende anche la conservazione e il trattamento dei dati relativi al traffico e dei dati relativi
   all'ubicazione. I dati relativi al traffico dovrebbero essere cancellati o resi anonimi non appena non sono più
   necessari ai fini della trasmissione. Il trattamento di tali dati può avvenire solo quando questi vengono resi
   anonimi o quando l'interessato ha dato il suo consenso.

   Sebbene la legislazione sulla protezione dei dati sia complessa e spesso ambigua, alcune norme possono
   essere automatizzate nei sistemi software. Negli ultimi anni è emersa una ricerca che si propone di estrarre
   diritti e obblighi dai documenti legali e che fornisce la tracciabilità tra le politiche sulla privacy (scritte) e le
   loro controparti software implementate.

   ##### 4.5.1.1 Proprietà

   In quanto concetto astratto e soggettivo, la declinazione della privacy varia a seconda delle problematiche
   sociali e culturali, delle discipline di studio, degli interessi degli stakeholder e del contesto applicativo. Le
   norme di privacy più comuni sono volte a consentire agli individui di controllare, modificare, gestire e
   cancellare informazioni su se stessi e decidere quando, come e in quale misura tali informazioni possono
   essere comunicate agli altri.

   La privacy si basa prevalentemente su due modelli di tutela:

   - _hard privacy_ (la privacy quale libertà negativa). Si basa sul concetto di libertà (e del relativo diritto)
       definendo un perimetro entro cui l’individuo può agire al riparo da invasioni esterne. Questa libertà
       dal controllo si esprime in una sfera di libertà di scelte e di comportamenti. Nella modellazione
       delle minacce è necessario tener conto delle seguenti entità: il fornitore di servizi, il titolare dei dati
       e l'ambiente con cui interagisce.
   - _soft privacy_ (privacy quale libertà positiva). Contrariamente al primo, si basa sul presupposto che
       l'interessato abbia concesso il controllo dei propri dati personali a terzi, e debba fidarsi dell'onestà
       e della competenza dei responsabili del trattamento. L'obiettivo di questo modello è quindi, di
       fornire la sicurezza dei dati ed elaborare questi con finalità e consenso specifici, tramite politiche,
       controllo degli accessi e audit. Il modello prevede che l'interessato fornisca i suoi dati personali e il
       responsabile del trattamento di tali dati è responsabile della loro protezione. Di conseguenza, si
       applica un modello di minaccia più debole, che include diverse parti con diversi poteri.

   Alla base del modello di privacy, ci sono alcune delle classiche proprietà di sicurezza quali:

   - **confidenzialità,** garantisce che le informazioni siano accessibili solo da parte di persone autorizzate;
   - **integrità,** garant isce l'accuratezza e la completezza delle informazioni e dei metodi di elaborazione;


   Linee Guida per la modellazione delle minacce ed individuazione delle azioni di mitigazione conformi ai principi del Secure/Privacy

   - **disponibilità** (o resistenza alla censura), garantisce che le informazioni siano accessibili agli utenti
       autorizzati;
   - **non ripudio,** garantisce che non si sia in grado di negare ciò che si è fatto.

   Le caratteristiche di queste proprietà si trovano nella norma ISO 17799^14. A queste si aggiungono ulteriori
   proprietà quali:

   - **Unlinkability**. Si riferisce alla capacità di nasconde il legame tra due o più azioni (ad esempio,
       nascondere i link tra due messaggi anonimi inviati dalla stessa persona), identità (ad esempio, due
       pagine web visitate da parte dello stesso utente o due persone collegate da una relazione di
       amicizia in un social network) o informazioni (ad esempio, voci presenti in due distinti database
       relativi alla stessa persona). La unlinkability consiste nel separare due o più elementi di interesse,
       detti IOI, (quali ad esempio, soggetti, messaggi, azioni, etc). Questa separazione assicura che
       all'interno del sistema (comprendente questi ed eventualmente altri elementi), l'aggressore non sia
       in grado di identificare in modo efficace se questi IOI sono collegati o meno.
   - **Anonymity**. Si riferisce alla capacità di nascondere il legame tra un'identità e un'azione o
       un'informazione (ad esempio, il mittente anonimo di una e-mail, l'autore di un testo, la persona che
       accede ad un servizio, la persona a cui si riferisce una voce presente in un database). Tale proprietà
       assicura che un eventuale attaccante non possa identificare in modo efficace il soggetto.
       L' anonimato può essere ricondotto anche alla precedente proprietà (unlinkability).
   - **Pseudonymity**. Suggerisce che è possibile costruire una reputazione su uno pseudonimo e utilizzare
       pseudonimi multipli per scopi diversi.
   - **Plausible deniability**. Si riferisce alla capacità di ostacolare la possibilità da parte di un attaccante di
       dimostrare che un soggetto conosce, ha fatto o ha detto qualcosa.
   - **Undetectability and unobservability**. Si riferisce alla capacità di nascondere le attività dell'utente.
   L’ _undetectability_ è vista come l’impossibilità di rilevare un elemento di interesse (IOI) da un punto
   di vista di un attaccante, il che significa che quest’ultimo non può distinguere quando l’elemento
   esiste da quando invece non esiste. L’ _unobservability_ è vista come l’impossibilità di osservare un
   elemento di interesse (IOI) da parte di tutti i soggetti non coinvolti.
   - **Confidentiality**. Si riferisce alla capacità di nascondere il contenuto dei dati o di controllare la
       divulgazione degli stessi (ad esempio, il trasferimento di e-mail crittografate, l'applicazione del
       controllo di accesso a un documento classificato o a un database contenente informazioni
       sensibili). NIST descrive la riservatezza come la capacità di mantenere le restrizioni autorizzative
       all'accesso e alla divulgazione delle informazioni, compresi i mezzi per proteggere la privacy e le
       informazioni proprietarie. Sebbene la riservatezza sia una proprietà di sicurezza, come si evince
       dalla definizione, essa è importante anche per preservare le proprietà dell'anonimato e di
       inscindibilità.
   - **Content awareness**. Si riferisce alla capacità di garantire che gli utenti abbiano la consapevolezza
   dei loro dati personali e di limitare l’uso delle informazioni necessarie per consentire l'esecuzione
   della funzione a cui si riferiscono. Quanto più sono elevate le informazioni personali identificabili
   divulgate dagli interessati, tanto maggiore è il rischio di violazione della privacy. L'utente deve
   essere consapevole delle conseguenze della condivisione delle informazioni. Queste conseguenze
   possono riferirsi alla violazione della privacy così come a risultati indesiderati fornendo informazioni
   incomplete o errate.
   - **Policy and consent compliance**. Si riferisce alle politiche in atto e alle proprietà di conformità sul
       consenso in merito al trattamento dei dati personali per informare l'interessato sulla politica di
       privacy del sistema, o consentire allo stesso di specificare i consensi in conformità con la
       legislazione, prima che gli utenti accedono al sistema.

   (^14) https://www.iso.org/standard/39612.html


   Linee Guida per la modellazione delle minacce ed individuazione delle azioni di mitigazione conformi ai principi del Secure/Privacy

   Le proprietà sopra esposte possono essere considerate tutte proprietà tipiche di sicurezza. Relativamente
   ai modelli di hard/soft privacy possono essere inoltre così suddivise:

   - unlinkability, anonimity, pseudonymity, plausible deniability, undetectability and unobservability,
       confidentiality possono essere considerate come proprietà di hard privacy;
   - content awareness, policy and consent compliance, possono essere considerate come proprietà di
       soft privacy.

   ##### 4.5.1.2 Principi ....................................................................................................................................................................

   La **Privacy by Design** è un concetto sviluppato alla fine degli anni 90 da Ann Cavoukian [3], commissario per
   l'informazione e la privacy dell'Ontario. Si tratta di un approccio ingegneristico che si concentra sull'intero
   processo a partire dai principi di privacy e protezione dei dati.

   La tutela della privacy non dovrebbe essere garantita solo dal rispetto delle norme e dai quadri normativi,
   in quanto non vi è alcuna utilità nelle norme giuridiche di codifica rigorosa se il sistema stesso non ha una
   solida base per la sicurezza e la tutela della privacy.

   La privacy by Design può essere raggiunta applicando i sette principi su cui si basa:

   - **Proattivo non reattivo, preventivo non correttivo** : le minacce alla privacy dovrebbero essere
       anticipate e prevenute, piuttosto che corrette dopo che queste si sono verificate.
   - **Privacy come impostazione predefinita** : la privacy dovrebbe essere lo standard. I dati personali
       dovrebbero essere protetti automaticamente, anche senza alcuna azione esplicita da parte
       dell'individuo interessato.
   - **Privacy incorporata nella progettazione** : la privacy non dovrebbe essere considerata un elemento
       aggiuntivo, ma dovrebbe essere integrata nella progettazione e nell'architettura dei sistemi
       software e delle attività di business in generale.
   - **Piena funzionalità - somma positiva, non somma zero** : la privacy dovrebbe coesistere con altri
       interessi di business. Dovrebbero tuttavia essere evitati compromessi non necessari (ad esempio
       privacy vs. sicurezza o privacy vs. performance). Si dovrebbe cercare di ottenere una somma
       positiva.
   - **Sicurezza end-to-end - Tutela dell'intero ciclo di vita** : la privacy richiede sicurezza durante l'intero
       ciclo di vita dei dati personali, garantendo una gestione sicura e completa di tutti i dati.
   - **Visibilità e trasparenza** : gli obiettivi di privacy dichiarati dall'organizzazione e conseguentemente
       adottati dai sistemi, devono essere visibili e trasparenti agli utenti.
   - **Rispetto per la privacy degli utenti** : devono essere applicate misure adeguate per responsabilizzare
       l'utente nel trattamento dei propri dati.

   Il panorama tecnologico della privacy è stato classificato da Gürses [14] secondo tre paradigmi che tuttavia,
   non si escludono a vicenda:

   - **Privacy come controllo**. I n quanto controllo, mira a fornire agli interessati un mezzo per controllare
       la divulgazione dei propri dati. Rientrano in questa categoria anche gli strumenti applicati
       dall’organizzazione per definire e applicare politiche di sicurezza dei dati e prevenire l'abuso di
       accessi non autorizzati. Esempi di tecnologie correlate, includono ad esempio, le impostazioni
       relative alla privacy, il controllo dell'accesso e la verifica dei dati.
   - **Privacy come riservatezza**. Questo paradigma impedisce la divulgazione delle informazioni o
       perlomeno ne minimizza il più possibile la divulgazione al fine di evitare di collegarle all'interessato.
       Le tecnologie di esempio sono: i protocolli di autenticazione anonimi e le reti di comunicazione
       anonime.
   - **Privacy come pratica**. Si concentra maggiormente sull'aspetto sociale della privacy e mira a rendere
       più trasparenti i flussi di informazioni attraverso strumenti di sensibilizzazione e feedback.


   Linee Guida per la modellazione delle minacce ed individuazione delle azioni di mitigazione conformi ai principi del Secure/Privacy

   ##### 4.5.1.3 Riferimenti normativi .............................................................................................................................................

   Il 27 aprile 2016 il Parlamento Europeo ha approvato il Regolamento generale sulla protezione dei dati
   personali afferenti a persona fisica (General Data Protection Regulation^15 ) che abroga la direttiva 95/46/CE,
   al fine di armonizzare le legislazioni dei singoli paesi, consolidare il diritto alla privacy dei cittadini dell’UE e
   garantire un’adeguata sicurezza dei dati sensibili trattati dalle aziende.

   Il regolamento si applica a tutti gli enti pubblici e le imprese che trattano dati personali e dati personali
   classificati (sensibili, biometrici, sanitari e giudiziari, etc.) e/o che raccolgono grandi quantità di dati
   personali.

   Tra gli elementi di maggiore innovazione ed interesse troviamo:

   - La responsabilizzazione del Titolare nell’adozione di comportamenti proattivi tali da dimostrare
       l’attuazione di misure concrete individuate attraverso una valutazione dell’impatto dei trattamenti
       previsti (Data Protection Impact Analysis - DPIA);
   - La nomina del Responsabile della protezione dei dati (Data Protection Officer - DPO) con il compito
       di vigilare, sui processi interni alla struttura, l’osservanza del Regolamento, fornire pareri in merito
       alla DPIA, indicare le misure tecniche e organizzative per attenuare i rischi per i diritti e gli interessi
       delle persone interessate, fungere da punto di contatto con l’autorità di controllo;
   - La comunicazione all’Autorità Garante di eventuali violazioni della sicurezza dei dati personali (Data
       Breach);
   - Il principio di “privacy by design” che prevede l’integrazione delle attività volte alla protezione dei
       dati personali in tutte le fasi del ciclo di vita dei sistemi e delle applicazioni IT, dalla fase di
       progettazione, messa in esercizio, utilizzo e dismissione finale;
   - Il principio di “privacy by default” che prevede il rispetto dei principi generali della protezione delle
       informazioni, quali la minimizzazione dei dati e la limitazione delle finalità, nelle impostazioni dei
       servizi e dei prodotti che trattato dati personali.

   La protezione della privacy richiesta dal GDPR presuppone quindi programmi di conformità sostenuti da
   tutta l’azienda, in modo da integrare i requisiti di sicurezza dei dati in tutte le fasi di ogni processo
   aziendale, dalla progettazione al rilascio.

   L’Articolo 25 del GDPR^16 – **Data protection “by default” “by design”** – chiede al titolare del trattamento di
   mettere in atto misure tecniche e organizzative adeguate:

   - volte ad attuare in modo efficace i principi di protezione dei dati, quali la pseudo-anonimizzazione e
       la minimizzazione, e a integrare nel trattamento le necessarie garanzie al fine di soddisfare i
       requisiti del regolamento e tutelare i diritti degli interessati (by design);
   - per garantire che siano trattati, by default, solo i dati personali necessari per ogni specifica finalità
       del trattamento. Tale obbligo vale per la quantità dei dati personali raccolti, la portata del
       trattamento, il periodo di conservazione e l’accessibilità. In particolare, dette misure garantiscono
       che, by default, non siano resi accessibili dati personali a un numero indefinito di persone fisiche
       senza l’intervento della persona fisica.

   Nel ciclo di vita del software in sicurezza, deve essere posta quindi maggiore attenzione quando si
   sviluppano applicativi che tratteranno dati personali, inserendo controlli mirati per ciascuna fase, secondo
   le best practices di sicurezza e secondo le indicazioni fornite dall’analisi dei rischi privacy (DPIA). Tali
   controlli devono essere formalmente verificati in fase di test e collaudo.

   Altri elementi da considerare durante le fasi del ciclo di sviluppo software, si evincono dall’Articolo 32 del
   GDPR^17 – **Sicurezza del trattamento** – nel quale viene chiesto al titolare e al responsabile del trattamento

   (^15) https://gdpr-info.eu/
   (^16) https://gdpr-info.eu/art-25-gdpr/
   (^17) https://gdpr-info.eu/art-32-gdpr/


   Linee Guida per la modellazione delle minacce ed individuazione delle azioni di mitigazione conformi ai principi del Secure/Privacy

   di mettere in atto misure tecniche e organizzative adeguate per garantire un livello di sicurezza adeguato al
   rischio, che comprendono, tra le altre, se del caso:

   - la pseudo-anonimizzazione e la cifratura dei dati personali;
   - la capacità di assicurare su base permanente la riservatezza, l’integrità, la disponibilità e la
       resilienza dei sistemi e dei servizi di trattamento;
   - la capacità di ripristinare tempestivamente la disponibilità e l’accesso dei dati personali in caso di
       incidente fisico o tecnico;
   - una procedura per testare, verificare e valutare regolarmente l’efficacia delle misure tecniche e
       organizzative al fine di garantire la sicurezza del trattamento.

   #### 4.5.2 Best practices per il trattamento dei dati personali

   - **Ridurre al minimo i dati personali utilizzati -** _Ridurre l’impatto dei rischi limitando la gestione di_
       _dati personali a ciò che è strettamente necessario per raggiungere lo scopo definito._
   o Comprovare che i dati personali siano sufficienti, pertinenti e non eccessivi rispetto all’intento;
   altrimenti, non raccogliere i dati.
   o Comprovare che i dati personali non rivelino (direttamente o indirettamente) l'origine razziale o
   etnica, le opinioni politiche, filosofiche o religiose, l'appartenenza sindacale, le informazioni
   sulla salute o le informazioni sulla vita sessuale di un individuo, tranne che per circostanze
   eccezionali.
   o Comprovare che i dati personali non si riferiscono a reati, sentenze penali o misure di sicurezza.
   o Evitare la raccolta di dati personali aggiuntivi.
   o Limitare la trasmissione di documenti elettronici contenenti dati personali allo stretto
   necessario.
   o Eliminare i dati personali che non sono più utili o le richieste di un soggetto dal sistema in
   esercizio o dai backup, se necessario.
   - **Gestire i periodi di conservazione dei dati personali -** _Ridurre l’impatto dei rischi assicurando che i_
       _dati personali non vengano mantenuti per più di quanto necessario._
   o Definire periodi di conservazione dei dati personali limitati nel tempo e appropriati allo scopo
   dell'elaborazione.
   o Verificare che l'elaborazione possa rilevare la scadenza del periodo di conservazione.
   o Verificare che l'elaborazione consenta la cancellazione dei dati personali a scadenza del periodo
   di conservazione e che il metodo scelto per l’eliminazione sia appropriato ai rischi legati alle
   libertà civili e la privacy dei soggetti interessati.
   o Eliminare immediatamente i dati personali quando il periodo di conservazione scade.
   - **Informare i soggetti e ottenere il consenso -** _Consentire ai soggetti interessati di effettuare una_
       _scelta libera, specifica e informata._
   o Determinare se l'elaborazione si basa su una base giuridica diversa dal consenso.
   o Determinare i mezzi pratici da attuare per ottenere il consenso degli interessati.
   o Assicurare che il consenso sia ottenuto prima che inizia l'elaborazione.
   o Assicurare che il consenso sia ottenuto liberamente.
   o Assicurare che il consenso sia ottenuto in modo notificato e trasparente in termini di finalità del
   trattamento.
   o Assicurare che il consenso sia ottenuto per uno scopo specifico.
   - **Partizionare i dati personali - Ridurre la possibilità che i dati personali possano essere correlati e**
       **che possa verificarsi una violazione di tutti i dati personali.**


   Linee Guida per la modellazione delle minacce ed individuazione delle azioni di mitigazione conformi ai principi del Secure/Privacy

o Identificare i dati personali utili solo per ogni processo aziendale.
o Separare i dati utili di ogni processo in modo logico. o Comprovare
regolarmente che i dati personali sia partizionati in modo efficace e
che i destinatari e le interconnessioni non siano stati associati.

::

   - **Cifrare i dati personali -** _Rendere incomprensibili i dati personali a chiunque senza autorizzazione di_
       _accesso._
   o Determinare tutto ciò che deve essere crittografato (incluso dischi rigidi, file, dati provenienti
   da un database o canali di comunicazione) in base alla forma in cui sono memorizzati i dati
   personali, i rischi individuati e le prestazioni richieste.
   o Scegliere il tipo di crittografia (simmetrica o asimmetrica) in base al contesto e ai rischi
   individuati.
   o Adottare soluzioni di crittografia basate su algoritmi pubblici notoriamente forti.
   o Definire misure per garantire la disponibilità, l'integrità e la riservatezza delle informazioni
   necessarie per recuperare le informazioni perse (incluse le password di amministratore e dati di
   ripristino).
   - **Anonimizzare i dati personali -** _Eliminare le caratteristiche che identificano i dati personali._
       o Determinare ciò che deve essere anonimo in base al contesto, alla forma in cui vengono
          memorizzati i dati personali (compresi i campi del database o estratti dai testi) e rischi
          individuati.
       o Anonimizzare permanentemente i dati che richiedono tale criterio di protezione in base alla
          forma dei dati (inclusi database e record testuali) e i rischi individuati.
       o Se questi dati non possono essere anonimizzati in modo permanente, scegliere strumenti
          (inclusi la cancellazione parziale, la cancellazione, la ricerca di hashing e l'indice) che rispondano
          innanzitutto alle esigenze funzionali.

   #### 4.5.3 Tecniche di modellazione e individuazione delle minacce

   ##### 4.5.3.1 LINDDUN

   La privacy sta diventando una questione chiave nell'e-society. È della massima importanza che la privacy sia
   integrata quanto prima nel ciclo di vita del software di sviluppo. LINDDUN^18 è una metodologia di analisi
   delle minacce alla privacy e supporta gli analisti nell'individuare i requisiti di riservatezza.

   LINDDUN è un nome mnemonico sviluppato da Mina Deng [15] per il suo dottorato di ricerca alla
   Katholieke Universiteit di Leuven, Belgium. Questa è una metodologia speculare alla modellazione delle
   minacce STRIDE (STRIDE-per-element) e tratta le violazioni delle seguenti proprietà sulla privacy:

   - Collegabilità (Linkability);
   - Identificabilità (Identifiability);
   - Non ripudio (Non Repudiation);
   - Rilevabilità (Detectability);
   - Divulgazione di informazioni (Disclosure of information);
   - Inconsapevolezza sul contenuto (Content Unawareness);
   - Inaderenza alla politica sul conseno (Policy and consent Non-compliance).

   (^18) https://www.linddun.org/


   Linee Guida per la modellazione delle minacce ed individuazione delle azioni di mitigazione conformi ai principi del Secure/Privacy

   LINDDUN viene presentato come un approccio completo alla modellazione delle minacce con un metodo di
   individuazione di processi, minacce e requisiti. Può essere ragionevole utilizzare LINDDDUN come
   framework per l’identificazione delle minacce sulla privacy, in sostituzione o in aggiunta alla STRIDE.

   In primo luogo, viene creato un diagramma di flusso dei dati (DFD), una rappresentazione grafica
   strutturata del sistema che utilizza quattro tipi principali di elementi: entità, archivi dati, flussi di dati e
   processi. Ciascun tipo di elemento DFD viene associato a una serie di categorie di minacce alla privacy (sono
   state identificate sette categorie di alto livello di minacce alla privacy: **L** -Linkability, **I** -Identifiability, **N** -Non
   Repudiation, **D** -Detectability, **D** -Disclosure of information, **U** -Content Unawareness e **N** -Policy and consent
   Non-compliance). Per identificare le minacce che insistono sul sistema analizzato, per ciascun elemento è
   necessario esaminare le minacce corrispondenti alle categorie di cui sopra.

   La tabella seguente, mostra la correlazione tra le minacce di privacy previste da LINDDUN e le tipologie di
   elementi DFD sopra descritte:

Elemento DFD

::

   ###### L I N D D U N

   **Archivio
   dati**

   ###### X X X X X X

   **Flusso dati** X X X X X X

   **Processo** X X X X X X

   **Entità** X X X

Tabella 17 - Minacce LINDDUN per elemento DFD

::

   La metodologia LINDDUN supporta l'analista fornendo una serie di alberi di minaccia che descrivono i
   percorsi d'attacco più comuni per ogni possibile combinazione tra le tipologie di minaccia e gli elementi
   DFD. Basandosi su questi alberi, l'analista potrà documentare le minacce identificate, utilizzando scenari di
   casi di abuso per descrivere in dettaglio i possibili attacchi. Le minacce vengono quindi considerate
   prioritarie in base al loro rischio. Tuttavia non fornisce esplicitamente un supporto per l'analisi del rischio.
   Le minacce che derivano da tale processo, possono quindi essere tradotte in requisiti di riservatezza. Infine,
   LINDDUN fornisce un elenco di soluzioni per la privacy al fine di mitigare le minacce individuate.

   La tabella seguente, riporta gli obiettivi di privacy basati sule varie tipologie di minaccia previste in
   LINDDUN, dove ( **E** -Entity, **DF** -DataFlow, **DS** -DataStore, **P** -Process).

Minacce LINDDUN Obiettivo elementare a tutela della privacy

::

Linkability of (E,E) Unlinkability of (E,E)

::

Linkability of (DF,DF) Unlinkability of (DF,DF)

::

Linkability of (DS,DS) Unlinkability of (DS,DS)

::

Linkability of (P,P) Unlinkability of (P,P)

::

Identifiability of (E,E) Anonymity/pseudonymity of (E,E)

::

Identifiability of (E,DF) Anonymity/pseudonymity of (E,DF)

::

Identifiability of (E,DS) Anonymity/pseudonymity of (E,DS)

::

Identifiability of (E,P) Anonymity/pseudonymity of (E,P)

::

Non-repudiation of (E,DF) Plausibledeniability of (E,DF)

::

Non-repudiation of (E,DS) Plausibledeniability of (E,DS)

::


   Linee Guida per la modellazione delle minacce ed individuazione delle azioni di mitigazione conformi ai principi del Secure/Privacy

Non-repudiation of (E,P) Plausibledeniability of (E,P)

::

Detectability of DF Undetectability of DF

::

Detectability of DS Undetectability of DS

::

Detectability of P Undetectability of P

::

Information Disclosure of DF Confidentiality of DF

::

Information Disclosure of DS Confidentiality of DS Information
Disclosure of P Confidentiality of P

::

Content Unawareness of E Content awareness of E

::

Policy and consent Noncompliance of the system Policy and consent
compliance of the system Tabella 18 - obiettivi di privacy basati sule
varie tipologie di minaccia previste in LINDDDUN

::

   4.5.3.1.1 Tecniche di mitigazione

   Nella metodologia LINDDUN, le proprietà e la corrispettive minacce alla privacy vengono classificate come
   hard e soft privacy. La tabella a seguire evidenzia tale classificazione:

Controlli di privacy Minaccia alla privacy

::

Hard privacy

::

   Unlinkability Linkability

   Anonymity & Pseudonymity Indentifiability

   Plausible deniability Non repudiation

   Undetectability & unobservability Detectability

   Confidentiality Disclosure of information

Soft privacy

::

   Content awareness Content Unawareness

   Policy and consent compliance Policy and consent non-compliance

Tabella 19 - LINDDUN Hard & Soft privacy

::

   LINDDUN fornisce per ogni tipo di potenziale minaccia identificata una o più classificazioni delle tecniche di
   mitigazione da mettere in campo attraverso una mappatura tra obiettivi e tecniche di miglioramento della
   privacy (PETs):

   **Tecniche di mitigazione U A P D C W O**

   Anonymity system (^) • Mix-networks (1981)

   - DC-networks (1985)
   - ISDN-mixes
   - Onion Routing (1996)
   - Crowds (1998)
   - Single proxy (90s) (Penet pseudonymous
       remailer (1993-1996), Anonymizer, SafeWeb)
   - Anonymous Remailer (Cipherpunk Type 0, Type
       1, Mixmaster Type 2 (1994), Mixminion Type 3
       (2003))
   - Low-latency communication (Freedom

   ###### X X X


   Linee Guida per la modellazione delle minacce ed individuazione delle azioni di mitigazione conformi ai principi del Secure/Privacy

Network (1999-2001), Java Anon Proxy (JAP) (2000), Tor (2004))

::

   - DC-net & MIX-net + dummy traffic
   - ISDN-mixes

   ###### X X X X

   - Broadcast systems + dummy traffic **X X X**

   Privacy preserving
   authentication

   - Private authentication
   - Anonymous credentials (single show, multi
       show)

   ###### X X

   - Deniable authentication **X**^ **X**^ **X**^
   - Off-the-record messaging **X X X X**

   Privacy preserving
   cryptographic protocols

Multi-party computation (Secure function evaluation)

::

   ###### X X

Anonymous buyer-seller watermarking protocol X X X

::

   Information retrieval Private information retrieval + dummy traffic **X X X**

Oblivious transfer X X X

::

Privacy preserving data mining X X X

::

   - Searchable encryption
   - Private search

   ###### X X

   Data anonymization • K-anonymity model

   - l-Diversity

   ###### X X

   Information hiding Steganography **X X X**

Covert communication X X X

::

Spread spectrum X X X

::

   Pseudonymity systems Privacy enhancing identity management system **X X**

User-controlled identity management system X X

::

Privacy preserving biometrics X X X

::

   Encryption techniques Symmetric key & public key encryption **X**

Deniable encryption X X

::

Homomorphic encryption X

::

Verifiable encryption X

::

   Access control
   techniques

Context-based access control X

::

Privacy-aware access control X

::

   Policy and feedback tools Policy communication (P3P) **X**

Policy enforcement (XACML, EPAL) X

::

Feedback tools for user privacy awareness X

::

Data removal tools (spyware removal, browser cleaning tools, activity
traces eraser, harddisk data

::

   ###### X


   Linee Guida per la modellazione delle minacce ed individuazione delle azioni di mitigazione conformi ai principi del Secure/Privacy

eraser) Tabella 20 - Mappatura tra obiettivi e tecniche di miglioramento
della privacy

::

   * **U** –Unlinkability, **A** –Anonymity/Pseudonymity, **P** –Plausible deniability, **D** –Undetectability/unobservability,
   **C** –Confidentiality, **W** –Content Awareness, **O** –Policy and consent compliance of the system

   ##### 4.5.3.2 PRoPAN ...................................................................................................................................................................

   Beckers et al. [4] ha creato un approccio in quattro fasi per l'identificazione semiautomatica delle minacce
   alla privacy. Il metodo ProPAn (Problem-based Privacy Analysis) contribuisce nella produzione dei requisiti
   di protezione della privacy ed è un approccio basato su problemi per l'identificazione semiautomatica delle
   minacce alla privacy durante l'analisi dei requisiti dei sistemi software. L'obiettivo di questa metodologia è
   quello di assistere gli ingegneri del software nella requisitazione al fine di ottenere le seguenti informazioni:

   - conoscenza del settore rilevante per la privacy;
   - dati personali trattati;
   - requisiti di riservatezza.

   La metodologia consiste in quattro fasi:

   - Disegno del diagramma di contesto e dei diagrammi dei problemi,
   - Aggiunta dei requisiti di privacy al modello,
   - Generazione di grafici delle minacce alla privacy,
   - Analisi dei grafici delle minacce alla privacy.

   Riferimento bibliografico: Kristian Beckers, Stephan Faßbender, Maritta Heisel, and Rene Meis. A Problem-
   based Approach for Computer Aided Privacy Threat Identification. In Privacy Technologies and Policy,
   volume 8319 of LNCS, pages 1–16. Springer, 2014.

   ##### 4.5.3.3 PriS ..........................................................................................................................................................................

   PriS [5] è un metodo di ingegnerizzazione dei requisiti di sicurezza, che integra i requisiti di riservatezza già
   nelle fasi iniziali del processo di sviluppo del sistema. PriS considera i requisiti relativi alla privacy come
   obiettivi organizzativi che devono essere soddisfatti e adotta l'uso di modelli di processi di privacy come un
   modo per:

   1. descrivere l'effetto dei requisiti relativi alla privacy sui processi aziendali;
   2. facilitare l'identificazione dell'architettura di sistema che meglio supporta i processi aziendali in
       relazione agli aspetti di privacy.

   In questo modo, PriS fornisce un approccio olistico che va dagli obiettivi di alto livello ai sistemi informatici
   "rispettosi della privacy". Il metodo si articola in quattro fasi:

   - individuare gli obiettivi di tutela della privacy,
   - analizzare l' impatto degli obiettivi di tutela della privacy sui processi organizzativi,
   - modellare i processi interessati utilizzando modelli di tutela della privacy
   - identificare le tecniche che meglio supportano o implementano i processi summenzionati.

   Riferimento bibliografico: Christos Kalloniatis, Evangelia Kavakli, and Stefanos Gritzalis. Addressing privacy
   requirements in system design: the PriS method. Requirements Engineering, 13(3):241–255, 2008.

   ##### 4.5.3.4 FPFSD ......................................................................................................................................................................

   Spiekermann e Cranor [6] hanno sviluppato un framework denominato (FPFSD). Questo è un framework
   per la progettazione di sistemi rispettosi della privacy (framework for privacy-friendly system design) in cui
   si attua una distinzione tra due diversi approcci alla privacy:


   Linee Guida per la modellazione delle minacce ed individuazione delle azioni di mitigazione conformi ai principi del Secure/Privacy

   - Privacy-by-policy, introduce l'approccio di notifica e consenso basato sui principi di Fair Information
       Practice Principles (FIPP) e implica che l'utente sia informato su quali informazioni vengono
       utilizzate e perché. Inoltre, l'utente può decidere di non fornire dati.
   - Privacy-by-architecture, incoraggia l'archiviazione dei dati presso il cliente invece di far archiviare le
       informazioni riservate dalle aziende stesse.

   Riferimento bibliografico: Sarah Spiekermann and Lorrie F. Cranor. Engineering privacy. IEEE Transactions
   on Software Engineering, 35(1):67–82, 2009.

   ##### 4.5.3.5 MPRA ......................................................................................................................................................................

   Gürses [7] propone una tecnica multilaterale per l'analisi dei requisiti in materia di tutela della privacy
   (multilateral privacy requirements analysis technique). Si articola in tre fasi principali: analisi degli
   stakeholder, analisi funzionale e analisi della privacy. In primo luogo vengono determinati gli attori e le parti
   interessate. Per ciascuno di questi, vengono determinati gli obiettivi funzionali che vengono poi collegati
   alle ipotesi di dominio. Viene inoltre creato un modello informativo. Nella fase finale, le problematiche sulla
   privacy sono determinate in base a ciascun stakeholder, in relazione al modello informativo e agli obiettivi
   funzionali individuati nella fase precedente. Tali problematiche possono anche tradursi in minacce alla
   privacy e documentate come casi di abuso. Infine, le problematiche (o minacce) vengono trasformate in
   obiettivi di tutela privacy come un'approssimazione giustificabile.

   Riferimento bibliografico: Fahriye Seda Gürses. Multilateral privacy requirements analysis in online social
   network services. PhD thesis, Department of Computer Science, KU Leuven, 2010.

   ##### 4.5.3.6 Privacy in the Cloud ................................................................................................................................................

   Mouratidis et al. [8] pone in particolare l’attenzione sulle applicazioni cloud proponendo un framework che
   supporta l'elicitazione dei requisiti di sicurezza e privacy. Il framework è composto da un linguaggio (basato
   su Secure Tropos) e da un processo (basato su PriS) a supporto dell'analisi della sicurezza e della privacy. Il
   processo si articola in tre fasi. Il primo passo (facoltativo) è la catalogazione delle minacce alla sicurezza e
   alla privacy, che mira a creare un punto di riferimento basato sull'esperienza passata da utilizzare poi
   successivamente. In secondo luogo, l'attività di analisi della sicurezza e della privacy consiste in due sotto-
   attività: la definizione del contesto organizzativo, in cui vengono identificati gli obiettivi organizzativi, gli
   attori e le dipendenze, i piani e le risorse e gli obiettivi di sicurezza e privacy; e la definizione delle possibili
   problematiche in materia di sicurezza e privacy, che consiste nell'identificare i requisiti, le misure e i
   meccanismi di sicurezza e privacy. Il terzo e ultimo passo è la selezione del provider dei servizi cloud in base
   al grado di soddisfazione dei meccanismi di sicurezza e privacy ottenuti dai potenziali fornitori cloud.
   Sebbene si tratti di un framework che fornisce procedure dettagliate per analizzare i requisiti di sicurezza e
   privacy, non è disponibile alcuna conoscenza reale della sicurezza e della privacy.

   Riferimento bibliografico: Haralambos Mouratidis, Shareeful Islam, Christos Kalloniatis, and Stefanos
   Gritzalis. A framework to support selection of cloud providers based on security and privacy requirements.
   Journal of Systems and Software, pages 2276–2293, 2013.

   ##### 4.5.3.7 Adaptive privacy .....................................................................................................................................................

   Omoronyia et al. [9] propone un framework di riferimento per supportare la divulgazione selettiva delle
   informazioni personali da parte di applicazioni software in un contesto in continuo cambiamento. Il
   framework si concentra sui requisiti di sensibilizzazione alla privacy (PAR - privacy awareness requirements)
   e descrive:

   1. come identificare gli attributi da monitorare per rilevare le minacce alla privacy,
   2. come scoprire le minacce alla privacy prima della divulgazione delle informazioni personali,
   3. come determinare la gravità, così come i benefici relativi a una minaccia scoperta.
   Il quadro normativo richiede tuttavia che i requisiti di riservatezza di tutti gli agenti siano già definiti e non
   fornisce indicazioni su come ottenerli.


   Linee Guida per la modellazione delle minacce ed individuazione delle azioni di mitigazione conformi ai principi del Secure/Privacy

   Riferimento bibliografico: Inah Omoronyia, Luca Cavallaro, Mazeiar Salehie, Liliana Pasquale, and Bashar
   Nuseibeh. Engineering adaptive privacy: on the role of privacy awareness requirements. In Proceedings of
   the 2013 International Conference on Software Engineering, ICSE ’13, pages 632–641. IEEE Press, 2013.

   ##### 4.5.3.8 STRAP ......................................................................................................................................................................

   STRAP [10] è un framework di analisi della privacy che è stato sviluppato sulla base dei risultati dell'analisi
   di sei framework esistenti (modelli di rischio [16], Patrick e Kenny [17], framework i* [18], Langheinrich
   [19], Bellotti e Sellen [20], e valutazione euristica [21]). Si tratta di un metodo a cinque fasi, che consiste in
   una analisi orientata agli obiettivi, analisi della vulnerabilità, perfezionamento e progettazione degli
   obiettivi, valutazione del progetto e iterazione. La fase di analisi della vulnerabilità è la fase principale in cui
   vengono combinati i framework esistenti. L'analisi si basa su una serie di domande analitiche per
   determinare la cattura e l'uso delle informazioni. In secondo luogo, viene utilizzata l'euristica per
   identificare potenziali problemi basati su difetti e requisiti comuni. Queste euristiche possono essere
   classificate secondo le FIPP degli Stati Uniti: notice/awareness, choice/consent, integrity/security,
   enforcement/redress. Sebbene queste categorie, basate sulla legislazione e sugli orientamenti in materia di
   protezione dei dati, siano molto importanti dal punto di vista della tutela della privacy, non tengono conto
   delle proprietà fondamentali quali l'anonimato, la non collegabilità e la non rilevabilità.

   Riferimento bibliografico: Carlos Jensen. Designing for privacy in interactive systems. PhD thesis, Georgia
   Institute of Technology, 2005.

   ##### 4.5.3.9 Microsoft privacy guidelines ...................................................................................................................................

   Le linee guida sulla privacy fornite da Microsoft descrivono alcuni concetti basilari di privacy [11], come
   diversi tipi di consenso o concetti di minimizzazione dei dati. Inoltre, per gli scenari selezionati vengono
   presentate alcune linee guida riguardanti i seguenti principi: avviso, scelta, trasferimento successivo,
   accesso, sicurezza e integrità dei dati. Tuttavia, contiene solo un elenco piatto degli orientamenti richiesti e
   raccomandati e non intende descrivere un approccio più strutturato. Queste linee guida possono essere
   utilizzate come ispirazione per determinare le possibili minacce, ad esempio per ampliare il catalogo degli
   alberi delle minacce^19.

   Riferimento bibliografico: Privacy guidelines for developing software products and services, version 3.1.
   Technical report, Microsoft Coorporation, Sept 2008.
   [http://download.microsoft.com/download/0/8/2/082448D8-2AED-45BC-A9A0-](http://download.microsoft.com/download/0/8/2/082448D8-2AED-45BC-A9A0-)
   094840E9E3A2/Microsoft_and%20Privacy_guidelines_for_developers.doc.

   ##### 4.5.3.10 PRET ......................................................................................................................................................................

   Miyazaki et al. [12] ha definito una tecnica di elicitazione dei requisiti di riservatezza informatizzata,
   denominata (PRET - privacy requirements elicitation technique). Questa tecnica restituisce i requisiti
   necessari affinché il sistema sia conforme alla legge, sulla base di un questionario compilato dall'ingegnere
   di sistema.

   Riferimento bibliografico: Seiya Miyazaki, Nancy Mead, and Justin Zhan. Computer-aided privacy
   requirements elicitation technique. Asia-Pacific Conference on Services Computing (APSCC’08), pages 367–
   372, 2008.

   (^19) [http://download.microsoft.com/download/0/8/2/082448D8-2AED-45BC-A9A0-](http://download.microsoft.com/download/0/8/2/082448D8-2AED-45BC-A9A0-)
   094840E9E3A2/Microsoft_and%20Privacy_guidelines_for_developers.doc.


   Linee Guida per la modellazione delle minacce ed individuazione delle azioni di mitigazione conformi ai principi del Secure/Privacy

   ## 5 LINEE GUIDA PER L’INDIVIDUAZIONE E LA RIVISITAZIONE DEI REQUISITI DI SICUREZZA E DI PRIVACY APPLICATIVI

   ### 5.1 Linee guida per la modellazione delle minacce

   #### 5.1.1 Identificazione degli obiettivi di sicurezza

   La sicurezza dei dati è assicurata quando vengono assicurate tre caratteristiche di fruizione di questi ultimi,
   che sono la riservatezza, l’integrità e la disponibilità.

   Per raggiungere la sicurezza vengono eseguite azioni, che in caso di:

   - riservatezza, proteggono i dati al fine di contrastare la divulgazione non autorizzata;
   - integrità, contrastano le modifiche non autorizzate dei dati;
   - disponibilità, contrastano la indisponibilità malevola dei dati/servizi.

   Gli obiettivi specifici di sicurezza sono un sottoinsieme degli obiettivi di progetto e dovrebbero essere
   utilizzati per guidare gli sforzi impiegati nella modellazione delle minacce.

   Identificare i principali obiettivi di sicurezza permette di concentrarsi con maggiore attenzione sulle aree da
   proteggere. Ad esempio, se si identificano i dettagli del profilo cliente come dati riservati, che devono
   essere protetti, è possibile esaminare la modalità di archiviazione sicura di tali dati e il modo in cui l'accesso
   a tali dati viene controllato e verificato.

   Per determinare gli obiettivi di protezione, occorre porsi le seguenti domande:

   - quali dati occorre proteggere?
   - Esistono requisiti di conformità? I requisiti di conformità possono includere criteri di protezione,
       leggi sulla privacy, regolamenti e standard.
   - Esistono requisiti di qualità specifici del servizio? I requisiti di qualità del servizio includono
       tipicamente la disponibilità e i requisiti prestazionali.
   - Esistono beni immateriali che devono essere protetti? Tali beni includono ad esempio, la
       reputazione dell’organizzazione, le informazioni commerciali sensibili e la proprietà intellettuale.

   Di seguito sono riportati alcuni esempi di obiettivi di sicurezza comuni:

   - impedire agli aggressori di ottenere dati sensibili, inclusi i codici di accesso e le informazioni sul
       profilo.
   - Soddisfare gli accordi a livello di servizio per la disponibilità delle applicazioni.
   - Proteggere la credibilità dell’organizzazione.

   #### 5.1.2 Creazione di un disegno ad alto livello dell’applicazione

   La modellazione delle minacce è un processo iterativo di analisi, dove ad ogni ciclo si scende sempre più in
   dettaglio, identificando di livello in livello le funzionalità chiave dell’applicazione, le sue caratteristiche ed i
   dati da proteggere.

   Per avere una panoramica dell'applicazione occorre:

   - Disegnare lo scenario di sviluppo dall’inizio alla fine;
   - Identificare i ruoli;
   - Identificare gli scenari d’ uso più significativi;
   - Identificare le tecnologie;
   - Identificare i meccanismi di sicurezza.

   Di seguito sono riportati i dettagli di ciascuna fase.


   Linee Guida per la modellazione delle minacce ed individuazione delle azioni di mitigazione conformi ai principi del Secure/Privacy

   **Disegnare lo scenario di sviluppo dall’inizio alla fine** - La prima attività consiste in una modellazione ad alto
   livello dell’applicazione (composizione e struttura dell'applicazione, relativi sottosistemi e caratteristiche di
   distribuzione). Dopo il primo disegno, si aggiungono i dettagli sui meccanismi di autenticazione,
   autorizzazione e comunicazione. Da notare che quando si inizia la modellazione non sempre si è a
   conoscenza di tutti i dettagli per cui deve essere sempre possibile ritornare sull’aspetto sotto analisi in un
   secondo momento per approfondire ulteriormente.

   La figura che segue riporta l’esempio di un diagramma iniziale che mostra l'architettura di una applicazione
   con alcuni dettagli.

Figura 8 - Esempio di disegno architetturale di una applicazione

::

   In generale il disegno architetturale deve evidenziare i seguenti elementi:

   - Topologia fisica e logica dei componenti: il collocamento dei server in rete (Intranet, Extranet e
       accesso a Internet). Iniziare con le topologie di rete logiche, per poi visualizzare le relative topologie
       fisiche quando si dispone di tali dettagli. È possibile aggiungere o rimuovere le minacce a seconda
       della scelta di topologie fisiche.
   - Livelli logici: il livello di presentazione (front-end), il livello di business (back-end) e i livelli di
       accesso ai dati. Successivamente occorre rifinire per includere, una volta noti, i limiti fisici del
       server;
   - Componenti chiave: i componenti importanti all'interno di ogni livello logico. In questa fase è
       possibile includere i limiti reali del componente e di processo una volta conosciuti;
   - Servizi chiave: eventuali servizi importanti. Una volta noti, da mostrare come processi;
   - Porte e protocolli di comunicazione: i server, i componenti e i servizi che comunicano tra di loro e
       come lo fanno. Da mostrare le specifiche dei pacchetti informativi in entrata e in uscita, una volta
       individuati;
   - Identità: le identità utente principali usate all’interno dell'applicazione e gli eventuali profili di
       servizio rilevanti;
   - Dipendenze esterne: le dipendenze dell’applicazione da eventuali sistemi esterni. Elencare queste
       dipendenze è utile per individuare eventuali vulnerabilità che potrebbero insorgere in un secondo
       momento se alcune assunzioni fatte inizialmente sul generico sistema esterno dovessero risultare
       non più vere o in qualche modo cambiate.

   È importante revisionare il disegno del sistema nel corso del tempo per verificare se tutti gli elementi
   individuati siano ancora come descritti, se devono essere cambiati o se hanno bisogno di un ulteriore livello
   di dettaglio.


   Linee Guida per la modellazione delle minacce ed individuazione delle azioni di mitigazione conformi ai principi del Secure/Privacy

   ##### 5.1.2.1 Identificazione dei Ruoli .........................................................................................................................................

   È importante identificare i ruoli all’interno dell’applicazione, ossia, chi può fare cosa.

   La fase di identificazione dei ruoli è utilizzata sia per determinare ciò che dovrebbe accadere (accesso alle
   risorse autorizzate come stabilito per lo specifico ruolo) che per determinare ciò che non dovrebbe
   accadere (accesso a risorse per le quali non si ha l’autorizzazione).

   L'assegnazione dei ruoli deve essere centralizzata e a ciascun ruolo deve essere associato un profilo
   ‘autorizzativo’ che regolamenta i comandi, le transazioni e gli accessi ai dati.

   Per ridurre la superficie d’attacco è necessario stabilire quali devono essere i privilegi minimi per ogni
   componente dell’applicazione. Nella gestione della sicurezza delle risorse (quali DB, Active Directory, file,
   etc.), i ruoli applicativi devono essere quindi stabiliti a partire dalla logica di business con l’obiettivo di
   delimitare il perimetro di azione nell’accesso alla risorsa.

   ##### 5.1.2.2 Identificare gli Scenari d’Uso Chiave .......................................................................................................................

   In questa fase occorre identificare le principali funzionalità e modalità d’uso e dettagliare gli aspetti legati
   alle attività di creazione, lettura, aggiornamento e cancellazione dei dati. Le caratteristiche chiave vengono
   spesso descritte nel contesto dei casi d’uso e permettono di far capire come l’applicazione è destinata ad
   essere utilizzata e come può essere utilizzata in modo improprio. I casi d’uso consentono di identificare i
   flussi di dati e di focalizzarsi sull’analisi di eventuali minacce nelle fasi successive di dettaglio della
   modellizzazione.

   ##### 5.1.2.3 Identificare le Tecnologie .......................................................................................................................................

   Occorre identificare tutte le tecnologie utilizzate e le loro caratteristiche: Sistemi operativi; Server Web;
   Server di Base Dati; le tecnologie utilizzate per implementare la presentazione dei dati a livello utente, per
   gestire le regole di business, per l’accesso ai dati sottostanti e il linguaggio di sviluppo utilizzato.

   L’identificazione delle tecnologie consente di concentrarsi in un momento successivo alla modellizzazione
   delle minacce che possono nascere, legate alle specifiche tecnologie in uso. Inoltre, aiuta a determinare le
   eventuali tecniche di mitigazione del rischio.

   ##### 5.1.2.4 Identificare Meccanismi di Sicurezza Applicativa ...................................................................................................

   Un’altra fase importante è l’identificazione dei meccanismi di sicurezza applicativa, in particolare occorre
   analizzare i seguenti aspetti:

   - Validazione input e dati;
   - Autenticazione;
   - Autorizzazione;
   - Gestione della configurazione;
   - Dati sensibili;
   - Gestione della sessione;
   - Crittografia;
   - Manipolazione dei parametri;
   - Gestione delle eccezioni;
   - Audit e gestione dei log.

   Lo scopo dell’identificazione di questi elementi è quello di aggiungere il più possibile ulteriori dettagli,
   anche poco conosciuti. Ad esempio è utile documentare come l'applicazione viene autenticata dalla base
   dati o come gli utenti vengono autorizzati, oppure quali sono le aree preposte all’autenticazione e
   l’autorizzazione.


   Linee Guida per la modellazione delle minacce ed individuazione delle azioni di mitigazione conformi ai principi del Secure/Privacy

   #### 5.1.3 Scomposizione dell’applicazione

   La scomposizione dell’applicazione è utile per scoprire le minacce e le vulnerabilità del sistema. Nell’ottica
   di sicurezza, i componenti più importanti sono:

   - confini di fiducia (trust boundaries);
   - flussi di dati;
   - punti di ingresso (entry points);
   - punti di uscita (exit points).

   ##### 5.1.3.1 Confini di fiducia (Trust boundaries) ......................................................................................................................

   Identificare i confini di fiducia dell’applicazione aiuta a concentrare l'analisi sulle aree di maggiore interesse.
   I confini di fiducia evidenziano dove cambiano i livelli di fiducia. In quest’ambito, la fiducia è intesa in chiave
   di riservatezza e integrità. Ad esempio, una modifica nei livelli di controllo di accesso all'applicazione, dove
   è necessario un livello o un privilegio specifico per accedere a una risorsa o un'operazione, sarebbe una
   modifica del livello di fiducia. Un altro esempio, potrebbe essere in un punto di entrata nell’applicazione
   ove è necessario filtrare i dati di accesso.

   Per identificare i confini di fiducia occorre:

   - Iniziare individuando i confini del sistema esterno. Ad esempio, l'applicazione può scrivere un file
       sul server X, può effettuare chiamate al database sul server Y e può chiamare il servizio Web Z.
       Questo definisce il tuo limite di sistema.
   - Identificare i punti di controllo di accesso o i luoghi chiave in cui l'accesso richiede privilegi
       aggiuntivi o l'appartenenza ad un dato ruolo. Ad esempio, l’accesso ad una pagina particolare,
       potrebbe essere limitata ai soli dirigenti, nel qual caso richiederebbe un accesso autenticato e
       inoltre che l’utente ricopra un certo ruolo.
   - Identificare i confini di fiducia da una prospettiva di flusso di dati. Per ogni sottosistema,
       considerare se il flusso di dati a monte o l'input dell'utente sia affidabile e se non lo è, considerare
       in che modo il flusso di dati e l'input possono essere autenticati e autorizzati. Conoscere quali punti
       di ingresso esistono tra i confini di fiducia, consente di concentrare l'identificazione delle minacce in
       questi punti chiave di accesso.

   Alcuni esempi di confini di fiducia sono: un firewall perimetrale, il confine tra il web server e il server di
   base dati, punti di ingresso di componenti aziendali che espongono dati privilegiati, dunque, protetti da
   ulteriori controlli di accesso, il limite tra l’applicazione e i servizi di terze parti.

   ##### 5.1.3.2 Flussi di Dati ............................................................................................................................................................

   È importante tracciare il flusso dei dati all’interno dell’applicazione dal punto di ingresso al punto d’uscita.
   Questa attività è necessaria per comprendere come interagisce l’applicazione con i sistemi esterni, i sistemi
   client e come interagiscono i componenti interni. È importante anche, prestare particolare attenzione al
   flusso di dati che attraversa i confini di fiducia e come tali dati vengono convalidati nel punto di entrata.
   Inoltre occorre fare molta attenzione ai dati sensibili e come questi attraversano il sistema, se passano
   attraverso una rete e/o se sono persistenti. Un buon approccio è quella di analizzare il flusso dei dati tra i
   singoli sottosistemi a partire dal livello più alto e poi via via a scendere ai livelli più bassi.

   ##### 5.1.3.3 Punti d’Ingresso (Entry Points) ...............................................................................................................................

   I punti di ingresso dell'applicazione servono anche come punti di ingresso per gli attacchi. Il front-end di
   una applicazione web che è in ascolto di richieste http è un esempio di punto di ingresso vulnerabile agli
   attacchi. Questo punto di ingresso è destinato ad essere esposto agli utilizzatori. Altri punti di ingresso,
   come i punti di accesso interni esposti dai sotto componenti negli strati dell'applicazione, possono esistere
   solo per supportare la comunicazione interna con altri componenti. Tuttavia, occorre conoscere dove sono


   Linee Guida per la modellazione delle minacce ed individuazione delle azioni di mitigazione conformi ai principi del Secure/Privacy

   localizzati e quali tipi di input ricevono nel caso in cui un aggressore riesca ad aggirare l’interfaccia
   dell'applicazione e attaccare direttamente un punto di ingresso interno.

   A titolo di esempio si elencano di seguito ulteriori esempi di Entry Points:

   - Front-e nd applicativo (form di Login, form di Ricerca);
   - Funzioni applicative (funzione di login, web service esposti, ..);
   - Console di amministrazione del database;
   - External reporting;
   - Porte TCP/UDP (network socket).

   ##### 5.1.3.4 Punti di Uscita (Exit Points) .....................................................................................................................................

   È importante identificare da dove l'applicazione invia i dati all’utente o ai sistemi esterni, dando priorità ai
   punti di uscita in cui l'applicazione scrive dati che includono l'input proveniente dall’utente o dati
   provenienti da fonti non attendibili, ad esempio basi dati condivise.

   A titolo di esempio si elencano di seguito ulteriori esempi di Exit Points:

   - File di Log;
   - Database;
   - Interfacce esterne (es. web service).

   #### 5.1.4 Identificazione delle minacce

   In questa fase, è possibile individuare minacce e attacchi che potrebbero compromettere l'applicazione e
   gli obiettivi di sicurezza. Il processo di identificazione consiste in sessioni di brainstorming tra i team di
   sviluppo e test. Idealmente, il team di lavoro è costituito da architetti applicativi, professionisti della
   sicurezza, sviluppatori, tester e amministratori di sistema.

   Esistono due approcci per affrontare questa fase:

   - Iniziare, elencando minacce e attacchi comuni. Con questo approccio, si inizia con un elenco di
       minacce comuni raggruppate per categorie di vulnerabilità. Successivamente, occorre adattare tale
       elenco alla propria architettura. Ad esempio, utilizzare gli scenari identificati per esaminare i flussi
       di dati, prestando particolare attenzione ai punti di ingresso e in particolare a quelli che
       attraversano i confini di fiducia. In questo modo si potranno eliminare immediatamente alcune
       minacce, in quanto non applicabili ai casi d’uso.
   - Utilizzare un approccio basato su domande. Un approccio basato su questionari può aiutare a
       identificare le minacce e i possibili attacchi. La categorizzazione STRIDE si basa su categorie di
       minacce molto estese, quali spoofing (assunzione impropria di identità), manomissione di dati,
       ripudio, divulgazione indesiderata di informazioni e interruzione di servizio. Il modello STRIDE deve
       essere usato per porre domande relative a qualsiasi aspetto dell'architettura e del design
       dell'applicazione. Questo è un approccio basato su obiettivi, in cui si prendono in considerazione
       tutti gli obiettivi di un possibile aggressore (punto di vista di un attaccante).

   Per identificare le minacce, si esaminano tutti i livelli dell’applicazione, livello per livello e funzione per
   funzione. Ponendo l’attenzione sulle categorie di vulnerabilità, ci si concentra sulle aree in cui vengono
   spesso effettuati errori di sicurezza. Occorre identificare le potenziali minacce e le possibili azioni che un
   aggressore potrebbe tentare di utilizzare per sfruttare le vulnerabilità a cui l'applicazione è esposta.
   Durante questa attività di identificazione delle minacce si eseguono le seguenti attività:

   - Identificazione delle minacce e degli attacchi comuni.
   - Identificazione delle minacce annidate nei casi d’uso.
   - Identificazione delle minacce annidate nei flussi di dati.


   Linee Guida per la modellazione delle minacce ed individuazione delle azioni di mitigazione conformi ai principi del Secure/Privacy

   ##### 5.1.4.1 Identificazione delle minacce e attacchi comuni ....................................................................................................

   Esistono una serie di minacce e attacchi comuni che si basano su vulnerabilità di carattere comune. Questa
   sezione identifica una serie di domande chiave da porsi per ciascuna categoria.

   Autenticazione:

   - Come potrebbe un aggressore rubare una identità?
   - Come potrebbe un utente malintenzionato accedere all'archivio delle credenziali?
   - Come potrebbe un aggressore portare un attacco? Come vengono memorizzate le credenziali
       dell'utente e quali criteri di codici di accesso vengono applicati?
   - Come può un utente malintenzionato modificare, intercettare o eludere il meccanismo di
       reimpostazione delle credenziali dell'utente?

   Autorizzazione:

   - Come potrebbe un utente malintenzionato influenzare i controlli di autorizzazione per accedere a
       operazioni privilegiate?
   - Come potrebbe un utente malintenzionato elevare i privilegi?

   Input e dati di convalida:

   - Come potrebbe un utente malintenzionato iniettare comandi SQL?
   - Come potrebbe un utente malintenzionato eseguire un attacco di cross-site scripting?
   - Come potrebbe un utente malintenzionato ignorare la validazione degli input?
   - Come potrebbe un utente malintenzionato inviare un input non valido per influenzare la logica di
       protezione adottata sul server?
   - Come potrebbe un utente malintenzionato inviare un errore di input per bloccare l'applicazione?

   Gestione della configurazione:

   - Come potrebbe un utente malintenzionato accedere alle funzioni di amministratore delle
       configurazioni?
   - Come potrebbe un utente malintenzionato accedere ai dati di configurazione dell’applicazione?

   Dati sensibili:

   - Dove e come l’applicazione memorizza i dati sensibili?
   - Quando e in quale punto i dati sensibili vengono passati attraverso la rete?
   - Come potrebbe un utente malintenzionato visualizzare i dati sensibili?
   - Come potrebbe un utente malintenzionato manipolare i dati sensibili?

   Gestione delle sessioni:

   - Si utilizza un algoritmo di crittografia personalizzato e ci si fida di tale algoritmo?
   - Come potrebbe un aggressore prendere il controllo di una sessione utente?
   - Come potrebbe un utente malintenzionato visualizzare o modificare lo stato della sessione di un
       altro utente?

   Crittografia:

   - Di cosa ha bisogno un aggressore per superare il meccanismo di crittografia adottato?
   - Come potrebbe un utente malintenzionato ottenere l'accesso alle chiavi crittografiche?
   - Quali standard crittografici si stanno utilizzando? Quali sono gli attacchi noti su questi standard?
   - Si vuole adottare un proprio meccanismo di crittografia?


   Linee Guida per la modellazione delle minacce ed individuazione delle azioni di mitigazione conformi ai principi del Secure/Privacy

   - In che modo la tipologia di distribuzione potenzialmente influenzerà la scelta dei metodi
       crittografici?

   Manipolazione dei parametri:

   - In che modo un aggressore potrebbe manipolare i parametri per influenzare la logica di protezione
       implementata sul server?
   - Come potrebbe un utente malintenzionato manipolare i dati sensibili presenti nei parametri?

   Gestione delle eccezioni:

   - Come potrebbe un utente malintenzionato bloccare l'applicazione?
   - Come potrebbe un utente malintenzionato ottenere dettagli utili ai propri fini?

   Revisione e registrazione (audit):

   - Come potrebbe un aggressore coprire le sue tracce?
   - Come si può dimostrare che un utente malintenzionato (o un utente legittimo) ha eseguito azioni
       specifiche?

   ##### 5.1.4.2 Identificazione delle potenziali minacce annidate nei casi d’uso ...........................................................................

   Occorre esaminare i casi d’uso chiave, che sono stati individuati nella fasi precedenti, per capire il modo in
   cui un utente potrebbe influenzare malevolmente o involontariamente l'applicazione ad eseguire
   un'operazione non autorizzata o a divulgare dati riservati o privati. In questa fase ci si pongono domande
   immedesimandosi nella figura dell’aggressore. Alcuni esempi di domande da porsi:

   - Come può un utente iniettare un input dannoso in questo caso d’uso?
   - I dati vengono pubblicati in base all’input da parte dell'utente o in base all’input non validato da
       parte dell’utente?
   - In che modo un aggressore potrebbe manipolare i dati della sessione?
   - Come potrebbe un utente malintenzionato ottenere dati sensibili quando vengono trasmessi
       attraverso la rete?
   - In che modo un aggressore potrebbe eludere i controlli di autorizzazione?

   ##### 5.1.4.3 Identificazione delle potenziali minacce annidate nei flussi di dati ........................................................................

   Occorre rivedere i casi d’uso e gli scenari chiave e analizzare i flussi di dati, in particolare, i flussi di dati tra i
   singoli componenti dell’architettura. Il flusso di dati che attraversa i confini di fiducia è richiede particolare
   attenzione. Nella stesura del codice, si deve assumere che, tutti i dati esterni al confine di fiducia
   dell’applicativo siano dannosi. Nel codice si dovrebbe eseguire una validazione dei dati molto esaustiva. Per
   identificare le minacce associate ai flussi di dati, ci si deve porre le seguenti domande:

   - Quale è il percorso del flusso di dati dal front-end al back-end dell’applicazione?
   - Quali componenti chiamano altri componenti?
   - Quale aspetto hanno i dati validi?
   - Dove viene eseguita la validazione dei dati?
   - Quali sono i vincoli imposti ai dati?
   - Come vengono validati i dati in base ai parametri previsti in termini di lunghezza, intervallo valori,
       formato e tipo?
   - Quali dati sensibili vengono trasmessi tra i componenti dell’applicazione e attraverso le reti, e come
       vengono protetti durante il transito?

   L’uso della documentazione quali ad esempio, i diagrammi DFD e i diagrammi di sequenza UML, aiuta
   nell’analisi dell'applicazione e nell’identificazione dei flussi di dati.


   Linee Guida per la modellazione delle minacce ed individuazione delle azioni di mitigazione conformi ai principi del Secure/Privacy

   ##### 5.1.4.4 Esplorare minacce ulteriori usando gli alberi delle minacce/attacchi ....................................................................

   Vedi Paragrafo 5.2.4.2.

   #### 5.1.5 Identificazione delle vulnerabilità................................................................................................................

   Così come è stato fatto nel processo di identificazione delle minacce, si fornisce di seguito una rassegna
   delle diverse categorie di vulnerabilità. In questa fase, l’obiettivo è quello di analizzare le vulnerabilità (le
   minacce sono state già trattate nel paragrafo precedente) partendo dal principio che per poter analizzare
   correttamente un’applicazione è necessario valutare le sue vulnerabilità ad ogni livello.

   Di seguito alcuni esempi di domande da porsi a secondo della fase.

   Autenticazione:

   - I nomi utente e le password sono inviati in chiaro su un canale non protetto? Si utilizza una
       crittografia ad hoc per informazioni sensibili?
   - Le credenziali sono memorizzate? Se vengono memorizzate, come vengono memorizzate e
       protette?
   - Viene imposto l’uso di strong authentication? Quali altre norme sull’uso dei codici di accesso
       vengono applicate?
   - Come vengono verificate le credenziali?
   - Come viene identificato l'utente autenticato dopo l'accesso iniziale?

   Occorre rivedere l'autenticazione cercando una corrispondenza tra le seguenti vulnerabilità di carattere
   comune:

   - Le credenziali di autenticazione o cookie di autenticazione vengano passate su collegamenti di rete
       non crittografati, che possono portare al furto delle credenziali o della sessione;
   - Si fa uso di codici d’accesso e procedure di accesso deboli, che possono portare ad un accesso non
       autorizzato;
   - Si fa uso di dati personali come forma di autenticazione.

   Autorizzazione:

   - Quali controlli di accesso vengono utilizzati nei punti di accesso dell'applicazione?
   - L’applicazione prevede l’uso di ruoli? Se utilizza ruoli, sono sufficientemente granulari ai fini del
       controllo degli accessi?
   - L’inserimento erroneo di un codice di accesso fallisce in maniera sicura?
   - È possibile limitare l'accesso alle risorse di sistema?
   - Vengono attuate politiche restrittive nell'accesso alla base dati?
   - Quale procedura di autorizzazione viene adottata a livello di base dati?

   Occorre esaminare l'autorizzazione cercando una corrispondenza tra le seguenti vulnerabilità di carattere
   comune:

   - Si fa uso di ruoli e profili utente sovra privilegiati;
   - Granularità di ruoli insufficiente;
   - Non viene attuata alcuna restrizione di accesso alle risorse di sistema o viene attuata limitatamente
       ad alcuni profili.

   Inserimento e Validazione Dati:

   - Occorre identificare le vulnerabilità nella convalida dei dati di ingresso e dei dati in generale,
       domandandosi quanto segue:


   Linee Guida per la modellazione delle minacce ed individuazione delle azioni di mitigazione conformi ai principi del Secure/Privacy

o I dati di ingresso vengono tutti validati? o I dati di ingresso,
vengono validati in termini di lunghezza, intervallo, formato e tipo? o
Si fa affidamento sulla sola validazione lato client? o Un aggressore
potrebbe iniettare comandi o dati dannosi nell'applicazione? o Non si
usano particolari accorgimenti nella scrittura dei dati all'interno
delle pagine Web o piuttosto si preferisce codificarli in HTML per
impedire gli attacchi di cross-site scripting? o L'input, viene validato
prima di essere utilizzato nella composizione delle istruzioni SQL al
fine di impedirne l'iniezione di malware? o I dati vengono validati al
punto di ingresso del componente destinatario in virtù del fatto che
oltrepassano sia il confine di fiducia del mittente che del
destinatario? o Ci si può fidare dei dati presenti nel database? o Si
accettano come input, i nomi dei file, gli URL e i nomi utente? Sono
state considerate le problematiche di canonicalizzazione?

::

   - Occorre rivedere la convalida degli input cercando una corrispondenza tra le seguenti vulnerabilità
       di carattere comune:
          o Ci si affida soltanto alla validazione lato client;
          o Viene eseguito un controllo a posteriori dei dati già immessi anziché un filtraggio dinamico
             al momento dell’inserimento;
          o Si fa uso di dati non validati indirizzati a pagine Web;
          o Si fa uso di input non validato per generare query SQL;
          o All’interno del codice sorgente, si fa uso di tecniche di accesso ai dati non sicure, che
             possono aumentare il rischio di minaccia da iniezione SQL;
          o Le decisioni intraprese nelle procedure di sicurezza si basano sui nomi di file, URL o nomi
             utente forniti in input.

   Gestione di Configurazione:

   - Come vengono protette le interfacce di amministrazione remote?
   - Si proteggono gli archivi di configurazione?
   - I dati di configurazione sensibili vengono crittografati?
   - I privilegi di amministratore vengono separati?
   - Vengono usati profili utente di processo e servizio con privilegi limitati?
   Rivedere la gestione delle configurazioni cercando una corrispondenza tra le seguenti vulnerabilità di
   carattere comune:
   - I dati confidenziali di configurazione, quali le stringhe di connessione e le credenziali del profilo
       utente di servizio, vengono memorizzati in chiaro;
   - Non esiste protezione negli aspetti di gestione della configurazione dell'applicazione, incluse le
       interfacce di amministrazione;
   - Si fa uso di profili utente di processo e profili utente di servizio con privilegi non strettamente
       necessari.

   Dati Sensibili:

   - I dati confidenziali vengono memorizzati in archivi di persistenza?
   - I dati sensibili, come vengono storicizzati?
   - I dati confidenziali presenti in memoria, vengono storicizzati?
   - Si trasferiscono dati sensibili attraverso la rete?
   - I dati sensibili vengono registrati nei log dell’applicazione?
   Rivedere i dati sensibili cercando una corrispondenza tra le seguenti vulnerabilità di carattere comune:


   Linee Guida per la modellazione delle minacce ed individuazione delle azioni di mitigazione conformi ai principi del Secure/Privacy

   - I dati confidenziali vengono memorizzati quando non è necessario memorizzarli;
   - I dati confidenziali vengono direttamente memorizzati nel codice dell’applicazione;
   - I dati confidenziali vengono memorizzati in chiaro;
   - I dati sensibili vengono passati in chiaro sulle reti.

   Gestione della Sessione:

   - Come vengono generati i cookie di sessione?
   - Come vengono scambiati gli identificatori di sessione?
   - Come viene protetto lo stato della sessione mentre attraversa la rete?
   - Come viene protetto lo stato della sessione per impedire il furto di sessione?
   - Come viene protetto lo stato della sessione?
   - La durata della sessione viene limitata?
   - In che modo l'applicazione esegue l’autenticazione utilizzando l'archivio delle sessioni?
   - Le credenziali sono trasmesse attraverso la rete e vengono mantenute all’interno dell'applicazione?
       Se sì, come vengono protette?

Controllare gli aspetti di gestione della sessione con il fine di
individuare una corrispondenza tra le seguenti vulnerabilità di
carattere comune:

::

   - Gli identificatori di sessione vengono passati su canali non crittografati;
   - La durata della sessione è prolungata;
   - Gli stati di sessione non vengono protetti;
   - Gli identificatori di sessione vengono passati nelle stringhe di query.

   Crittografia:

   - Quali algoritmi e tecniche di crittografia vengono usate?
   - Vengono impiegati algoritmi di crittografia personalizzati?
   - Perché vengono utilizzati determinati algoritmi?
   - Quale è la durata di validità prevista per le chiavi crittografiche e come queste vengono protette?
   - Quante volte vengono riciclate le chiavi?
   - Come vengono distribuite le chiavi crittografiche?

Occorre esaminare la crittografia cercando una corrispondenza tra le
seguenti vulnerabilità di carattere comune:

::

   - Vengono impiegati algoritmi crittografici personalizzati;
   - Si fa uso di un algoritmo errato o di una chiave di dimensione troppo piccola;
   - Le chiavi crittografiche non vengono protette;
   - Si fa uso della stessa chiave per un periodo di tempo prolungato.

   Manipolazione dei Parametri:

   - Tutti i valori dei parametri di ingresso vengono validati?
   - Tutti i valori dei parametri inseriti nei campi della pagina GUI, nei dati dei cookie e nelle intestazioni
       http, subiscono un processo di validazione?
   - I dati sensibili vengono trasferiti attraverso i parametri?
   - L'applicazione rileva la manomissione di parametri?
   Esaminare gli aspetti di gestione dei parametri cercando una corrispondenza tra le seguenti
   vulnerabilità di carattere comune:


   Linee Guida per la modellazione delle minacce ed individuazione delle azioni di mitigazione conformi ai principi del Secure/Privacy

   - Non è possibile validare tutti i parametri di ingresso. Ciò rende l’applicazione suscettibile ad
       attacchi di tipo “interruzione di servizio” e ad attacchi indirizzati alla modifica del codice
       sottostante, quali SQL injection e XSS.
   - I dati sensibili vengono inclusi nei cookie non crittografati. I dati del cookie possono essere
       modificati lato client o possono essere acquisiti e modificati in quanto vengono passati attraverso la
       rete.
   - I dati sensibili vengono inclusi nelle stringhe di query e nei campi delle pagine di front-end. Le
       stringhe di query e i campi all’interno di pagine di front-end sono facilmente modificabili lato client.
   - Si fa affidamento sulle informazioni presenti nell'intestazione HTTP. Queste informazioni sono
       facilmente modificabili lato client.

   Gestione delle Eccezioni:

   - In che modo l'applicazione gestisce le condizioni di errore?
   - Viene mai permesso alle eccezioni di propagarsi fino al client?
   - Che tipo di dati presentano i messaggi di eccezione?
   - Vengono rivelate troppe informazioni al client?
   - Dove vengono registrati i dettagli delle eccezioni? I file di log vengono protetti?
   Occorre esaminare i meccanismi di gestione delle eccezioni cercando una corrispondenza tra le
   seguenti vulnerabilità di carattere comune:
   - Non è possibile convalidare tutti i parametri di ingresso;
   - Vengono rivelate troppe informazioni al client.

   Audit and Gestione dei Log:

   - Sono state individuate delle attività chiave per l'audit?
   - L'attività di audit copre tutti i livelli e i server dell’applicazione?
   - Come vengono protetti i file di log?

Occorre esaminare i meccanismi di logging cercando una corrispondenza
tra le seguenti vulnerabilità di carattere comune:

::

   - Mancata revisione e registrazione (audit) dei tentativi d’accesso falliti;
   - Mancata protezione dei file di audit;
   - Mancata revisione e registrazione (audit) nei vari livelli del server dell’applicazione.

   Indicazioni aggiuntive. Dopo aver completato l'attività di modellazione delle minacce, si procede come
   segue:

   - Se si vuole descrivere il modello delle minacce in un documento, mantenere il documento di facile
       lettura in modo da potere essere consultato frequentemente. I contenuti chiave dovrebbero
       includere gli obiettivi di sicurezza, gli scenari chiave, le risorse protette, un elenco di minacce e un
       elenco di vulnerabilità.
   - Utilizzare le vulnerabilità per contribuire a predisporre la progettazione e l'implementazione della
       sicurezza.
   - Utilizzare le vulnerabilità per pianificare e implementare il test di sistema.
   - Tracciare e aggiornare l’elenco di vulnerabilità in un sistema di tracciamento.
   - Se sono state identificate delle minacce a cui sono state attribuite una priorità molto alta, ma per le
       quali non sono state individuate delle vulnerabilità corrispondenti, è necessario decidere se o non


   Linee Guida per la modellazione delle minacce ed individuazione delle azioni di mitigazione conformi ai principi del Secure/Privacy

indagare ulteriormente con il rischio di essere esposti a possibili
attacchi, oppure di continuare l'analisi alla ricerca di una possibile
vulnerabilità.

::

   - Comunicare le informazioni acquisite ai membri del team di lavoro.

   ### 5.2 IDENTIFICAZIONE DEL PROCESSO DI SVILUPPO DEL SOFTWARE SICURO

   L’applicazione di un processo di gestione del rischio nello sviluppo di un sistema abilita le organizzazioni a
   bilanciare i requisiti per la protezione delle informazioni e degli asset proprietari con il solo costo di
   implementare le strategie di controllo della sicurezza e di mitigazione attraverso l’SDLC. Il processo di
   gestione del rischio, identifica le attività e gli asset critici, nonché le vulnerabilità sistemiche a cui è esposta
   l’organizzazione. I rischi sono spesso condivisi in tutta l'organizzazione e non sono specifici per sole
   determinate architetture di sistema.

   Alcuni dei vantaggi apportati con l'integrazione degli aspetti di sicurezza nel ciclo di vita di sviluppo del
   sistema, sono:

   - L’individuazione preventiva e la mitigazione delle vulnerabilità e dei problemi di sicurezza presenti
       nella configurazione dei sistemi, con conseguente riduzione dei costi per l'implementazione dei
       controlli di sicurezza e delle tecniche di mitigazione delle vulnerabilità;
   - La consapevolezza delle potenziali sfide ingegneristiche dovute ai controlli di sicurezza obbligatori;
   - L’identificazione dei servizi di sicurezza condivisi e riutilizzo delle strategie e degli strumenti di
       sicurezza che riducono i costi di sviluppo e migliorano la condizione di sicurezza complessiva del
       sistema, attraverso l'applicazione di metodi e tecniche collaudate;
   - La facilitazione nell'attuazione delle decisioni prese da parte dei dirigenti, attraverso l'applicazione
       tempestiva di un processo completo di gestione del rischio;
   - La documentazione di importanti decisioni di sicurezza prese durante il processo di sviluppo, per
       informare la direzione sulle considerazioni di sicurezza intraprese durante tutte le fasi dello
       sviluppo;
   - Il miglioramento dell'organizzazione e della fiducia dei suoi utenti nel promuovere l'adozione e
       l'uso dei propri sistemi;
   - Una migliore interoperabilità e integrazione dei sistemi che sarebbe difficile raggiungere se la
       sicurezza fosse considerata separatamente ai vari livelli.

   Uno studio della Forrester Consulting sullo stato della sicurezza applicativa ha riportato che le
   organizzazioni che implementano un processo MS-SDL hanno mostrato risultati di ROI migliori rispetto agli
   altri approcci metodologici. Anche, la Aberdeen Group ha dimostrato come l'adozione di un processo MS-
   SDL aumenti la sicurezza e riduca la gravità e il costo degli incidenti di vulnerabilità, generando al contempo
   un ritorno sugli investimenti (quattro volte maggiore) rispetto ad altri approcci di sicurezza adottati nello
   sviluppo di software.

   MS-SDL è supportato da una rilevante quantità di risorse, tra cui documentazione, tutorial e strumenti
   software a supporto. Tale ricchezza di informazioni e strumenti rende sicuramente SDL un'opzione
   interessante per le organizzazioni che intendono adottare nuove iniziative di sicurezza del software.

   La modellazione delle minacce è un approccio per analizzare la sicurezza di un'applicazione. Si tratta di un
   approccio strutturato che consente di identificare, quantificare e affrontare i rischi di sicurezza associati a
   un'applicazione. La modellazione delle minacce non è un approccio alla revisione del codice, ma integra il
   processo di revisione del codice da un punto di vista della sicurezza. L'inclusione della modellazione delle
   minacce nell'SDLC può contribuire a garantire che le applicazioni vengano sviluppate con la sicurezza
   integrata fin dall'inizio (Secure by Design/ Secure by default). Questo, in combinazione con la
   documentazione prodotta nell'ambito del processo di modellazione delle minacce, può fornire al revisore
   una maggiore comprensione del sistema. Consente inoltre al revisore di vedere dove si trovano i punti di
   accesso all'applicazione e quali sono le potenziali minacce associabili a ciascun punto di accesso. Il concetto
   di modellazione delle minacce non è nuovo, ma negli ultimi anni si è verificato un chiaro cambiamento di
   mentalità. La modellazione delle minacce, oggi guarda ad un sistema dal punto di vista di un potenziale


   Linee Guida per la modellazione delle minacce ed individuazione delle azioni di mitigazione conformi ai principi del Secure/Privacy

   attaccante, piuttosto che dal punto di vista del difensore. Microsoft è stata forte sostenitrice del processo
   negli ultimi anni. Hanno fatto della modellazione delle minacce una componente fondamentale del loro
   SDLC, che sostengono essere una delle ragioni della maggiore sicurezza dei loro prodotti negli ultimi anni.

   Quando l'analisi del codice sorgente, ad esempio di applicazioni esistenti, viene eseguita al di fuori
   dell'SDLC, i risultati della modellazione delle minacce, aiutano a ridurre la complessità dell'analisi del codice
   sorgente, promuovendo un approccio maggiormente approfondito. Invece di rivedere tutto il codice
   sorgente con uguale attenzione, è possibile assegnare una priorità alla revisione di sicurezza del codice,
   basandosi sul risultato ottenuto dal processo di modellazione che individua le minacce a più alto rischio.

   Questi, i vantaggi introdotti dal processo di modellazione delle minacce:

   - la conferma dell'idoneità degli elementi di sicurezza individuati da attuare;
   - l’individuazione di eventuali lacune nelle caratteristiche di sicurezza da attuare;
   - l’identificazione di eventuali altri elementi di sicurezza;
   - l’identificazione dei requisiti di policy e di processo;
   - l’identificazione dei requisiti da inserire nelle operazioni di sicurezza;
   - l’identificazione dei requisiti in materia di tracciamento e monitoraggio;
   - arrivare ai casi di abuso, se utilizzati, secondo la metodologia Agile;
   - la comprensione dei requisiti di business continuity;
   - la comprensione dei requisiti in materia di capacità e disponibilità.

   L' esecuzione del processo di modellazione delle minacce, in fase di progettazione, aiuta nella:

   - identificazione delle vulnerabilità che devono essere colmate a livello di progettazione e di
       inserimento nella fase di realizzazione;
   - identificazione dei beni informativi che necessitano di controlli di sicurezza;
   - mappatura dei controlli di sicurezza, identificati in controlli tecnico/amministrativi/fisici a seconda
       dei casi (questa attività può essere svolta anche a livello di architettura, ma farlo a livello di
       progettazione aiuta ad essere più precisi);
   - identificazione dei casi di “test di sicurezza”/”scenari di test di sicurezza” nella verifica dei requisiti
       di sicurezza.

   La modellazione delle minacce è il processo di valutazione e documentazione dei rischi associati alla
   sicurezza di un particolare sistema e/o applicazione software. Mediante l’adozione di opportune tecniche
   già discusse in precedenza nel documento, è possibile identificare strategie di mitigazione efficaci per
   contrastare potenziali minacce a cui potrebbe essere soggetta l’applicazione. La modellazione delle
   minacce consente inoltre, di giustificare l’introduzione o l’eliminazione di eventuali feature all’interno
   dell’applicazione oltre che governare, al fine di proteggere gli asset dell’applicazione, l’introduzione di
   nuove policy o pratiche di sicurezza all’interno del sistema. La categorizzazione delle minacce di sicurezza
   può essere ottenuta mediante l’adozione di un modello denominato STRIDE che è l'acronimo che riunisce la
   gamma dei rischi a cui può essere soggetta l'applicazione e per i quali deve essere protetta.

   Nell’ambito della fase progettuale dell’SDL, nel processo di definizione dei requisiti di sicurezza, un modello
   come STRIDE può essere di aiuto nel definire i pattern di attacco, tra cui estrarre il modello di attacco
   (ovvero il sottoinsieme dei possibili attacchi) per il nostro sistema applicativo. Lo STRIDE ha l'indubbio
   vantaggio di non essere eccessivamente astratto ma è piuttosto facilmente riconducibile a situazioni reali.
   In gran parte della letteratura il modello STRIDE viene definito come un sistema per modellare le minacce.
   Ma in realtà (in accordo con Gary McGraw) si ritiene più opportuno pensare che STRIDE sia un modello
   relativo ai possibili attacchi, legando la "minaccia" agli attori (umani e non) che sono invece gli artefici degli
   attacchi stessi. Le sei categorie di rischi a cui la STRIDE afferisce (Spoofing, Tampering, Repudiation,
   Information disclosure, Denial of Service, and Elevation of privilege) consentono di identificare le
   vulnerabilità ed i possibili vettori di attacco nelle applicazioni software.

   Le linee guida per la modellazione delle minacce ispirata a MS-SDL si suddivide nelle seguenti fasi:


   Linee Guida per la modellazione delle minacce ed individuazione delle azioni di mitigazione conformi ai principi del Secure/Privacy

   - Identificazione degli asset. Cosa il sistema dovrebbe proteggere?
   - Creazione di una panoramica dell'architettura. Concentrarsi sui confini di fiducia, ovvero sui flussi di
       dati scambiati tra componenti posseduti da un'entità e componenti posseduti da un'altra entità.
   - Scomposizione del sistema in sotto-componenti fino al livello più basso possibile.
   - Identificazione delle minacce. Utilizzare la STRIDE o un albero delle minacce per facilitare
       l'enumerazione delle stesse.
          o STRIDE è un acronimo di spoofing, tampering, repudiation, information disclosure, denial of
             service e elevation of privilege. Queste descrizioni di vulnerabilità non sono intese come
             categorie che si escludono a vicenda, ma piuttosto come una tecnica euristica per
             l'enumerazione. Esaminare ciascun componente, concentrandosi sui confini di fiducia, e
             valutare se questo presenta vulnerabilità precedentemente indicate.
          o Gli Attack tree, possono eventualmente sostituire la STRIDE.
   - Documentazione delle minacce.
   - Valutazione delle minacce secondo il modello DREAD, un acronimo che indica il danno potenziale,
       la riproducibilità, l'utilizzabilità, gli utenti interessati, l’esposizione. Le minacce che si collocano ai
       primi posti in ciascuna di queste categorie dovrebbero avere una priorità più elevata.

   ### 5.3 MODELLAZIONE E INDIVIDUAZIONE DELLE MINACCE CON STRIDE

   Un evidente vantaggio dell'approccio STRIDE è l'indipendenza dal codice. Ciò è vantaggioso in quanto aiuta
   a identificare i problemi di sicurezza nella fase di analisi e progettazione del sistema software. Inoltre
   consente a tutto il team (oltre agli sviluppatori) di partecipare alla definizione del modello delle minacce del
   sistema stesso.

   Il processo può portare benefici laddove non si dispone di un esperto di sicurezza all'interno del proprio
   team. L’impiego della STRIDE consente a questi team di individuare le vulnerabilità e le tecniche di
   mitigazione da attuare per difendersi dalle eventuali minacce identificate.

   Le organizzazioni, possono inoltre beneficiare del processo sia per i nuovi progetti che per i progetti in
   essere, in cui potrebbero esistere delle vulnerabilità non identificate all'interno del codice.
   L'implementazione di una metodologia che identifica e classifica le minacce è un processo ripetibile
   strutturato che può portare benefici a qualsiasi tipo di progetto.

   Il risultato finale è, un elenco di vulnerabilità che i team di sviluppo e gli stakeholder dei prodotti possono
   quindi valutare, al fine di effettuare una accurata valutazione dei rischi, che insistono sulle vulnerabilità
   individuate (Risk Assessment).

   La STRIDE è stata identificata come metodologia leader di Threat Modeling nell'industria del software.

   Il successo di questa metodologia è dovuto ad un approccio ben strutturato alla modellazione delle
   minacce, ed è un eccellente supporto ed una risorsa per gli utenti.

   A volte la STRIDE viene indicata come "categorie STRIDE" o " tassonomia STRIDE". Tuttavia si evidenzia che
   la STRIDE non nasce come strumento di categorizzazione, ma con l'obiettivo di aiutare a trovare i possibili
   attacchi.

   ### 5.4 VALUTAZIONE DEL RISCHIO DERIVANTE DALLE MINACCE INDIVIDUATE CON DREAD

   La metodologia DREAD è stata sviluppata da Microsoft nell’ambito della definizione del Security
   Development Lifecycle e del Threat Modeling. L’adozione della metodologia DREAD prodiga i seguenti
   benefici:

   1. è utile per focalizzarsi sui reali rischi di una minaccia specifica;
   2. obbliga a considerare fattori aziendali come la criticità del sistema e l'impatto sul business;


   Linee Guida per la modellazione delle minacce ed individuazione delle azioni di mitigazione conformi ai principi del Secure/Privacy

   3. le cinque categorie sono tra loro scarsamente correlate (una di esse non implica le altre):
       considerare fattori indipendenti è un’ottima garanzia per formulare una corretta valutazione del
       rischio.
   4. è largamente impiegata (ad es. OWASP^20 e OpenStack^21 ).

   ### 5.5 MODELLAZIONE E INDIVIDUAZIONE DELLE MINACCE DI PRIVACY CON LINDUN

   La privacy è un aspetto molto importante, soprattutto nella società di oggi, dove i dati personali sono
   onnipresenti. Purtroppo questa, viene spesso trascurata durante lo sviluppo del software. Nonostante
   emergono diverse metodologie orientate alla produzione di requisiti di tutela della privacy (vedi paragrafo
   5.5.3), queste non soddisfano appieno quelle che sono le aspettative, o comunque, non sono in grado di
   fornire una guida metodologica sostanziale da adottare nel corso dell'analisi o mancano del necessario
   supporto alla tutela della privacy. Per colmare questa lacuna, si propone la metodologia LINDDUN, descritta
   nei capitoli precedenti. LINDDUN si ispira infatti a STRIDE, ovvero, un approccio consolidato per la
   modellazione e l’identificazione delle minacce alla sicurezza. Inoltre, la metodologia LINDDUN è stata
   costruita sulla base delle classificazioni esistenti in materia di tutela della privacy. Anche se LINDDUN non è
   una tecnica di conformità, attua diversi principi imposti dalla legislazione sulla protezione dei dati (ad
   esempio consenso, minimalizzazione, sensibilizzazione, ecc.) e richiama esplicitamente l'attenzione sulla
   necessità di conformità normativa. Inoltre, le proprietà sulla privacy, riportate nel paragrafo 5.5.1.1,
   costituiscono la base delle categorie di minacce gestite da LINDDUN. Infine, LINDDUN aderisce anche ai
   principi della Privacy by Design in quanto mira a introdurre la privacy nelle prime fasi del ciclo di vita di
   sviluppo del software.

   (^20) https://www.owasp.org/index.php/Threat_Risk_Modeling
   (^21) https://wiki.openstack.org/wiki/Security/OSSA-Metrics#DREAD


   Linee Guida per la modellazione delle minacce ed individuazione delle azioni di mitigazione conformi ai principi del Secure/Privacy

   ## 6 UN ESEMPIO APPLICATIVO: CASO D’USO “EASY WEB SITE”

   Lo use case si riferisce a un classico sito web disponibile su Internet che implementa un servizio per i propri
   clienti, i quali vi accedono attraverso un browser.

   A titolo di esempio, si suppone che:

   - il sito web acceda a una base dati di tipo SQL sia in lettura sia in scrittura;
   - il sito web esponga funzionalità sia per i clienti del servizio sia per gli amministratori del servizio;
   - l’utenza non autenticata (ad esempio, gli anonymous users) non possa accedere al sistema.

   Sulla base delle assunzioni fatte, andiamo a rappresentare il sistema in oggetto attraverso un diagramma,
   facendo uso del simbolismo DFD, tipicamente utilizzato nella modellazione delle minacce (vedi paragrafo
   5.2.3.1). Il diagramma che segue, mostra una scomposizione del sistema in oggetto ponendo in evidenza
   quelle che sono le sue componenti principali (Browser Client, Web Server e SQL Database), i confini di
   fiducia (Generic Trust Border Boundary e Internet Boundary) nonché i flussi dati di interscambio tra le
   singole componenti del sistema ([BC2WS] HTTPS Req (Credentials&Data) - Browser Client to Web Server,
   [WS2BC] HTTPS Req (Data) - Web Server to Browser Client, [WS2SQLDB] (Credentials&Data) Web Server to
   SQL Database e [WS2SQLDB] (Data) SQL Database to Web Server) dette anche interazioni.

   ### 6.1 DIAGRAMMA: USE CASE

   ## Figura 9 - Diagramma dello use case

   A seguire, per ciascuna interazione/flusso dati, vengono individuate le possibili minacce sulla base
   dell’analisi STRIDE. Per ciascuna minaccia viene fornita la categoria STRIDE/Compliance di pertinenza a cui
   la minaccia appartiene, una breve descrizione e alcune contromisure da attuare nel processo di
   mitigazione. Viene inoltre indicato, attraverso l’analisi DREAD, un indice di priorità (ALTO, MEDIO e BASSO)
   da considerare nella risoluzione della minaccia stessa (DREAD Score).


   Linee Guida per la modellazione delle minacce ed individuazione delle azioni di mitigazione conformi ai principi del Secure/Privacy

   ### 6.2 INTERAZIONE: DA BROWSER CLIENT A WEB SERVER

   ## Figura 10 - Interazione tra Browser Client e Web Server

   #### 6.2.1 Assunzioni

   Si assume che il Browser Client si autentica nei confronti del Web Server utilizzando una username e una
   password, ed esegue una post http per leggere e modificare i dati.

   Si suppone inoltre, come già detto, che, l’utenza non autenticata (ovvero gli anonymous users) non possa
   accedere al sistema.

   Il protocollo utilizzato è HTTPS, il quale garantisce:

   - Autenticazione della Destinazione (Web Server);
   - Confidenzialità;
   - Integrità.
   A seguire vengono riportate le minacce individuabili nell’interazione in oggetto.

   #### 6.2.2 Accesso a internet non valido

   ### Categoria: Compliance

   ### Descrizione: L'applicazione Web (qui "Server Web") non dovrebbe essere collegata direttamente a

   ### Internet.

   ### Contromisure: Interconnettere il "Browser Client" con il "Server Web" tramite un gateway di protezione

   ### (firewall).

   **Valutazione della priorità della minaccia (Ranking)**

   **DREAD Descrizione Score**

   Damage Potential Se il Web Server è esposto direttamente sulla rete Internet, un attaccante
   può facilmente compromettere il sistema.

   ###### 3

   Reproducibility L’attacco può essere condotto in qualunque momento. 3

   Exploitability L’attacco non è banale: occorre una figura senior. 2

   Affected Users 100%. 3

   Discoverability Occorre identificare un exploit (es. per mancanza di patching adeguato del
   Sistema Operativo) cui la macchina su cui il Web Server è installato risulta
   vulnerabile.

   ###### 1

   **DREAD Score: 12/15 (ALTO)**


   Linee Guida per la modellazione delle minacce ed individuazione delle azioni di mitigazione conformi ai principi del Secure/Privacy

   #### 6.2.3 Mancanza di convalida dell'input da parte del "Web Server"

   ### Categoria: Tampering

   ### Descrizione: Il 'Web Server' non verifica che i dati di input siano nel formato previsto. Questa è la causa

principale di un numero molto elevato di problemi sfruttabili.
Considerate tutti i percorsi e il modo in cui si gestiscono i dati di
input. Verificare che tutti gli input siano verificati e, se in

::

   ### formato non previsto, scartati o sanitizzati.

   ### Contromisure:

   - La validazione dell'input deve essere eseguita prima che l'input entri nel 'Web Server' o
       venga elaborato da quest’ultimo.
   - La convalida dei dati ricevuti deve comprendere almeno:
       o La verifica del tipo di dato;
       o Il controllo dell'intervallo di ammissibilità dei valori dei dati per garantire che i
          valori forniti siano entro i limiti prestabiliti (minimo e massimo / dimensione);
       o Il controllo sulla base delle regole di business previste.
   - Definire il set consentito di caratteri da accettare. La convalida basata su White list è da
       preferire a quella basata su Black list. La White list prevede la definizione esatta di ciò
       che è consentito, e per definizione, tutto il resto non è ammesso. L’utilizzo di
       espressioni regolari può facilitare l'implementazione di schemi di validazione basati su
       White list. La Black List cerca di rilevare caratteri e modelli di attacco ed è un approccio
       sconsigliato, in quanto è possibile per un aggressore eludere tali filtri.

   ### • Mettere in campo un meccanismo di controllo degli accessi efficace capace di garantire

   ### l’accettazione dei dati solo da parte di utenti autorizzati.

   **Valutazione della priorità della minaccia (Ranking)**

   **DREAD Descrizione Score**

   Damage Potential La mancanza di validazione dell’input da parte del Web Server lo espone a
   un’ampia varietà di attacchi che possono anche arrivare a compromettere
   la macchina su cui il Web Server è installato come nel caso di “Command
   Injection”.

NOTA BENE Si tratta di una minaccia molto generica che vuole focalizzare
l'attenzione sul principio “all input is evil”. Nel prosieguo vengono
esaminate minacce più specifiche legate alla mancanza di validazione
dell'input (cross-site scripting, sql injection, ecc.).

::

   ###### 3

   Reproducibility L’attacco può essere condotto in qualunque momento 3

   Exploitability L’attacco non è banale: occorre una figura senior. 2

   Affected Users 100% 3

   Discoverability Occorre identificare un exploit, attraverso la manomissione dei dati di
   input, cui il Web Server risulta vulnerabile.

   ###### 1

   **DREAD Score: 12/15 (ALTO)**


   Linee Guida per la modellazione delle minacce ed individuazione delle azioni di mitigazione conformi ai principi del Secure/Privacy

   #### 6.2.4 Cross Site Scripting

   ### Catogoria: Tampering

   ### Descrizione: Il 'Web Server' potrebbe essere soggetto ad un attacco di Cross-Site Scripting in quanto non

prevede la sanitizzazione dell'input non affidabile (untrusted) che
potrebbe contenere script

::

   ### malevoli

   ### Contromisure:

   - Eseguire l’escape del testo HTML prima di inserire i dati non attendibili nel contenuto
       degli elementi HTML.
   - Eseguire l'escape del valore di un attributo prima di inserire dati non attendibili in
       attributi HTML.
   - Eseguire l'escape del testo JavaScript prima di inserire dati non attendibili nel codice
       JavaScript.
   - Eseguire l’escape HTML di valori JSON prima di inserire i dati nel contenuto degli
       elementi HTML e leggere i dati con “JSON.parse”.
   - Eseguire l’escape CSS e attuare rigorose validazioni prima di inserire i dati non
       attendibili nei valori di proprietà di stile HTML.
   - Eseguire l’escape dell’URL prima di inserire dati non attendibili nei valori dei parametri
       dell’URL.
   - Sanitizzare i Markup HTML con una libreria progettata a tale scopo.
   - Utilizzare il flag HTTPOnly per i cookie.
   - Implementare la politica Content Security Policy.
   - Utilizzare un sistema Auto-Escaping Template System.

   ### • Utilizzare l’X- XSS-Protection Response Header.

   **Valutazione della priorità della minaccia (Ranking)**

   **DREAD Descrizione Score**

   Damage Potential Lo script malevolo può accedere a qualsiasi cookie, token di sessione o
   altre informazioni sensibili conservate dal browser (qui Browser Client) e
   utilizzati esclusivamente nel dialogo con il sito d’origine (qui Web Server).
   Questi script possono anche riscrivere il contenuto della pagina HTML. In
   definitiva il Tampering dell’url produce Information Disclosure, tra cui la
   compromissione del token di sessione che abilita il “Session hijacking” (che
   è una forma di furto di identità – spoofed identity). Nel peggiore dei casi,
   l’attaccante potrebbe impersonare l’amministratore del Web Server.

   ###### 2

   Reproducibility L’attacco funziona sempre. Tuttavia il token di sessione (che è il dato la cui
   compromissione è particolarmente grave: spoofed identity) è utilizzabile
   finché la sessione non scade.

   ###### 2

   Exploitability L’attacco non è banale: occorre una figura senior. 2

   Affected Users 100% (nel caso in cui l’attaccante arrivasse a impersonare
   l’amministratore.)

   ###### 3

   Discoverability Occorre identificare un url in cui un input utente ritorna in output senza
   aver subito sanitizzazioni o che può modificare il “DOM” enviroment.

   ###### 1

   **DREAD Score: 10/15 (MEDIO)**


   Linee Guida per la modellazione delle minacce ed individuazione delle azioni di mitigazione conformi ai principi del Secure/Privacy

   #### 6.2.5 Ripudio di dati da parte del 'Browser Client'

   ### Categoria: Repudiation

   ### Descrizione: Il 'Client Browser' sostiene di non aver inviato i dati al 'Web Server'.

   ### Contromisure:

   - È consigliabile che l’applicazione ricevente (qui 'Web Server') utilizzi file di log o di audit
       per registrare l'origine, l'ora e il riepilogo dei dati ricevuti, affinché il mittente di
       informazioni non possa negare l'invio delle stesse.
   - Si raccomanda inoltre che il destinatario autentichi il mittente per assicurare che la
       comunicazione avvenga con il mittente corretto.
   - Implementare le protezioni contro la manomissione dei dati di log/audit poiché, dati di
       log/audit manomessi possono produrre potenziali repudiation.
   - Considerare di far sì che l’applicazione ricevente richieda al mittente di firmare i dati
       trasmessi per garantire che il mittente di informazioni non possa negare l'invio delle
       stesse.

   **Valutazione della priorità della minaccia (Ranking)**

   **DREAD Descrizione Score**

   Damage Potential A fronte della elaborazione dati o dell’esecuzione di transazioni
   disconosciute dalla sorgente, non si ha modo di attribuire il
   malfunzionamento alla parte che ne è responsabile.

   ###### 1

   Reproducibility L’attacco può essere condotto in qualunque momento. 3

   Exploitability Per la natura del servizio, l’attacco richiede un’utenza autenticata. 2

   Affected Users 100% (qualunque utente potrebbe tentare la repudiation). 3

   Discoverability Il rilevamento della minaccia è contestualizzato nell’ambito di un’utenza
   autenticata.

   ###### 2

   **DREAD Score: 11/15 (MEDIO)**

   #### 6.2.6 Crash o fermo del processo 'Web Server'

   ### Categoria: Denial Of Service

   ### Descrizione: Il 'Web Server' va in crash, si ferma o risponde lentamente, in ogni caso violando una

metrica di disponibilità.

::

   ### Contromisure:

   - Convalidare tutti i dati di input per assicurare che i valori non possano causare il crash
       del 'Web Server'.
   - Gestire tutti i casi di errore (sia le exceptions del linguaggio di programmazione sia i casi
       di errore nelle condizioni logiche) in modo graceful, ossia in modo che non provochi
       crash o servizi degradati.
   - I log devono indicare se è in atto o meno una corretta validazione degli input (per
       evitare crash) e come vengono trattati i casi eccezionali.
   - Prevedere il ripristino del sistema: Si consideri l'utilizzo di un meccanismo di recupero
       (ad esempio il watchdog) per riavviare il ‘Web Server’ in caso di crash.


   Linee Guida per la modellazione delle minacce ed individuazione delle azioni di mitigazione conformi ai principi del Secure/Privacy

   ### • Utilizzare le tecniche di throttling e rate-limiting per evitare che il ‘Web Server’collassi.

   **Valutazione della priorità della minaccia (Ranking)**

   - Si considera lo scenario del DDOS, oggi disponibile “As-a -Service” sul Dark Web.
   **DREAD Descrizione Score**

   Damage Potential L’attaccante può impedire agli utenti del sistema di interagire con esso
   (del tutto o in modo degradato).

   ###### 2

   Reproducibility L’attacco funziona solo in certe finestre temporali: un attacco DDOS ha
   per sua natura una durata limitata nel tempo.

   ###### 1

   Exploitability L’attacco richiede un figura senior capace di organizzare un DDOS. 1

   Affected Users 100% (la piattaforma è resa indisponibile o comunque ne viene
   degradato il funzionamento).

   ###### 3

   Discoverability L’attaccante dovrà impegnare parecchie risorse per sfruttare la
   vulnerabilità (deve probabilmente sapersi muoversi sul Dark Web e
   pagare il “servizio”).

   ###### 1

   **DREAD Score (DDOS): 8/15 (MEDIO)**

   **Valutazione della priorità della minaccia (Ranking)**

   - Si considera lo scenario del crash, nell’ipotesi richieda lo sfruttamento di una vulnerabilità 0-day del
       ‘Web Server’.
   **DREAD Descrizione Score**

   Damage Potential L’attaccante può impedire agli utenti del sistema di interagire con esso. 2

   Reproducibility L’attacco funziona fino all’applicazione della patch (che richiede la
   scoperta dello 0-day, la produzione della patch, il testing della patch,
   l’installazione della patch).

   ###### 2

   Exploitability L’attacco richiede una figura senior capace di trovare una vulnerabilità
   tale da provocare il crash di Web Server.

   ###### 1

   Affected Users 100% (la piattaforma è resa indisponibile o comunque ne viene
   degradato il funzionamento).

   ###### 3

   Discoverability L’attaccante dovrà impegnare parecchie risorse per scoprire la
   vulnerabilità sfruttabile. Lo sforzo potrebbe non valere il risultato.

   ###### 1

   **DREAD Score (Crash): 9/15 (MEDIO)**

   **DREAD Score complessivo (il peggiore tra i due): 9/15 (MEDIO)**

   #### 6.2.7 Interruzione del flusso dati HTTPS (o inaccessibilità da parte del 'Web Server')

   ### Categoria: Denial Of Service

   ### Descrizione: Un agente esterno interrompe i dati che fluiscono attraverso '[BC2WS] HTTPS Req

   ### (Credentials&Data) - Browser Client to Web Server' in entrambe le direzioni.


   Linee Guida per la modellazione delle minacce ed individuazione delle azioni di mitigazione conformi ai principi del Secure/Privacy

   ### Contromisure:

   - Se il "Client Browser" non è in grado di proseguire l'elaborazione, dovrebbe fornire
       risposte appropriate agli utenti in attesa.
   - Rilevamento: Si consideri l'utilizzo di un meccanismo di allarme che, rilevando lo
       spostamento del comportamento del Server Web da metriche predefinite, consenta di
       segnalare la sospetta condizione di DOS (per attivare le risposte appropriate).

   ### • 3) Ridondanza: considerare la possibilità di configurare un secondo "Web Server" per

   ### essere utilizzato come un backup di quello sotto attacco.

   **Valutazione della priorità della minaccia (Ranking)**

   **DREAD Descrizione Score**

   Damage Potential L’attaccante può impedire agli utenti del sistema di interagire con esso. 2

   Reproducibility Non sembra verosimile che l’attaccante “a comando” / ”a piacimento”
   possa interrompere il flusso dati in qualunque momento. Sembra
   ragionevole assumere che l’attacco funzioni solo in certe condizioni che si
   raggiungono raramente.

   ###### 1

   Exploitability L’attacco, sia esso condotto sul piano dell’interruzione fisica della
   connessione o sul piano dell’interruzione logica del flusso dei dati, è
   complesso.

   ###### 1

   Affected Users 100% (la piattaforma è resa indisponibile). 3

   Discoverability L’attaccante dovrà impegnare parecchie risorse per organizzare l’attacco. 1

   **DREAD Score: 8/15 (MEDIO)**

   #### 6.2.8 Elevazione di privilegi attraverso l’esecuzione remota di codice da parte del 'Web Server'

   ### Categoria: Elevation Of Privilege

   ### Descrizione: 'Client Browser' potrebbe essere in grado di eseguire codice in remoto sul sistema ' Web

   ### Server'.

   ### Contromisure:

   - Il processo non deve contenere percorsi che mandano in esecuzione dati presi dal flusso
       di input (es. il nome di un eseguibile).

   ### • Se un processo manda in esecuzione dati presi dal flusso di input, questi devono essere

   ### convalidati in modo da escludere che venga eseguito codice arbitrario.

   **Valutazione della priorità della minaccia (Ranking)**

   **DREAD Descrizione Score**

   Damage Potential L’attaccante potrebbe prendere il controllo dell’intero sistema,
   attraverso tecniche di “lateral moving” (il “lateral moving” di solito
   comporta attività legate alla ricognizione <<information gathering>>,
   furto di credenziali e spostamenti su altri computer).

   ###### 3

   Reproducibility L’attacco può essere condotto in qualunque momento. 3


   Linee Guida per la modellazione delle minacce ed individuazione delle azioni di mitigazione conformi ai principi del Secure/Privacy

   Exploitability Per la natura del servizio, l’attacco richiede un’utenza autenticata. Si
   richiedono anche skill elevati.

   ###### 1

   Affected Users 100% (se l’esito finale fosse effettivamente il controllo del sistema). 3

   Discoverability L’attaccante dovrà impegnare parecchie risorse per scoprire la
   vulnerabilità sfruttabile (l’attacco di norma sfrutta una catena di
   debolezze).

   ###### 1

   **DREAD Score: 11/15 (MEDIO)**

   #### 6.2.9 Elevazione dei privilegi attraverso il cambiamento del flusso di esecuzione nel codice del 'Web Server'

   ### Categoria: Elevation Of Privilege

   ### Descrizione: Un attaccante può passare dati al 'Web Server' in modo da cambiare a suo vantaggio il

   ### flusso di esecuzione del programma all'interno del 'Web Server' stesso.

   ### Contromisure:

   - Convalidare in modo appropriato gli input e gestire le eccezioni per evitare percorsi di
       esecuzione imprevisti.
   - Impiegare meccanismi di protezione contro il buffer overflow e altri problemi di
       gestione della memoria.
   - Applicare principio del minimo privilegio.
   - Implementare le protezioni contro la manomissione dei percorsi di autenticazione e di
       autorizzazione (ad esempio, se l'autenticazione e l'autorizzazione dipendono dai dati del
       database, i percorsi di codice che interagiscono con il database devono essere protetti
       per garantire l'integrità di tali dati).
   - Utilizzare implementazioni dell’Address Space Layout Randomization (ASLR) per rendere
       più difficile l'esecuzione di istruzioni privilegiate agli indirizzi noti in memoria tramite
       buffer overruns.
   - Utilizzare compilatori che bloccano il buffer overruns.

   **Valutazione della priorità della minaccia (Ranking)**

   **DREAD Descrizione Score**

   Damage Potential L’attaccante potrebbe prendere il controllo del Web Server, se riuscisse a
   elevare i propri privilegi fino a livello appunto di amministratore del Web
   Server.

   ###### 2

   Reproducibility L’attacco può essere condotto in qualunque momento. 3

   Exploitability Per la natura del servizio, l’attacco richiede un’utenza autenticata. 2

   Affected Users 100% (se l’esito finale fosse effettivamente il controllo del sistema). 3

   Discoverability L’attaccante dovrà impegnare parecchie risorse per scoprire la
   vulnerabilità sfruttabile.

   ###### 1

   **DREAD Score: 11/15 (MEDIO)**


   Linee Guida per la modellazione delle minacce ed individuazione delle azioni di mitigazione conformi ai principi del Secure/Privacy

   #### 6.2.10 Cross Site Request Forgery

   ### Categoria: Elevation Of Privilege

   ### Descrizione: Il Cross Site Request Forgery (CSRF o XSRF) è un tipo di attacco in cui un attaccante fa in

modo che un utente vittima (qui un Autheticated User del Web Server)
invii involontariamente una richiesta HTTPS dal suo browser (qui Client
Browser) al sistema web (qui Web Server) dove è attualmente autenticato.
L'attaccante deve: a) trovare un difetto (flaw) lato server (qui Web
Server) tale per cui il sito web processa una richiesta di cambio stato
a fronte della sola presenza di una sessione valida (che attesta una
precedente autenticazione); b) indurre un utente ignaro (qui un
Autheticated User del Web Server) ad esercitare un url che sfrutta il
difetto di cui sopra mentre quell'utente ha una sessione aperta sul
server (qui Web Server). Il sistema, vulnerabile al CSRF, riceve dal
browser dell'utente la richiesta contraffatta (dietro cui, cioè, si cela
un'azione studiata dall'attaccante) con un cookie di sessione valido
(dal momento che la vittima è stata precedentemente autenticata e la
sessione è ancora attiva) e la elabora.

::

   ### Contromisure: Fare in modo che tutte le richieste di cambiamento di stato oltre ad essere autenticate

includano un ulteriore elemento di payload segreto (canary o CSRF token)
conosciuto solo dal sito legittimo e dal browser (parti che comunicano
tra loro in modo protetto tramite

::

   ### HTTPS).

   **Valutazione della priorità della minaccia (Ranking)**

   **DREAD Descrizione Score**

   Damage Potential L’attaccante può eseguire richieste di cambio stato al sistema che sono
   prerogativa di Autheticated User o, peggio, dell’Administrator (es. la
   modifica di configurazioni o il furto/modifica di dati privati).

   ###### 2

   Reproducibility L’attacco funziona finché la sessione della vittima non scade. 1

   Exploitability L’attacco non è banale: occorre una figura senior. 2

   Affected Users In genere l’attacco è condotto con tecniche di social engineering: gli utenti
   coinvolti sono una quota parte del totale.

   ###### 2

   Discoverability Occorre identificare un url che presenti la vulnerabilità XSRF. 1

   **DREAD Score: 8/15 (MEDIO)**


   Linee Guida per la modellazione delle minacce ed individuazione delle azioni di mitigazione conformi ai principi del Secure/Privacy

   ### 6.3 INTERAZIONE: DA WEB SERVER A BROWSER CLIENT

   ## Figura 11 - Interazione tra Web Server e Browser Client

   #### 6.3.1 Assunzioni

   Si assume che il Browser Client si autentica nei confronti del Web Server utilizzando una username e una
   password, ed esegue una post http per leggere e modificare i dati.

   Si suppone inoltre, come già detto, che, l’utenza non autenticata (ovvero gli anonymous users) non possa
   accedere al sistema.

   Il protocollo utilizzato è HTTPS, il quale garantisce:

   - Autenticazione della Destinazione (Web Server);
   - Confidenzialità;
   - Integrità.

   #### 6.3.2 Analisi delle minacce e mitigazioni

   Valgono le raccomandazioni già proposte in “Interazione: da Browser Client a Web Server”.

   ### 6.4 INTERAZIONE: DA WEB SERVER A SQL DATABASE

   ## Figura 12 - Interazione tra Web Server e SQL Database

   #### 6.4.1 Assunzioni

   Si assume che il Web Server si autentica nei confronti del SQL Server utilizzando una username e una
   password, e può inserire, leggere, modificare, cancellare dati.

   Si suppone che l’interazione avvenga all’interno di un Trusted Boundary.

   A seguire vengono riportate le minacce individuabili nell’interazione in oggetto.

   #### 6.4.2 Vulnerabilità di SQL Injection nel 'SQL Database'

   ### Categoria: Tampering

   ### Descrizione: La SQL Injection è una tecnica di attacco di tipo “code injection”, usata per attaccare un


   Linee Guida per la modellazione delle minacce ed individuazione delle azioni di mitigazione conformi ai principi del Secure/Privacy

database, nella quale viene inserito del codice SQL malevolo all'interno
di parametri di input in modo che vada in esecuzione sul database sotto
attacco (es. per inviare all'attaccante /modificare/distruggere il
contenuto del database e, in certi casi, “saltare dal DB al Sistema
Operativo” e prendere il controllo della macchina). A patto che la query
risultante da questo tipo di attacco sia sintatticamente corretta, il
database la eseguirà.

::

   ### Contromisure:

   - Usare i Prepared Statements con query parametrizzate.
   - Usare le Stored Procedures.
   - Eseguire la validazione di tipo White List di ogni input esterno usato per costruire
       statements SQL.

   ### • 4) Eseguire l’escape di ogni input utente.

   **Valutazione della priorità della minaccia (Ranking)**

   **DREAD Descrizione Score**

   Damage Potential La possibilità di eseguire codice malevolo sul database dell’applicazione la
   espone potenzialmente alla totale compromissione.

   ###### 3

   Reproducibility L’attacco può essere condotto in qualunque momento. 3

   Exploitability Per la natura del servizio, l’attacco richiede un’utenza autenticata. 2

   Affected Users 100%. 3

   Discoverability Occorre identificare un exploit, attraverso la manomissione dei dati di
   input, cui il Web Server risulta vulnerabile.

   ###### 1

   **DREAD Score: 12/15 (MEDIO)**

   #### 6.4.3 Possibile corruzione del 'SQL Database'

   ### Categoria: Tampering

   ### Descrizione: Assicurare l'integrità dei dati all'interno dell'archivio 'SQL Database'.

   ### Contromisure:

   - Autenticare tutti gli utenti.
   - Mettere in pratica un efficace meccanismo di controllo degli accessi che garantisca che i
       dati possono essere scritti o modificati solo da utenti autorizzati.
   - Rispettare il principio del privilegio minimo.

   ### • Attuare controlli che seguano e registrino correttamente le azioni degli utenti.

   **Valutazione della priorità della minaccia (Ranking)**

   **DREAD Descrizione Score**

   Damage Potential La possibilità, senza averne diritto, di modificare i dati all’interno del
   database dell’applicazione la espone potenzialmente alla totale
   compromissione.

   ###### 3

   Reproducibility L’attacco può essere condotto in qualunque momento. 3

   Exploitability Per la natura del servizio, l’attacco richiede un’utenza autenticata. 2


   Linee Guida per la modellazione delle minacce ed individuazione delle azioni di mitigazione conformi ai principi del Secure/Privacy

   Affected Users 100%. 3

   Discoverability Occorre identificare un exploit, attraverso la manomissione dei dati di
   input, cui il Web Server risulta vulnerabile.

   ###### 1

   **DREAD Score: 12/15 (MEDIO)**

   #### 6.4.4 Consumo eccessivo di risorse da parte del 'Web Server' o del 'SQL Database'

   ### Categoria: Denial Of Service

   ### Descrizione: Il "Web Server" o il "SQL Database" adottano passi espliciti per controllare il consumo di

risorse? Fare attenzione che le richieste di risorse non producano
deadlock e che, nel caso

::

   ### peggiore, vadano in timeout.

   ### Contromisure:

   - Non bloccare (deadlock) le richieste di risorse.
   - Impostare i timeout per le richieste di risorse, se è applicabile.
   - Validare i dati di input che si riferiscono al consumo di risorse.
   - Limitare la dimensione dei dati elaborati dall'applicazione.
   - Eseguire il rilascio delle risorse quando non sono più necessarie.

   ### • Gli audit devono dare indicazioni sul consumo eccessivo di risorse da parte

   ### dell'applicazione.

   **Valutazione della priorità della minaccia (Ranking)**

   **DREAD Descrizione Score**

   Damage Potential L’attaccante può degradare le prestazioni del sistema fino a renderlo
   potenzialmente indisponibile.

   ###### 2

   Reproducibility L’attacco funziona sempre. 3

   Exploitability Per la natura del servizio, l’attacco richiede un’utenza autenticata. 2

   Affected Users 100% (la piattaforma è resa indisponibile o comunque ne viene
   degradato il funzionamento).

   ###### 3

   Discoverability Il rilevamento della minaccia è contestualizzato nell’ambito di un’utenza
   autenticata.

   ###### 2

   **DREAD Score (Crash): 12/15 (ALTO)**


   Linee Guida per la modellazione delle minacce ed individuazione delle azioni di mitigazione conformi ai principi del Secure/Privacy

   ### 6.5 INTERAZIONE: DA SQL DATABASE A WEB SERVER

   ## Figura 13 - Interazione tra SQL Database e Web Server

   #### 6.5.1 Assunzioni

   Il Web Server si autentica nei confronti del SQL Database utilizzando una username e una password ed
   inserisce, legge, modifica e cancella dati.

   Si suppone che l’interazione avvenga all’interno di un Trusted Boundary.

   A seguire vengono riportate le minacce individuabili nell’interazione in oggetto.

   #### 6.5.2 Persistent Cross Site Scripting

   ### Categoria: Tampering

   ### Descrizione: Il 'Server Web' potrebbe essere soggetto ad un attacco di cross-site scripting di tipo

persistente in quanto non sanitizza i dati di input al ‘SQL Database’ in
fase di scrittura (che potrebbero contenere uno script malevolo) e non
esegue l'escape dei dati di output dal ‘SQL Database’ in fase di lettura
(ciò che si traduce nel mandare in esecuzione su ‘Browser Client’

::

   ### lo script malevolo).

   ### Contromisure: Applicare le tecniche di sanitizzazione e di escaping come nel caso di Cross Site Scripting.

   **Valutazione della priorità della minaccia (Ranking)**

   **DREAD Descrizione Score**

   Damage Potential Lo script dannoso può accedere a qualsiasi cookie, token di sessione o altre
   informazioni sensibili conservate dal browser (qui Browser Client) e
   utilizzati esclusivamente nel dialogo con il sito d’origine (qui Web Server).
   Questi script possono anche riscrivere il contenuto della pagina HTML. In
   definitiva il Tampering dell’url produce Information Disclosure, tra cui la
   compromissione del token di sessione che abilita il “Session hijacking” (che
   è una forma di furto di identità – spoofed identity). Nel caso pessimo,
   l’attaccante potrebbe impersonare l’amministratore del Web Server.

   ###### 2

   Reproducibility L’attacco funziona sempre. Tuttavia il token di sessione (che è il dato la cui
   compromissione è particolarmente grave: spoofed identity) è utilizzabile
   finché la sessione non scade.

   ###### 2

   Exploitability L’attacco non è banale: occorre una figura senior. 2

   Affected Users 100% (nel caso in cui l’attaccante arrivasse a impersonare
   l’amministratore).

   ###### 3


   Linee Guida per la modellazione delle minacce ed individuazione delle azioni di mitigazione conformi ai principi del Secure/Privacy

   Discoverability Occorre identificare un url che ritorni in output, senza aver subito alcun
   encoding, un input utente malevolo, precedentemente persistito senza
   sanitizzazioni sul database.

   ###### 1

   **DREAD Score: 10/15 (MEDIO)**

   #### 6.5.3 Controllo accesso debole per una risorsa

   **Valutazione della priorità della minaccia (Ranking)**

   **DREAD Descrizione Score**

   Damage Potential La possibilità, senza averne diritto, di leggere i dati all’interno del database
   dell’applicazione espone potenzialmente l’owner del sistema a violazioni di
   normative di legge (es. Privacy) o a danno reputazionale o a divulgazione di
   informazioni di business riservate.

   ###### 2

   Reproducibility L’attacco può essere condotto in qualunque momento. 3

   Exploitability Per la natura del servizio, l’attacco richiede un’utenza autenticata. 2

   Affected Users 100%. 3

   Discoverability Occorre identificare un exploit, attraverso la manomissione dei dati di
   input, cui il Web Server risulta vulnerabile.

   ###### 1

   **DREAD Score: 11/15 (MEDIO)**

   ### Categoria: Information Disclosure

   ### Descrizione: Una inadeguata protezione dei dati a livello di " SQL Database" può consentire a un

attaccante di leggere informazioni non destinate alla divulgazione.
Esaminare le

::

   ### impostazioni di autorizzazione.

   ### Contromisure:

   - Autenticare tutti gli utenti.
   - Mettere in pratica un efficace meccanismo di controllo degli accessi che garantisca che i
       dati possono essere letti solo da utenti autorizzati.
   - Rispettare il principio del minimo privilegio.
   - Attuare controlli che seguano correttamente e registrino le azioni degli utenti
   - Crittografare i dati.

   ### • Assicurarsi che le utilità o le tecniche di riservatezza dei data store vengano

appropriatamente utilizzate in modo che la riservatezza dei dati sia
mantenuta e gestita

::

   ### in base alle esigenze aziendali/regole.


   Linee Guida per la modellazione delle minacce ed individuazione delle azioni di mitigazione conformi ai principi del Secure/Privacy

   ## 7 BIBLIOGRAFIA

   [1] H. E. a. P. D. Shafiq Hussain, Threat modeling using Formal Methods: A New Approach to Develop Secure Web
   Applications.

   [2] G. Zannone, Towards the development of privacy-aware systems, 2009.

   [3] A. Cavoukian, Privacy by Design.

   [4] S. F. M. H. a. R. M. Kristian Beckers, «A Problem-based Approach for Computer Aided Privacy Threat
   Identification. In Privacy Technologies and Policy, volume 8319 of LNCS,» Springer, 2014, p. pages 1–16...

   [5] E. K. a. S. G. Christos Kalloniatis, Addressing privacy requirements in system design: the PriS method.
   Requirements Engineering.

   [6] S. S. a. L. F. Cranor, «Engineering privacy. IEEE Transactions on Software Engineering,» 2009, p. 35(1):67–82.

   [7] F. S. Gürses, Multilateral privacy requirements analysis in online social network services., 2010.

   [8] S. I. C. K. a. S. G. Haralambos Mouratidis, « A framework to support selection of cloud providers based on security
   and privacy requirements. Journal of Systems and Software,» 2013, p. pages 2276–2293.

   [9] L. C. M. S. L. P. a. B. N. Inah Omoronyia, « Engineering adaptive privacy: on the role of privacy awareness
   requirements. In Proceedings of the 2013 International Conference on Software Engineering,» 2013, pp. 632-641.

   [10] C. Jensen, «Designing for privacy in interactive systems. PhD thesis,» Georgia Institute of Technology, 2005.

   [11] « Privacy guidelines for developing software products and services, version 3.1. Technical report, Microsoft
   Coorporation, .,» Sept 2008.

   [12] N. M. a. J. Z. Seiya Miyazaki, «Computer-aided privacy requirements elicitation technique,» Asia-Pacific
   Conference on Services Computing (APSCC’08), 2008, p. pages 367–372.

   [13] A.I. Antón, J.B. Earp, and A. Reese. Analyzing website privacy requirements using a privacy goal taxonomy. In
   Requirements Engineering, 2002. Proceedings. IEEE Joint International Conference on, pages 23–31, 2002.

   [14] Fahriye Seda Gürses. Multilateral privacy requirements analysis in online social network services. PhD thesis,
   Department of Computer Science, KU Leuven, 2010.

   [15] Mina Deng, Kim Wuyts, Riccardo Scandariato, Bart Preneel, and Wouter Joosen. A privacy threat analysis
   framework: supporting the elicitation and fulfillment of privacy requirements. Requirements Engineering Journal,
   16(1):3–32, 2011.

   [16] Jason I. Hong, Jennifer D. Ng, and Scott Lederer. Privacy risk models for designing privacy-sensitive ubiquitous
   computing systems. In Designing Interactive Systems (DIS2004), pages 91– 100. ACM Press, 2004.

   [17] Andrew Patrick and Steve Kenny. From privacy legislation to interface design: Implementing information privacy
   in humancomputer interactions. In Privacy Enhancing Technologies, volume 2760 of LNCS, pages 107–124.
   Springer, 2003.

   [18] Eric Yu and Luiz Marcio Cysneiros. Designing for privacy and other competing requirements. In Proceedings of the
   2nd Symposium on Requirements Engineering for Information Security (SREIS), pages 15–16, 2002.

   [19] Marc Langheinrich. Privacy by design - principles of privacyaware ubiquitous systems. In Proceedings of the 3rd
   International Conference on Ubiquitous Computing, UbiComp ’01, pages 273–291, 2001.

   [20] Victoria Bellotti and Abigail Sellen. Design for privacy in ubiquitous computing environments. In Proceedings of
   the Third Conference on European Conference on Computer-Supported Cooperative Work, pages 77–92, 1993.

   [21] Jakob Nielsen and Rolf Molich. Heuristic evaluation of user interfaces. In Proceedings of the SIGCHI conference


   Linee Guida per la modellazione delle minacce ed individuazione delle azioni di mitigazione conformi ai principi del Secure/Privacy

on Human factors in computing systems: Empowering people, CHI '90, pages
249–256, 1990. \``\`
