.. _best-practices-per-lo-sviluppo-in-sicurezza:

7 BEST PRACTICES PER LO SVILUPPO IN SICUREZZA
=============================================

Molte delle sviste di programmazione sono da attribuire alla scarsa
conoscenza, da parte degli sviluppatori, delle principali vulnerabilità
che minano il software. Il presente capitolo fornisce una vista delle
principali vulnerabilità e delle relative contromisure, contestualizzate
per ogni specifica area di sviluppo (C/C++, Java, PL/SQL, etc), anche in
termini di tecniche da utilizzare per riconoscerle e difendersi
opportunamente.

.. _cc-1:

.. _cc-1:

7.1 C/C++
---------

Il C++ (o CPP acronimo di “C plus plus”) è un linguaggio di
programmazione orientato agli oggetti, con tipizzazione statica. È stato
sviluppato (in origine col nome di “C con classi”) da Bjarne Stroustrup
ai Bell Labs nel 1983 come un miglioramento del linguaggio C. Poiché i
linguaggi C e C++ hanno caratteristiche molto simili, ai fini della
sicurezza del codice, le vulnerabilità e le contromisure di cui di
seguito, sono da considerarsi valide per entrambi i linguaggi.

.. _cross-site-scripting-xss-1:

.. _cross-site-scripting-xss-1:

7.1.1 Cross-site scripting (XSS)………………………………………………………………………………………………………………
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**Come riconoscerla**

Il Cross-site scripting (XSS) è una vulnerabilità che affligge siti web
dinamici che impiegano un insufficiente controllo dell'input nei form.
Un XSS permette ad un Cracker di inserire o eseguire codice lato client
al fine di attuare un insieme variegato di attacchi quali ad esempio:
raccolta, manipolazione e reindirizzamento di informazioni riservate,
visualizzazione e modifica di dati presenti sui server, alterazione del
comportamento dinamico delle pagine web ecc. Rientrano nelle
problematiche di tipo XSS:  CGI Reflected XSS. Gli attacchi di tipo CGI
Reflected XSS sono attacchi informatici a siti web. L'attacco consiste
nell'infettare script inerenti a web server (messaggio di errore,
risultato di ricerca, o qualsiasi altra risposta che include alcuni o
tutti gli input inviato al server come parte della richiesta). Reflected
XSS è anche talvolta indicato come non-persistente o di tipo II XSS. 
CGI Stored XSS. I comandi di tipo CGI Stored XSS sono quelli in cui lo
script iniettato viene memorizzato in modo permanente sui server di
destinazione, come ad esempio in un database, in un forum di messaggi,
registro dei visitatori, in un campo commentato, etc. La vittima poi
recupera lo script dannoso dal server quando richiede le informazioni
memorizzate. Stored XSS è anche talvolta indicato come persistente o di
tipo I XSS.

**Come difendersi**

::

    Convalidare tutti gli input, indipendentemente dalla fonte: la convalidazione dovrebbe essere
   basata su una whitelist (tramite es. una matrice di controllo): accettare solo i dati che
   corrispondono una struttura specifica, piuttosto che rifiutare modelli pericolosi. Controllare in
   particolare:
   o Data type,
   o Size,
   o Range,
   o Format,
   o Expected values.
    Codificare completamente tutti i dati dinamici al fine di ottenere una integrazione dei dati in uscita.
   La codifica dovrebbe essere context-sensitive. Ad esempio:
   o HTML encoding per HTML content,
   o HTML Attribute encoding per data output tramite valori definiti,
   o JavaScript encoding per server-generated JavaScript.
    Si consiglia di utilizzare sia la libreria di codifica ESAPI, o le funzionalità della piattaforma built-in.
   Per alcune versioni è possibile utilizzare la libreria AntiXSS.
    Nell'intestazione di risposta HTTP Content-Type, definire in modo esplicito la codifica dei caratteri
   (charset) per l'intera pagina.
    Impostare il flag HttpOnly sui cookie di sessione, per evitare tentativi di furto tramite cookie nelle
   problematiche di tipo XSS.

Esempio: L'applicazione utilizza la stringa campo “Referer” per
costruire la HttpResponse: public class ReflectedXssAllClients { public
static void foo(HttpRequest Request, HttpResponse Response) { string
Referer = Request.QueryString[“Referer”]; Response.BinaryWrite(Referer);
} }

Per ulteriori informazioni si veda:
http://cwe.mitre.org/data/definitions/79.html, CWE-79: Improper
Neutralization of Input During Web Page Generation (‘Cross-site
Scripting’).

.. _command-injection:

7.1.2 Command Injection
~~~~~~~~~~~~~~~~~~~~~~~

**Come riconscerla**

Tramite questa vulnerabilità un aggressore potrebbe eseguire comandi di
sistema arbitrari sull'host del server dell'applicazione. In base alle
autorizzazioni dell'applicazione che potrebbero essere carpite, queste
potrebbero includere:  alterazione dei privilegi sulla manipolazione di
File (read / create / modify / delete);  permettere delle connessioni
di rete non autorizzate verso il server da parte dell'attaccante; 
permettere ad utenti malintenzionati la gestione dei servizi con
possibili Start and stop dei servizi di sistema;  acquisizione completa
del server da parte dell'attaccante. Attraverso questa vulnerabilità
l'applicazione viene portata ad eseguire dei comandi voluti dall'utente
malintenzionato piuttosto che eseguire il proprio codice applicativo.
L'operazione spesso viene effettuata concatenando stringhe di input
dell'utente a codice dannoso. Potrebbero così essere eseguiti
direttamente sul server comandi anche molto pericolosi per il sistema o
per la sicurezza dei dati.

**Come difendersi**

Di seguito un elenco delle azioni da intraprendere:  Rimodulare il
codice per evitare una qualsiasi esecuzione diretta di script di
comandi. Eventualmente utilizzare API fornite dalle aziende produttrici
di software relativo;  Se è non e' possibile rimuovere l'esecuzione del
comando, eseguire solo stringhe statiche che non includono l'input
dell'utente;  Validare tutti gli input, indipendentemente dalla
sorgente. La convalida dovrebbe essere basata su una whitelist:
dovrebbero essere accettati solo i dati che adattano a una struttura
specificata, e scartati i dati che non rientrono in questa categoria. I
parametri devono essere limitati a un set di caratteri consentito e
l'ingresso non valido deve essere eliminato. Oltre ai caratteri,
verificare: o Data type; o Size; o Range; o Format; o Expected values;

::

    Configurare l'applicazione da eseguire utilizzando un account utente limitato che non disponga di
   privilegi non necessari all'applicativo stesso;
    Se possibile, isolare tutta l'esecuzione dinamica per utilizzare un account utente separato e
   dedicato che abbia privilegi solo per le operazioni e i file specifici utilizzati dall'applicazione, in base
   al principio denominato "Principle of Least Privilege". Il principio stabilisce che agli utenti venga
   attribuito il più basso livello di “diritti” che possano detenere rimanendo comunque in grado di
   compiere il proprio lavoro.

Per ulteriori informazioni si veda:
http://cwe.mitre.org/data/definitions/77.html, CWE-77: Improper
Neutralization of Special Elements used in a Command (‘Command
Injection’).

.. _connection-string-injection:

7.1.3 Connection String Injection
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

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
attack). Per comunicare con il proprio database o con un altro server
(ad esempio Active Directory), l'applicazione costruisce dinamicamente
una sua stringa di connessione. Questa stringa di connessione include
valori concatenati inseriti dall'utente per l'autenticazione stessa. Se
i valori immessi dall'utente non sono stati verificati né tantomeno
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

.. _resource-injection:

7.1.4 Resource Injection
~~~~~~~~~~~~~~~~~~~~~~~~

**Come riconoscerla**

Un utente malintenzionato potrebbe aprire una backdoor che potrebbe
permettere all'attaccante di connettersi direttamente al server con
possibili conseguenze molto gravi per la sicurezza.Tramite questa

vulnerabilità un possibile malintenzionato potrebbe utilizzare eventuali
connessioni aperte dall'utente, nel caso non fossero gestite
adeguatamente.

**Come difendersi**

::

    Non consentire a un utente di definire i parametri relativi ai sockets di rete.

Per ulteriori informazioni si veda:
http://cwe.mitre.org/data/definitions/99.html, CWE-99: Improper Control
of Resource Identifiers (‘Resource Injection’).

.. _second-order-sql-injection:

7.1.5 (Second Order) SQL Injection
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**Come riconoscerla**

Un utente malintenzionato potrebbe accedere direttamente a tutti i dati
del sistema. L'attaccante potrebbe rubare qualsiasi informazione
riservata memorizzata dal sistema (ad esempio i dati personali
dell'utente o le carte di credito) e eventualmente modificare o
cancellare i dati esistenti. L'applicazione comunica con il suo database
inviando una query SQL in formato testo. L'applicazione crea la query
semplicemente concatenando le stringhe, tra cui i dati ottenuti dal
database. Poiché questi dati possono essere stati precedentemente
ottenuti dall'input dell'utente e non sono stati verificati né tantomeno
sanificati, i dati potrebbero contenere comandi SQL che verrebbero
interpretati come tali dal database.

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
    Non concatenare le stringhe ma:
   o Utilizzare componenti di database sicuri come le procedure memorizzate, query parametrizzate
   e le associazioni degli oggetti (per comandi e parametri);
   o Una soluzione ancora migliore è quella di utilizzare una libreria ORM, come EntityFramework,
   Hibernate o iBatis;
    Limitare l'accesso agli oggetti e alle funzionalità di database, in base al "Principle of Least Privilege"
   (non fornire diretti agli utenti maggiori di quelli strettamente necessari).

Per ulteriori informazioni si veda:
http://cwe.mitre.org/data/definitions/89.html, CWE-89: Improper
Neutralization of Special Elements used in an SQL Command (‘SQL
Injection’).

.. _ldap-injection:

7.1.6 LDAP Injection
~~~~~~~~~~~~~~~~~~~~

**Come riconoscerla**

L'attacco di tipo LDAP injection è una tecnica di code injection, usata
per attaccare applicazioni di gestione dati relative a server di posta,
archivi di utenti che possono accedere etc., con la quale vengono
inseriti delle stringhe di codice malevolo all'interno di campi di input
in modo che vengano eseguiti (es. per fare inviare il contenuto del
database del server di posta all'attaccante). LDAP Injection è un
attacco utilizzato per sfruttare le applicazioni web based che
costruiscono le dichiarazioni LDAP in base all'input dell'utente. Quando
un'applicazione non riesce a disinfettare correttamente l'input
dell'utente è possibile modificare le dichiarazioni LDAP tramite
tecniche simili a SQL

Injection. Attacchi di iniezione LDAP potrebbe comportare la concessione
di autorizzazioni per query non autorizzate e la modifica dei contenuti
all'interno della struttura LDAP. Gli attacchi di tipo LDAP Injection
sono possibili soprattutto a causa dei due seguenti fattori:  La
mancanza di parametri nelle interfacce LDAP interfacce che rendono le
query più insicure.  L'uso diffuso di LDAP per autenticare gli utenti
ai sistemi.

**Come difendersi**

::

    Tenere i dati di input separati da comandi e query:
   o L’opzione preferita è quella di usare API sicure che eviti l’uso di un interprete o che fornisca
   un’interfaccia parametrizzata;
   o Se non sono disponibili API parametrizzate, è necessario evitare caratteri speciali usando
   soluzioni sintattiche (escape) specifiche per quell’interprete. OWASP’s ESAPI ad esempio ha
   alcune di queste escaping routines;
   o La validazione di input in “white list”, non basta, poichè alcune applicazioni richiedono caratteri
   speciali nei loro input, e in ogni caso un attaccante potrebbe usare un’altra codifica per
   rappresentare un determinato carattere.
    Difese primarie:
   o Eliminazione di tutte le variabili utilizzando le funzionalita’ di “right LDAP encoding function”;
    Difese aggiuntive:
   o Utilizzazione di un framework (come LINQtoAD) che implementa automaticamente la funzione
   di eliminazione delle variabili presenti.

Per ulteriori informazioni si veda:
http://cwe.mitre.org/data/definitions/90.html, CWE-90: Improper
Neutralization of Special Elements used in an LDAP Query (‘LDAP
Injection’).

.. _process-control:

7.1.7 Process Control
---------------------

**Come riconoscerla**

La vulnerabilità di tipo “Process Control” consiste nella possibilità
per un utente malintenzionato di poter eseguire comandi o caricare
librerie da una fonte non attendibile o in un ambiente non attendibile
causando l'instabilità o il controllo del sistema stesso. La
vulnerabilità di tipo “Process Control” può assumere due diverse forme
di attacco:  nella prima l'utente malintenzionato può modificare
direttamente il comando eseguito dal programma: l'aggressore controlla
esplicitamente il comando.  nella seconda l'utente malintenzionato può
modificare l'ambiente in cui il comando viene eseguito: l'aggressore
controlla implicitamente ciò che significa il comando.

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
    Evitare di costruire dinamicamente stringhe di connessione. Se è necessario creare dinamicamente
   una stringa di connessione, cercare di non includere l'input dell'utente. In ogni caso, utilizzare
   utilità basate sulla piattaforma, come SqlConnectionStringBuilder di .NET, o almeno codificare
   l'input validato come il piu' idoneo per la piattaforma utilizzata.

Per ulteriori informazioni si veda:
http://cwe.mitre.org/data/definitions/114.html, CWE-114: Process
Control.

.. _ulteriori-indicazioni-per-lo-sviluppo-sicuro:

7.1.8 Ulteriori indicazioni per lo sviluppo sicuro
--------------------------------------------------

La raccolta di Best Practices che segue, è conforme ai dettami degli
standard CERT C / C++ Programming Language Secure Coding.

.. _dichiarazioni-..:

7.1.8.1 Dichiarazioni ………………………………………………………………………………………………………………………………………..
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

::

    E’ consigliato dimensionare gli array non utilizzando costanti numeriche ma piuttosto costanti
   simboliche definite.
   Esempio - Forma non corretta:
   int mesi[13];
   Esempio - Forma corretta:
   int mesi[TOT_MESI + 1];
    Dichiarare le costanti utilizzando la keyword "const”.
   Esempio - Forma non corretta:
   int mesi = 12;
   Esempio - Forma corretta:
   const unsigned int mesi = 12;
    Dichiarare le variabili che possono avere valori positivi utilizzando la keyword "unsigned";
    Il tipo "char" deve essere unsigned;
    Non utilizzare float e double quando non è necessario (calcoli scientifici);
    Le classi che hanno funzioni virtuali devono sempre avere distruttori virtuali.

.. _inizializzazioni:

7.1.8.2 Inizializzazioni ………………………………………………………………………………………………………………………………………
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

::

    Tutte le variabili locali devono essere inizializzate prima di essere utilizzate;
    Tutte le variabili locali che sono inizializzate con valori "dummy" o momentanei devono essere
   reinizializzate con i valori reali al momento dell'uso;
    Tutte le variabili legate ai cicli devono essere reinizializzate con l'entrata in una nuova iterazione;
    Tutte le variabili legate ai cicli devono essere reinizializzate prima di essere riutilizzate in un nuovo
   ciclo;
    Tutte le strutture devono essere azzerate prima del loro utilizzo;
    Tutti i buffer devono essere azzerati prima del loro utilizzo o riutilizzo.

.. _utilizzo-dei-tipi-di-dati:

7.1.8.3 Utilizzo dei tipi di dati ……………………………………………………………………………………………………………………………
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

::

    Stringhe.
   o Tutte le stringhe devono essere terminate dal carattere NULL. Evitare errori logici di
   programmazione che agevolino l’insorgere di una condizione contraria. Attenzione deve essere
   riposta nell’utilizzo di funzioni che non aggiungono al termine di una stringa copiata in un buffer
   di destinazione il carattere NULL se questo non risiede nel buffer sorgente.
   Esempio - Forma non corretta:
   strncpy(dest, source, sizeof(dest));
   Esempio - Forma corretta:
   strncpy(dest, source, sizeof(dest);
   dest[sizeof(dest) – 1] = ‘\0’;
   o Il codice non deve tentare di operare un’operazione su una stringa (o un char array) che non è
   terminato dal carattere NULL;
   o L’input proveniente dall’utente deve sempre essere convalidato e scremato da caratteri invalidi
   ( ;|! & ~ ' " - * % ` \ / < >? $ @ : ( ) [ ] { }. ) prima di essere
   passato alle successive elaborazioni dell’applicazione (ad esempio alla funzione system() );
   o Utilizzare le funzioni strspn(), strcspn() e strpbrk() per filtrare l’input utente;
   o Il formato delle stringhe deve sempre essere specificato nei parametri delle funzioni che lo
   richiedono. In questo contesto le funzioni considerate critiche e soggette a problematiche di
   format string overflow, se non correttamente utilizzate, sono: printf(), fprintf(), sprintf(),
   snprintf(), vprintf(), vfprintf(), vsprintf(), vsnprintf(), scanf(), fscanf(), sscanf(), vscanf(),
   vsscanf(), vfscanf(), wprintf(), fwprintf(), swprintf(), vwprintf(), vfwprintf(), vswprintf().
   Esempio - Forma non corretta:
   printf(buffer1);
   snprintf(dest, sizeof(dest), buf);
   fprintf(FILE, num, stringa);
   Esempio - Forma corretta:
   printf(“%s\r\n”, buffer1);
   snprintf(dest, sizeof(dest), “%s”, buf);
   fprintf(FILE, “%d: %s%\n”, num, stringa);

 **Buffers**. Tutti i buffer devono essere abbastanza grandi per
contenere i dati a loro destinati, inoltre: o Evitare l'utilizzo di
funzioni che non consentono di specificare la dimensione delle stringhe
copiate da un buffer sorgente ad uno di destinazione. Le funzioni
considerate critiche in questo contesto e che non devono mai essere
utilizzate sono: strcpy(), wcscpy(), sprintf(), strcat(), gets(),
scanf(), vsprintf() e wcscat(); o Quando i dati vengono copiati
all'interno di un buffer deve essere sempre verificata la loro
dimensione con quella del buffer di destinazione. Le funzioni
considerate critiche per errori di bound-checking, pur la possibilità di
specificare la lunghezza delle stringhe soggette a copia da un buffer
all'altro, sono: strncpy(), wcsncpy(), snprintf(), strncat(),
vsnprintf(), wcsncat(), memcpy(), memmove(), memset(), strxfrm(),
wcsxfrm(), wmemset(), wmemcpy(), wmemmove(), wcstombs(), wcsrtombs(),
mbstowcs(), mbsrtowcs(), swprintf() e vswprintf().

::

   Di seguito alcuni esempi di funzioni solitamente considerate sicure. ma utilizzate in modo
   errato.
   Esempio - Forma non corretta:
   char dest[512];
   char *source;
   // puntatore char source manipolabile
   // dall’utente
   strncpy(dest, source, strlen(source));
   #define LEN 5000
   // LEN superiore alla capacità
   // di contenimento massima di
   // dest
   char dest[1024];
   // variabile source manipolabile
   // dall’utente
   char source[LEN];
   memcpy(dest, source, LEN);
   Esempio - Forma corretta:
   char dest[512];
   strncpy(dest, source, sizeof(dest);
   /* inserimento di NULL alla fine di
   dest

.. _section-41:

.. _section-41:

\*/
^^^

::

   #define LEN 1024;
   char dest[1024];
   // variabile source manipolabile
   // dall’utente
   char source[LEN];
   memcpy(dest, source, LEN - 1);
   /* inserimento di NULL alla fine di
   dest
   */

.. _bitfields-.:

7.1.8.4 Bitfields ……………………………………………………………………………………………………………………………………………….
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Se nel codice vengono svolte operazioni di shifting o si utilizzano
bitfield, bisogna indicare le piattaforme con cui il codice è
compatibile per mitigare problemi/errori di porting.

.. _macro:

7.1.8.5 Macro …………………………………………………………………………………………………………………………………………………
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Se le macro sono espanse, i parametri passati non devono causare effetti
collaterali.

Esempio - Forma non corretta: #define max(a, b) (a) > (b)? (a) : (b)
risultato = max(i, j) + 3; / tutto questo viene espanso in \* risultato
= (i) > (j)? (i) : (j)+3; /

Esempio - Forma corretta: #define max(a,b) ( (a) > (b)? (a) : (b) )

Pertanto gli argomenti delle macro devono essere accuratamente racchiusi
in parentesi.

.. _loperatore-sizeof-ed-il-passaggio-di-dati-come-parametri-.:

7.1.8.6 L'operatore sizeof ed il passaggio di dati come parametri ………………………………………………………………………….
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Il passaggio della dimensione di una struttura dati come parametro ad
una funzione deve essere effettuato in maniera corretta, tramite
l'utilizzo della funzione sizeof(). A tal proposito, è obbligatorio
prendere visione degli errori qui menzionati, e non ripeterli:

Esempio - Forma non corretta: strlen(struttura) sizeof(ptr)
sizeof(\ *array) /* \* Dimensione di un solo elemento \*/ sizeof(array)

Esempio - Forma corretta: sizeof(struttura) sizeof(\ *ptr) sizeof(array)
/*

-  Dimensione di un solo elemento \*/ sizeof(array[0])

Pertanto gli argomenti delle macro devono essere accuratamente racchiusi
in parentesi.

.. _allocazione-dinamica-.:

7.1.8.7 Allocazione dinamica …………………………………………………………………………………………………………………………….
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

::

    Lo spazio di memoria allocato dinamicamente (ad esempio con le funzioni malloc(), calloc()
   e realloc() ) deve essere appropriato alla dimensione dei dati che deve contenere;
    L’applicazione deve provvedere all’allocazione ed alla deallocazione della sua memoria.
   Nell’ambito della programmazione multithreaded, vale lo stesso principio: ogni thread deve
   allocare e deallocare la propria memoria senza delegare la deallocazione ad altri thread;
    Non preferire in un sorgente C++ l’utilizzo di funzioni standard del C. Esempio: utilizzare "new"
   invece che malloc(), calloc(), e realloc();

.. _deallocazione:

7.1.8.8 Deallocazione ………………………………………………………………………………………………………………………………………
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

::

    Gli array non devono essere cancellati come dati scalari.
   Esempio - Forma non corretta:
   delete mioarray;
   Esempio - Forma corretta:
   delete [ ] mioarray;
    Non devono esistere puntatori a risorse distrutte: contestualmente alla distruzione delle risorse
   vanno dereferenziati tutti i puntatori;
    I puntatori relativi alla memoria allocata dinamicamente devono essere impostati a NULL subito
   dopo essere stati rilasciati;
    I puntatori ottenuti via malloc(), calloc(), realloc() devono essere distrutti con free()
   (mai usare delete);
    I puntatori ottenuti via new devono essere distrutti con delete (mai usare free());
    Mai liberare un’area di memoria (ad esempio con free() ) già deallocata. Evitare errori logici nel
   codice che consentano l’insorgere di problematiche di questo tipo;
    Mai tentare di scrivere in un buffer residente in heap memory dopo la sua deallocazione. Evitare
   l’insorgere di errori logici di questo tipo.

.. _puntatori:

7.1.8.9 Puntatori
~~~~~~~~~~~~~~~~~

::

    Gestire opportunamente i puntatori a NULL;
   Esempio- Forma non corretta:
   char tmpchar1 (char *s)
   {
   return *s;
   }
   //”s” == NULL  CRASH
   Esempio- Forma corretta:
   char tmpchar1 (char *s)
   {
   if (s == NULL) return ‘\0’;
   return *s;
   }

.. _casting-e-problematiche-di-gestione-delle-variabili-numeriche-.:

7.1.8.10 Casting e problematiche di gestione delle variabili numeriche ………………………………………………………………….
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

::

    Il tipo NULL deve essere corretto mediante casting quando passato come parametro ad una
   funzione;
    Ridurre al minimo le comparazioni fra interi di tipo signed. Se due interi di tipo signed vengono
   comparati deve essere previsto il caso “minore di zero” ( < 0 ) soprattutto quando la
   comparazione avviene con un valore costante.
   Esempio - Comparazione non signed:
   if ((int)val1 < (unsigned int)val2)
   /* in questo caso unsigned ha la precedenza essendo un tipo più grande di
   signed. Entrambi i valori
   (val1 e val2) vengono quindi
   convertiti ad unsigned prima di essere comparati
   */
   if ((int)val < sizeof(costante))
   // l’operatore sizeof è unsigned
   Esempio - Comparazione signed:
   if ((int)val < 256)
   if (unsigned short)val1 < (short)val2)
   /* la seguente comparazione dovrebbe, in base al tipo di compilatore, essere
   signed perchè entrambi gli short dovrebbero essere convertiti a signed
   integer prima di essere comparati
   */
    Evitare di utilizzare variabili signed integer come length specifier, ovvero come indicatori
   dell’allocazione/dimensione di un buffer o di un array.
    Evitare che un intero, a seguito di un’operazione di moltiplicazione, addizione o sottrazione, cresca
   oltre il suo valore massimo o decresca sotto il suo valore minimo. Ad esempio su architettura a 32
   bit se un intero signed a 16 bit dal valore 32767 viene incrementato di una unità, il suo valore
   diverrà -32768. E’ bene assicurarsi che questo genere di condizioni non si verifichi in alcun caso,
   soprattutto su input fornito dall’utente, in prossimità dell’allocazione di un buffer o della copia di
   dati da un buffer all’altro.
    La conversione fra interi di differenti dimensioni deve essere il più possibile evitata. La conversione
   di un intero di grandi dimensioni ad uno più piccolo (da 32 a 16 bit o da 16 a 8 bit) può causare il
   troncamento del valore memorizzato in una variabile o determinarne il cambio di segno. Ad
   esempio convertire l’intero signed a 16 bit -1 in intero unsigned a 32 bit darà come risultato il
   valore 4.294.967.295
    In particolare sono negate tutte le conversioni riportate nella seguente tabella:
   Da A
   16 bit signed 32 bit unsigned
   32 bit signed 16 bit unsigned
   32 bit unsigned 16 bit signed
   32 bit signed 16 bit signed
    Il codice non deve affidarsi a conversioni implicite e/o dedotte dal compilatore.

.. _computazione-e-condizionali-.:

7.1.8.11 Computazione e Condizionali ……………………………………………………………………………………………………………….
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

::

    I dati devono essere appropriatamente confrontati con altri dello stesso tipo, specialmente per i
   tipi float e double.
   Esempio:
   if ( variabile == 0.1 ) questa condizione potrebbe non rivelarsi mai vera, per le proprietà
   di arrotondamento del compilatore;
    Le variabili dichiarate come unsigned non devono mai essere confrontate con lo zero utilizzando
   l'operatore "maggiore di".
   Esempio:
   if ( variabile > 0) risulta sempre vero se variabile è unsigned;
    Le variabili dichiarate come signed, non devono mai essere confrontate con TRUE.
   Esempio: if (variabile)
    Se ad esempio variabile può assumere un valore negativo è meglio prevedere questo caso con un
   controllo del tipo: if (variabile != 0) oppure ancora più esplicito controllando il segno dell’intero.

.. _controllo-del-flusso-..:

7.1.8.12 Controllo del flusso ……………………………………………………………………………………………………………………………..
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

::

    Variabili di controllo
   o E’ obbligatorio utilizzare sempre un limite superiore "inclusive" e il limite inferiore come
   "esclusive".
   Esempio - Forma non corretta:
   x >= 23 e x <= 42
   Esempio - Forma corretta:
   x >= 23 e x < 43
    Switches
   o Ogni blocco di codice appartenente ad ogni caso di uno switch deve essere terminato dalla
   keyword "break";
   o Ogni switch deve avere un caso di default.

.. _passaggio-di-argomenti-..:

7.1.8.13 Passaggio di argomenti ………………………………………………………………………………………………………………………..
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

::

    I tipi di dati esterni non devono essere passati "per valore" (by value);
    I vettori e le strutture devono sempre essere passati per indirizzo o per riferimento;
    E’ auspicabile utilizzare la keyword “const” per i paramatri (strutture o vettori) passati in ingresso
   ad una funzione.

.. _valori-di-ritorno-.:

7.1.8.14 Valori di ritorno ………………………………………………………………………………………………………………………………….
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

::

    I tipi di dati devono essere appropriati per memorizzare i valori di ritorno delle funzioni;
    Se i parametri delle funzioni sono passati come riferimenti “const”, i valori di ritorno devono
   anche essere ritornati come riferimenti "const".

.. _chiamate-a-funzioni-.:

7.1.8.15 Chiamate a funzioni …………………………………………………………………………………………………………………………….
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

::

    Ogni chiamata a fprintf() deve avere il suo argomento FILE pointer inizializzato;
    Ogni chiamata a funzione deve contenere i parametri corretti, coerenti con il tipo ed il formato del
   prototipo della funzione.

.. _files-.:

7.1.8.16 Files ………………………………………………………………………………………………………………………………………………….
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

::

    Ogni nome di file temporaneo deve essere unico e non predicibile;
    Ogni puntatore a file deve essere chiuso prima di essere riutilizzato (Esempio: fclose()).

.. _gestione-degli-errori:

7.1.8.17 Gestione degli errori ……………………………………………………………………………………………………………………………
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

::

    I valori di ritorno di tutte le chiamate di sistema devono essere controllati per determinare lo stato
   di esecuzione del programma. Funzioni come perror(), ferror() ed strerror() e la
   costante errno devono essere utilizzate per determinare o riportare all’utente il tipo di errore
   occorso;
    errno non deve essere dichiarato manualmente come un extern se risiede in uno degli include
   dell’implementazione C/C++ utilizzata;
    Al verificarsi di un errore critico o imprevisto a seguito di una chiamata di sistema, tutti i puntatori
   e le aree di memoria utilizzate devono essere dereferenziati/disallocate prima della chiusura del
   programma.

.. _sicurezza-dellapplicazione-..:

7.1.8.18 Sicurezza dell'applicazione …………………………………………………………………………………………………………………..
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

::

    I risultati dei controlli, delle procedure di sicurezza ed i relativi dati non devono risiedere in
   memoria per lunghi periodi. Ad esempio le chiavi crittografiche devono permanere in memoria solo
   per il tempo necessario al loro utilizzo e devono essere sovrascritte con dati casuali o garbage data
   al termine del loro impiego;
    I dati critici non devono mai essere serializzati.
