---
title: 'Ho ottimizzato (un minimo) un vecchio fisso su Windows'
date: 2025-07-26T12:00:32+02:00
tags: ['👨‍💻 Echo 404']
ShowWordCount: false
hideAuthor: true
ShowPostNavLinks: false
description: "a.k.a come ottimizzare i pc fissi che ci sono negli uffici"
layout: 'article'
ShowShareButtons: true
---

Da quando ho cominciato a lavorare (a parte un breve stage dove avevo Ubuntu) ho sempre lavorato su Windows, in particolare Windows 10 (da quando lavoro in ambito tech) e Windows 7 (quando facevo tutt'altro).

Però, quello che mi ha sempre fatto cristonare, non è il lavorare con Windows (per quanto mi faccia schifo), ma il fatto di dover lavorare su pc fissi dell'ante guerra che non reggono più gli ultimi aggiornamenti. Come possono confermare _(credo)_ buona parte della gente che lavora in ufficio, buona parte dei pc fissi che ci sono nei posti di lavoro hanno già qualche anno sulle spalle e una dimensione disco molto misera.

Ricordo che tempo fa dovevo lavorare sun un fisso vecchissimo con ancora Windows 7 che almeno 2/3 volte a settimana mi dava spazio insufficente e lo slero era sempre dietro l'angolo.

Poi, un giorno, capito su [questo canale](https://www.youtube.com/@nFire/videos) (chiedo venia ma non ricordo ma non riesco a trovare il video in particolare) dove mostra le directory su Windows dove ci sono i file temporanei. 

Tempo di finire il video, mi metto lì e provo a fare un attimo uno script bash che fa le stesse operazioni. 

Ora è da un pò che lo uso (mi sembra quasi 2 anni, ma la mia memoria è così bruciata che non ricordo bene il spazio temporale) su tutti i pc su cui ho lavorato e, devo ammettere, mi ha sempre aiutato a velocizzare Windows

```shell
    @Echo off
    Del/Q "C:\Users\%USERNAME%\AppData\Local\Temp"
    Del/Q "C:\Windows\Temp"
```