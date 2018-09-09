.. _figura-16-flusso-di-valutazione-necessità-dpia:

Figura 16 – Flusso di valutazione necessità DPIA
================================================

Pertanto, se il trattamento, le sue modalità di attuazione o i dati
trattati rientrano in quelli descritti nella Tabella 8, e non si
configurano eccezioni – individuate all'interno di elenchi che dovranno
essere redatti dagli Stati Membri (ad oggi non risultano essere stati
ancora individuati) - sarà necessario svolgere una DPIA.

(^) Pag. 91 of 121 **Tipologia di trattamento Descrizione 1 -
Valutazione di profilazione o scoring** Tutti quei trattamenti che
analizzano i dati presenti all'interno dei propri archivi allo scopo di
trarne informazioni riguardo il rendimento professionale, la situazione
economica, la salute, le preferenze o gli interessi personali,
l'affidabilità o il comportamento, l'ubicazione o gli spostamenti
dell'interessato **2 - Decisioni automatizzate** Tutti quei trattamenti
che producano effetti giuridici sulla persona fisica ovvero che incidono
in modo analogo significativamente su dette persone fisiche **3 -
Monitoraggio sistematico** Tutti quei trattamenti che sono utilizzati
per osservare, monitorare o controllare gli interessati, compresa la
raccolta di dati attraverso reti o la sorveglianza di un'area
accessibile al pubblico **4 - Dati sensibili o estremamente personali**
Tutti quei trattamenti che si riferiscono a particolari categorie di
dati sensibili o estremamente personali **5 - Dati trattati su larga
scala** Tutti i trattamenti che gestiscono dati personali su larga
scala, in relazione al numero di soggetti interessati, al volume dei
dati, alla durata o all'ambito geografico **6 - Combinazioni o raffronto
di insieme di dati** Tutti quei trattamenti nei quali è prevista una
presenza congiunta di due o più titolari distinti, secondo modalità che
esulano dalle ragionevoli aspettative dell'interessato **7 - Dati
relativi a interessati vulnerabili** Tutti quei trattamenti in cui la
tipologia delle informazioni trattate determina uno squilibrio fra
interessato e titolare, nel senso della mancanza del potere, in capo al
primo, di acconsentire o di opporsi al trattamento. Si inseriscono in
questa categoria i dati dei minori, dei dipendenti o delle persone
richiedenti specifiche tutele **8 - Utilizzi innovativi** Tutti quei
trattamenti che utilizzano tecnologie o tecniche innovative per la
raccolta o l'utilizzo dei dati personali, dato che il livello di
conoscenza tecnologica, in un dato momento storico, non è in grado
valutare il livello di rischio connesso all'innovazione **9 -
Trattamenti che impediscono di esercitare un diritto o avvalersi di un
servizio o contratto** Tutti quei trattamenti che impediscono agli
interessati di esercitare un diritto di avvalersi di un servizio o di un
contratto, ossia tutti i trattamenti dai quali l'interessato non può
esimersi qualora volesse accedere a detto servizio o concludere detto
contratto **Tabella 7 - Tipologie di trattamento che rappresentano un
rischio elevato** Nel caso in cui la DPIA sia stata valutata come
necessaria (cfr. DR-10), si potrà procedere con l'analisi degli impatti
potenziali sui diritti e le libertà dell'interessato (persone fisiche),
a fronte del trattamento dei relativi dati personali, allo scopo di
porre in essere le opportune attività di trattamento dei rischi per la
protezione dei dati personali. In linea con quanto previsto da
regolamenti e standard applicabili in materia (cfr. DR-6 ), tale
attività costituisce un processo composto da un insieme di attività ben
definite, da compiersi in sequenza ordinata, nell'ambito delle seguenti
fasi: 1) **Definizione del contesto** , tramite la comprensione
dell'organizzazione, dell'architettura tecnologica e dei fattori che
potrebbero influenzare la gestione del rischio privacy;

(^) Pag. 92 of 121 2) **Privacy risk assessment** , attraverso cui si
identificano, si analizzano e si valutano i rischi per gli interessati;
3) **Privacy risk treatment** , in cui si identificano le strategie e le
modalità operative per l'implementazione delle misure di sicurezza
adeguate alla copertura dei rischi rilevati in sede di risk assessment.
(I requisiti di protezione per la privacy, da implementare all'interno
del piano di trattamento dei rischi individuati per il software possono
essere ricavati dai controlli descritti nella ISO/IEC 29151 (cfr. DR-7 )
**10.1.4.1 Riconoscere le informazioni personali identificabili (PII)**
Per poter definire adeguatamente il trattamento del rischio privacy per
i software, sarà necessario individuare le tipologie di informazioni
personali identificabili (PII), ossia quelle da cui possono essere
ricavati dei dati personali, che potrebbero essere trattate da un
applicativo software. Per determinare se una persona fisica debba o meno
essere considerata identificabile, sarà necessario prendere in
considerazione diversi fattori. In particolare, si dovrebbe tenere conto
dei mezzi che possono ragionevolmente essere utilizzati dai software per
il trattamento dei dati personali. I software dovrebbero supportare
meccanismi adeguati ad informare l'interessato, raccogliere il consenso
e progettare i suoi dati personali. Le seguenti specificazioni
forniscono degli ulteriori chiarimenti su come determinare se una
informazione possa essere considerata PII. **Identificativi** In alcuni
casi, l'identificabilità dell'interessato potrebbe essere molto semplice
(e.g. quando l'informazione contiene o è associata ad un identificatore
che è usato per riferirsi o per comunicare con l'interessato). Le
informazioni possono essere considerate PII almeno nei seguenti casi: o
se contiene o è associato a un identificatore che fa riferimento a una
persona fisica (ad esempio, il codice fiscale); o se contiene o è
associato a un identificatore che può essere correlato a una persona
fisica (ad esempio, numero del passaporto, numero di conto); o se
contiene o è associato a un identificatore che può essere utilizzato per
stabilire una comunicazione con o una persona fisica identificata (ad
esempio, una posizione geografica precisa, un numero di telefono); o se
contiene un riferimento che collega i dati a uno degli identificatori di
cui sopra. **Altre caratteristiche identificative** Le informazioni non
devono necessariamente essere associate a un identificatore per poter
essere considerate PII. Le informazioni saranno considerate PII anche se
contengono o sono associate a una caratteristica che distingue una
persona fisica da altre persone fisiche, ad esempio i dati biometrici.
Qualsiasi attributo che assume un valore che identifica univocamente un
l'interessato deve essere considerato come una caratteristica
identificativa. Si noti che indipendentemente dal fatto che una
determinata caratteristica distingue una persona fisica da altre
potrebbe cambiare a seconda del contesto di utilizzo. Ad esempio, mentre
il cognome di una persona fisica potrebbe essere insufficiente per
identificare quella persona naturale su una globale scala, sarà spesso
sufficiente distinguere una persona fisica su una scala aziendale.
Inoltre, ci possono anche essere situazioni in cui una persona fisica è
identificabile anche se non c'è singolo attributo che lo identifica in
modo univoco. Questo è il caso in cui una combinazione di diversi
attributi presi insieme distingue questa persona da altre, ad esempio la
combinazione degli attributi “femmina”, “45” e “avvocato” può essere
sufficiente per identificare una persona fisica all'interno di una
determinata organizzazione, ma spesso sarà insufficiente per
identificare quella persona fisica al di fuori di tale contesto. La
Tabella 9 fornisce alcuni esempi di attributi che potrebbero essere PII,
a seconda del dominio.

(^) Pag. 93 of 121 Età o bisogni speciali delle persone fisiche
vulnerabili Accuse di condotta criminale Qualsiasi informazione raccolta
durante i servizi sanitari Conto bancario o numero di carta di credito
Identificatore biometrico Estratto conto della carta di credito Condanne
penali o reati commessi Rapporti di indagini penali Numero cliente Data
di nascita Informazioni sanitarie diagnostiche disabilità Fatture del
medico Stipendi dei dipendenti e file di risorse umane Profilo
finanziario Genere Posizione GPS Traiettorie GPS Indirizzo di casa
indirizzo IP Posizione derivata dai sistemi di telecomunicazione Storia
medica Nome Identificativi nazionali (ad es. Numero di passaporto)
Indirizzo e-mail personale Numeri di identificazione personale (PIN) o
password Interessi personali derivati dall'utilizzo di tracciamento di
siti Web Profilo personale o comportamentale Numero di telefono
personale Fotografia o video identificabili con una persona fisica
Preferenze di prodotto e servizio Origine razziale o etnica Credenze
religiose o filosofiche Orientamento sessuale Appartenenza sindacale
Bollette **Tabella 8 - Esempi di Attributi per indentificare una
persona** **Dati pseudonimizzati** Al fine di limitare la capacità del
titolare o del responsabile di identificare l'interessato, la sua
identità e le sue informazioni possono essere sostituite da degli
pseudonimi. Questa sostituzione viene solitamente eseguita da un
soggetto terzo prima di trasmettere le PII a un destinatario. Questo è
spesso il caso in cui i dati sensibili devono essere elaborati titolari
che non li hanno raccolti. La sostituzione è considerata
pseudonimizzazione quando: (a) gli attributi collegati allo pseudonimo
non sono sufficienti per identificare l'interessato; (b) l'assegnazione
degli pseudonimi è tale da non poter essere invertita da parte delle
persone che l'hanno eseguita. La pseudonimizzazione evita il
collegamento. Ma esseno diversi i dati collegabili allo stesso
pseudonimo, ci sarà il rischio che la pseudonimizzazione sia violata, in
quanto più grande è il set di dati associato a un dato pseudonimo,
maggiore è il rischio che la proprietà (a) sia violata. Inoltre, più
piccolo è il gruppo di persone fisiche a cui un insieme di dati
pseudonimi si riferisce, maggiore sarà la probabilità che un interessato
sia identificabile. Gli attributi contenuti direttamente nelle
informazioni in questione e gli attributi che possono essere facilmente
collegati a queste informazioni (ad es. utilizzando un motore di ricerca
o dei riferimenti incrociati con altri database) devono essere presi in
considerazione nel determinare se l'informazione si riferisce a un
elemento identificabile dell'interessato. La pseudonimizzazione è in
contrasto con l'anonimizzazione. I processi di anonimizzazione
soddisfano anche le proprietà (a) e (b) sopra, ma eliminano il
collegamento. Durante l'anonimizzazione, le informazioni sull'identità
vengono cancellate o sostituito da pseudonimi per i quali la funzione di
assegnazione viene distrutta. Quindi, i dati resi anonimi non sono più
PII. **Metadati** Le PII possono essere memorizzate in un sistema ICT in
modo tale da non essere facilmente visibili all'utente del sistema. Ad
esempio, la memorizzazione del nome dell'interessato come metadato nelle
proprietà di un documento, nei commenti o nelle modifiche. L'interessato
deve essere a conoscenza

::

   Pag. 94 of 121

dell'esistenza delle PII sotto forma di metadati o del trattamento delle
PII per tale scopo, in quanto potrebbe preferire che le PII non vengano
elaborate in questo modo o condivise pubblicamente.

**Dati non richiesti**

Anche le PII non richieste da un titolare, cioè non intenzionalmente
ottenute, potrebbero essere memorizzate da un software. Ad esempio,
l'interessato potrebbe fornire delle PII anche quando non è stato
richiesto dal trattamento (ad es. ulteriori informazioni personali
fornite nel contesto di un modulo di feedback anonimo su un sito Web).
Il rischio di raccogliere informazioni personali indesiderate può essere
ridotto considerando le misure di tutela della privacy al momento della
progettazione del software.

I dati personali stabiliti dal GDPR (cfr. DR-1 ) sono suddivisi nelle
seguenti categorie di dati personali:

::

   Categorie di dati
   personali
   Descrizione

**Dati identificativi** I dati identificativi rappresentano tutti quei
dati che possono identificare, direttamente o indirettamente una
persona, con particolare riferimento a un identificativo come il nome,
un numero di identificazione, dati relativi all'ubicazione, un
identificativo online.

**Dati Sensibili** I dati sensibili sono tutti quei dati personali che
rivelino l'origine razziale o etnica, le opinioni politiche, le
convinzioni religiose o filosofiche, o l'appartenenza sindacale, nonché
dati genetici dati biometrici intesi a identificare in modo univoco una
persona fisica, dati relativi alla salute o alla vita sessuale o
all'orientamento sessuale della persona.

**Dati giudiziari** I dati giudiziari rappresentano tutti quei dati
relativi alle condanne penali e ai reati o a connesse misure di
sicurezza.

.. _flusso-informativo-del-trattamento:

10.1.5 Flusso informativo del trattamento
-----------------------------------------

Per definire l'architettura e il design di un software i progettisti
dovranno prendere in considerazione la struttura del flusso informativo,
descrivendo le interazioni tra interessato, titolare, responsabile e
terze parti all'interno dell'applicativo software. Gli attori
identificati possono interagire tra loro in vari modi, secondo i
seguenti scenari, maturati dalla ISO/IEC 29134:2017 (cfr. DR-6 ):

(^) **Interessato Titolare del trattamento Responsabile del trattamento
Terze parti**\ :sup:`Raccolta Archiviazione Registrazione utente Dato`
**Raccoglie**\ :sup:`Archivia Dato Fornisce` **Dato**

::

   Pag. 95 of 121
   Utilizzo
   Trasferimento
   Cancellazione
