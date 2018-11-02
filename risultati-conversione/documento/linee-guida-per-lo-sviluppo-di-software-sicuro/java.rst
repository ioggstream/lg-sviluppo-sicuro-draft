.. _java:

7.2 JAVA
========

Java è un linguaggio di programmazione orientato agli oggetti, derivato
dal C++ e progettato a partire dal 1991 da James Gosling assieme ad un
gruppo di impiegati di Sun Microsystem. Le caratteristiche del
linguaggio lo rendono oggi l'alternativa più diffusa sia per la
progettazione di applicazioni client-server che per lo sviluppo di Web
Services, seppure l'ambito in cui ha attualmente riscosso maggiore
successo è proprio quello Web. Sun Microsystem, che ancora oggi ne
detiene il mantenimento e ne detta le linee di sviluppo, ha recentemente
rilasciato le diverse tecnologie che compongono Java (J2EE, J2ME, etc..)
sotto licenza open source **GPL**.

Di seguito le principali vulnerabilità e relative contromisure da
adottare.

.. _cross-site-scripting-xss-2:

.. _cross-site-scripting-xss-2:

7.2.1 Cross-site scripting (XSS)………………………………………………………………………………………………………………
--------------------------------------------------------------------------

**Come riconoscerla**

::

    Reflected XSS All Clients - puo' utilizzare anche strumenti di tipo "Social engineering" per carpire
   informazioni dagli utenti web tramite tecniche di bassa tecnologia sviluppate da malintenzionati
   per ottenere informazioni personali.
   Ad esempio possono essere simulate pagine quasi identiche ad altri siti di largo utilizzo per ottenere
   informazioni riservate.
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
   desiderato. La codifica dovrebbe essere context-sensitive. Ad esempio:
   o Codifica HTML per pagine HTML;
   o Attributi HTML codificati per gli output dei dati relativi;
   o Codifica JavaScript per server-generated JavaScript.
    Si consiglia di utilizzare la libreria di codifica ESAPI o le funzioni di libreria sistema incorporate;
    Nell'intestazione di risposta Content-Type HTTP, definire esplicitamente la codifica dei caratteri
   (charset) per l'intera pagina;
    Impostare la flag httpOnly sul cookie della sessione, per impedire che eventuali tentativi di tecniche
   fraudolente di XSS possano venire in possesso del cookie stesso.

Per ulteriori informazioni si veda:
http://cwe.mitre.org/data/definitions/79.html, CWE-79: Improper
Neutralization of Input During Web Page Generation (‘Cross-site
Scripting’).

.. _code-injection:

7.2.2 Code Injection
--------------------

**Come riconoscerla**

Accade quando l'applicazione utilizza, concatenandole, stringhe in input
non bonificate. L'attaccante potrebbe introdurvi azioni che potrebbero
essere eseguite direttamente nell'application server. Ciò potrebbe
portare ad azioni indesiderate.

**Come difendersi**

::

    Evitare di eseguire del codice dinamicamente, specialmente se costruito con input proveniente
   dall’esterno.
    Occorre verificare sempre l’input, fissando controlli rigidi che impediscano di immettere caratteri e
   tipi di dati potenzialmente dannosi. L’optimum è designare una white list di valori ammessi e
   scartare tutto ciò che non vi rientra.
   Esempio
   Il seguente codice permette di eseguire qualunque stringa provenga dall’esterno, senza controlli.
   public class CodeInjection {
   static void main(String[] args){
   System.load(args[0]);
   }
   }
   Nel codice seguente, l’input viene controllato contro una white list di valori ammessi:
   public class CodeInjectionFixed {
   static void main(String[] args){
   String fileName = null;
   switch(args[0]){
   case "First":
   fileName="First.txt";
   break;
   case "Second":
   fileName="Second.txt";
   break;
   case "Third":
   fileName="Third.txt";
   break;
   default :
   fileName="none.txt";
   }
   System.load(fileName);
   }
   }

Si veda: http://cwe.mitre.org/data/definitions/94.html, CWE-94: Improper
Control of Generation of Code (‘Code Injection’).

.. _command-injection-1:

.. _command-injection-1:

7.2.3 Command Injection
-----------------------

**Come riconoscerla**

Accade quando l'applicazione esegue comandi di sistema operativo sul
server che la ospita. Un attaccante potrebbe utilizzare questa
caratteristica per eseguire comandi dannosi. In base alle autorizzazioni
dell'applicazione che potrebbero essere carpite, queste potrebbero
includere:  Alterazione dei privilegi sulla manipolazione di File (read
/ create / modify / delete)  Permettere delle connessioni di rete non
autorizzate verso il server da parte dell'attaccante  Permettere ad
utenti malintenzionati la gestione dei servizi con possibili Start and
stop dei servizi di sistema  Acquisizione completa del server da parte
dell'attaccante

Attraverso questa vulnerabilità l'applicazione viene portata ad eseguire
dei comandi voluti dall'utente malintenzionato piuttosto che eseguire il
proprio codice applicativo. L'operazione spesso viene effettuata
concatenando stringhe di input dell'utente a codice dannoso. Potrebbero
così essere eseguiti direttamente sul server comandi anche molto
pericolosi per il sistema o per la sicurezza dei dati.

**Come difendersi**

::

    Scrivere il codice in modo che non esegua nessuna shell dei comandi. Utilizzare a questo scopo le
   API messe a disposizione delle librerie java;
    Se dovessero permanere shell dirette, fare in modo che siano stringhe statiche che on utilizzino
   l’input dell’utente;
    È comunque meglio validare l’input, filtrando i caratteri pericolosi, attraverso una struttura definita
   per l’input, o – meglio ancora – imponendo una white list di valori ammessi.
   Esempio
   caso in cui si potrebbe avere command injection:
   public class CommandInjection {
   public static void main(String[] args) throws IOException {
   Runtime runtime = Runtime.getRuntime();
   Process proc = runtime.exec( "fileNumber" + args[0] + ".exe" );
   }
   }
   Nel codice seguente, invece, l’injection non sarebbe possibile:
   public class CommandInjectionFixed {
   public static void main(String[] args) throws IOException {
   int num = Integer.parseInt(args[0]);
   // Controlli sul numero immesso
   Runtime runtime = Runtime.getRuntime();
   Process proc = runtime.exec( "fileNumber" + num + ".exe" );
   }
   }

Per ulteriori informazioni si veda:
http://cwe.mitre.org/data/definitions/77.html, CWE-77: Improper
Neutralization of Special Elements used in a Command (‘Command
Injection’).

.. _connection-string-injection-1:

.. _connection-string-injection-1:

7.2.4 Connection String Injection
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
nel database (tramite un brute-force attack) Per comunicare con il
proprio database o con un altro server (ad esempio Active Directory),
l'applicazione costruisce dinamicamente una sua stringa di connessione.
Questa stringa di connessione include valori concatenati inseriti
dall'utente per l'autenticazione stessa. Se i valori immessi dall'utente
non sono stati verificati né tantomeno sanificati, l'input potrebbe
essere utilizzato per manipolare malamente la stringa di connessione.

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
   Esempio
   Il seguente codice:
   public class ConnectionStringInjection {
   public static void main(String[] args) throws SQLException {
   Scanner userInputScanner = new Scanner(System.in);
   System.out.print("\nEnter url name: ");
   String connURL = userInputScanner.nextLine();
   Connection con = DriverManager.getConnection(connURL,
   "username", "password");
   }
   }
   Andrebbe corretto come segue:
   public class ConnectionStringInjectionFixed {
   public static void main (String[] args) throws SQLException {
   HashMap<String, String> sanitize = new HashMap<String,
   String>();
   sanitize.put("DB_url_1", "DB_url_1");
   sanitize.put("DB_url_2", "DB_url_2");
   sanitize.put("DB_url_3", "DB_url_3");
   Scanner userInputScanner = new Scanner(System.in);
   System.out.print("\nEnter url name: ");
   String connURL = userInputScanner.nextLine();
   Connection con =
   DriverManager.getConnection(sanitize.get(connURL), "username",
   "password");
   }
   }
   Il valore è valido se è uno di quelli memorizzati nell’hashmap.

Per ulteriori informazioni si veda:
http://cwe.mitre.org/data/definitions/99.html, CWE-99: Improper Control
of Resource Identifiers (‘Resource Injection’).

.. _ldap-injection-1:

.. _ldap-injection-1:

7.2.5 LDAP Injection
--------------------

**Come riconoscerla**

Si verifica quando l'applicazione riceve le credenziali d'accesso dal un
server LDAP. Se la query a quest'ultimo è effettuata tramite una stringa
che concatena l'input dell'utente, l'attaccante potrebbe modificare il
suo input in maniera tale da accedere all'applicazione facendosi passare
per un'utente abilitato, accedendo così a dati ai quali non avrebbe
dovuto accedere. Questa vulnerabilità (LDAP Injection) riguarda la
gestione delle query di tipo LDAP che vengono effettuate dalle
applicazioni e che potrebbero essere utilizzate in modo improprio da un
utente malintenzionato. Le operazioni che dovrebbero essere eseguite a
tal fine sono le seguenti:  Effettuare il login con un utente diverso
da quello inserito dall'utente,  Venire in possesso di privilegi di
sistema non autorizzati,  Rubare le informazioni. Per comunicare con il
proprio database o con un altro server (ad esempio Active Directory),
l'applicazione costruisce dinamicamente una sua stringa di connessione.
Questa stringa di connessione include valori concatenati inseriti
dall'utente per l'autenticazione stessa. Se i valori immessi dall'utente
non sono stati verificati, né tantomeno sanificati, l'input potrebbe
essere utilizzato per manipolare malamente la stringa di connessione.

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
   Esempio
   Invece di utilizzare una stringa incontrollata:
   String userName = Request.QueryString["user"];
   Utilizzare una stringa sottoposta a un filtro:
   String userName = Request.QueryString["user"];
   userName = Regex.Replace(userName, "^\\d{3}-\\d{3}-\\d{4}$", "");

Per ulteriori informazioni si veda:
http://cwe.mitre.org/data/definitions/90.html, CWE-90: Improper
Neutralization of Special Elements used in an LDAP Query (‘LDAP
Injection’).

.. _resource-injection-1:

.. _resource-injection-1:

7.2.6 Resource Injection
------------------------

**Come riconoscerla**

Si verifica quando l'applicazione ha la necessità di far aprire un
socket da parte dell'utente. Un utente malintenzionato potrebbe aprire
una backdoor che potrebbe permettere all'attaccante di connettersi
direttamente al server con possibili conseguenze molto gravi per la
sicurezza. Tramite questa vulnerabilità un possibile malintenzionato
potrebbe utilizzare eventuali connessioni aperte dall'utente, nel caso
non fossero gestite adeguatamente.

**Come difendersi**

::

    Non consentire a un utente di definire i parametri relativi ai sockets di rete.
    Validare l’input raffrontandolo con una white list di valori possibili ammessi.
   Esempio
   La situazione iniziale:
   public class ResourceInjection {
   public static void main(String[] args) {
   Scanner userInputScanner = new Scanner(System.in);
   System.out.print("\nEnter port number: ");
   int portNumber = Integer.parseInt(userInputScanner.nextLine());
   try {
   ServerSocket serverSocket = new ServerSocket(portNumber);
   } catch (Exception e) {
   System.err.println("Caught Exception: " +
   e.getMessage());
   }
   }
   }
   Viene risolta limitando le possibilità a poche scelte (white list):
   public class ResourceInjectionFixed {
   public static void main(String[] args) {
   Scanner userInputScanner = new Scanner(System.in);
   System.out.print("\nEnter port name: ");
   String portName = userInputScanner.nextLine();
   int portNum;
   switch (portName) {
   case "ftps":
   portNum = 989;
   break;
   case "ftp":
   portNum = 20;
   break;
   case "smtp":
   portNum = 25;
   break;
   default:
   portNum = 80;
   }
   try {
   ServerSocket serverSocket = new ServerSocket(portNum);
   } catch (Exception e) {
   System.err.println("Caught Exception: " +
   e.getMessage());
   }
   }
   }

Per ulteriori informazioni si veda:
http://cwe.mitre.org/data/definitions/99.html, CWE-99: Improper Control
of Resource Identifiers (‘Resource Injection’).

.. _second-order-sql-injection-1:

.. _second-order-sql-injection-1:

7.2.7 (Second Order) SQL Injection
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
   o Expected values;
    Invece di concatenare le stringhe si consiglia di:
   o Utilizzare componenti di database sicuri come le procedure memorizzate, query parametrizzate
   e le associazioni degli oggetti (per comandi e parametri).
   o Una soluzione ancora migliore è quella di utilizzare una libreria ORM, come EntityFramework,
   Hibernate o iBatis,
    Limitare l'accesso agli oggetti e alle funzionalità di database, in base al "Principle of Least Privilege"
   (non fornire diretti agli utenti maggiori di quelli strettamente necessari).
    Occorre validare in ogni caso l’input e vanno accettati solo valori che corrispondono a un elenco di
   valori ammessi (white list).
    Per evitare la SQL Injection è necessario evitare di concatenare le stringhe e affidarsi alle stored
   procedures e alle query parametriche (prepared statement). Meglio ancora utilizzare una libreria
   ORM come EntityFramework, Hibernate, or iBatis.
   Esempio
   public class SQL_Injection {
   public static void getUserId(Connection con) {
   System.out.println("enter user name");
   Scanner in = new Scanner(System.in);
   String user = in.nextLine();
   String query = "select user_id from User where user = " + user;
   try {
   Statement stmt = con.createStatement();
   ResultSet rs = stmt.executeQuery(query);
   } catch (Exception e) {
   e.printStackTrace();
   }
   }
   }
   public class SQL_Injection_Fixed {
   public static void getUserId(Connection con) {
   System.out.println("enter user name");
   Scanner in = new Scanner(System.in);
   String user = in.nextLine();
   user = user.replaceAll("'", "");
   String query = "select user_id from User where user = " + user;
   try {
   Statement stmt = con.createStatement();
   ResultSet rs = stmt.executeQuery(query);
   } catch (Exception e) {
   e.printStackTrace();
   }
   }
   }

Per ulteriori informazioni si veda:
http://cwe.mitre.org/data/definitions/89.html, CWE-89: Improper
Neutralization of Special Elements used in an SQL Command (‘SQL
Injection’).

.. _xpath-injection:

7.2.8 XPath Injection
---------------------

**Come riconoscerla**

Si ha quando:  L'applicazione interroga un documento xml usando una
query XPath, creata concatenando stringhe provenienti dall'esterno.
L'attaccante potrebbe immettere una stringa che modifica la query XPath,
ottenendo dal documento xml informazioni non dovute.  A seconda del
tipo di informazioni contenute nel documento XML interrogato, un utente
malintenzionato potrebbe, manipolandole, causare gravi danni all'utente
come il furto di dati non autorizzati oppure la sostituzione dell'utente
stesso.  L'applicazione interroga un documento XML utilizzando una
query XPath testuale. L'applicazione crea la query semplicemente
concatenando le stringhe tra cui l'input dell'utente. Poiché l'input
dell'utente non è stato verificato per la validità del tipo di dati né
successivamente sanificato, l'i nput potrebbe essere manipolato, in tal
modo potrebbe essere possibile avere delle selezioni finali sbagliate
dal documento XML durante l'esecuzione dell'applicazione.

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
    Validare tutti gli input che provengono dall’esterno, così come in tutti i casi di injection;
    La soluzione ideale consiste nell’evitare che le query xpath dipendano dall’input dell’utente. Se
   proprio è necessario farlo, occorre costruire query parametriche, nelle quali solo alcuni valori
   provengono dall’esterno. L’input va comunque validato, filtrando eventualmente caratteri
   potenzialmente dannosi.
   Esempio
   public class XPath_Injection {
   public static void main(String[] args) {
   Scanner userInputScanner = new Scanner(System.in);
   System.out.print("\nEnter xpath expression: ");
   String expression = userInputScanner.nextLine();
   // read a string value
   XPath xPath = XPathFactory.newInstance().newXPath();
   try {
   XPathExpression email = xPath.compile(expression);
   } catch (XPathExpressionException e) {
   e.printStackTrace();
   }
   }
   }
   L’input dell’utente deve essere ricondotto a valori ammessi (white list):
   public class XPath_Injection_Fixed {
   public static void main(String[] args) {
   HashMap<String, String> sanitize = new HashMap<String, String>();
   sanitize.put("student", "/class/student");
   sanitize.put("graduate", "/class/graduate");
   sanitize.put("professor", "/class/professor");
   Scanner userInputScanner = new Scanner(System.in);
   System.out.print("\nEnter xpath expression: ");
   String expression = userInputScanner.nextLine();
   // read a string value
   XPath xPath = XPathFactory.newInstance().newXPath();
   try {
   XPathExpression email = xPath.compile(sanitize.get(expression));
   } catch (XPathExpressionException e) {
   e.printStackTrace();
   }
   }
   }

Per ulteriori informazioni si veda:
http://cwe.mitre.org/data/definitions/643.html, CWE-643: Improper
Neutralization of Data within XPath Expressions (‘XPath Injection’).

.. _ulteriori-indicazioni-per-lo-sviluppo-sicuro-1:

.. _ulteriori-indicazioni-per-lo-sviluppo-sicuro-1:

7.2.9 Ulteriori indicazioni per lo sviluppo sicuro
--------------------------------------------------

La seguente raccolta di Best Practices è riconosciuta ufficialmente da
Oracle Java.

.. _inizializzazione-..:

7.2.9.1 Inizializzazione ……………………………………………………………………………………………………………………………………..
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

::

    Evitare le dipendenze dall’inizializzazione:
   o scrivere le classi in modo che, prima di utilizzare l’oggetto, questo sia stato correttamente
   inizializzato.
    Per evitare l’allocazione di oggetti non inizializzati:
   o rendere tutte le variabili private e, se necessario fornirne l’accesso dall’esterno della classe
   stessa: questo deve sempre essere consentito esclusivamente attraverso i metodi get() e set();

o aggiungere in ogni oggetto una variabile booleana privata (es:
isInizialized) e fare in modo che ogni costruttore, come ultima
operazione, la inizializzi a “true"; o in ogni metodo che non sia un
costruttore verificare che la variabile di inizializzazione della classe
sia impostata a true prima di eseguire qualsiasi operazione; Esempio
public class MyClass { private boolean isInizialized; private String
nome; public MyClass(String nome){ this.nome = nome; this.isInizialized
= true; } public String getNome(){ return (isInizialized == true?
this.nome : null); } }  Se la classe ha costruttori statici è
necessario seguire la stessa procedura ma a livello di classe: o rendere
tutte le variabili statiche private e, se necessario fornirne l'accesso
dall'esterno della classe stessa: questo deve sempre essere consentito
esclusivamente attraverso i metodi get() e set(); o aggiungere alla
classe una variabile booleana privata statica (es: isClassInizialized) e
fare in modo che ogni costruttore statico, come ultima operazione, la
inizializzi a "true"; o prima di eseguire qualsiasi operazione, in ogni
metodo statico ed ogni costruttore si deve verificare che la variabile
"isClassInitialized” sia impostata a "true";  Gestione delle
allocazioni / deallocazioni di memoria dinamica;  Prima di uscire da
una classe ricordarsi sempre di azzerare il contenuto delle variabili.
Si supponga, nel seguente esempio, che la variabile k contenesse la
chiave per decriptare un messaggio cifrato: Esempio - Forma non
corretta: public class Decodificatore { private byte[] k; } Esempio -
Forma corretta: public class Erase { private byte[] k; public void
clear() { for(int i = 0; i < k.length; i++) k [i] = (byte) 0x00; } } 
Limitare l'accesso alle classi, ai metodi ed alle variabili;  Ogni
classe, metodo e variabile dovrebbe essere definita come private o
protected. I casi del tutto eccezionali dovrebbero essere ampiamente
motivati e documentati. Ogni variabile Private è accessibile unicamente
attraverso metodi set() e get() per mantenere l'oggetto al sicuro.
Esempio public class Studente { private int eta; public int getEta(){
return this.eta; } public int setEta(int eta){ this.eta = eta; } }

::

    Ogni costante deve essere definita con i modificatori Static Final per mantenere il valore della
   costante immutabile e renderla accessibili staticamente.
   Esempio
   static final int key = 1;

.. _visibilità:

7.2.9.2 Visibilità ………………………………………………………………………………………………………………………………………………
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

::

    Non dipendere dalla visibilità del package.
    Classi, metodi e variabili devono essere esplicitamente marcate come private, protette o pubbliche,
   per limitare il livello di accesso da parte di altri oggetti.

.. _modificatori:

7.2.9.3 Modificatori …………………………………………………………………………………………………………………………………………
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

::

    Rendere sempre le classi, i metodi e le variabili di tipo finale.
    Ogni classe, metodo e variabile dovrebbe essere definita di tipo final. I casi del tutto eccezionali
   dovrebbero essere ampiamente motivati e documentati. L'utilizzo di questo modificatore, inoltre,
   consente di aumentare l'efficienza del programma in fase di esecuzione in quanto non consente il
   "late binding"
   Esempio
   public final class MyFinalClass {
   [...]
   }
   public class MyClass {
   final int myConst = 123;
   [...]
   }
   public class MyClass {
   [...]
   public final void stopOverriding() {
   [...]
   }
   }
    Evitare l’utilizzo di variabili di tipo static;
    Ove possibile evitare sempre l’utilizzo di variabili di tipo static.

.. _utilizzo-degli-oggetti-mutevoli-..:

7.2.9.4 Utilizzo degli oggetti mutevoli ………………………………………………………………………………………………………………..
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Gli oggetti mutevoli (ad esempio array, liste, vettori, etc..) non
dovrebbero mai essere ritornati a codice potenzialmente insicuro e non
dovrebbero mai essere memorizzati internamente in modo diretto
(dovrebbero invece essere opportunamente clonati) se provenienti da
codice potenzialmente insicuro. Esempio 1 - Forma non corretta: public
Date getDate() { return fDate; } Esempio 1 - Forma corretta: public Date
getDate() { return new Date(fDate.getTime()); } Esempio 2 - Forma non
corretta: public void useDate(Date date) { if (isValid(date))
scheduleTask(date);

.. _section-42:

.. _section-42:

}
^

Esempio 2 - Forma corretta: public void useDate(Date date) { Date
copied_date = new Date(date.getTime()); if (isValid(copied_date))
scheduleTask(date); }

.. _definizione-delle-classi-..:

7.2.9.5 Definizione delle classi …………………………………………………………………………………………………………………………..
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

::

    Evitare l’utilizzo di classi interne (inner). L’utilizzo di Inner Classess deve essere sempre evitato. Nei
   casi del tutto eccezionali, comunque, le classi interne devono sempre essere definite come private.
   Esempio - Forma non corretta:
   package esempio;
   public class MyFirstClass {
   [...]
   private class MySecondClass {
   }
   [...]
   }
   Esempio - Forma corretta:
   package esempio;
   public class MyFirstClass {
   [...]
   }
   class MySecondClass {
   [...]
   }
    Dotare ogni classe di un codice di versione
    Inserire un codice di versione per ogni classe, collocandolo all’interno di una variabile pubblica final,
   ed effettuare i controlli per la coerenza di versione sulle classi del package.

.. _codice-e-permessi-speciali-..:

7.2.9.6 Codice e permessi speciali ……………………………………………………………………………………………………………………..
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

::

    Evitare di assegnare al codice e permessi speciali.
    Evitare di firmare il codice prodotto cercando sempre di scriverlo in modo che non abbia bisogno di
   permessi speciali diversi da quelli definiti nella sandbox. Nei casi del tutto eccezionali in cui il codice
   necessiti di privilegi speciali al fine di effettuare particolari operazioni (es. rilevare le proprietà del
   sistema, leggere files anche se collocati in java.home, aprire sockets, scrivere files o assegnargli le
   proprietà, caricare librerie dinamiche mediante System.loadLibrary o
   Runtime.getRuntime.loadLibrary, etc.), è necessario accertarsi che il livello di privilegi concessi sia il
   minimo indispensabile, motivare e documentare ampiamente le necessità ed effettuare una
   verifica approfondita del codice stesso. Se è necessario firmare il codice prodotto, le classi
   interessate dovrebbero essere raggruppate tutte in un unico archivio.

.. _esecuzione-dei-comandi-di-sistema:

7.2.9.7 Esecuzione dei comandi di sistema …………………………………………………………………………………………………………
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Supponiamo che un aggressore assegni alla variabile filename un valore
del tipo: filename ="joe; /bin/rm – rf /*"; Nell'esempio, sotto
riportato: nella forma non corretta verrà eseguito il codice malevolo;
nella forma corretta, il codice malevolo sarà, invece, ignorato.

Esempio - Forma non corretta: void method (String filename) {
System.exec(“more” + filename); }

Esempio - Forma corretta: void method (String filename){ if (new
File(filename).exists()){ System.exec(“more” + filename); } }

.. _oggetti-..:

7.2.9.8 Oggetti ………………………………………………………………………………………………………………………………………………..
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

::

    Rendere le classi e gli oggetti non clonabili. Di seguito viene riportato un esempio su come è
   possibile rispettare questa regola:
   [...]
   public final void clone() throws java.lang.CloneNotSupportedException {
   throw new java.lang.CloneNotSupportedException();
   }
   [...]
    Rendere le classi e gli oggetti non clonabili. Nei casi eccezionali, che dovrebbero essere motivati e
   ampiamente documentati, rendere i metodi che consentono la clonazione di tipo final in modo da
   evitare potenziali malevoli override dei metodi stessi. Di seguito viene riportato un esempio su
   come è possibile gestire queste eccezioni:
   [...]
   public final void clone() throws java.lang.CloneNotSupportedException {
   super.clone();
   }
   [...]
    Comparazione degli oggetti di classe. Non effettuare mai la comparazione per nome degli oggetti di
   classe. Di seguito viene riportato un esempio su come è possibile rispettare questa regola:
   Esempio - Forma non corretta:
   public class MyClass {
   public boolean sameClass (Object o) {
   Class thisClass = this.getClass();
   Class otherClass = o.getClass();
   return (thisClass.getName() == otherClass.getName());
   }
   }
   Esempio - Forma corretta:
   package esempio;
   public class MyClass {
   public boolean sameClass (Object o) {
   Class thisClass = this.getClass();
   Class otherClass = o.getClass();
   return (thisClass == otherClass);
   }
   }

.. _serializzazione-e-deserializzazione..:

7.2.9.9 Serializzazione e deserializzazione…………………………………………………………………………………………………………..
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

::

    Rendere le classi e gli oggetti non serializzabili. Di seguito viene riportato un esempio su come è
   possibile rispettare questa regola:
   [...]
   private final void writeObject(ObjectOutputStream out) throws
   java.io.IOException {
   throw new java.io.IOException("L’oggetto non può essere serializzato ");
   }
   [...]
    Rendere le classi e gli oggetti non deserializzabili. Di seguito un esempio su come è possibile
   rispettare questa regola:
   [...]
   private final void readObject(ObjectInputStream in) throws
   java.io.IOException {
   throw new java.io.IOException("L’oggetto non può essere
   deserializzato");
   }
   [...]

.. _memorizzazione-delle-informazioni-riservate:

7.2.9.10 Memorizzazione delle informazioni riservate …………………………………………………………………………………………
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

::

    Non inserire informazioni riservate all’interno del codice
    Informazioni riservate, come chiavi crittografiche, passwords, certificati, etc., non devono mai
   essere inserite e presenti all’interno del codice o nelle librerie utilizzate.

.. _packages:

7.2.9.11 Packages ……………………………………………………………………………………………………………………………………………
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

::

    Creazione dei packages.
    Creare i packages in base alle funzioni e non ai layer dell’applicazione. Già in fase di progettazione
   dell’applicazione è indispensabile far confluire funzioni identiche o simili per genere, nello stesso
   package.
    Protezione dei packages.
   o E’ necessario proteggere i package a livello globale, contro l’immissione di codice malevolo
   o alterato. Di seguito vengono riportati due esempi su come rispettare questa regola
   // Inserire la seguente linea nel file java.security properties.
   // Ciò causerà un’eccezione nel loader defineClass non appena
   // si proverà a definire una nuova classe all’interno del pacchetto,
   // a meno che il codice non sia stato dotato del seguente permesso
   // RuntimePermission("defineClassInPackage."+package)
   [...]
   package.definition=Pacchetto1 [,Paccchetto2,...,Pacchetton]
   [...]
   o E’ anche possibile inserire le classi del pacchetto in un file JAR sigillato. In questo modo
   nessun codice può ottenere il permesso ad ampliare il pacchetto e non c’è quindi motivo di
   modificare il file java.security properties.
   o E’ necessario proteggere l’accesso. Ciò può essere fatto inserendo la seguente linea nel file
   java.security properties:
   [...]
   package.access=Pacchetto1 [,Pacchetto2,...,Pacchetton]
   [...]
   Ciò causerà un’eccezione nel loader loadClass non appena si proverà ad accedere ad una
   classe all’interno del pacchetto, a meno che il codice non sia stato dotato del seguente
   permesso:
   [...]
   RuntimePermission("accessClassInPackage."+package)
   [...]

.. _gestione-delle-eccezioni:

7.2.9.12 Gestione delle eccezioni ………………………………………………………………………………………………………………………
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

::

    Non consentire l’input nullo. Nel caso si crei un’eccezione, il programma ritornerà un errore
   sconosciuto. La forma corretta nell’esempio che segue, mostra come utilizzare le capacità di logging
   di Java per mantenere traccia delle eccezioni.
   Esempio - Forma non corretta:

import java.io.\ *; import java.util.*; public class BadEmptyCatch {
List quarks = new ArrayList(); quarks.add(“hello word”);
FileOutputStream file = null; ObjectOutputStream output = null; try{
file = new FileOutputStream(“quarks.ser”); output = new
ObjectOutputStream(file); output.writeObject(quarks); } catch(Exception
exception){System.err.println(exception); } finally{ try { if (output !=
null) { output.close(); } } catch(Exception exception){ } } Esempio -
Forma corretta: import java.io.\ *; import java.util.*; import
java.util.logging.*;

public class ExerciseSerializable {

public static void main(String args) { List quarks = new ArrayList();
quarks.add(“hello word”); ObjectOutput output = null; try{ OutputStream
file = new FileOutputStream( “quarks.ser”); OutputStream buffer = new
BufferedOutputStream( file ); output = new ObjectOutputStream(buffer);
output.writeObject(quarks); } catch(IOException ex){
fLogger.log(Level.SEVERE, “Cannot perform output.”, ex); } finally{ try
{ if (output != null) { output.close(); } } catch (IOException ex ){
fLogger.log(Level.SEVERE, “Cannot close output stream.”, ex); } }

::

    Specificare la clausola throws. Evitare di raggruppare le eccezioni in una classe di eccezioni
   generica, in quanto rappresenterebbe una perdita di informazioni importanti.
   Esempio - Forma non corretta:
   import java.io.*;
   import java.util.*;
   public class BadGenericThrow {
   public void makeFile() throws Exception {
   //create a Serializable List
   List<String> quarks = new ArrayList<String>();
   quarks.add("hello word");
   FileOutputStream file = null;
   ObjectOutputStream output = null;
   try{
   file = new FileOutputStream("quarks.ser");
   output = new ObjectOutputStream(file);
   output.writeObject(quarks);
   }
   finally{
   if (output != null) {
   output.close();
   }
   }
   }
   }
   Esempio - Forma corretta:
   import java.io.*;
   import java.util.*;
   public class BadGenericThrow {
   public void makeFile() throws IOException, FileNotFoundException{
   //create a Serializable List
   List<String> quarks = new ArrayList<String>();
   quarks.add("hello word");
   FileOutputStream file = null;
   ObjectOutputStream output = null;
   try{
   file = new FileOutputStream("quarks.ser");
   output = new ObjectOutputStream(file);
   output.writeObject(quarks);
   }
   finally{
   if (output != null) {
   output.close();
   }
   }
   }
   }

.. _java-applet-..:

7.2.9.13 Java Applet ………………………………………………………………………………………………………………………………………..
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

::

    Non memorizzare informazioni critiche. Non memorizzare mai nel codice informazioni critiche,
   relative ad aspetti di sicurezza (es. password, chiavi crittografiche, etc.) e che possono essere, in
   qualche modo, nocive. Questa regola è valida, anche se vengono utilizzati meccanismi di
   offuscamento o crittografia della Applet.
    Visibilità. Ogni classe, metodo o variabile devono essere dichiarati di tipo Private a meno che non vi
   sia una buona ragione per non farlo e, in questo caso, la scelta deve essere ampiamente
   documentata ed approvata.
    Overriding. A meno che non vi sia una valida ragione, non effettuare mai l’overriding dei metodi di
   gestione dei thread (java.lang.Thread) (es. wait(), notify(), etc.).
    Modificatori. Analogamente, tutti i metodi delle classi devono essere definiti di tipo final a meno
   che non vi sia una buona ragione per non farlo e, in questo caso, la scelta deve essere ampiamente
   documentata ed approvata.
    Firma delle applet. Il codice di una Applet deve essere firmato solo se assolutamente necessario. In
   tal caso il certificato utilizzato deve essere valido in tutte le sue parti, emesso da una Certification
   Authority riconosciuta a livello internazionale e sempre verificabile dal browser che esegue
   l’Applet. Certificati temporanei e di test non dovrebbero mai essere utilizzati né in ambiente di
   collaudo né in ambiente di esercizio.
    Validazione delle informazioni trasferite. Tutte le informazioni, trasferite in qualsiasi modo e con
   qualsiasi protocollo, da un’Applet verso un componente server devono sempre essere validate
   anche lato server.
    Utilizzo delle Applet di terze parti. Non devono mai essere utilizzate Applet di dubbia/non
   certificata provenienza e/o delle quali non si dispone del relativo codice sorgente. In qualsiasi caso,
   possono essere utilizzate (in tutti gli ambienti - sviluppo, collaudo ed esercizio) esclusivamente
   previa analisi del codice relativo e previa ricompilazione: andata a buon fine e senza warnings.

.. _java-servlet-..:

7.2.9.14 Java Servlet ………………………………………………………………………………………………………………………………………..
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

::

    Utilizzo delle richieste di tipo HTTP POST e HTTP GET. L’invio di informazioni tramite HTML Form
   deve avvenire esclusivamente tramite richieste di tipo HTTP POST, pertanto, l’implementazione del
   metodo doGet() delle Servlet deve contenere soltanto la corrispondente e corretta gestione
   dell’errore.
    Filtraggio dell’input. Qualsiasi parte di un HTTP-Request non validata da un sistema di controllo
   server-side è “pericolosa” dal punto di vista della sicurezza. E’ necessario, pertanto, assicurarsi che i
   parametri di una HTTP Request vengano validati prima di un loro effettivo utilizzo. Queste
   informazioni (es: URL, Cookies, Form Fields, Hidden Fields, Headers, etc. ottenute ad esempio dai
   metodi getParameter(), getCookie(), o getHeader() degli oggetti HttpServletReques), prima di
   essere utilizzate, devono essere rigorosamente validate server-side e ne deve essere effettuata la
   canonicalizzazione (semplificazione della codifica).
   Ogni informazione in input (singolo parametro) deve essere analizzata in modo tale da specificare
   quale tipo di dato può essere ammesso in ingresso. I parametri da controllare in fase di validazione
   sono:
   o il tipo di dato (string, integer, real, etc.);
   o il set di caratteri consentito;
   o la lunghezza minima e massima;
   o controllare se permesso il tipo NULL;
   o controllare se il parametro richiesto o meno;
   o controllare se sono permessi i duplicati;
   o intervallo numerico;
   o specificare i valori ammessi (numerazione) ;
   o specificare i pattern (espressioni regolari) ;
   Tali informazioni, inoltre, devono essere accuratamente scansionate con l’obiettivo di ricercare
   qualsiasi carattere speciale e sostituirlo con il corrispondente carattere HTML. Questa deve essere
   sempre eseguita all’interno dei metodi doGet() e doPost() di tutte le Servlet che compongono la
   Web Application. La tabella seguente mostra un’esemplificazione dei caratteri speciali che devono
   essere ricercati e le corrispondenti sostituzioni HTML che devono essere effettuate.
   Carattere speciale da ricercare:

.. _section-43:

.. _section-43:

< > ( ) # &
^^^^^^^^^^^

Carattere HTML sostitutivo: < > &40; &41; &35; &38; Il Web Application
server più evoluti mettono a disposizione funzioni native che svolgono
questa operazione (es. weblogic.servlet.security.Utils.encodeXSS() di
BEA WLS). Se si utilizza uno di questi Web Application server è sempre
preferibile utilizzare queste funzioni built-in piuttosto che crearne di
custom. Esempio: o Se il si utilizza BEA WLS e la variabile ‘user_input’
contiene le informazioni inserite dall'utente tramite una HTML Form,
sostituire una istruzione di questo tipo: out.print(“User input:” +
user_input); o con questa istruzione: out.print((“User input:” +
weblogic.security.servlet.encodeXSS(user_input) + “!”); E' fortemente
raccomandato accettare in input informazioni composte esclusivamente da
caratteri ammissibili per il contesto dell'informazione stessa. Ad
esempio, se un utente sta trasferendo l'informazione sulla sua età
tramite un HTML Form, i caratteri che possono essere accettati sono
soltanto cifre (0-9); non c'è alcuna ragione che trasferisce qualsiasi
altro carattere diverso e tantopiù caratteri speciali.  Utilizzo dei
Web Application Firewall. Ove possibile utilizzare/integrare i Web
Application Firewall che forniscono meccanismi di validazione dell'input
e di protezione per tutti i tipi di dati ricevuti da un HTTP request,
inclusi le URL, i form, i cookie, le query string, gli hidden field e i
parametri.  Proteggere i dati personali e/o sensibili. Tutte le
transazioni che prevedono la ricezione da parte di una Servlet di dati
personali e/o sensibili (es: login, password, fede religiosa, malattie,
etc.) devono sempre avvenore in modo sicuro e almeno su protocollo HTTP
protetto via SSL (HTTPS). In quest'ottica il processo di autenticazione
e di autorizzazione di un utente deve sempre avvenire tramite protocollo
HTTPS.  Switching tra SSL e non-SSL. Per le risorse web che devono
essere protette tramite SSL non deve mai essere consentito lo switch a
non-SSL. Tali risorse devono essere accessibili esclusivamente tramite
protocollo HTTPS e mai tramite il protocollo http non protetto. Ciò può
essere ottenuto utilizzando un Servlet Filter che rifiuta ogni richiesta
non-SSL adi accesso alle risorse protette. Di seguito un esempio di
implementazione, completo del sorgente Java della classe di redirezione
e delle istruzioni per la configurazione nel file web.xml. Esempio: o
Descrivere il filtro nel file web.xml:

… SecureRedirect org.secure.secureRedirectFilter port your_port_number

::

   </init-param>
   </filter>

… o Descrivere il mapping per questo filtro nel file web.xml: …
SecureRedirect /login/\* … La classe filtro: package org.secure; import
java.io.IOException; import java.io.PrintStream; import javax.servlet.*;
import javax.servlet.http.HttpServletRequest; import
javax.servlet.http.HttpServletResponse; public class
secureRedirectFilter implements Filter { private FilterConfig config;
private static boolean no_init = true; public secureRedirectFilter() { }
public void init(FilterConfig filterconfig) throws ServletException {
config = filterconfig; no_init = false; } public void destroy() { config
= null; } public FilterConfig getFilterConfig() { return config; }
public void setFilterConfig(FilterConfig filterconfig) { if (no_init) {
no_init = false; config = filterconfig; } } public void
doFilter(ServletRequest servletrequest, ServletResponse servletresponse,
FilterChain filterchain) throws IOException, ServletException { String s
= servletrequest.getScheme(); if (!s.equalsIgnoreCase(“http”)) {
filterchain.doFilter(servletrequest, servletresponse); } else {
HttpServletResponse httpservletresponse = (HttpServletResponse)
servletresponse; HttpServletRequest httpservletrequest =
(HttpServletRequest) servletrequest; int i =
httpservletrequest.getServerPort(); String s1 = “https://” +
httpservletrequest.getServerName(); String s2 =
httpservletrequest.getQueryString(); String s3 =
config.getInitParameter(“port”); if (s3 != null) {

s1 = s1 + “:” + s3; } s1 = s1 + httpservletrequest.getRequestURI(); if
(s2 != null) { s1 = s1 + “?” + s2; }
httpservletresponse.sendRedirect(s1); return; } } }  Statements SQL. Se
una Servlet accede ad un database, i relativi statements SQL non devono
mai essere costruiti utilizzando concatenazioni di stringhe; tantopiù
concatenazioni di informazioni inserite dagli utenti, anche se
verificate e validate. A tal proposito è necessario utilizzare
l'interfaccia PreparedStatement che, tramite il driver JDBC, effettua la
canonicalizzazione dei parametri in modo automatico. Di seguito un
esempio di utilizzo dell'interfaccia PreparedStatement. Esempio:

… String selectStatement = “SELECT \* FROM User WHERE userId =?”;
PreparedStatement prepStmt = con.prepareStatement(selectStatement);
prepStmt.setString(1, userId); ResultSet rs = prepStmt.executeQuery(); …
 Token di sessione. Evitare di creare token di sessione ad-hoc
utilizzando preferibilmente quelli messi a disposizione del web
container (o web application server) in uso, gestendo le sessioni utente
tramite l'apposita interfaccia javax.servlet.http.HttpSession. In
qualsiasi caso i token di sessione dovrebbero sempre rispettare le
seguenti regole: o non devono mai essere inclusi nelle URL; o devono
essere lunghe e complicate catene di numeri randomici che non possano
essere facilmente indovinati; o dovrebbero cambiare di frequente durante
una sessione; o dovrebbero cambiare quando si passa ad utilizzare
protocolli come SSL; o non devono mai essere utilizzati token scelti da
un utente.  Utilizzo dei cookies con le Servlet. L'utilizzo dei cookies
con Servlet deve sempre rispettare le seguenti regole minime: o i
cookies non devono essere mai utilizzati per memorizzare dati personali
o informazioni sensibili (es: login, password, fede religiosa, malattie,
etc.); o prima di trasferire informazioni personali o sensibili verso un
utente è necessario richiedere sempre la sua autenticazione ed
autorizzazione tramite inserimento di login e password: non basarsi mai
sulla presenza o meno di un cookie precedentemente memorizzato; o
configurare i session cookies in modo tale che scadano quando l'utente
esce dal browser; o assicurarsi che tutte le informazioni contenute nei
cookies siano accuratamente verificate e filtrate prima di essere
utilizzate e/o inserite nei documenti HTML.  Limitare la dimensione
delle risposte http. Ove possible limitare sempre la lunghezza delle
risposte HTTP al massimo necessario troncando quelle che hanno una
dimensione eccedente.  HTTP Referer. Ove possible verificare sempre il
campo Referer dell'header HTTP (es. metodo getHeader(java.lang.String
name) dell'interfaccia javax.servlet.http.HttpServletRequest) e
rigettare le informazioni provenienti da host o link incorretti e/o
inaspettati.

::

    Trattamento dei files e degli oggetti embedded. Una Servlet non deve mai accettare in input
   contenuti sottomessi da un utente che contengano tag HTML tipici dell’iclusione di file od oggetti
   come: <EMBED>, <OBJECT> e <SCRIPT>.
    Corretta gestione degli errori e delle eccezioni. Tutte le eccezioni che si verificano durante
   l’esecuzione delle Servlet che costituiscono l’applicazione web devono essere catturate e gestite
   opportunamente. I relativi mesaggi di errore sollevati (es. dump di databse o codici di errore - out
   of memory, null pointer exceptions, system call failure, database unavailable, network timeout),
   devomo essere visualizzati verso l’utenza in accordo ad uno schema ben dettagliato: agli utenti
   generici devono essere inviate le informazioni minime in grado di aiutarli nella comprensione degli
   errori stessi (senza rivelare dettagli superflui) mentre le informazioni sulla diagnostica devono
   essere inviate per la visualizzazione esclusivamente agli amministratori dell’applicazione stessa. Il
   meccanismo di gestione errori deve essere in grado di gestire ogni tipo di dati in ingresso e nel
   frattempo di garantire la sicurezza. Devono essere previsti dei messaggi di errore semplici, in grado
   di indicare la causa e di archiviare i tentativi di intrusione in modo tale da poterli verificare in un
   secondo tempo. La gestione degli errori non deve essere concentrata soltanto sui dati forniti in
   ingresso dall’utente, ma deve includere anche tutti gli errori che possono essere generati da
   componenti interni come system call, query sul db o altre funzioni interne.
    Limitare l’utilizzo delle risorse macchina. Dove possibile implementare meccanismi che consentono
   di limitare al massimo il numero di risorse allocate per ogni singolo utente. Per gli utenti
   auntenticati, è possibile fissare una quota in modo da poter limitare il carico massimo che un
   utente può applicare al sistema. Per gli utenti non autenticati, si dovrebbero evitare tutti gli accessi
   al data base o ad altre applicazioni avide di risorse ritenute superflue mantenendo ad esempio in
   una cache il contenuto dei dati ricevuti da questi utenti invece di eseguire delle query direttamente
   sul DB.
