---
title: "Come realizzare un sito web da vero soydevs"
date: 2024-09-18T17:08:17+02:00
tags: ['👨‍💻 Echo 404','👨‍💻 Web development','👨‍💻 Node.JS']
ShowWordCount: false
hideAuthor: true
ShowPostNavLinks: false
description: "Corri a prendere il tuo caffè Starbucks, è ora di scrivere qualche riga in Javascript"
layout: 'article'
ShowShareButtons: true
---

Ciao bambino! Come dici?? Ti piace La Silicon Valley? I Cofee Shop? Vuoi essere un programmatore e lavorare con il macbook che è costato 3 stipendi di tuo padre ma non sai come come fare dato che conosci solo HTML e Javascript? 

Nessun problema bambino! Diventa un [soydev](https://www.urbandictionary.com/define.php?term=Soydev)! Scaricati Visual Studio Code e Node.js e preparati a Sviluppare i migliori siti web di tutta internet! Come? non sai come utilizzare questi strumenti? Nessun problema, [eccoti una guida per poter creare un sito web con Node.jS e EJS](https://www.digitalocean.com/community/tutorials/how-to-use-ejs-to-template-your-node-application)  oppure, se sei pigro e non hai voglia di leggere un articolo in inglese, eccoti qua sotto una versione tradotta. Preparati a diventare il nuovo Bill Gates.

![](../../posts/soydev.jpg)

##  Come creare un sito web con Node.JS e EJS

Quando si crea un sito web non bisogna ogni volta mettersi lì e ricreare ogni volta la ruota per arrivare sempre allo stesso risultato, per questo sono stati creati i template, per permetterci di risparmiare tempo e completare il nostro sito web il più velocemente possibile. 

Quando si creano applicazioni Node, una via veloce è usare appunto dei template nel momento necessario. In questo caso, gli [Embedded JavaScript templates (EJS)](https://ejs.co/) possono essere dei template più che validi. Cominciamo!

Innanzitutto, apri la finestra del terminale e crea una nuova directory di progetto:

```shell
mkdir ejs-demo
```

Quindi, entriamo dentro la cartella appena creata e inizializziamo un nuovo progetto npm:

```shell
npm init -y
```

Successivamente, dovrai installare Il pacchetto `express`:

```shell
npm install express@4.17.1
```

Quindi installare il pacchetto `ejs`:

```shell
npm install ejs@3.1.6
```

A questo punto, sei pronto ad usare Express e EJS.

###  Fase 1 — Configurazione con `server.js`

Cominciamo creando un file server.js, dove mettere all'interno queste righe di codice:

```js
var express = require('express');
var app = express();

// set the view engine to ejs
app.set('view engine', 'ejs');

// use res.render to load up an ejs view file

// index page
app.get('/', function(req, res) {
  res.render('pages/index');
});

// about page
app.get('/about', function(req, res) {
  res.render('pages/about');
});

app.listen(8080);
console.log('Server is listening on port 8080');
```

Questo codice definisce l'applicazione ed è raggiungibile sulla porta `8080`

Per impostare anche EJS come motore di visualizzazione per l'applicazione Express utilizziamo `app.set('view engine', 'ejs');`

Nota come il codice invia una visualizzazione all'utente utilizzando `res.render()`- Si'. È importante notare che `res.render()`Si guarderà in un `views`La cartella per la vista. Quindi devi solo definire `pages/index`Dal momento che il percorso completo è `views/pages/index`

### Fase 2 - Creazione dei partials EJS

Come molte delle applicazioni che costruisci, ci sarà un sacco di codice che viene riutilizzato. Questi sono considerati _partials_.  Creiamo quelli che serviranno a noi.

Cominciamo col creare una cartella `views` e la sua subdirectory `partials`:

```shell
mkdir views
mkdir views/partials
```

All'interno di partials, creiamo un file `head.ejs` dove aggiungiamo:

```html
<meta charset="UTF-8">
<title>EJS Is Fun</title>

<!-- CSS (load bootstrap from a CDN) -->
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/twitter-bootstrap/4.5.2/css/bootstrap.min.css">
<style>
  body { padding-top:50px; }
</style>
```

Questo codice contiene i metadati per `head`Per un documento HTML. Include anche gli stili [Bootstrap](https://getbootstrap.com/).

Ora, creiamo il file `header.ejs`, che contiene la navigazione per un documento HTML e utilizza diverse classi di Bootstrap per lo styling:

```html
<nav class="navbar navbar-expand-lg navbar-light bg-light">
  <a class="navbar-brand" href="/">EJS Is Fun</a>
  <ul class="navbar-nav mr-auto">
    <li class="nav-item">
      <a class="nav-link" href="/">Home</a>
    </li>
    <li class="nav-item">
      <a class="nav-link" href="/about">About</a>
    </li>
  </ul>
</nav>
```

Infine, creiamo il file `footer.ejs`, che contiene informazioni sul copyright e utilizza diverse classi di Bootstrap per lo styling.

```html
<p class="text-center text-muted">&copy; Copyright 2020 The Awesome People</p>
```
### Passaggio 3 - Aggiunta dei Partials EJS al View

Ora è arrivato il momento di includere, tramite il comando `include`, le tre partials che abbiamo creato prima. Per incorporare un partials EJS in un altro file uso 
`<%-include(=='RELATIVE/PATH/TO/FILE'==) %>` .

Quindi, creiamo una subdirectory `pages`:

```shell
mkdir views/pages
```

In questa directory, creare una nuovo file `index.ejs`:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <%- include('../partials/head'); %>
</head>
<body class="container">

<header>
  <%- include('../partials/header'); %>
</header>

<main>
  <div class="jumbotron">
    <h1>This is great</h1>
    <p>Welcome to templating using EJS</p>
  </div>
</main>

<footer>
  <%- include('../partials/footer'); %>
</footer>

</body>
</html>
```

Salviamo le modifiche e vediamo come stiamo andando. Fai partire l'applicazione tramite `node server.js` e visita il link `http://localhost:8080/`

![](../../posts/EJS01.png)

Ora, invece, creiamo il file `about.ejs`, aggiunge una barra laterale di Bootstrap, giusto per differenziarlo dall'altro:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <%- include('../partials/head'); %>
</head>
<body class="container">

<header>
  <%- include('../partials/header'); %>
</header>

<main>
<div class="row">
  <div class="col-sm-8">
    <div class="jumbotron">
      <h1>This is great</h1>
      <p>Welcome to templating using EJS</p>
    </div>
  </div>

  <div class="col-sm-4">
    <div class="well">
      <h3>Look I'm A Sidebar!</h3>
    </div>
  </div>
</div>
</main>

<footer>
  <%- include('../partials/footer'); %>
</footer>

</body>
</html>
```

E, dopo aver fatto ripartire l'applicazione, visitiamo `http://localhost:8080/about`

![](../../posts/EJS2.png)

Ora puoi iniziare a utilizzare EJS per passare i dati dall'applicazione Node alle views.
### Passo 4 - Passare dati

Definiamo alcune variabili di base e un elenco da passare alla pagina index. 

modifichiamo un attimo `server.js`  aggiungendo altro codice. All'interno di `app.get('/')` definiamo un array chiamato `mascots` e una stringa chiamata `tagline`:

```js
var express = require('express');
var app = express();

// set the view engine to ejs
app.set('view engine', 'ejs');

// use res.render to load up an ejs view file

// index page
app.get('/', function(req, res) {
  var mascots = [
    { name: 'Sammy', organization: "DigitalOcean", birth_year: 2012},
    { name: 'Tux', organization: "Linux", birth_year: 1996},
    { name: 'Moby Dock', organization: "Docker", birth_year: 2013}
  ];
  var tagline = "No programming concept is complete without a cute animal mascot.";

  res.render('pages/index', {
    mascots: mascots,
    tagline: tagline
  });
});

// about page
app.get('/about', function(req, res) {
  res.render('pages/about');
});

app.listen(8080);
console.log('Server is listening on port 8080');
```

_**Rendering una singola variabile in EJS**_

Per trasferire  una singola variabile, è possibile utilizzare `<%= tagline %>`.

All'interno di `index.ejs`, aggiungiamo queste due righe dentro al `<main>`, in modo da visualizzare il valore `tagline`nell'index: 

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <%- include('../partials/head'); %>
</head>
<body class="container">

<header>
  <%- include('../partials/header'); %>
</header>

<main>
  <div class="jumbotron">
    <h1>This is great</h1>
    <p>Welcome to templating using EJS</p>

    <h2>Variable</h2>
    <p><%= tagline %></p>
  </div>
</main>

<footer>
  <%- include('../partials/footer'); %>
</footer>

</body>
</html>
```

_**Loop dei dati**_

Per loop sui dati, è possibile utilizzare `.forEach`:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <%- include('../partials/head'); %>
</head>
<body class="container">

<header>
  <%- include('../partials/header'); %>
</header>

<main>
  <div class="jumbotron">
    <h1>This is great</h1>
    <p>Welcome to templating using EJS</p>

    <h2>Variable</h2>
    <p><%= tagline %></p>

    <ul>
      <% mascots.forEach(function(mascot) { %>
        <li>
          <strong><%= mascot.name %></strong>
          representing <%= mascot.organization %>,
          born <%= mascot.birth_year %>
        </li>
      <% }); %>
    </ul>
  </div>
</main>

<footer>
  <%- include('../partials/footer'); %>
</footer>

</body>
</html>
```

Vediamo come sta uscendo:

![](../../posts/EJS3.png)

_**Trasferire i dati ad un partials**_

È possibile definire e passare variabili a un partials EJS usando una sintassi come questa:

```html
(views/pages/about.ejs)

...
<header>
  <%- include('../partials/header', {variant: 'compact'}); %>
</header>
...
```

Ma devi ancora fare attenzione ad presumere che sia stata definita una variabile.

Se si desidera fare riferimento a una variabile in una parziale che potrebbe non essere sempre definita, e darle un valore predefinito, è possibile farlo in questo modo:

```html
views/partials/header.ejs

...
<em>Variant: <%= typeof variant != 'undefined' ? variant : 'default' %></em>
...
```

Nella riga precedente, il codice EJS sta rendendo il valore di `variant`Se è definito, altrimenti lo lascia `default`.


## I LINK !!1!!

- [How To Use EJS to Template Your Node Application](https://www.digitalocean.com/community/tutorials/how-to-use-ejs-to-template-your-node-application)
- [Costruire un sito web senza diventare un “soydev”](https://worldofmatthew.com/post/soydev/)
- [Che cosa è Soydev? E perché lo odio](https://storopoli.com/blog/2023-11-10-soydev/)
