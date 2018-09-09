.. _python:

7.5 PYTHON
==========

Python è un linguaggio di programmazione ad alto livello, orientato agli
oggetti, adatto, tra gli altri usi, per sviluppare applicazioni
distribuite, scripting, computazione numerica e system testing.

Di seguito un elenco delle principali vulnerabilità e delle contromisure
da adottare.

.. _cross-site-scripting-xss-4:

.. _cross-site-scripting-xss-4:

7.5.1 Cross-site scripting (XSS)………………………………………………………………………………………………………………
--------------------------------------------------------------------------

**Come riconoscerla**

::

    Reflected XSS All Clients - puo' utilizzare anche strumenti di tipo "Social engineering" per carpire
   informazioni dagli utenti web tramite tecniche di bassa tecnologia sviluppate da malintenzionati
   per ottenere informazioni personali.
    Ad esempio possono essere simulate pagine quasi identiche ad altri siti di largo utilizzo per
   ottenere informazioni riservate.
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

Al fine di prevenire le problematiche inerenti la vulnerabilita' “Stored
XSS” si consiglia di mettere in atto le indicazioni come di seguito: 
Validare tutti gli input, indipendentemente dalla sorgente. Per la
validazione, si consiglia l'approccio whitelist (sono accettati solo i
dati che adottano una struttura specificata nella whitelist, scartando
quelli che non la rispettano). Controllare: o Data type; o Size; o
Range; o Format; o Expected values;  La validazione non è un sostituto
per la codifica. E' necessario ai fini della sicurezza codificare
completamente tutti i dati dinamici, indipendentemente dalla sorgente,
prima di incorporare queste informazioni in un output. La codifica
dovrebbe essere sensibile al contesto. Per esempio: o Codifica HTML per
pagine HTML; o Attributi HTML codificati per gli output dei dati
relativi; o Codifica JavaScript per server-generated JavaScript.  Si
consiglia di utilizzare la libreria di codifica ESAPI o le funzioni di
libreria sistema incorporate.  Nell'intestazione di risposta
Content-Type HTTP, definire esplicitamente la codifica dei caratteri
(charset) per l'intera pagina.  Impostare la flag httpOnly sul cookie
della sessione, per impedire che eventuali tentativi di tecniche
fraudolente di XSS possano venire in possesso del cookie stesso.

Per ulteriori informazioni si veda:
http://cwe.mitre.org/data/definitions/79.html, CWE-79: Improper
Neutralization of Input During Web Page Generation (‘Cross-site
Scripting’).

.. _code-injection-1:

.. _code-injection-1:

7.5.2 Code Injection
--------------------

**Come riconoscerla**

Un utente malintenzionato potrebbe eseguire codice arbitrario nell'host
del server di applicazioni. A seconda delle autorizzazioni
dell'applicazione che potrebbero essere carpite, si potrebbero avere le
seguenti problematiche:  Alterazione dei privilegi sulla manipolazione
di File (read / create / modify / delete);  Modifiche della struttura
del sito web;  Permettere delle connessioni di rete non autorizzate
verso il server da parte dell'attaccante;  Permettere ad utenti
malintenzionati la gestione dei servizi con possibili Start and stop dei
servizi di sistema;  Acquisizione completa del server da parte
dell'attaccante.

**Come difendersi**

::

    Se possibile, peferire sempre delle whitelist prefissate e riutilizzare l'input anziché una blacklist;
    Evitare qualsiasi compilazione dinamica, esecuzione o valutazione del codice. Se è necessario
   eseguire l'esecuzione dinamica, eseguire tutto il codice dinamico in una sandbox isolata, ad
   esempio AppDomain di .NET o bloccare un thread isolato;
    L'applicazione non deve compilare, eseguire o valutare i dati non attendibili, in particolare
   eventuale input dell'utente;
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
   valori;
    Configurare l'applicazione da eseguire utilizzando un account utente limitato che non disponga di
   privilegi non necessari all'applicativo stesso;
    Se possibile, isolare tutta l'esecuzione dinamica per utilizzare un account utente separato e
   dedicato che abbia privilegi solo per le operazioni e i file specifici utilizzati dall'applicazione, in base
   al principio denominato "Principle of Least Privilege". Il principio stabilisce che agli utenti venga
   attribuito il più basso livello di “diritti” che possano detenere rimanendo comunque in grado di
   compiere il proprio lavoro

Per ulteriori informazioni si veda:
http://cwe.mitre.org/data/definitions/94.html, Improper Control of
Generation of Code (‘Code Injection’) CWE-94

.. _command-injection-2:

.. _command-injection-2:

7.5.3 Command Injection
-----------------------

**Come riconoscerla**

Tramite questa vulnerabilità un aggressore potrebbe eseguire comandi di
sistema arbitrari sull'host del server dell'applicazione. In base alle
autorizzazioni dell'applicazione che potrebbero essere carpite, queste
potrebbero includere:  Alterazione dei privilegi sulla manipolazione di
File (read / create / modify / delete)  Permettere delle connessioni di
rete non autorizzate verso il server da parte dell'attaccante 
Permettere ad utenti malintenzionati la gestione dei servizi con
possibili Start and stop dei servizi di sistema

::

    Acquisizione completa del server da parte dell'attaccante

Attraverso questa vulnerabilità, inoltre, l'applicazione viene portata
ad eseguire dei comandi voluti dall'utente malintenzionato piuttosto che
eseguire il proprio codice applicativo. L'operazione spesso viene
effettuata concatenando stringhe di input dell'utente a codice dannoso.
Potrebbero così essere eseguiti direttamente sul server comandi anche
molto pericolosi per il sistema o per la sicurezza dei dati.

**Come difendersi**

::

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

Per ulteriori informazioni si veda:
http://cwe.mitre.org/data/definitions/77.html, CWE-77: Improper
Neutralization of Special Elements used in a Command (‘Command
Injection’).

.. _connection-string-injection-2:

.. _connection-string-injection-2:

7.5.4 Connection String Injection
---------------------------------

**Come riconoscerla**

Un utente malintenzionato potrebbe manipolare la stringa di connessione
dell'applicazione al database oppure al server. Utilizzando strumenti e
modifiche di testo semplici, l'aggressore potrebbe essere in grado di
eseguire una delle seguenti operazioni:  Danneggiare le performance
delle applicazioni (ad esempio incrementando il valore relativo al MIN
POOL SIZE);  Manomettere la gestione delle connessioni di rete (ad
esempio, tramite TRUSTED CONNECTION);  Dirigere l'applicazione sul
database falso dell'attaccante al posto dell'originario;  Scoprire la
password dell'account di sistema nel database (tramite un brute-force
attack).

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
   Esempio. Codice Python per la vulnerabilità “Connection String Injection”.
   Forma non corretta : L'applicazione crea una stringa di connessione usando l'input dell'utente:
   from sys import stdin
   import cx_Oracle
   print 'Insert your ID: '
   userInput = stdin.readline()
   connection = cx_Oracle.connect(userInput + '/password@99.999.9.99:PORT/SID')
   Forma corretta: il valore inserito dall'utente come numero viene trasferito
   in una stringa prima dell'uso.
   from sys import stdin
   import cx_Oracle
   print 'Insert your ID: '
   userInput = stdin.readline()
   connection = cx_Oracle.connect(str(int(userInput)) +
   '/password@99.999.9.99:PORT/SID')

Per ulteriori informazioni si veda:
http://cwe.mitre.org/data/definitions/99.html, CWE-99: Improper Control
of Resource Identifiers (‘Resource Injection’).

.. _ldap-injection-2:

.. _ldap-injection-2:

7.5.5 LDAP Injection
--------------------

**Come riconoscerla**

Questa vulnerabilità riguarda la gestione delle query di tipo LDAP che
vengono effettuate dalle applicazioni e che potrebbero essere utilizzate
in modo improprio da un utente malintenzionato. Le operazioni che
potrebbero essere eseguite a tal fine sono le seguenti:  Effettuare il
login con un utente diverso da quello inserito dall'utente;  Venire in
possesso di privilegi di sistema non autorizzati;  Rubare le
informazioni. Per comunicare con il proprio database o con un altro
server (ad esempio Active Directory), l'applicazione costruisce
dinamicamente una sua stringa di connessione. Questa stringa di
connessione include valori concatenati inseriti dall'utente per
l'autenticazione stessa. Se i valori immessi dall'utente non sono stati
verificati, né tantomeno sanificati, l'input potrebbe essere utilizzato
per manipolare malamente la stringa di connessione.

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
Injection’).

.. _resource-injection-3:

.. _resource-injection-3:

7.5.6 Resource Injection
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
   Esempio Python:
   Forma non corretta – L'applicazione apre una socket di rete utilizzando un nome host immesso
   dall'utente
   from sys im port stdin
   import socket
   import sys
   userInput = stdin.readline()
   HOST = userInput
   PORT = 8888 # Arbitrary non-privileged port

s = socket.socket(socket.AF_INET, socket.SOCK_STREAM) **print** ‘Socket
created’ #Bind socket to local host and port try: s.bind((HOST, PORT))
**except** socket.error **as** msg: **print** ‘Bind failed. Error Code
:’ + str(msg[0]) + ' Message ' + msg:ref:`section-9` sys.exit()
**print** ‘Socket bind complete’

::

   Forma corretta - L'applicazione indica uno o piu' indirizzi host codificati in una white-list che
   l'utente puo' scegliere tra questi.
   import socket
   import sys
   HOST = '' # Symbolic name, meaning all available interfaces
   PORT = 8888 # Arbitrary non-privileged port
   s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
   print 'Socket created'
   #Bind socket to local host and port
   try:
   s.bind((HOST, PORT))
   except socket.error as msg:
   print 'Bind failed. Error Code : ' + str(msg[0]) + ' Message ' + msg[1]
   sys.exit()
   print 'Socket bind complete'

Per ulteriori informazioni si veda:
http://cwe.mitre.org/data/definitions/99.html, CWE-99: Improper Control
of Resource Identifiers (‘Resource Injection’).

.. _second-order-sql-injection-3:

.. _second-order-sql-injection-3:

7.5.7 (Second Order) SQL Injection
----------------------------------

**Come riconoscerla**

Un utente malintenzionato potrebbe accedere direttamente a tutti i dati
del sistema. Utilizzando strumenti e modifiche di testo semplici,
l'aggressore potrebbe rubare qualsiasi informazione riservata
memorizzata dal sistema (ad esempio i dati personali dell'utente o le
carte di credito) e eventualmente modificare o cancellare i dati
esistenti. L'applicazione comunica con il suo database inviando una
query SQL in formato testo. L'applicazione crea la query semplicemente
concatenando le stringhe tra cui i dati ottenuti dal database. Poiché
questi dati possono essere stati in precedenza ottenuti dall'input
dell'utente e non sono stati verificati la validità del tipo di dati né
successivamente sanificati, i dati potrebbero contenere comandi SQL che
verrebbero interpretati come tali dal database.

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
   e le associazioni degli oggetti (per comandi e parametri);
   o Una soluzione ancora migliore è quella di utilizzare una libreria ORM, come EntityFramework,
   Hibernate o iBatis.
    Limitare l'accesso agli oggetti e alle funzionalità di database, in base al "Principle of Least Privilege"
   (non fornire diretti agli utenti maggiori di quelli strettamente necessari).

Per ulteriori informazioni si veda:
http://cwe.mitre.org/data/definitions/89.html, CWE-89: Improper
Neutralization of Special Elements used in an SQL Command (‘SQL
Injection’).

.. _xpath-injection-1:

.. _xpath-injection-1:

7.5.8 XPath Injection
---------------------

**Come riconoscerla**

Sulla base della tipologia di informazioni contenute nel documento XML
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
   o Expected values;
    Evitare che la costruzione della query xpath sia dipendente dalle informazioni inserite dall'utente.
   Possibilmente mappare la query di tipo XPath con i parametri utente mantenendo la separazione
   tra dati e codice. Nel caso fosse necessario includere l'input del'utente nella query, l'input stesso
   dovra' essere precedentemente validato correttamente.
   Esempio
   o Forma non corretta - L'applicazione utilizza una stringa inserita dall'utente per costruire una
   query XPath:
   from sys import stdin
   import xpath
   print 'Insert item number: '
   userInput = stdin.readline()
   xpath.find('//item' + userInput, doc)
   o Forma corretta - La stringa inserita dall'utente viene trasformata in un numero intero prima
   dell'uso nella query XPath:
   from sys import stdin
   import xpath
   print 'Insert item number: '
   userInput = stdin.readline()
   xpath.find('//item' + str(int(userInput)), doc)

Per ulteriori informazioni si veda:
http://cwe.mitre.org/data/definitions/643.html, CWE-643: Improper
Neutralization of Data within XPath Expressions (‘XPath Injection’).

.. _os-access-violation:

7.5.9 OS Access Violation
-------------------------

**Come riconoscerla**

Un utente malintenzionato potrebbe preparare un set di dati dannosi in
input che potrebbero causare una violazione di accesso, perdita di dati
privati, danneggiamento di dati o un arresto di eventuali servizi con
possibile arresto dell'applicazione stessa. Il modulo Python OS fornisce
un'interfaccia portatile destinata all'utilizzo della funzionalità del
sistema operativo. Il modulo OS di Python consente l'accesso e la
manipolazione di file arbitrari. Nel caso in cui un aggressore fosse in
grado di passare un percorso di input specifico per il modulo OS,
potrebbero verificarsi situazioni di violazione di accesso o di
corruzione dei dati.

**Come difendersi**

::

    Trust boundaries - Non utilizzare il modulo OS per la manipolazione di file host ricevuti da una
   fonte non attendibile o controllata dall'utente. Normalmente l'applicazione potrebbe fidarsi dei
   dati provenienti dal proprio server (DB, cache, ecc.).
    Comunicazione protetta - Se un'applicazione riceve un nome di attributo da un'applicazione
   attendibile in un ambiente attendibile, assicurarsi che venga utilizzata una connessione di rete
   crittografata.
    Assicurarsi che il path di un file che si vuole manipolare sia validato in modo corretto:
   o Evitare, se possibile, che il path di un file possa essere inserito da un utente in modo dinamico.
   o Assicurarsi che il path di un file rispecchi completamente delle regole canoniche.
   o Limitare l'accesso al percorso di file all'interno di una directory specifica (sandbox).
    Creare una whitelist di file o directory che possono essere manipolati in modo sicuro e consentire
   l'accesso solo a questi file o directory.
   Esempio Python
   o Forma non corretta - l'applicazione riceve un file path dall'utente e rimuove il file stesso:
   import os
   import sys
   path = sys.stdin.readline()[:-1]
   os.remove(path)
   o Forma corretta - l'applicazione restringe l'accesso ad un file ad una specifica directory:
   import os
   import sys
   def is_safe_path (basedir, path):
   return os.path.abspath(path).startswith(basedir)
   path = sys.stdin.readline()[:-1]
   if not is_safe_path('/tmp/userfiles', path):
   sys.stdout.write('Not allowed!\n')
   sys.exit()
   os.remove(path)
