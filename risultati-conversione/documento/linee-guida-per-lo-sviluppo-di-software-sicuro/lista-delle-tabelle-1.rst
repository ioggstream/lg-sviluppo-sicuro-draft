.. _lista-delle-tabelle-1:

.. _lista-delle-tabelle-1:

LISTA DELLE TABELLE
===================

-  1 INTRODUZIONE

   -  1.1 SCOPO

   -  1.2 AMBITO DI APPLICABILITÀ

   -  1.3 STRUTTURA DEL DOCUMENTO

-  2 RIFERIMENTI

   -  2.1 DOCUMENTI DI RIFERIMENTO

-  3 DEFINIZIONI E ACRONIMI

   -  3.1 DEFINIZIONI

   -  3.2 ACRONIMI…………………………………………………………………………………………………………………………………………..

-  4 SVILUPPARE APPLICAZIONI SICURE

-  5 PROGETTAZIONE E SVILUPPO DELL'APPLICAZIONE: DIRETTIVE STANDARD

   -  5.1 PROGETTAZIONE DELL'APPLICAZIONE

   -  5.2 SVILUPPO DELL'APPLICAZIONE – CRITERI GENERALI

      -  5.2.1 Performance

      -  5.2.2 Password nel codice sorgente

      -  5.2.3 Privilegi esecutivi minimi

      -  5.2.4 Metodo TRACE

      -  5.2.5 Assenza di codice malevolo

      -  5.2.6 Fattore integrità

      -  5.2.7 Input data validation

      -  5.2.8 Gestione dell'output

   -  5.3 FORMATTAZIONE DEL CODICE

      -  5.3.1 Stile e sintassi

      -  5.3.2 Algoritmi

      -  5.3.3 Utilizzo funzioni di gestione delle stringhe

      -  5.3.4 Specifica del formato delle stringhe

      -  5.3.5 Casting e variabili numeriche

   -  5.4 TRACCIAMENTO E RACCOMANDAZIONI DI “ALARM DETECTION”

      -  5.4.1 Tracciamento eventi

      -  5.4.2 Tracciamento eventi di “Alarm Detection”

      -  5.4.3 Scopo e campo di applicazione per eventi di “Alarm
         Detection”

      -  5.4.4 Raccomandazioni generali per eventi di “Alarm Detection”

   -  5.5 COMPILAZIONE
      DELL'APPLICAZIONE……………………………………………………………………………………………………………..

      -  5.5.1 Stack Canary

      -  5.5.2 Correttezza del sorgente

   -  5.6 AMBIENTE OPERATIVO DELL'APPLICAZIONE

      -  5.6.1 Separazione degli ambienti

      -  5.6.2 Test dell'Applicazione

      -  5.6.3 Strumenti

      -  5.6.4 Profili utente

      -  5.6.5 Trattamento dei dati

      -  5.6.6 Protezione dei sorgenti e delle librerie

   -  5.7 AUTENTICAZIONE, AUTORIZZAZIONE E GESTIONE DEGLI ACCESSI

      -  5.7.1 Policy standard “Everything is generally forbidden unless
         expressly permitted”

      -  5.7.2 Assegnazione dei privilegi utente

      -  5.7.3 Procedura di accesso dell'applicazione

      -  5.7.4 Account standard

      -  5.7.5 Autorizzazione

      -  5.7.6 Generazione dei token

      -  5.7.7 Generazione dei cookie

      -  5.7.8 Contenuto del cookie

      -  5.7.9 Scadenza del cookie

      -  5.7.10 Logout utente

      -  5.7.11 Timeout di sessione

      -  5.7.12 Isolamento delle funzioni dall'applicazione

   -  5.8 PASSWORD, CHIAVI E CERTIFICATI

      -  5.8.1 Gestione di password, chiavi e certificati

      -  5.8.2 Trasmissione delle password in rete

      -  5.8.3 Generazione/conservazione delle password nel
         filesystem/DB

      -  5.8.4 Batch Job dell'applicazione

      -  5.8.5 Storage dei dati applicativi

      -  5.8.6 Integrità delle informazioni

      -  5.8.7 Meccanismi di autenticazione

      -  5.8.8 Non ripudio delle sessioni

      -  5.8.9 Schemi di sicurezza e crittografici

      -  5.8.10 Weak Keys e Collision

      -  5.8.11 URL cifrati

      -  5.8.12 Normalizzazione dei dati cifrati

-  6 PRINCIPALI VULNERABILITÀ DERIVANTI DA ERRORI DI PROGRAMMAZIONE:
   OVERVIEW

   -  6.1 VALIDAZIONE DELL' INPUT

      -  6.1.1 Shell Execution Command

      -  6.1.2 File Inclusion

      -  6.1.3 Cross Site Scripting (XSS)

      -  6.1.4 Directory Traversal

      -  6.1.5 SQL Injection

   -  6.2 SESSION MANAGEMENT

      -  6.2.1 Session Stealing ed Hjihacking

         -  6.2.1.1 Cookie
            …………………………………………………………………………………………………………………………………………………

         -  6.2.1.2 Token di
            sessione………………………………………………………………………………………………………………………………….

         -  6.2.1.3 Accesso ad aree non autorizzate
            …………………………………………………………………………………………………………….

   -  6.3 CRITTOGRAFIA

      -  6.3.1 Sniffing ed algoritmi crittografici deboli

      -  6.3.2 Brute Forcing

      -  6.3.3 Rainbow Table e Salt Value

      -  6.3.4 Archiviazione insicura

   -  6.4 GESTIONE DEGLI ERRORI, DELLE ECCEZIONI

      -  6.4.1 User Enumeration

      -  6.4.2 Information Disclosure

      -  6.4.3 Directory Listing

      -  6.4.4 Denial of Service

      -  6.4.5 Race Condition

      -  6.4.6 Privilege Escalation e Bypassing dei permessi utente

   -  6.5 BOUND CHECKING E PROBLEMATICHE DI OVERFLOW

      -  6.5.1 Stack
         Overflow……………………………………………………………………………………………………………………………

      -  6.5.2 Off-by-one/Off-by-few

      -  6.5.3 Format String

      -  6.5.4 Heap Overflow

      -  6.5.5 Integer Overflow ed altri errori logici di programmazione

   -  6.6 PROCESSI DI TRACCIAMENTO

      -  6.6.1 Agevolazione delle attività malevole dell'aggressore

      -  6.6.2 Oscuramento delle attività dell'aggressore

-  7 BEST PRACTICES PER LO SVILUPPO IN SICUREZZA

   -  7.1 C/C++

      -  7.1.1 Cross-site scripting
         (XSS)………………………………………………………………………………………………………………

      -  7.1.2 Command Injection

      -  7.1.3 Connection String Injection

      -  7.1.4 Resource Injection

      -  7.1.5 (Second Order) SQL Injection

      -  7.1.6 LDAP Injection

   -  7.1.7 Process Control

   -  7.1.8 Ulteriori indicazioni per lo sviluppo sicuro

      -  7.1.8.1 Dichiarazioni
         ………………………………………………………………………………………………………………………………………..

      -  7.1.8.2 Inizializzazioni
         ………………………………………………………………………………………………………………………………………

      -  7.1.8.3 Utilizzo dei tipi di dati
         ……………………………………………………………………………………………………………………………

      -  7.1.8.4 Bitfields
         ……………………………………………………………………………………………………………………………………………….

      -  7.1.8.5 Macro
         …………………………………………………………………………………………………………………………………………………

      -  7.1.8.6 L'operatore sizeof ed il passaggio di dati come
         parametri ………………………………………………………………………….

      -  7.1.8.7 Allocazione dinamica
         …………………………………………………………………………………………………………………………….

      -  7.1.8.8 Deallocazione
         ………………………………………………………………………………………………………………………………………

      -  7.1.8.9 Puntatori

      -  7.1.8.10 Casting e problematiche di gestione delle variabili
         numeriche ………………………………………………………………….

      -  7.1.8.11 Computazione e Condizionali
         ……………………………………………………………………………………………………………….

      -  7.1.8.12 Controllo del flusso
         ……………………………………………………………………………………………………………………………..

      -  7.1.8.13 Passaggio di argomenti
         ………………………………………………………………………………………………………………………..

      -  7.1.8.14 Valori di ritorno
         ………………………………………………………………………………………………………………………………….

      -  7.1.8.15 Chiamate a funzioni
         …………………………………………………………………………………………………………………………….

      -  7.1.8.16 Files
         ………………………………………………………………………………………………………………………………………………….

      -  7.1.8.17 Gestione degli errori
         ……………………………………………………………………………………………………………………………

      -  7.1.8.18 Sicurezza dell'applicazione
         …………………………………………………………………………………………………………………..

-  7.2 JAVA

   -  7.2.1 Cross-site scripting
      (XSS)………………………………………………………………………………………………………………

   -  7.2.2 Code Injection

   -  7.2.3 Command Injection

   -  7.2.4 Connection String Injection

   -  7.2.5 LDAP Injection

   -  7.2.6 Resource Injection

   -  7.2.7 (Second Order) SQL Injection

   -  7.2.8 XPath Injection

   -  7.2.9 Ulteriori indicazioni per lo sviluppo sicuro

      -  7.2.9.1 Inizializzazione
         ……………………………………………………………………………………………………………………………………..

      -  7.2.9.2 Visibilità
         ………………………………………………………………………………………………………………………………………………

      -  7.2.9.3 Modificatori
         …………………………………………………………………………………………………………………………………………

      -  7.2.9.4 Utilizzo degli oggetti mutevoli
         ………………………………………………………………………………………………………………..

      -  7.2.9.5 Definizione delle classi
         …………………………………………………………………………………………………………………………..

      -  7.2.9.6 Codice e permessi speciali
         ……………………………………………………………………………………………………………………..

      -  7.2.9.7 Esecuzione dei comandi di sistema
         …………………………………………………………………………………………………………

      -  7.2.9.8 Oggetti
         ………………………………………………………………………………………………………………………………………………..

      -  7.2.9.9 Serializzazione e
         deserializzazione…………………………………………………………………………………………………………..

      -  7.2.9.10 Memorizzazione delle informazioni riservate
         …………………………………………………………………………………………

      -  7.2.9.11 Packages
         ……………………………………………………………………………………………………………………………………………

      -  7.2.9.12 Gestione delle eccezioni
         ………………………………………………………………………………………………………………………

      -  7.2.9.13 Java Applet
         ………………………………………………………………………………………………………………………………………..

      -  7.2.9.14 Java Servlet
         ………………………………………………………………………………………………………………………………………..

-  7.3 PL/SQL

   -  7.3.1 Cross-site scripting
      (XSS)………………………………………………………………………………………………………………

   -  7.3.2 Resource Injection

   -  7.3.3 (Second Order) SQL Injection

   -  7.3.4 Ulteriori indicazioni per lo sviluppo sicuro

      -  7.3.4.1 Posizionamento delle procedure PL/SQL
         ………………………………………………………………………………………………….

      -  7.3.4.2 Tipologie di procedure vulnerabili
         …………………………………………………………………………………………………………..

      -  7.3.4.3 Filtraggio dei tipi di input iniettabile
         ………………………………………………………………………………………………………..

      -  7.3.4.4 Filtraggio di caratteri potenzialmente dannosi
         ………………………………………………………………………………………….

      -  7.3.4.5 Direttive per Oracle
         ………………………………………………………………………………………………………………………………

-  7.4 JAVASCRIPT

   -  7.4.1 DOM-based XSS

      -  7.4.1.1 Client DOM Code Injection
         …………………………………………………………………………………………………………………….

      -  7.4.1.2 Client DOM stored Code Injection

      -  7.4.1.3 DOM Stored XSS
         …………………………………………………………………………………………………………………………………..

      -  7.4.1.4 Client DOM XSS
         …………………………………………………………………………………………………………………………………….

   -  7.4.2 Client Resource Injection

   -  7.4.3 Client Second Order Sql Injection

   -  7.4.4 Client Sql Injection

-  7.5 PYTHON

   -  7.5.1 Cross-site scripting
      (XSS)………………………………………………………………………………………………………………

   -  7.5.2 Code Injection

   -  7.5.3 Command Injection

   -  7.5.4 Connection String Injection

   -  7.5.5 LDAP Injection

   -  7.5.6 Resource Injection

   -  7.5.7 (Second Order) SQL Injection

   -  7.5.8 XPath Injection

   -  7.5.9 OS Access Violation

-  7.6 C#

   -  7.6.1 Cross-site scripting
      (XSS)………………………………………………………………………………………………………………

   -  7.6.2 Code Injection

   -  7.6.3 Command Injection

   -  7.6.4 Connection String Injection

   -  7.6.5 LDAP Injection

   -  7.6.6 Resource Injection

   -  7.6.7 (Second Order) SQL Injection

   -  7.6.8 XPath Injection

   -  7.6.9 Ulteriori indicazioni per lo sviluppo sicuro

      -  7.6.9.1 Managed Wrapper per l'implementazione del codice nativo
         ……………………………………………………………………

      -  7.6.9.2 Library Code che espone risorse protette
         ………………………………………………………………………………………………

      -  7.6.9.3 Richieste di autorizzazione
         …………………………………………………………………………………………………………………..

      -  7.6.9.4 Modificatori
         ……………………………………………………………………………………………………………………………………….

      -  7.6.9.5 Definizione delle classi
         …………………………………………………………………………………………………………………………

      -  7.6.9.6 User input
         ………………………………………………………………………………………………………………………………………….

      -  7.6.9.7 Oggetti
         ………………………………………………………………………………………………………………………………………………

      -  7.6.9.8 Serializzazione e
         deserializzazione…………………………………………………………………………………………………………

-  7.7 ASP………………………………………………………………………………………………………………………………………………..

   -  7.7.1 Cross-site scripting
      (XSS)…………………………………………………………………………………………………………….

   -  7.7.2 Code Injection

   -  7.7.3 Command Injection

   -  7.7.4 Connection String Injection

   -  7.7.5 LDAP Injection

   -  7.7.6 XPath Injection

   -  7.7.7 Resource Injection

   -  7.7.8 SQL Injection

-  7.8 ASP.NET

   -  7.8.1 Cross-site scripting
      (XSS)…………………………………………………………………………………………………………….

   -  7.8.2 Code Injection

   -  7.8.3 Command Injection

   -  7.8.4 Connection String Injection

   -  7.8.5 LDAP Injection

   -  7.8.6 Resource Injection

   -  7.8.7 SQL Injection

   -  7.8.8 Xpath Injection

   -  7.8.9 Ulteriori indicazioni per lo sviluppo sicuro

      -  7.8.9.1 ASP.NET Web Form
         …………………………………………………………………………………………………………………………….

      -  7.8.9.2 ASP.NET MVC
         ……………………………………………………………………………………………………………………………………..

-  7.9 PHP

   -  7.9.1 Cross-site scripting
      (XSS)…………………………………………………………………………………………………………….

   -  7.9.2 Code Injection

   -  7.9.3 Command Injection

   -  7.9.4 File Disclosure

      -  7.9.5 Remote File Inclusion

      -  7.9.6 File Manipulation

      -  7.9.7 LDAP Injection

      -  7.9.8 Reflected Injection

      -  7.9.9 SQL Injection

      -  7.9.10 Xpath Injection

   -  7.10 VBNET

      -  7.10.1 Cross-site scripting (XSS)

      -  7.10.2 Code Injection

      -  7.10.3 Command Injection

      -  7.10.4 Connection String Injection

      -  7.10.5 LDAP Injection

      -  7.10.6 Resource Injection

      -  7.10.7 SQL Injection

      -  7.10.8 Xpath Injection

   -  7.11 AJAX

      -  7.11.1 Client Dom Code Injection

      -  7.11.2 Client DOM Stored Code Injection

      -  7.11.3 Client Dom Stored XSS

      -  7.11.4 Client Dom XSS

      -  7.11.5 Client Resource Injection

      -  7.11.6 Client Second Order Sql
         Injection……………………………………………………………………………………………….

      -  7.11.7 Client Sql Injection

      -  7.11.8 Cross-Site Request Forgery (CSRF)

   -  7.12 GO

      -  7.12.1 Client Dom Stored XSS

      -  7.12.2 SQL Injection

      -  7.12.3 Ulteriori indicazioni per lo sviluppo sicuro

         -  7.12.3.1 Validazione dell'INPUT
            ………………………………………………………………………………………………………………………

         -  7.12.3.2 Gestione Sessione, Controlli Accessi e Crittografia
            ………………………………………………………………………………..

         -  7.12.3.3 Gestione degli Errori e delle Eccezioni
            …………………………………………………………………………………………………

         -  7.12.3.4 Sicurezza del Database
            ………………………………………………………………………………………………………………………

-  Tabella 2 - Documenti di Riferimento Tabella 1 - Documenti
   Applicabili Errore. Il segnalibro non è definito.

-  Tabella 3 – Definizioni

-  Tabella 4 - Acronimi

-  Figura 1: Schema per la sicurezza dell'applicazione LISTA DELLE
   FIGURE
