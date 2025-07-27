---
title: 'Usare Telegram come un lettore di Feed RSS'
date: 2024-01-31T19:04:26+02:00
tags: ['👨‍💻 Echo 404','👨‍💻 Telegram','👨‍💻 RSS']
ShowWordCount: false
hideAuthor: true
ShowPostNavLinks: false
description: "Tieniti sempre aggiornato grazie a Telegram e i feed RSS"
layout: 'article'
ShowShareButtons: true
---

I feed RSS sono quelle cose che, durante la mia “carriera/vita” su internet, gira girato tornano a fare capolinea ogni tanto.

Il primo ricordo che ho con questi strumenti risalgono al lontano 2019 quando tentai, fallendo miseramente, di creare un bot Telegram che, dato i feed RSS di un paio di fansub, mi mandava una notifica ogni volta che usciva una nuova puntata sottotitolata. In questi 6 anni sono stati utilizzati dal sottoscritto in molti progetti, partendo dai più semplici (un pagina in php che mi leggeva il Feed RSS di un giornale e mi mostrava gli ultimi 10 articoli) fino a robe più malsane (Ricreare una copia della sezione “Seguiti” del mio profilo Tik Tok tramite feed RSS).

## Fluent Reader

Ma è da solo un anno, all'incirca aprile 2023, che i feed RSS sono diventati parte della mia quotidianità. In quel periodo sono venuto a conoscenza di [Fluent Reader](https://github.com/yang991178/fluent-reader) che, nel giro di poche settimane, diventò il mio compagno di giornate, colui che mi teneva aggiornato sulle ultime notizie, degli ultimi dischi usciti e, per un periodo, mi teneva aggiornato anche sulle uscite dei canali YouTube.

Un programma fighissimo, non c'è niente da dire, ma, da persona fissata con l'essere minimalista su internet, il fatto di dover avere installato un applicazione apposta sul mio pc per fare una cosa non mi andava tanto a genio (sì lo so è una roba strana da gente non proprio a posto, ma che ci posso fare sono fatto così).

Per questo ogni tanto cercavo in giro se c'erano soluzioni che potevano interessarmi e spingermi ad abbandonare Fluent Reader, però non trovavo mai niente.... fino a questa settimana.

Per chi non è su LS o per chi non si è accorto, questo lunedì, sul [blog di Ed](https://log.livellosegreto.it/edmael/), è uscito [questo articolo](https://log.livellosegreto.it/edmael/feed-rss-torniamo-a-scegliere-i-nostri-contenuti), dove si parlava di feed RSS e di cosa ha deciso di utilizzare per averli sempre con se... ed è lì che ho trovato la risposta ai miei quesiti.

## Telegram

“[RSS to Telegram Bot](https://github.com/Rongronggg9/RSS-to-Telegram-Bot)” è un bot di Telegram che fa praticamente quello che ho detto fino ad adesso, ovvero leggere i feed RSS e mandarti un messaggio quando esce un nuovo articolo. Finalmente la svolta che volevo trovare.

Mi sono messo sotto e, leggendo un attimo in giro, sono riuscito a realizzare quello che sto usando adesso: _un intera cartella chat con all'interno tutti i feed RSS che avevo suddivisi per argomento/categoria._

Ma come ho fatto?

## Istruzioni guidate

Per realizzare quello che per ora è il mio lettore di Feed RSS su Telegram, ho fatto queste poche azioni che posso riassumere in 3 passaggi:

1. Ho creato un canale Telegram privato per ogni categoria che mi interessa _**(Politica, Musica, Tecnologia, Blog, Notifiche dei video PeerTube, Intrattenimento)**_ ed ho aggiunto “RSS to Telegram Bot” come moderatore in tutti i canali

2. Sono tornato sul bot è ho composto il seguente messaggio: _/sub @ID-Canale linkFeedRSS1 linkFeedRSS2 linkFeedRSS3_ in modo da collegare quei determinati feed a quel determinato canale. Per trovare l'ID del canale privato bisogna andare sulla versione web di Telegram, cliccare sul canale e, dalla barra di ricerca, prendere il numero finale che inizia con **-100** _(es. -10010000000000)_

3. Ho creato una cartella, chiamata “My Feed”, dove all'interno ho messo tutti i canali e il bot. Se non sai creare delle cartelle su Telegram clicca [qua](https://telegram.org/tour/chat-folders/it)

E questo è tutto.

Per concludere, voglio ringrazie <a href="https://livellosegreto.it/@ed">Ed</a> per avermi ispirato in questo progetto.<br />
Un saluto a tutti
