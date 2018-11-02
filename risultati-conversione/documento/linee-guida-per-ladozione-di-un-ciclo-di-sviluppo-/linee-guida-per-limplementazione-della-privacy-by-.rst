.. _linee-guida-per-limplementazione-della-privacy-by-design-nel-sdlc:

10 LINEE GUIDA PER L'IMPLEMENTAZIONE DELLA PRIVACY BY DESIGN NEL SDLC
=====================================================================

.. _introduzione-e-concetti-base:

10.1 INTRODUZIONE E CONCETTI BASE
---------------------------------

.. _principi-della-privacy:

10.1.1 Principi della Privacy
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

::

   All’interno dalla ISO/IEC 29100:2011 (cfr. DR-2 ) sono descritti undici principi sulla privacy, che devono
   essere presi in esame per orientare la progettazione, lo sviluppo e l’implementazione dei requisiti di
   protezione per la privacy (10.1.4). Inoltre, devono essere ulteriormente utilizzati come riferimento per il
   monitoraggio e la misurazione delle prestazioni del software e come aspetti del controllo dei programmi di
   gestione della privacy in un’organizzazione.
   Principi Descrizione

1. Consenso e scelta Il principio del consenso prevede di presentare
   all'interessato la scelta se acconsentire o meno al trattamento dei
   propri dati personali (Consenso Informato). Aderire al principio
   della scelta significa fornire all'interessato - in maniera chiara,
   facilmente comprensibile, accessibile e conveniente - i meccanismi
   per esercitare la scelta e di fornire il consenso in relazione al
   trattamento dei suoi dati personali al momento di raccolta, al primo
   utilizzo o non appena possibile.

2. Scopo legittimo e specifico Il principio di legittimità e specificità
   dello scopo assicura che quest'ultimo sia conforme alla legge
   applicabile e si basi su una base giuridica ammissibile.

3. Limitazione della raccolta Il principio della limitazione della
   raccolta prevede la limitazione della raccolta dei dati personali a
   ciò che è strettamente necessario per gli scopi specificati.

4. Minimizzazione dei dati Il principio della minimizzazione dei dati
   prevede la progettazione e l'implementazione e l'elaborazione dei
   dati, attraverso procedure o sistemi ICT, in modo da ridurre al
   minimo i dati personali che vengono elaborati e il numero di parti
   interessate della privacy.

5. Limitazione dell'utilizzo, conservazione e divulgazione

::

   Tale principio prevede la limitazione dell'utilizzo, della conservazione e della
   divulgazione (incluso il trasferimento) dei dati personali a ciò che è necessario
   per soddisfare gli scopi specifici, espliciti e legittimi del trattamento.

6. Precisione e qualità Il principio di accuratezza e qualità assicura
   che i dati personali elaborati siano accurati , completi, aggiornati
   (a meno che non vi sia una base legittima per mantenere dati
   obsoleti), e adeguati e pertinenti ai fini del trattamento.

7. Apertura, trasparenza e preavviso

::

   Tale principio prevede di fornite informazioni chiare e facilmente accessibili sulle
   politiche stabilite dal titolare del trattamento e delle procedure e delle pratiche
   relative al trattamento dei dati personali.

8. Partecipazione individuale e accesso

::

   Il principio della partecipazione e dell’accesso individuale prevede di fornire agli
   interessati la possibilità di accedere e di rivedere i proprio dati personali, a
   condizione che la loro identità autenticata con un livello adeguato di garanzia e
   tale accesso non sia vietato dalla legge applicabile.

9.  Responsabilizzazione Il principio della responsabilità prevede di
    documentare e comunicare in modo appropriato tutte le politiche, le
    procedure e le pratiche relative alla privacy. Prevede altresì
    l'assegnazione ad un individuo specifico all'interno
    dell'organizzazione del compito di attuare le politiche, le
    procedure e le best practice relative alla privacy.

10. Sicurezza delle informazioni Il principio di sicurezza delle
    informazioni prevede di proteggere i dati personali sotto la propria
    autorità con dei controlli appropriati a livello operativo,

::

   Pag. 88 of 121
   funzionale e strategico. Al fine di garantire l'integrità, la riservatezza e la
   disponibilità dei dati personali e proteggerli dai rischi, quali l’accesso non
   autorizzato, la distruzione, l’utilizzo non consentito, la modifica, la divulgazione o
   la perdita in tutto il ciclo di vita dell’informazione.

11. Conformità alla privacy Il principio della conformità alla privacy
    prevede di verificare e dimostrare che il trattamento rispetti la
    protezione dei dati e la tutela della privacy, attraverso requisiti
    specifici e mediante verifiche periodiche – anche attraverso il
    ricorso a revisori interni o esterni. **Tabella 5 - Principi
    generali della privacy**

.. _obiettivi-di-protezione:

10.1.2 Obiettivi di protezione
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

::

   Gli obiettivi di protezione mirano a fornire delle proprietà astratte, ossia indipendenti dal contesto per i
   sistemi IT. Nella sicurezza ICT la triade della riservatezza, dell’integrità e della disponibilità è stata
   ampiamente accettata. Sebbene siano state proposte diverse estensioni e perfezionamenti, questi obiettivi
   di protezione core sono rimasti stabili per decenni e sono serviti da base per molte metodologie di sicurezza
   ICT. (cfr. DR-4). A completamento di questi obiettivi di protezione della sicurezza, sono stati proposti tre
   obiettivi di protezione specifici per la privacy: l’incollegabilità, la trasparenza e l’intervenibilità.
   Obiettivo Descrizione
   Incollegabilità L’incollegabilità garantisce che i dati rilevanti per la privacy non possano essere
   collegati tra domini costituiti da uno scopo e contesto comuni. Ciò significa che i
   processi devono essere gestiti in modo tale che i dati rilevanti per la privacy non
   siano collegabili a qualsiasi altro insieme di dati rilevanti sulla privacy al di fuori del
   dominio.
   La trasparenza La trasparenza garantisce che tutte le elaborazioni dei dati rilevanti per la privacy,
   comprese le impostazioni legali, tecniche e organizzative, possano essere comprese
   e ricostruite in qualsiasi momento. Le informazioni devono essere disponibili prima,
   durante e dopo l'elaborazione. Pertanto, la trasparenza deve riguardare non solo
   l'elaborazione effettiva, ma anche l'elaborazione pianificata (trasparenza ex ante) e
   il tempo trascorso dall'elaborazione per sapere cosa è successo esattamente
   (trasparenza ex post)
   L’intervenibilità L'intervenibilità garantisce l'intervento in relazione a tutti i trattamenti di dati
   relativi alla privacy in corso o pianificati, in particolare da parte di coloro i cui dati
   vengono elaborati. L'obiettivo dell'intervenibilità è l'applicazione di misure
   correttive e controbilanci ove necessario. L' intervenibilità è legata ai principi relativi
   ai diritti degli individui, ad es. i diritti di rettifica e cancellazione dei dati, il diritto di
   revocare il consenso o il diritto di presentare un reclamo o di sollevare una
   controversia per ottenere il rimedio.

.. _privacy-by-design:

10.1.3 Privacy by design
~~~~~~~~~~~~~~~~~~~~~~~~

::

   10.1.3.1 Definizione della Privacy by design
   La Privacy by Design (PbD) è definita come “un approccio olistico concettuale che può essere applicato -
   end-to-end - all’interno di un’organizzazione, includendo le sue tecnologie informatiche, le sue pratiche
   commerciali, i suoi processi, la progettazione finisca e le infrastrutture di rete” (cfr. DR-11). Secondo questa
   impostazione, l'utente dovrebbe essere considerato il centro di un sistema di protezione dei dati personali
   (per definizione, quindi il sistmea è "user centric"). Qualsiasi progetto - sia strutturale, sia concettuale -
   andrebbe realizzato considerando, sin dalla fase di progettazione, la riservatezza e la protezione dei dati
   personali. La PbD comprende una trilogia di applicazioni:

(^) Pag. 89 of 121

-  i sistemi IT;

-  Le pratiche di business;

-  La progettazione delle reti (cfr. DR-5 ).

Ed è in questo contesto che si inserisce la necessità di prevedere
l'ingegnerizzazione della privacy by design in ogni fase del ciclo di
vita del software.

**10.1.3.2 I sette principi della privacy by design**

**Principio Descrizione**

Proattivo non reattivo; Preventivo non correttivo

::

   L'approccio di Privacy by Design (PbD) è caratterizzato da misure
   proattive piuttosto che reattive. Essa è diretta ad anticipare e previene
   gli eventi invasivi della privacy prima che accadano. PbD non attende
   che i rischi per la privacy si materializzino, né offre rimedi per la
   risoluzione delle infrazioni della privacy una volta che si sono verificati,
   in quanto è diretta ad impedire che si verifichino.

Privacy come impostazione predefinita

::

   La Privacy by Design è diretta a garantire il massimo grado di privacy
   prevedendo che i dati personali siano automaticamente protetti in
   qualsiasi sistema IT o di business. Nessuna azione è richiesta da parte
   dei singoli per proteggere la loro privacy, in quanto è integrata nei
   sistemi per impostazione predefinita.

Privacy incorporata nel design La *Privacy by Design* è incorporato nel
design e nell'architettura dei sistemi IT e di business. Non è attuata
successivamente ad un evento. Il risultato è che la privacy diventa una
componente essenziale delle funzionalità principali. La privacy è parte
integrante del sistema, senza diminuirne la funzionalità.

Funzionalità completa; somma positiva, non somma zero

::

   La Privacy by Design cerca di tutelare tutti i legittimi interessi e gli
   obiettivi in un’ottica win-win , senza prevedere delle soluzioni a somma
   zero che includano degli inutili trade-off. Privacy by Design evita la
   pretesa di false dicotomie, come la sicurezza a discapito della privacy, in
   quanto dimostra che è possibile averle entrambe.

Sicurezza end-to-end - Protezione completa del ciclo di vita

::

   La Privacy by Design che è stata incorporata in un sistema sin dal primo
   momento, si estende in modo sicuro durante l'intero ciclo di vita dei
   dati coinvolti: prevedendo robuste misure di sicurezza - essenziali per la
   privacy - dall'inizio alla fine di un ciclo di vita. Ciò garantisce che tutti i
   dati vengano conservati e distrutti – in modo sicuro e tempestivamente

-  alla fine del processo. Pertanto, la *Privacy by Design* garantisce
   una gestione delle informazioni sicura end-to-end.

Visibilità e trasparenza - Keep it Open

::

   La Privacy by Design cerca di assicurare a tutti gli stakeholder che
   qualunque sia la pratica aziendale o la tecnologia coinvolta, essa
   opererà secondo le promesse e gli obiettivi dichiarati, anche
   assoggettandosi a verifiche indipendenti. Le sue componenti e le sue
   operazioni rimangono visibili e trasparenti, sia per gli utenti che per i
   fornitori.

Rispetto per la privacy degli utenti - Mantenerlo incentrato sull'utente

::

   La Privacy by Design richiede ai progettisti e agli operatori di garantire
   gli interessi dei singoli, offrendo robuste misure di privacy per
   impostazione predefinita. Prevedendo degli avvisi appropriati e
   potenziando le opzioni user-friendly, pertanto garantendo
   l’impostazione user-centric.
   Pag. 90 of 121
   Tabella 6 - I sette principi della Privacy by Design

.. _data-protection-impact-assessment:

10.1.4 Data protection Impact Assessment
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

La progettazione di qualsiasi software che coinvolga il trattamento dei
dati personali deve essere preceduta da un'identificazione dei requisiti
di protezione per la privacy, in quanto dal trattamento o
dall'elaborazione dei dati personali potrebbero derivare dei rischi. I
rischi per la privacy negli applicativi software che comportano il
trattamento dei dati personali, dovrebbero essere trattati prima della
loro implementazione, ossia sin dalla fase di progettazione (
*Engineering Privacy by Design* ). Dovranno quindi essere analizzati i
rischi collegati alle applicazioni software.

In linea con i requisiti di attuazione previsti dal Regolamento (UE) 679
del 2016 (cfr. DR-1 ), di seguito indicato come **GDPR** , qualora un
trattamento dei dati personali possa presentare un rischio elevato per i
diritti e le libertà delle persone fisiche, i titolari di quest'ultimo
dovranno effettuare una valutazione dell'impatto del trattamento sulla
protezione dei dati personali o *Data Protection Impact Assessment* , di
seguito indicata come “DPIA” (cfr. Art. 35 DR-1 ), quest'obbligo è
applicabile anche al ciclo di vita del software.

Sulla base di quanto stabilito dal WP Art. 29 (cfr. DR-10), sarà
necessario effettuare una valutazione della necessità di svolgere una
DPIA, basandosi sulla mappa concettuale definita nella Figura 16\ **.**

In particolare, al fine di valutare se il trattamento - posto in essere
all'interno di un'applicazione software - possa comportare un rischio
elevato per i diritti e le libertà delle persone fisiche (Cfr. ART. 35
DR-1 ) sarà necessario determinare se rientra tra quelli indicati nella
Tabella 8- in cui sono descritte alcune tipologie di trattamento che
obbligano il titolare a svolgere una Data Protection Impact Assessment
DPIA.
