---
id: 16
title: 'Raspberry Pi 2 &#8211; Acceso remoto via SSH'
date: 2013-07-18T14:09:28+00:00
author: aletsh
layout: post
guid: http://alejandroguerrero.es/2013/07/18/raspbery-pi-2-acceso-remoto-via-ssh/
permalink: /raspbery-pi-2-acceso-remoto-via-ssh/
categories:
  - Uncategorized
---
Si habéis seguido el anterior tutorial ya deberíais de tener una distro instalada en vuestra sd. En este tutorial me basaré en Raspbian, que es la distro más usada, para configurar el acceso remoto a la raspi. Esto nos permitirá entre otras cosas:

  * Manejar nuestra raspi sin necesidad de tener conectado físicamente teclado ni ratón ni tan siquiera una pantalla a la raspi.
  * Controlarla mediante consola de comandos desde cualquier otra máquina / smartphone / tablet
  * Controlarlo remotamente desde fuera de nuestra red local
  * Subir y descargar ficheros mediante SFTP

Para ello necesitamos primero de todo tener la raspi conectada a la red siempre que queramos acceder a ella (capitán obvio) y habilitar el protocolo ssh.

## 1. Habilitar SSH {#1habilitarssh}

Tecleamos el siguiente comando en la terminal

sudo raspi-config

Y nos saldrá el\*\* asistente de configuración\*\* de la raspi.

![](http://learn.adafruit.com/system/assets/assets/000/002/858/medium800/raspi-config_main.png?1354632726) 

Seleccionaremos la opción **“ssh”** y seguidamente “enable”. Luego ya podemos salir del asistente seleccionando “<finish>” o con Ctrl+C

## 2. Establecer una dirección IP estática {#2establecerunadireccinipesttica}

Por defecto la mayoría de routers asignan una IP local automáticamente al conectarse un dispositivo al router. Así puedes tener una ip un día, y al día siguiente otra, lo cual no nos interesa para poder conectarnos a nuestra raspi ya que de lo contrario cada vez tendríamos que averiguar qué IP se nos ha asignado a nuestra raspi. ¿La solución? establecer en la configuración de red que queremos que\*\* nuestra raspi siempre tenga la misma ip\*\*, que estableceremos a continuación.

Editaremos el\*\* fichero de interfaces de red\*\*:

sudo nano /etc/network/interfaces

Y ahí reemplazamos la siguiente línea

iface eth0 inet dhcp</p> 

Por esta:

iface eth0 inet static address 192.168.1.160 netmask 255.255.255.0 gateway 192.168.1.1</p> 

Evidentemente tendréis que ajustar la ip a la configuración que teneis en el router. En mi caso, para no tener conflictos con los demás equipos que tengo conectados por dhcp, le he puesto la última ip del rango configurado que da mi router. Guardamos con Ctrl-X y S. Reiniciamos nuestra raspi.

En el caso de que tengais la raspi conectada por wifi, debereis buscar por la línea

iface wlan0 inet dhcp

## 3. Abrir los puertos del router y acceder por SSH {#3abrirlospuertosdelrouteryaccederporssh}

Lo siguiente es abrir los puertos del router si quereis acceder remotamente desde fuera de vuestra red local. De momento **necesitaremos el puerto 22 TCP/UDP** para la ip que habeis especificado como estática.

Desde fuera de nuestra red local podremos acceder mediante nuestra ip publica y el puerto 22 (y desde dentro de nuestra red con la ip privada) mediante nuestro intérprete ssh como puede ser _putty_ para windows o en linux y mac abriendo una terminal con el comando

ssh -X pi@tu_ip

![](http://learn.adafruit.com/system/assets/assets/000/003/149/medium800/putty_connected.png?1356000744) 

## 4. Utilizar un dominio no-ip para direcciones dinámicas {#4utilizarundominionoipparadireccionesdinmicas}

![](http://www.redeszone.net/content/images/no-ip_logo.jpg) 

Si tienes ip dinámica (te cambia la ip pública cada vez que reinicias el router) necesitarás **crearte un dominio gratuito en no-ip.com** para no tener que mirar cada día la ip pública que se te ha asignado. Para ello iremos a no-ip.com y nos crearemos una cuenta, añadiendo el alias que más rabia nos de (que es el que utilizaremos en vez de nuestra ip pública). También podemos añadir hasta 2 alias más entrando en nuestra cuenta de no-ip, en Hosts/Redirects > Add a Host

En nuestra raspi\*\* instalaremos el cliente no-ip\*\* que nos actualizará el alias con nuestra ip pública actual cada 30 min (por defecto) con los siguientes comandos:

cd /usr/local/src wget <http://www.no-ip.com/client/linux/noip-duc-linux.tar.gz> tar xzf noip-duc-linux.tar.gz cd no-ip-2.1.9 sudo make sudo make install

Y procederemos a configurar nuestro cliente no-ip respondiendo a las preguntas que nos aparecerán en pantalla. Una de ellas será “Do you wish to update all hosts” en la cual si respondemos que sí machacaremos todos los hosts que tengamos configurados y apuntarán todos a la ip de nuestra raspi. Si solo tienes un host o quieres que todos apunten a la raspi puedes responder que sí.

/usr/local/bin/noip2 -C

Ahora solo tenemos que arrancar nuestro cliente no-ip

`/usr/local/bin/noip2`

## 5. Arrancar no-ip automáticamente {#5arrancarnoipautomticamente}

Para que se\*\* inicie al arranque de la raspi\*\*, tendremos que crear un\*\* script de inicio\*\* en _/etc/init.d_

sudo nano /etc/init.d/noip</p> 

Que contendrá el siguiente código:

# ! /bin/sh # /etc/init.d/noip ### BEGIN INIT INFO # Provides: noip # Required-Start: $remote\_fs $syslog # Required-Stop: $remote\_fs $syslog # Default-Start: 2 3 4 5 # Default-Stop: 0 1 6 # Short-Description: Script para noip by David Alexa # Description: Script de www.alejandroguerrero.es para iniciar noip al arranque de la maquina by David Alexa ### END INIT INFO case "$1" in start) echo "Starting noip" /usr/local/bin/noip2 ;; stop) echo "Stopping noip" killall noip2 ;; *) echo "Usage: /etc/init.d/noip {start|stop}" exit 1 ;; esac exit 0 {#binshetcinitdnoipbegininitinfoprovidesnoiprequiredstartremote_fssyslogrequiredstopremote_fssyslogdefaultstart2345defaultstop016shortdescriptionscriptparanoipbydavidalexadescriptionscriptdewwwalejandroguerreroesparainiciarnoipalarranquedelamaquinabydavidalexaendinitinfocase1instartechostartingnoipusrlocalbinnoip2stopechostoppingnoipkillallnoip2echousageetcinitdnoipstartstopexit1esacexit0}

Hacemos nuestro\*\* script ejecutable\*\*

sudo chmod 755 /etc/init.d/noip.sh

Probamos de arrancarlo, y miramos si está el proceso _noip2_ con el comando _top_ (o con _htop_, que es un gestor más bonito pero no viene instalado por defecto)

sudo /etc/init.d/noip.sh start

Probamos si podemos parar el proceso y miramos que ya no está en el top

sudo /etc/init.d/noip.sh stop

Vamos a **registrar el script** para que se inicie en el arranque de la raspi

sudo update-rc.d noip defaults

Si por alguna razón lo queremos\*\* quitar del arranque\*\*, ejecutamos el siguiente comando.

sudo update-rc.d -f noip remove

Este procedimiento se puede aplicar a cualquier proceso que querramos iniciar al arranque de un sistema linux basado en debian.</p> 

Y ya está! Ya podemos desconectar nuestro teclado y el monitor de la raspi, porque mientras la raspi tenga acceso a la red podremos controlarla via ssh.

Espero que os haya sido de utilidad! En el próximo tutorial os enseñaré a mostrar la interfaz gráfica remotamente via vnc.