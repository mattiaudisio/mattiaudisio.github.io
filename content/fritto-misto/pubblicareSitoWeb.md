---
title: 'Come pubblicare gratuitamente un sito web (statico o dinamico)'
date: 2023-01-19T21:26:12+02:00
tags: ['👨‍💻 Echo 404', '👨‍💻 Web development']
ShowWordCount: false
hideAuthor: true
ShowPostNavLinks: false
description: "Fatto il sito? È il momento di andare online!"
layout: 'article'
ShowShareButtons: true
---

Stai realizzando il tuo sito web, l'hai praticamente completato e non vedi l'ora di pubblicarlo ma, purtroppo, non hai i soldi per prenderti per prendere un servizio di hosting dove caricarlo?

Tranquillo, so cosa vuol dire (anzi tutt'ora vivo sta situazione) e so che quando sei in questo stato ti metti a cercare qualsiasi sito disponibile e rischi di capitare sui peggio servizi. Ma tranquillo, è ora di risolvere questo problema, e come aiutante avrai me, il classico mr. nessuno di provincia che, dopo una serie di fregature una dietro l'altro, a trovato 2 metodi affidabili che ti aiutano a diminuire i costi per un hosting ed avere lo stesso il tuo sito online e pronto per essere visitato.

Partiamo da una piccola premessa.. Cosa intendo con **gratuitamente**?

Di norma, per avere online un sito web, bisogna avere due importanti strumenti: un hosting ed un dominio _(che ovviamente è un servizio **solo** a pagamento)_.

## Pubblicare un sito statico

Partiamo dai siti che a livello tecnico sono i più facili, ovvero i siti statici, semplici siti fatti in HTML,CSS e JavaScript.

Per i siti statici il consiglio che posso dare è affidarti a servizi come GitHub ci permette di ovviare al costo di un hosting per il nostro sito dandoci la possibilità di mettere online gratuitamente il nostro sito _(rigorosamente statico)_ direttamente dal nostro repository.

Se si hanno dei repository pubblici su Github, che al loro interno contengono dei siti web, si ha la possibilità di creare delle GitHub Pages, un servizio che consente di pubblicare un sito Web o un'applicazione Web in modo gratuito.

Questi siti in particolare hanno l'url composto da nomeUtente.github.io ed il nome del repository in cui c'è il codice di norma viene aggiunto dopo.

In poche parole un hosting su Github.

Ora, è possibile tra le altre cose aggiungere degli url personalizzati e, per farlo, basta andare nella seziona Pages del repository, andare fino alla parte del Custom Domain e aggiungere l'url che si vuole collegare (es. ilmiosito.it)

**P.S.**

_Poi bisogna attivare anche l'Enforce HTTPS per avere HTTPS abilitato_

Subito dopo, andando sul sito che dove hai comprato il tuo dominio, bisogna modificare il DNS creando questi record:

**A**

```html
 185.199.108.153
 185.199.109.153
 185.199.110.153
 185.199.111.153

```

**AAA**

```html
 2606:50c0:8000::153
 2606:50c0:8001::153
 2606:50c0:8002::153
 2606:50c0:8003::153

```

È ora il tuo sito è **online**!

## Pubblicare un sito dinamico

Volendo fare i professori si può copiare una qualsiasi parte di testo che trovi online dove si dice _“i siti dinamici hanno pagine web il cui contenuto viene generato in tempo reale e che ciò è reso possibile grazie all'utilizzo di un linguaggio di scripting come ad esempio il PHP, e a MySQL, un database per la memorizzazione di dati”_ però deduco che se sei in sto pezzo del post da benissimo cosa è e da cosa è formato un sito dinamico.

Se sai com'è fatto un sito dinamico, sai benissimo che (nella maggior parte dei casi) per funzionare ha bisogno di un database, altrimenti si perde proprio l'essenza di un sito dinamico.

Quindi abbiamo bisogno di un servizio che ci dia la possibilità di avere una database su cui appoggiarci.

**Piccola premessa prima di continuare**

Il sito che ti sto per descrivere ora te lo sto dicendo per un semplice motivo, perché è un servizio che ho provato personalmente su dei miei progetti, quindi posso darti la conferma sul suo funzionamento, ma non posso dirti niente riguardo il tema privacy e trattamento dei dati.

Se sei una persona interessata a questi temi, ti consiglio di prendere con le pinze quello che sto per scrivere, perché può essere che non ti troverai d'accordo.

Il sito che più mi sento di consigliarti è [Altervista](https://it.altervista.org/) (sì il famoso altervista.org che ti capita di vedere se nella tua vita girovagavi per fansub). Per quanto lo si può deridere, bisogna dire che è un servizio molto utile che ti offre non solo la possibilità di caricare direttamente il tuo sito (sì che anche l'opzione Hosting con file manager, non solo l'hosting con sopra Wordpress) e ti offre un posto in cui appoggiare il tuo database MYSQL.
Per creare un sito con altervista basta seguire questi semplici passaggi:

1. Andare su [questa pagina](https://it.altervista.org/crea-sito-gratis.php)
2. Cliccare sul “Crea sito” presente nella zona “Hosting con file manager”
3. Scrivi il nome che vuoi dare al tuo sito e poi clicca su prosegui
4. Crea un account
5. tempo un paio di giorni, ti arriverà una mail con il link per creare il sito

Appena creato, verrai reindirizzato nella bacheca principale dove, per caricare i file che formano il tuo sito, ti basterà andare su Gestione File (sotto il titolo Applicazioni) mentre, per aggiungere il database, basta andare sotto nella sezione Risorse e cliccare su “accedi a phpmyadmin” dove, se sei già abituato ad usare XAMPP, ti troverai subito a casa.

Fatto questo, potrai dire che il tuo sito è finalmente online ma, se vuoi avere un dominio personalizzato, dovrai comprare il dominio prima, ovvero durante la creazione dell'account.

## Non me ne frega niente del dominio personalizzato, come posso fare?

Se non te ne frega niente di avere un dominio personalizzato ma vuoi mettere online lo stesso il tuo sito tranquillo, so cosa consigliarti (togliendo i siti dinamici, che ti ho spiegato nel capitolo prima).

Se vuoi pubblicare un sito statico ti servirà primo su tutti un profilo o su GitHub o su GitLab, dove poter creare un repository dove mettere il tuo sito, poi ti do la scelta tra 2 piattaforme di hosting per applicazioni web e siti statici: [Netlify](https://www.netlify.com/) e [Vercel](https://vercel.com/).
tutti e due si basano sui seguenti passagi:

1. cliccare su “create website/new project”
2. cliccare deploy su github o gitlab
3. selezionare il repository dove c'è il sito
4. cliccare su deploy-site
 

Ed il gioco è fatto, il nostro sito web è **online**!