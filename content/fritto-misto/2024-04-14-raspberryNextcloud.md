---
title: 'Come ho installato Nextcloud su un Raspberry Pi 3'
date: 2024-04-14T19:32:17+02:00
tags: ['👨‍💻 Echo 404', '👨‍💻 selfhosting', '👨‍💻 privacy']
ShowWordCount: false
hideAuthor: true
ShowPostNavLinks: false
description: "Crea il tuo Drive personale tramite un Raspberry Pi"
layout: 'article'
ShowShareButtons: true
---

Qualche tempo fa ho perso un paio di neuroni dietro ad uno sfizio che mi avevo lì da un pò di tempo: Installare Nextcloud sopra il Raspberry Pi 3 che ho in casa.

Una roba semplicissima mi direte, peccato che ho avuto a che fare con un paio di problemi che mi hanno dato abbastanza da pelare e questo articolo serve proprio per questi problemi.

Tutto quello che c'è scritto qua dentro è una specie di cronologia che mi permetterà in futuro di rifare la stessa operazione senza avere ulteriori problemi (spero).

## Installare Nextcloud

Prima di installare NextCloud, è necessario disporre di alcuni prerequisiti sul sistema. NextCloud ha bisogno di un server web con Apache, MySQL (MariaDB) e PHP, in particolare di alcuni moduli PHP.

```shell
 sudo apt install apache2 mariadb-server libapache2-mod-php
 sudo apt install php-gd php-json php-mysql php-curl php-mbstring php-intl php-imagick php-xml php-zip
```

Attendi qualche minuto per il completamento dell'installazione e riavviare Apache per caricare i nuovi moduli PHP:

``` shell
 sudo service apache2 restart

```

Per installare Nextcloud bisogna andare nelle cartelle di Apache web e installare l'ultima releas di Nextcloud

```shell
 cd /var/www/html
 sudo wget https://download.nextcloud.com/server/releases/latest.zip
 sudo unzip latest.zip

```

Se ti da dei problemi ad estrarre i file devi modificare i permessi della cartella per consentire ad Apache di accedervi

```shell
 sudo chmod 750 nextcloud -R
 sudo chown www-data:www-data nextcloud -R
```

NextCloud è quasi pronto per essere utilizzato, ma dobbiamo prima creare un database MySQL per memorizzare i suoi dati.

## Configura MYSQL

Dopo l'installazione del server MariaDB, viene creato un utente root che può essere utilizzato solo dalla riga di comando. Connettiti a MYSQl tramite ```sudo mysql``` e copia questo file sql

```sql
 -- Create the new user
 CREATE USER 'nextcloud' IDENTIFIED BY 'password';
 -- Create the new database
 CREATE DATABASE nextcloud;
 -- Give all permissions
 GRANT ALL PRIVILEGES ON nextcloud.* TO 'nextcloud'@localhost IDENTIFIED BY 'password';
 FLUSH PRIVILEGES;
 quit

```

Il database è pronto e possiamo finire l'installazione di NextCloud.

## Errori
Ora, se hai provato ad accedere a questo link https://IP/nextcloud e ti escono degli errori rimani in questa sezione, altrimenti puoi tranquillamente andare avanti.
Il problema mi usciva colpa la versione di PHP che avevo installato. Ho risolto così:

installo PHP 8.3

```shell
 sudo wget -qO /etc/apt/trusted.gpg.d/php.gpg https://packages.sury.org/php/apt.gpg
 echo "deb https://packages.sury.org/php/ $(lsb_release -sc) main" | sudo tee /etc/apt/sources.list.d/php.list
 sudo apt update
 sudo apt install -y php8.3-common php8.3-cli
```

Poi ho cambiato la versione di Default con questi comandi:

```shell
 sudo a2dismod php* 
 sudo a2enmod php8.3 
 sudo systemctl restart apache2 
```

## Configura Nextcloud

Ora è possibile accedere alla pagina di configurazione di NextCloud e completare la configurazione.

Apri il seguente URL nel browser: https://IP/nextcloud. sostitusci "IP" con l'indirizzo IP di Raspberry Pi.

Viene visualizzato un modulo in cui scegliere un nome utente e una password per NextCloud.

La seconda parte chiede dove si desidera memorizzare i file di NextCloud.
È possibile mantenere il valore predefinito se si dispone di una sola partizione principale, oppure modificarlo per utilizzare, ad esempio, un'unità USB esterna.

La terza parte è la configurazione del database.
Inserite le credenziali appena create in MySQL:
- -Utente: nextcloud
- -Password: "password" (la password che avete usato nei comandi di MySQL)
- -Database: nextcloud
- -Host: localhost

Quindi fare clic su "Installa" e attendere qualche minuto.

Riapri il seguente URL nel browser: https://IP/nextcloud e ti troverai davanti al form di login.

## Le Fontih!

Guida/articolo/bozza realizzata grazie a questi tre articoli:

1. [Installing NextCloud on Your Raspberry Pi (2 ways)](https://raspberrytips.com/install-nextcloud-raspberry-pi/)
2. [Install PHP 8.3 on Raspberry Pi](https://lindevs.com/install-php-on-raspberry-pi)
3. [How to Change Default PHP Version on Ubuntu](https://tecadmin.net/switch-between-multiple-php-version-on-ubuntu/)