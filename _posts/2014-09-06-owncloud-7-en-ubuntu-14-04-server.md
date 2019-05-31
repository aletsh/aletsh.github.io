---
id: 41
title: Owncloud 7 en Ubuntu 14.04 Server
date: 2014-09-06T22:00:35+00:00
author: aletsh
layout: post
guid: http://alejandroguerrero.es/2014/09/06/owncloud-7-en-ubuntu-14-04-server/
permalink: /owncloud-7-en-ubuntu-14-04-server/
categories:
  - Uncategorized
tags:
  - owcloud
  - tutorial
  - ubuntu
---
En este post voy a explicaros como instalar en vuestra maquina un Owncloud. Es bastante sencillo si necesitais ayuda os puedo dar soporte solamente teneis que ir a la página de contacto y escribir en ese formulario.</p> 

# Requisitos {#requisitos}

  1. Tener una máquina con el Ubuntu 14.04 instalada. Yo emplee Ubuntu 14.04 server (minimal)

* * *

# Instrucciones {#instrucciones}

apt-get install php-pear php-xml-parser php5-sqlite php5-json sqlite mp3info curl libcurl3-dev zip

apt-get install mysql-server php5-mysql

Esperar a que instale…

mysql -u root -p

Pedirá contraseña… ponla!

Aparecerá la linea de comandos de “mysql> “…

mysql> create database nombre\_de\_nuestra\_base\_de_datos;

mysql> quit

Descargar el archivo setup-owncloud.php desde [aquí](https://download.owncloud.com/download/community/setup-owncloud.php).

mkdir /var/www/html/ownlcoud cd /var/www/html/owncloud wget <https://download.owncloud.com/download/community/setup-owncloud.php>

Probamos en nuestro navegador a acceder mediante la ip o el dominio apuntado: midominio.com/owncloud/setup-owncloud.php y nos debe aparecer esta pantalla o similar:

[![owncloud-pantalla-1](http://alejandroguerrero.es/content/images/2014/09/Captura-de-pantalla-2014-09-06-a-las-19.31.09-600x369.png)](/content/images/2014/09/Captura-de-pantalla-2014-09-06-a-las-19.31.09.png)

Continuamos con el asistente rellenando los campos que nos vaya pidiendo.

Listo k-listo!

😉

* * *

# Posibles errores {#posibleserrores}

*_PHP module curl not installed. Please ask your server administrator to install the module:_

sudo apt-get install curl libcurl3 libcurl3-dev php5-curl service apache2 restart

Volver a probar…</p> 

*\*El ódulo PHP GD no está instalado. Consulte al administrador de su servidor para instalar el módulo. \*_Los módulos PHP se han instalado, pero aparecen listados como si faltaran. Consulte al administrador de su servidor para reiniciar el servidor web._

apt-get install php5-gd php5-json php5-mysql php5-curl service apache2 restart

Volver a probar…</p> 

*_Advertencia de seguridad_  
_Su directorio de datos y sus archivos son probablemente accesible <span class="IL_AD" id="IL_AD1">desde Internet</span>. El archivo. Htaccess que establece ownCloud no está funcionando. Le recomendamos que configure su <span class="IL_AD" id="IL_AD7">servidor web</span> de una manera que el directorio de datos ya no es accesible o se mueve el directorio de datos fuera de la raíz del documento servidor web._

a2enmod rewrite service apache2 restart nano /etc/apache2/sites-available/000-default.conf

Introducir despues de la linea “_DocumentRoot /var/www/html_“:

<Directory "/var/www/html"> AllowOverride All </Directory>

Quedando de esta manera:

<VirtualHost *:80> # The ServerName directive sets the request scheme, hostname and port that # the server uses to identify itself. This is used when creating # redirection URLs. In the context of virtual hosts, the ServerName # specifies what hostname must appear in the request&#8217;s Host: header to # match this virtual host. For the default virtual host (this file) this # value is not decisive as it is used as a last resort host regardless. # However, you must set it for any further virtual host explicitly. #ServerName www.example.com ServerAdmin <info@alejandroguerrero.es> DocumentRoot /var/www/html **<Directory "/var/www/html"> AllowOverride All </Directory>** # Available loglevels: trace8, &#8230;, trace1, debug, info, notice, warn, # error, crit, alert, emerg. # It is also possible to configure the loglevel for particular # modules, e.g. #LogLevel info ssl:warn ErrorLog ${APACHE\_LOG\_DIR}/error.log CustomLog ${APACHE\_LOG\_DIR}/access.log combined # For most configuration files from conf-available/, which are # enabled or disabled at a global level, it is possible to # include a line for only one particular virtual host. For example the # following line enables the CGI configuration for this host only # after it has been globally disabled with "a2disconf". #Include conf-available/serve-cgi-bin.conf </VirtualHost> # vim: syntax=apache ts=4 sw=4 sts=4 sr noet

Guardar y reiniciar apache2:

service apache2 restart

Volver a probar…</p> 

* * *

# Bibliografía {#bibliografa}

  * SSL Certificate – <https://www.digitalocean.com/community/tutorials/how-to-create-a-ssl-certificate-on-apache-for-ubuntu-12-04>
  * LAMP Server: <https://www.digitalocean.com/community/tutorials/how-to-install-linux-apache-mysql-php-lamp-stack-on-ubuntu-14-04>
  * [Crea tu propio servidor de datos en la nube con OwnCloud](http://blog.desdelinux.net/crea-tu-propio-servidor-de-datos-en-la-nube-con-owncloud/ "Crea tu propio servidor de datos en la nube con OwnCloud")