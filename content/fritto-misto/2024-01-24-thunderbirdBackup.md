---
title: 'Usare Thunderbird come backup per le mail di Gmail'
date: 2024-01-24T21:50:21+02:00
tags: ['👨‍💻 Echo 404', '👨‍💻 privacy']
ShowWordCount: false
hideAuthor: true
ShowPostNavLinks: false
description: "Un modo veloce e open source di libeare spazio sulla tua mail Google"
layout: 'article'
ShowShareButtons: true
---

In questi anni ho notato una tendenza che trovo particolare. Nel mondo del lavoro, molte persone, in particolare nelle piccole imprese, tendono ad usare utilizzare la propria mail personale.

Ora, lasciando da parte il dibattuto se questa scelta sia un ottima scelta _(non è un ottima scelta)_ oppure no _(cof. cof. **è una scelta di merda** cof. cof.)_, parliamo di un avvenimento capitato vicino a me ma che può essere d'aiuto a qualcuno... **il tuo account gmail ti segna 15GB su 15 GB utilizzati** (sì lo so può sembrare strano a qualcuno ma vi giuro che ho visto quella scritta con i miei occhi).

In questi casi però il caro e vecchio “cancella tutte le mail” non può venirci in aiuto, dato che la suddetta mail viene usata per un lavoro in cui servono documenti e queste mail sono piene di documenti che servono. La soluzione che ti consiglio: fare un backup in locale.


## Gmail

Cominciamo dalla parte più facile, Gmail. Mettiamo l'esempio che ti vuoi scaricare le mail di un determinato anno (ad esempio tutte le mail del 2022), come fare?

Semplice. Selezioni tutte le mail ricevute nel 2022, clicchi su **“etichette”** _(Il simbolo che sembra una casa rovesciata in orizzontale)_, vai su **Crea Nuova**, la chiami 2022 e clicchi **Crea**.

Ora, per scaricarla, basta andare sulla pagina di [Google Takeout](https://takeout.google.com/settings/takeout), Deselezionare tutto, andare alla voce **Posta**, cliccare su _“Tutti i dati della posta inclusi”_, togliere il flag a “Includi tutti i messaggi nella Posta” e deselezionare tutto. Successivamente basta solo flaggare la voce 2022, premere ok, andare il fondo alla pagina dove c'è il button “Passaggio successivo”, selezionare la grandezza dello zip e aspettare che Google mandi la mail con il link per scaricare questo zip.

## Thunderbird

Come dice il [sito](https://www.thunderbird.net/it/), _Thunderbird è un'applicazione libera e gratuita per la gestione della posta elettronica_, ma molto probabilmente se sei qua a leggere questa pagina sai già cos'è.... allora andiamo subito al punto.

Per aggiungere i file mbox a Thunderbird ci servirà un estensione, ImportExportTools NG, e per scaricarla ci basterà andare su Impostazioni _(La trovi in basso a sinistra)_, Componenti aggiuntivi _(Lo trovi in basso a sinistra)_, cercare [ImportExportTools NG](https://addons.thunderbird.net/it/thunderbird/addon/importexporttools-ng/) e aggiungerlo a Thunderbird.

Dopo averlo scaricato, basterà cliccare su **Cartelle locali** (Che trovi sotto le mail), anda re su ImportExportTools NG e, all'interno del menù a tendina che si apre, selezionare **importa file mbox**, dove potrete selezionare il vostro file MBOX.

Fatto questo bisognerà aspettare Thunderbird che scarichi e sincronizzi il tutto (ci vorranno un paio di minuti) e voilà, ecco un bel backup in locale di tutte le vostre mail!


## Update (14 maggio 2025)

Dopo più di un anno rimetto mano a questo articolo per aggiungere una funzione che può tornare utile.

Per chi come me ha Proton Mail gratutito sa che non è possibile collegarlo a thunderbird (o almeno... sì ma con dei giri strani, che ho provato a fare, ma che alla fine mi obbligavano sempre a fare l'upgrade del profilo), ma finalmente ho trovato due soluzioni, facili e veloci, utilizzando gli EML. Questi due metodi richiedono solo una premessa: bisogna scaricarsi gli EML a mano (Da Proton, vai sulla mail desiderata, _clicca sui 3 puntini_, clicca su _Esporta_). È un processo lungo, ma è doveroso per quello che segue.

**Metodo 1: Script da Terminale**

Se utilizzi Linux o macOS, puoi usare un semplice script da terminale per unire i file EML in un file MBOX:

```shell
for e in *.eml
do
  date +"From - %a %b %d %H:%M:%S %Y" >> file.mbox
  cat "$e" >> file.mbox
  echo >> file.mbox
done
```

Assicurati che nella directory non esista già un file chiamato `file.mbox` prima di eseguire lo script. Questo comando aggiunge ogni file EML al file MBOX, separandoli correttamente.

**Metodo 2: direttamente da Thunderbird**

Vai su thunderbird e crea una nuova cartella, seleziona _ImportExportTools NG_ > _Importa file EML_ e scegli i file da importare.

Dopo aver importato i messaggi, fai clic destro sulla cartella, seleziona _ImportExportTools NG_ > _Esporta cartella_ e salva il file MBOX.