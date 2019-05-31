---
id: 12
title: 'Raspberry Pi 1 &#8211; Instalar una distibución Linux'
date: 2013-06-24T09:42:35+00:00
author: aletsh
layout: post
guid: http://alejandroguerrero.es/2013/06/24/raspberry-pi-1-instalar-una-distibucion-linux/
permalink: /raspberry-pi-1-instalar-una-distibucion-linux/
categories:
  - Uncategorized
---
Bien, ya tenemos nuestra raspi y todos los accesorios necesarios para trabajar con ésta, así que enchufamos el conector mini-usb de la corriente y…….. no arranca. ¿Por qué? Pues porque tenemos que instalar un sistema operativo!!! En el caso de que os hayais comprado un kit, muy probablemente ya venga con el S.O. Raspbian instalado por lo que os podéis saltar este paso. Para los que no tienen ningún S.O. esto es para vosotros.

Lo primero que tenemos que hacer es descargarnos una de las distribuciones Linux disponibles para arquitecturas ARM (lo que viene siendo nuestra raspi).

  * [Raspbian](http://www.raspberrypi.org/downloads) es el más utilizado y el más apropiado para principiantes y en el que basaré la gran mayoría de los tutoriales que publicaré.
  * [Occidentalis](http://learn.adafruit.com/adafruit-raspberry-pi-educational-linux-distro/) es la versión de Raspbian optimizada y modificada por Adafruit diseñada especialmente para controlar LED’s, sensores, botones que le conectemos a la raspi.
  * Archlinux, Pidora (Fedora para raspi).
  * Raspbmc, Xbmc (diseñados para hacer funcionar la raspi como mediacenter).

Aunque hay otras distros minoritarias (como por ejemplo una [versión reducida de Raspbian](http://www.linuxsystems.it/2012/06/raspbian-wheezy-armhf-raspberry-pi-minimal-image/) que cabe en una SD de 2GB) estas son las más utilizadas.

Ahora que tenemos nuestro S.O. de nuestra elección hay que copiarlo a nuestra SD. Para esto tenemos varios métodos. Primero insertamos nuestra SD en nuestro ordenador y descomprimimos nuestra distro hasta que nos quede un fichero .img:

  * Para Win Vista / 7:

Nos bajamos [este instalado](http://fedoraproject.org/wiki/Fedora_ARM_Installer#Windows_Vista_.26_7) [r](http://fedoraproject.org/wiki/Fedora_ARM_Installer#Windows_Vista_.26_7), lo extraemos y lo ejecutamos.

![](http://learn.adafruit.com/system/assets/assets/000/002/847/medium800/fail1.PNG?1354548383) 

En source, le damos a browse y seleccionamos nuestra distro linux (.img).

En destination marcamos la unidad de nuestra SD y le damos a start.

En unos minutos tendremos nuestra SD lista.

  * Para Mac:

Nos bajamos este [otro instalador](https://github.com/RayViljoen/Raspberry-PI-SD-Installer-OS-X), haciendo click en el botón “zip” de la página.

Descomprimimos dicho zip en una carpeta y metemos ahí dentro nuestra distro .img .

Abrimos una terminal en esa carpeta y ejecutamos el comando

sudo ./install nombre\_del\_fichero_img.img

Nos saldrá una pantalla como ésta donde tendremos que elegir el número que corresponde a nuestra SD (mucho ojo!!, a ver si no os formateais otro disco que no sea la SD, no me hago responsable si os equivocais de tecla!!).

![](http://learn.adafruit.com/system/assets/assets/000/002/852/medium800/02_screen_select_drive.png?1354548680) 

Nada más presioneis el número correspondiente comenzará a instalarse el S.O. en vuestra sd. En unos minutos (dependiendo de la clase de la sd) os saldrá “All done!” y lo tendréis listo.

  * <span style="line-height: 13px"><a href="http://elinux.org/RPi_Easy_SD_Card_Setup">Otros métodos</a> para los que tengais otro S.O. que no sea win7/vista/mac.</span>

Ahora solo queda probar a ver si arranca!! Introducid la sd en la raspi y enchufadla a la corriente. Si os aparecen un montón de letras (típico de distros Linux) y luego os pide el login, ¡enhorabuena!

Por defecto el login es pi y la contraseña raspberry

Esto es todo de momento. Hasta el próximo tutorial!!