.. _javascript:

7.4 JAVASCRIPT
==============

JavaScript è un linguaggio di scripting orientato agli oggetti e agli
eventi. Generalmente viene utilizzato nella programmazione Web, lato
client, per creare effetti dinamici interattivi attraverso l'uso
funzioni di script invocate da eventi innescati a loro volta in vari
modi dall'utente sulla pagina web in uso (mouse, tastiera, caricamento
della pagina ecc.).

Di seguito vengono analizzate le principali vulnerabilità e le
contromisure da adottare.

.. _dom-based-xss:

7.4.1 DOM-based XSS
-------------------

.. _client-dom-code-injection-.:

7.4.1.1 Client DOM Code Injection …………………………………………………………………………………………………………………….
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Consiste nell'infettare codice Javascript o HTML superando le normali
protezioni del sistema contro attacchi di tipo Cross-Site Scripting
(XSS). L'XSS, acrononimo di Cross Site scripting, viene realizzato
tramite l'inclusione di codice (HTML o Javascript per la Client DOM Code
Injection) all'interno di una pagina web per effettuare operazioni
malevoli quali il prelievo di cookies privati. La vulnerabilità “Client
DOM Code Injection” puo' utilizzare anche strumenti di tipo “Social
engineering” per carpire informazioni dagli utenti web tramite tecniche
di bassa tecnologia sviluppate da malintenzionati per ottenere
informazioni personali. Ad esempio possono essere simulate pagine quasi
identiche ad altri siti di largo utilizzo per ottenere informazioni
riservate.

**Come difendersi**

::

    Evitare di eseguire codice dinamicamente, in particolare se costruito con input proveniente
   dall’esterno.
    Occorre verificare sempre l’input, imponendo controlli rigidi che impediscano di immettere
   caratteri e tipi di dati potenzialmente dannosi. L’approccio ottimo è stilare una white list di valori
   ammessi e scartare tutto ciò che non vi rientra. E’ necessario quindi codificare completamente tutti
   i dati dinamici prima di incorporarli nella pagina web.
    La codifica deve essere allineata al contesto, ad esempio:
   o Codifica HTML per contenuti HTML e per i relativi attributi;
   o Codifica JavaScript per sorgenti di tipo JavaScript.
    Si consiglia di utilizzare librerie conosciute, come ad esempio le librerie di tipo ESAPI.
   Esempio. Evitare di chiamare dinamicamente una funzione senza averne prima sanitizzato l'input.
   Forma non corretta:
   var input = document.getElementById("id").value;
   window.setInterval( myFunc(input), 1000);
   Forma corretta:
   var input = document.getElementById("id").value;
   var trusted = escape(input);
   window.setInterval( myFunc(trusted), 1000);
   Forma corretta per l’aggiornamento dinamico dell'HTML nel DOM:
   document.write("<%=Encoder.encodeForJS(Encoder.encodeForHTML(untrustedD
   ata))%>");
    Per le chiamate dinamiche, vanno utilizzati solo metodi predefiniti o codice Javascript non
   influenzabile da variabili dinamiche o non dipendente da routine tipo “eval()” non particolarmente
   sicure.
   o Forma corretta per codice javascript sicuro:
   window.setInterval( "timedFunction();", 1000);

Per ulteriori informazioni si veda:
http://cwe.mitre.org/data/definitions/94.html, Improper Control of
Generation of Code (‘Code Injection’) CWE-94

.. _client-dom-stored-code-injection:

7.4.1.2 Client DOM stored Code Injection
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Una vulnerabilità XSS persistente (o stored) come la “Client DOM Stored
Code Injection” è una variante più devastante di cross-site scripting
con manipolazione di codice: si verifica quando i dati forniti
dall'attaccante vengono salvati sul server, e quindi visualizzati in
modo permanente sulle pagine normalmente fornite agli utenti durante la
normale navigazione.

**Come difendersi**

::

    Evitare qualsiasi compilazione dinamica, esecuzione o valutazione del codice. Nel caso sia
   necessaria l'esecuzione dinamica, invece di utilizzare i dati lato client (inclusi i dati
   precedentemente memorizzati dall'applicazione stessa), utilizzare solo dati rigidamente controllati
   tramite liste prefissate o dati attendibili dal server.
   Esempio. Evitare di chiamare dinamicamente una funzione senza averne prima sanitizzato l'input.
   Per delle chiamate dinamiche vanno utilizzati solo metodi predefiniti o codice Javascript non
   influenzabile da variabili dinamiche o non dipendente da routine tipo “eval()” non particolarmente
   sicure.

.. _forma-corretta-di-codice-javascript-sicuro:

Forma corretta di codice javascript sicuro:
-------------------------------------------

::

   window.setInterval( "timedFunction();", 1000);

Per ulteriori informazioni si veda:
http://cwe.mitre.org/data/definitions/94.html, Improper Control of
Generation of Code (‘Code Injection’) CWE-94

.. _dom-stored-xss-..:

7.4.1.3 DOM Stored XSS …………………………………………………………………………………………………………………………………..
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Attraverso questa vulnerabilità, un utente malintenzionato potrebbe
intercettare lo scambio di informazioni sensibili tra un'applicazione e
i database responsabili della storicizzazione delle stesse e inviare
dati dannosi. Una vulnerabilità XSS persistente (o stored) come la
“Client DOM Stored XSS” è una variante più devastante di cross-site
scripting con manipolazione di codice: si verifica quando i dati forniti
dall'attaccante vengono salvati sul server, e quindi visualizzati in
modo permanente sulle pagine normalmente fornite agli utenti durante la
normale navigazione.

**Come difendersi**

::

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

 La validazione comunque non sostituisce la codifica. Devono essere
completamente codificati tutti i dati dinamici, indipendentemente dalla
sorgente, prima di incorporare idati stessi in un output. La codifica
dovrebbe essere allineata al contesto, ad esempio: o Codifica HTML per
un contesto di tipo HTML; o Codifica degli attributi HTML per output
degli attributi relativi; o Codifica Javascript per server-generated di
tipo Javascript; Esempio di HTML richiamato nel codice Javascript. La
stringa in uscita è codificata nella pagina Html prima che venga
visualizzata nella relativa etichetta: public class StoredXssFixed {
**public string foo** (Label lblOutput, SqliteConnection connection,
HttpServerUtility Server, **string** id) { SqliteConnection connection =
**new** SqliteConnection(connectionString) **string** sql = “select
email from CustomerLogin where customerNumber =” + id; SqliteCommand cmd
= **new** SqliteCommand(sql, connection); **string** output = (
**string** )cmd.ExecuteScalar(); lblOutput.Text =
String.IsNullOrEmpty(output)? “Customer Number does not exist” :
Server.HtmlEncode(output); } }

::

   Esempio Javascript per Client Dom Stored XSS
   Forma non corretta (routine completa):
   <!DOCTYPE html>
   <html>
   <head>
   <meta charset="utf-8">
   <title>XSS Example</title>
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
   </head>
   <body>
   <form method="post">
   <p>
   <select id="users" name="users">
   <option
   value="bad">&lt;script&gt;alert(&#x27;xss&#x27;);&lt;/script&gt;</option>
   </select>
   </p>
   </form>
   </body>
   </html>
   Codice sanitizzato (fix relativa alle stringa modificata)
   // after() accepts a DOM element so lets create a text node
   select.after(document.createTextNode(option.text()));

Per ulteriori informazioni si veda:
http://cwe.mitre.org/data/definitions/97.html CWE-97: Improper
Neutralization of Server-Side Includes (SSI) Within a Web Page

.. _client-dom-xss-.:

7.4.1.4 Client DOM XSS …………………………………………………………………………………………………………………………………….
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Un utente malintenzionato potrebbe utilizzare metodologie di “social
engineering” (es. falsificazione di siti web di largo accesso con
richiesta di credenziali o dati sensibili) per carpire informazioni
importanti tramite codice manipolato all'interno di pagine web degli
applicativi falsificati. Possono essere prelevate password, dati di
carte di credito etc.

**Come difendersi**

::

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
   Esempio
   Per creare HTML dinamico in JavaScript, utilizzare la libreria OWASP ESAPI4JS:
   window.location = ESAPI4JS.encodeForURL(input);
   Per creare dinamicamente URL in JavaScript, utilizzare la libreria OWASP ESAPI4JS:
   window.location = ESAPI4JS.encodeForURL(input);

Per ulteriori informazioni si veda:
http://cwe.mitre.org/data/definitions/97.html, CWE-97: Improper
Neutralization of Server-Side Includes (SSI) Within a Web Page

.. _client-resource-injection:

7.4.2 Client Resource Injection
-------------------------------

**Come riconoscerla**

Un utente malintenzionato potrebbe aprire un backdoor che gli consente
di connettersi direttamente al server delle applicazioni prendendone il
controllo o comunque effettuare attacchi diretti al server con effetti
pericolosi.

**Come difendersi**

Non consentire a un utente di venire in possesso delle informazioni
relative alle definizioni dei parametri di gestione relativi ai “network
sockets”. Esempio *:* Javascript per Client Resource Injection

.. _client-second-order-sql-injection:

7.4.3 Client Second Order Sql Injection
---------------------------------------

**Come riconoscerla**

Un utente malintenzionato potrebbe accedere direttamente a tutti i dati
del sistema. L'attaccante potrebbe rubare qualsiasi informazione
riservata, memorizzata dal sistema (ad esempio i dati personali
dell'utente o le carte di credito), ed eventualmente modificare o
cancellare i dati esistenti.

**Come difendersi**

::

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
    Invece di concatenare le stringhe:
   o Utilizzare componenti di database sicuri come le procedure memorizzate, query parametrizzate
   e le associazioni degli oggetti (per comandi e parametri).
   o Una soluzione ancora migliore è quella di utilizzare una libreria ORM, come EntityFramework,
   Hibernate o iBatis.
    Limitare l'accesso agli oggetti e alle funzionalità di database, in base al principio del minimo
   privilegio.
   Esempio. Javascript per Client Second Order Sql Injection
   Forma non corretta:
   var userId = 5;
   var query = connection.query('SELECT * FROM users WHERE id = ?', [userId],
   function(err, results) {
   //query.sql returns SELECT * FROM users WHERE id = '5'
   });
   Forma corretta
   var post = {id: 1, title: 'Hello MySQL'};
   var query = connection.query('INSERT INTO posts SET ?', post, function(err,
   result) {
   //query.sql returns INSERT INTO posts SET `id` = 1, `title` = 'Hello MySQL'
   });

.. _client-sql-injection:

7.4.4 Client Sql Injection
--------------------------

**Come riconoscerla**

L' utente malintenzionato potrebbe utilizzare i canali di comunicazione
tra l'applicazione e il suo database inviando una query SQL testuale.
L'applicazione viene attaccata con il risultato di avere una query
modificata di interrogazione al db semplicemente concatenando le
stringhe tra cui l'input dell'utente. Poiché l'input utente non è stato
verificato per la validità del tipo di dati né successivamente
sanificato, l'input potrebbe contenere comandi SQL che verrebbero
interpretati come tali dal database.

**Come difendersi**

::

    Validare tutti i dati di input, indipendentemente dalla sorgente. La convalida dovrebbe essere
   basata su una whitelist (lista prefissata): dovranno essere accettati solo i dati che rispettano una
   una struttura specificata, bloccando i dati che presentano schemi che non rientrano in queste
   casistiche.
    E’ necessario quindi codificare completamente tutti i dati dinamici prima di incorporarli nella
   pagina web. La codifica deve essere sensibile al contesto. Per esempio:
   o Data type;
   o Size;
   o Range;
   o Format;
   o Expected values;
    Invece di concatenare le stringhe adottare le seguenti metodologie:
   o Utilizzare componenti di database sicuri come le procedure memorizzate, query parametrizzate
   e le associazioni degli oggetti (per comandi e parametri).
   o Una soluzione ancora migliore è quella di utilizzare una libreria ORM, come EntityFramework,
   Hibernate oppure iBatis.
    Limitare l'accesso agli oggetti e alle funzionalità del database, in base alle regole definite dal
   "Principle of Least Privilege". Il principio in sintesi stabilisce che agli utenti venga attribuito il più
   basso livello di “diritti” che possano detenere rimanendo comunque in grado di compiere il proprio
   lavoro.
   Esempio. Javascript per Client SQL Injection
   Forma non corretta
   var info = {
   userid: message.author.id
   }
   connection.query("SELECT * FROM table WHERE userid = '" + message.author.id
   + "'", info, function(error) {
   if (error) throw error;
   });
   Forma corretta
   var sql = "SELECT * FROM table WHERE userid = ?" ;
   var inserts = [message.author.id];
   sql = mysql.format(sql, inserts);

Per ulteriori informazioni si veda:
http://cwe.mitre.org/data/definitions/89.html, CWE-89: Improper
Neutralization of Special Elements used in an SQL Command (‘SQL
Injection’)
