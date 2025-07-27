---
title: "Implementare le API di Google Calendar sul tuo sito Laravel"
date: 2025-04-18T22:53:54+02:00
tags: ['👨‍💻 Echo 404','👨‍💻 Laravel','👨‍💻 Web development']
ShowWordCount: false
hideAuthor: true
ShowPostNavLinks: false
description: "Piccolo tutorial fatto per evitare altre novantamila bestemmie"
layout: 'article'
ShowShareButtons: true
---

Stai creando un sito web con Laravel? Hai intenzione di implementare le API di Google Calendar perchè ti servono da qualche parte? Stai facendo fatica a capire come fare? 

Tranquillo, anch'io ci ho messo un momento a trovare qualcosa di utile. Ho fatto anch'io fatica a ricavare le informazioni utili a quello che mi servivano e, dato che so quanto ho sclerato per trovare queste informazioni, ho fatto che creare questa piccola guida, in modo da darti (o ridarmi) una mano.

Cominciamo!

## Impostare il servizio Google

Accedere con l’account Google che ci serve su https://console.cloud.google.com/ e cliccare sul bottone “Seleziona un progetto” (presente in alto a sinistra vicino al logo Google Cloud).

Se non ci sono progetti e dobbiamo crearne uno, facciamo clic in alto su _Nuovo progetto_->_Dai un nome_ al tuo progetto (località possiamo anche lasciarla vuota)->clicca sul pulsante Crea.

Subito dopo la creazione, se non siamo stati indirizzati sulla pagina di benvenuto, accedere al progetto dal menù a tendina.

Fare clic sul pulsante “_IAM & Admin_”, selezionandolo dal menu di navigazione a sinistra. Appena entrati, cliccare dal menu di navigazione a sinistra la sezione Service account, che al momento troviamo vuota. Cliccare il pulsante Crea service account e diamo un nome e una descrizione al nostro service account. 

**PRENDIAMO NOTA DELL'INDIRIZZO EMAIL** (lorem-ipsum@ababababa-1112222.iam.gserviceaccount.com) che ci servirà più avanti. Clicca su “_Crea e continua_” e salta pure i prossimi due passaggi, sono opzionali.

Appena tornati alla pagina di prima, dove vediamo il nuovo service account creato, fare clic su _Azioni_ e accedere alla sezione _Gestisci chiavi_, trovandosi poi su una pagina con un elenco vuoto di chiavi.  Fare clic su _Aggiungi Chiave_->_Crea nuova chiave_.

Assicurarsi che “_JSON_” sia selezionato e scegliere “_Crea_”. Il tuo browser scaricherà automaticamente un file contenente la tua chiave privata. **QUESTA È LA TUA CHIAVE PRIVATA, DEVE ESSERE ACCESSIBILE MA NON DEVE ESSERE PUBBLICO A CHIUNQUE**.

Dopo aver scaricato il file, ritornare alla pagina principale (https://console.cloud.google.com/) e, dal menù a sinistra, fare clic su _API e servizi_ e, una volta dentro, cliccare su Abilita API e servizi. Si aprirà una pagina, che contiene le librerie API di Google, dove bisogna cercare **Google Calendar API**, fai clic e, una volta dentro, clicca su abilita, per venire poi indirizzato alla voce per l'API del calendario dalla pagina "_API e servizi abilitata_", mostrando le statistiche per tale API.

## Impostare il sito per utilizzare le API

Scaricare tra i pacchetti del sito, tramite composer, i pacchetti PHP di Google API:

```php
composer require google/apiclient:^2.15.0
```

Dopo aver fatto, cominciamo a scaricare il pacchetto di Spatie:

```php
composer require spatie/laravel-google-calendar
php artisan vendor:publish --provider="Spatie\GoogleCalendar\GoogleCalendarServiceProvider"
```

Questo creerà  un file chiamato google-calendar.php

Prendiamo il file JSON che abbiamo scaricato prima e carichiamolo su _app/google-calendar/_ e inseriamo il nuovo percorso in _credentials_json_.

## Consentire all'account di servizio di accedere al calendario

Prima di poter accedere al calendario dal sito, devi condividerlo con il tuo account di servizio.

Andiamo su [Calendar](https://calendar.google.com/) e creiamo un nuovo calendario (consiglio di crearne uno nuovo perché con quello di default ho avuto dei problemi).

Entriamo nelle impostazioni del nuovo calendario e andiamo in fondo, alla sezione _Condivisione con_, e aggiungiamo una nuova persona, ovvero la mail che è stata creata durante la creazione del Service account, dandogli tutti i permessi necessari.

Scorriamo verso il basso, nella sezione Integra calendario, e copiamo l’ID del calendario (una cosa simile a _64254d8f5gf8f5gf6d4f8s@group.calendar.google.com_).

E questo è tutto. Ora, a meno di problemi specifichi legati ai pacchetti, dovrebbe essere tutto a posto.

Per il rispetto delle fonti, lascio qua sotto i link che mi sono serviti di più.

## link

- [Link all'articolo del programmatore di Spatie](https://dev.to/dnsinyukov/how-to-integrate-google-calendar-api-and-friendship-with-laravel-4cok)
- [Un tutorial che poteva tornarmi utile ma alla fine no, però è un buon tutorial](https://learninglaravel.net/learn-how-to-integrate-google-calendar-with-laravel)
- [L'articolo che alla fine mi ha svoltato la ricerca](https://naich.net/wordpress/index.php/using-the-google-calendar-api-from-your-web-site-with-php/)
- [Serie YouTube che mi ha incuriosito e a qualcuno può tornare utile](https://www.youtube.com/watch?v=uLzU47bEa2U&list=PLdA9EoV1lTrKD7515tYSOxZPV9FiBBxW_&index=5)

