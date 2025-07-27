---
title: "Come ho customizzato Linux Mint Cinnamon"
date: 2024-10-07T21:01:57+02:00
tags: ['👨‍💻 Echo 404','👨‍💻 Linux']
ShowWordCount: false
hideAuthor: true
ShowPostNavLinks: false
description: "UX porn"
layout: 'article'
ShowShareButtons: true
---

Oggi, dopo 4 mesi che ho installato Linux Mint sul mio portatile principale, ho trovato il tempo per mettermi seduto e personalizzarlo a dovere. Questo che state leggendo è una guida veloce di quello che ho fatto, in modo che se vi piace potete configurarlo anche voi (e anche per darmi una mano se in futuro cambio di nuovo distro perdendo le modifiche fatte...) 
## Cosa serve?
- **Icone**: [Tela](https://www.gnome-look.org/p/1279924/)
- **Tema per Plank Dock**: [Gtk Theme - Whitesur Gtk Theme Light/Dark](https://github.com/vinceliuice/WhiteSur-gtk-theme)
- **Tema**: [Orchis Theme](https://github.com/vinceliuice/Orchis-theme)

## Installare il tema 

**Partiamo da un punto:** *come installare Orchis*

Scarica il [repostiory Github](https://github.com/vinceliuice/Orchis-theme), entra nella directory scaricata ed esegui il file `install.sh`. Se vuoi inserire qualcosa di particolare [basta che copi i tweaks nel README](https://github.com/vinceliuice/Orchis-theme?tab=readme-ov-file#tweaks-for-orchis). nel mio caso:

`/install.sh -t green --tweaks black --tweaks macos`

Dopo aver scaricato [Tela](https://www.gnome-look.org/p/1279924/) e [Orchis](https://github.com/vinceliuice/Orchis-theme), sposta la cartella scaricata in `.icons`, poi apri il programma *Temi* e modifica *Icone* con le icone di Tela e *Applicazioni* e *Desktop* con le icone di Orchis.

Se vuoi modificare il layout dei bottoni, vai su *Impostazioni di sistema > Finestre > Pulsanti* e modificali a piacere *(nel mio caso Mac Classico)* .

Se vuoi cambiare l'anteprima di Alt-Tab basta che dalla finestra *Finestre* clicchi su Alt-Tab. *(Io ho messo Icone e anteprime delle finestre)*.
## Personalizzare il pannello

Il pannello è molto semplice da personalizzare: *Tasto destro sul pannello > sposta > spostalo sopra*. 

Poi, cliccando su modifica pannello:
 - rimuovi il gruppo delle icone dei programmi
 - sposta l'orologio da destra al centro
 - Tramite *applets* installae aggiungi **Cinnamenu**, dopo spostalo al posto del menù
	 - Se vuoi impostare un logo diverso ti basta fare *tasto destro > Configura > aspetto*

## Installare e configurare Plank Dock

Cominciamo subito con l'istallazione di Plank Dock, ovvero `sudo apt install plank`. 

Dopo aver scaricato sul pc il [tema GTK](https://github.com/vinceliuice/WhiteSur-gtk-theme) , andiamo dentro `WhiteSur-gtk-theme/src/other/plank`, copiamo le cartelle **theme-dark** e **theme-light** e incolliamo all'interno di `.local/share/plank/themes`.

Aprendo _Plank Dock_ dall'elenco dei programmi, apparirà la dock. Cliccate tasto destro sulla dock e successivamente su _Preferences_. 

![](../../posts/customlinuxmint_01.png)

Cliccando sul menù a tendina di *Tema*, selezionate *theme-dark* o *theme-light*

## Riferimenti
- [Post Reddit](https://www.reddit.com/r/unixporn/comments/ehlads/muttercinnamon_less_is_more_linux_mint_cinnamon/)
- [How to Customize Your Cinnamon Desktop Look Like MacOS Big Sur](https://invidious.nerdvpn.de/watch?v=DMs7DX3Um9E)
- [Customizing Cinnamon on Mint | Easy Guide](https://invidious.nerdvpn.de/watch?v=wZmNMIq82U0)
