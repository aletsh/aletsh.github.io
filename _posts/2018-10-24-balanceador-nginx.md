---
layout: post
id: 71
title: Reverse proxy con NGiNX
date: 'Wed Oct 24 2018 21:00:00 GMT+0200 (hora de verano de Europa central)'
author: aletsh
guid: 'http://alejandroguerrero.es/2018/10/24/balanceador-nginx/'
permalink: /balanceador-nginx/
categories:
  - linux
tags:
  - nginx
  - raspberry
  - reverse proxy
published: true
---
En este post explicaré brevemente la forma de acceder a las webs que esten alojadas en diferentes máquinas empleando el puerto HTTP/s (80 / 443).

¿Puedo servir 2 o mas &#171;webs&#187; por el mismo puerto http/s (80 / 443) en mi casa?

Sí, haciendo lo siguiente (modo resumen):

  1. Crear una maquina virtual o en su lugar tener una Raspberri Pi. (Supongamos que la IP de esta máquina es la 10.1.1.101)
  2. Abrir el puerto 80 en nuestro router (NAT) apuntando a la ip 10.1.1.101
  3. Instalar y configurar nginx en la maquina 10.1.1.101
  4. Crear las maquinas que queramos sirviendo en el puerto que queramos, 10.1.1.102, 10.1.1.103&#8230; 10.1.1.*.

Ahora lo voy a detallar un poco más;

## Instalar y configurar reverse proxy con NGiNX {#instalar-y-configurar-reverse-proxy-con-nginx}

Instalar en nuestra maquina (Debian por ejemplo) con la ip 10.1.1.101 el NGiNX:

    apt-update
    apt-get install nginx

Probar que esta funcionando accediendo mediante el navegador Web a la IP del servidor http://10.1.1.101

También probaremos el funcionamiento de los otros servidores los cuales deseamos acceder por ejemplo al servidor 10.1.1.102 mediante el dominio domain1.com y al 10.1.1.103 con el dominio domain2.com.

### Configurar reverse proxy {#configurar-reverse-proxy}

En el servidor 10.1.1.101 editar el archivo:

    vi /etc/nginx/sites-available/default

Introducir lo siguiente:

    server {
        listen 80 default_server;
        server_name _;
        return 301 https://$host$request_uri;
    }
    
    server {
        listen 80;
        server_name domain1.com www.domain1.com;
    
        add_header X-Frame-Options "SAMEORIGIN";
    
        location / {
            proxy_pass http://10.1.1.102:32768$request_uri;
        }
    }
    
    server {
        listen 80;
        server_name domain2.com www.domain2.com;
    
        add_header X-Frame-Options "SAMEORIGIN";
    
        location / {
            proxy_pass http://10.1.1.103:5000$request_uri;
        }
    }
    
    server {
        listen 80;
        server_name minube.domain1.com;
    
        #add_header X-Frame-Options "SAMEORIGIN";
        location /{
            proxy_pass http://10.1.1.104;
        }
    
        client_max_body_size 10G;
    }

### Probar reverse proxy en nuestra red local {#probar-reverse-proxy-en-nuestra-red-local}

Acceder al archivo hosts de nuestro ordenador local para realizar las pruebas.

En windows está en:

    C:WindowsSystem32driversetc

En Debian está en:

    /etc/hostname

Introducir lo siguiente:

    domain1.com 10.1.1.101
    domain2.com 10.1.1.101

Como se puede observar los dos dominios atacarán al servidor con el reverse proxy configurado.

Si todo a ido bien, desde internet ya podremos resolver los dos dominios los cuales son dos máquinas diferentes y estan &#171;empleando&#187; el mismo puerto.

Enjoy!
