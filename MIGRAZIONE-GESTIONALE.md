# Gestionale GitHub — piano di migrazione sicura

## Principio fondamentale
Conservare il Gestionale Unico Google Apps Script in produzione. La versione GitHub Pages resta un'interfaccia parallela e non sostituisce il gestionale originale.

## Stato verificato (15 novembre 2026)
- Acquisiti e analizzati `Index.html` e `Codice.gs` forniti dall'amministratore.
- La pagina `gestionale-github.html` è già disponibile come dashboard e indice dei moduli.
- I pulsanti verso i gestionali esistenti sono semplici collegamenti: non significano che la gestione dati sia stata trasferita.
- Il progetto Apps Script contiene autenticazione, sessioni e autorizzazioni con ruoli admin e decano.
- Il backend utilizza Google Drive, Google Sheets, PropertiesService, CacheService e altri servizi Apps Script: non può essere eseguito direttamente su GitHub Pages.

## Aree server individuate nel file fornito
- Login, logout, profilo, gestione utenti e ruoli.
- Archivio documentale, download controllato e cestino.
- Centro notifiche.
- Richieste documentali e consegne.
- Archivio amministrativo.
- Cruscotto del Vicario.
- Calendario integrato.
- Statistiche aggregate dei Decanati.
- Collegamento al gestionale Diaconi.

## Vincoli di protezione
1. Non pubblicare `Codice.gs` nel repository pubblico.
2. Non pubblicare dati personali, password, token di sessione, chiavi, ID di archivi riservati o fogli con dati reali.
3. Non implementare credenziali direttamente in JavaScript sul browser.
4. Non usare il parametro `ticket` del gestionale Diaconi come una chiave permanente nel sito pubblico.
5. Non considerare GitHub Pages un sistema di autenticazione: chiunque può visualizzarne HTML e JavaScript.
6. L'accesso dei Decani e i permessi dei gestionali esterni devono essere verificati singolarmente; una dashboard pubblica non conferisce autorizzazioni.

## Prossime fasi
1. Definire un endpoint API separato e autenticato con risposte JSON per le operazioni consentite, valutando CORS, sessioni, CSRF e rate limiting.
2. Collaudare l'API con dati sintetici e un account di prova senza alterare l'applicazione originale.
3. Collegare un primo modulo del frontend GitHub, inizialmente in sola lettura, mediante l'API protetta.
4. Aggiungere eventuali operazioni di scrittura solo dopo aver verificato i permessi lato server e la coerenza dei dati.
5. Ripetere la procedura modulo per modulo, conservando sempre la versione Apps Script originale come riferimento.

## Stato della sincronizzazione
**Non attiva.** Nessuna doppia scrittura o sincronizzazione viene dichiarata finché non è configurata, verificata e collaudata l'API sicura.
