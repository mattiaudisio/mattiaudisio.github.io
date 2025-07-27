---
title: 'Come ho installato localmente invidious'
date: 2024-06-03T21:02:25+02:00
tags: ['👨‍💻 Echo 404', '👨‍💻 selfhosting', '👨‍💻 privacy']
ShowWordCount: false
hideAuthor: true
ShowPostNavLinks: false
description: "Un mondo alternativo di guardare YouTube"
layout: 'article'
ShowShareButtons: true
---

Piccolo articolo veloce per spiegare come installare localmente una propria istanza invidious, in modo da vedere i video dei tuoi youtuber preferiti senza essere tracciato da YouTube.

## Pacchetti richiesti

Invidious può essere installato sia tramite Docker che tramite Podman, ma in questo caso vedremo la seconda opzione.

Quindi, prima di cominciare, bisogna installare Podman sul nostro computer tramite questo comando:

```shell
 sudo dnf install podman-compose pwgen
```

Ora possiamo cominciare.

## Installare Invidious

In primis bisogna scaricare la Github il repository ufficiale di Invidious ed entrare dentro la directory appena creata

```shell
git clone https://github.com/iv-org/invidious.git
cd invidious
```


Il passo successivo consiste nell'editare il file _docker-compose.yml_ con queste modifiche:

**Aggiungi l'image di Invidious**:

    image: quay.io/invidious/invidious:latest

**Cambiare la Porta**:

     ports: - "3000:3000"

**Cambiare l'hmac_key**. È necessario impostare un valore casuale generato per il parametro hmac_key. Su Linux è possibile generarlo utilizzando il comando *pwgen 20 1*

    .Prima
    hmac_key: "CHANGE_ME!!"

    .Dopo
    hmac_key: saeNg5xufooraofeevee


A fine modifiche, il file docker_compose.yml deve assomigliare a questo qui sotto:

    # Warning: This docker-compose file is made for development purposes.
    # Using it will build an image from the locally cloned repository.
    #
    # If you want to use Invidious in production, see the docker-compose.yml file provided
    # in the installation documentation: https://docs.invidious.io/installation/

    # Warning: This docker-compose file is made for development purposes.
    # Using it will build an image from the locally cloned repository.
    #
    # If you want to use Invidious in production, see the docker-compose.yml file provided
    # in the installation documentation: https://docs.invidious.io/installation/

    version: "3"
    services:
    
     invidious:
     image: quay.io/invidious/invidious:latest
     build:
          context: .
         dockerfile: docker/Dockerfile
        restart: unless-stopped
        ports:
            - "3000:3000"
        environment:
        # Please read the following file for a comprehensive list of all available
        # configuration options and their associated syntax:
        # https://github.com/iv-org/invidious/blob/master/config/config.example.yml
        INVIDIOUS_CONFIG: |
            db:
                dbname: invidious
                user: kemal
                password: kemal
                host: invidious-db
                port: 5432
            check_tables: true
            # external_port:
            # domain:
            # https_only: false
            # statistics_enabled: false
            hmac_key: Ees6vou2IekaipeiCeib
        healthcheck:
            test: wget -nv --tries=1 --spider http://127.0.0.1:3000/api/v1/comments/jNQXAC9IVRw || exit 1
            interval: 30s
            timeout: 5s
            retries: 2
        depends_on:
         - invidious-db
  
        invidious-db:
            image: docker.io/library/postgres:13
            restart: unless-stopped
            volumes:
                - postgresdata:/var/lib/postgresql/data
                - ./config/sql:/config/sql
                - ./docker/init-invidious-db.sh:/docker-entrypoint-initdb.d/init-invidious-db.sh
            environment:
                POSTGRES_DB: invidious
                POSTGRES_USER: kemal
                POSTGRES_PASSWORD: kemal
            healthcheck:
                test: ["CMD-SHELL", "pg_isready -U $$POSTGRES_USER -d $$POSTGRES_DB"]

        volumes:
            postgresdata:

<br />

**Piccola nota a margine**: A causa di vari problemi, Invidious deve essere riavviato spesso, almeno una volta al giorno, idealmente ogni ora.

## Eseguire invidious

Per eseguire Invidious, basta entrare dentro la directory _invidious_ ed eseguire il comando _podman-compose up_ 

     cd invidious/
     podman-compose up

Per ottimizzare quest'operazione ho creato un piccolo script shell che mi permette di accendere, spegnere e aggiornare invidious

     #!/bin/bash

     clear
     # Mostra il primo menu
     echo "Scegli un'opzione:"
     echo "1. Accendi"
     echo "2. Spegni"
     echo "3. aggiorna"
     read -p "Inserisci il numero corrispondente: " scelta

     # Esegui l'azione in base alla scelta
     case $scelta in
         1)  cd invidious/ # Cambia la directory in "invidious/"
             podman-compose up # Esegui "podman-compose up"
             ;;
        
         2)
             cd invidious/
             podman-compose stop
             echo "Invidious spento!"
             ;;
         3)
             cd invidious/
             podman-compose pull
             podman-compose up -d
             podman image prune -f
             echo "Invidious aggiornato!"
             ;;
     esac