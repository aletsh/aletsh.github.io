---
id: 66
title: Servidor de impresion y Google Cloud Print con Raspberry Pi
date: 2016-11-18T19:02:01+00:00
author: aletsh
layout: post
guid: http://alejandroguerrero.es/2016/11/18/servidor-de-impresion-y-google-cloud-print-con-raspberry-pi/
permalink: /servidor-de-impresion-y-google-cloud-print-con-raspberry-pi/
categories:
  - Uncategorized
tags:
  - cloud print
  - cloudprint
  - cups
  - google print
  - prints
  - rapsberry
  - raspberry pi
  - raspi
  - raspy
  - server
  - Servidor de impresion
---
> Tenía la necesidad de poder imprimir (en mi **HP LaserJet 1020**) sin tener que estar encendiendo el ordenador cada vez. Aun así era bastante cómodo el hecho de imprimir desde cualquier lado y sin tocar nada, se imprimía el documento que había mandado por Google Print y lo único que tenía que hacer era pulsar el boton _power_ del ordenador que tenía la impresora.
> 
> Pues bien, ahora mismo ya no tengo la necesidad de encender el ordenador si no que hay uno ya encendido siempre, una Raspberry Pi compartiendo la impresora por la red y en Google Print.

## Pre-requisitos {#prerequisitos}

  * **Raspberry Pi** (la que sea, yo he empleado la 2)
  * **MicroSD** (yo tengo una de 8Gb)
  * Carcasa / Caja de la Raspberry Pi ¿?
  * **Impresora** (Claro está… La mia es la HP LaserJet 1020 bastante antigua pero funciona genial)

## Instrucciones {#instrucciones}

Hay que **montar** el **sistema operativo**. Yo uso [Raspbian](https://www.raspberrypi.org/downloads/), distro basada en Debian, vosotros usad la que queráis. Ahora mismo esta la version Jessie Lite. No os voy a decir como montarla lo siento, para eso hay mil videos en Youtube que te encantarán.

Una vez tengamos nuestra Raspberry Pi lista, **os aconsejo ponerle la ip fija** por llevar un orden en tu red mas que nada y para poder configurar la Raspberry remotamente sin necesidad de que un día se vaya la luz, se rompa tu router (adios servidor DHCP) y tengas que encender la Raspberry conectada a un monitor por HDMI únicamente para ver que ip tiene (_ifconfig_). Bueno os he puesto en un caso poco frecuente, pero quien sabe…

### [Ip fija para la raspberry](/ip-fija-raspberry-pi-eth0/) (eth0) {#ipfijaparalaraspberryeth0}

Hay que **editar** el siguiente \*\*archivo \*\*

<span class="s1">/etc/network/interfaces</span>

Haced una copia antes, por si se rompe algo…

<span class="s1">$ cp /etc/network/interfaces /etc/network/interfaces_old $ vi /etc/network/interfaces</span>

<span class="s1">#Contenido del archivo auto eth0</span><span class="s1">iface lo inet loopback</span><span class="s1">iface eth0 inet static</span> <span class="s1">address rasp.berry.pi.ip</span> <span class="s1">netmask net.mask.rasp.berry</span> <span class="s1">gateway gate.way.rasp.berry</span><span class="s1">allow-hotplug wlan0</span><span class="s1">iface wlan0 inet manual</span><span class="s1"><span class="Apple-converted-space">    </span>wpa-conf /etc/wpa_supplicant/wpa_supplicant.conf</span><span class="s1">allow-hotplug wlan1</span><span class="s1">iface wlan1 inet manual</span><span class="s1"><span class="Apple-converted-space">    </span>wpa-conf /etc/wpa_supplicant/wpa_supplicant.conf</span>

Guardar, Reiniciar y vovler a conectar vía SSH (a la nueva IP) .

### Actualizar dependencias {#actualizardependencias}

$ sudo apt-get update && upgrade

### Instalar Servidor de impresión CUPS {#instalarservidordeimpresincups}

Eliminamos los paquetes de HP y gestores de dispositivos innecesarios: <span class="anchor" id="line-26"></span><span class="anchor" id="line-27"></span>

$ apt-get purge hplip* system-config-printer-udev

**Instalar** Servidor de impresión **CUPS**, luego podremos acceder **vía web** a la configuración y **podremos añadir** nuestra **impresora** (<http://ip.de.la.raspberry>:**631**).

$ apt-get install cups hpijs-ppds build-essential foomatic-filters $ sudo usermod -a -G lpadmin pi

Una vez tengamos el servicio CUPS instalado tenemos que configurar el archivo de configuracion cups.conf para permitir el acceso desde nuestra red a la administracion via navegador de CUPS porque por defecto solo se puede administrar localmente (osea desde localhost):

$ nano /etc/cups/cupsd.conf

Aquí dentro deberemos de realizar estos cambios:

<span class="s1">&#8230; # Only listen for connections from the local machine.</span><span class="s1"># Listen <em>:631</span><span class="s1">Port 631 &#8230; </span><span class="s1"># Restrict access to the server&#8230;</span><span class="s1"><Location /></span><span class="s1"><span class="Apple-converted-space">  </span>Order allow,deny</span><span class="s1"><span class="Apple-converted-space">  </span>Allow @local</span><span class="s1"></Location></span><span class="s1"># Restrict access to the admin pages&#8230;</span><span class="s1"><Location /admin></span><span class="s1"><span class="Apple-converted-space">  </span>Order allow,deny</span><span class="s1"><span class="Apple-converted-space">  </span>Allow @local</span><span class="s1"></Location></span><span class="s1"># Restrict access to configuration files&#8230;</span><span class="s1"><Location /admin/conf></span><span class="s1"><span class="Apple-converted-space">  </span>AuthType Default</span><span class="s1"><span class="Apple-converted-space">  </span>#Require user @SYSTEM</span><span class="s1"><span class="Apple-converted-space">  </span>Allow 192.168.1.</em></span><span class="s1"><span class="Apple-converted-space">  </span>Order allow,deny</span><span class="s1"></Location> &#8230;</span></p> 

<p>
  Reiniciar el servicio CUPS para que inicie con los nuevos parametros:
</p>

<p>
  service cups restart
</p>

<h3 id="driversfoo2zjshplaserjet1020encups">
  Drivers Foo2zjs (HP LaserJet 1020 en CUPS)
</h3>

<p>
  El <strong>controlador</strong> que debemos <strong>instalar</strong> es <strong><a href="http://foo2zjs.rkkda.com/">foo2zjs</a>.</strong>
</p>

<p>
  A continuación se muestra los pasos a seguir para poder <strong>instalar la HP LaserJet 1020 en CUPS</strong>
</p>

<blockquote>
  <p>
    Si no es vuestro caso seguro que existen tutoriales para poder instalar la vuestra sin problemas**.**
  </p>
</blockquote>

<p>
  Seguir estos pasos para instalar los <strong>Drivers foo2zjs para la HP LaserJet 1020</strong>:
</p>

<p>
  $ wget -O foo2zjs.tar.gz <a href="http://foo2zjs.rkkda.com/foo2zjs.tar.gz">http://foo2zjs.rkkda.com/foo2zjs.tar.gz</a> $ tar zxf foo2zjs.tar.gz $ cd foo2zjs $ make $ ./getweb 1020 $ make install $ make install-hotplug $ make cups
</p>

<p>
  Desde es administrador de cups, <strong>dar de alta la nueva impresora</strong>, con el <strong>controlador</strong> “HP LaserJet 1020** Foomatic/foo2zjs-z1**“.
</p>

<p>
  A mi me ha quedado de esta manera:
</p>

<p>
  <img src="/content/images/2016/11/cups-raspberry-alejandroguerrero-es-1.png" alt="cups-raspberry-alejandroguerrero-es-1" />
</p></p> 

<p>
  <strong>Para probar</strong> la impresora se puede <strong>imprimir</strong> una <strong>pagina de prueba</strong> pulsando en el desplegable de “<strong>Mantenimiento</strong>“, “<strong>Imprimir pagina de prueba</strong>“.
</p>

<h2 id="imprimirdesdeairplay">
  Imprimir desde Airplay
</h2>

<p>
  Para imprimir desde los dispositivos de apple únicamente hay que instalar un paquete que a lo mejor ya se instalo al realizar la instalación de CUPS:
</p>

<p>
  <span class="s1">apt-get install avahi-daemon</span>
</p>

<h2 id="googleprintenlaraspberrypi">
  Google Print en la Raspberry Pi
</h2>

<p>
  Una vez este lista la impresora e imprima correctamente, podemos compartirla para que podamos imprimir desde cualquier dispositivo Android o navegador Google Chrome etc.
</p>

<p>
  Para ello vamos a <strong>añadir</strong> unos <strong>repositorios</strong> en las <em><strong>sources.list</strong></em> y vamos a instalar el paquete necesario para conectarnos con el conector de Google Print
</p>

<h3 id="aadirelrepositorioanuestrosourcelist">
  Añadir el repositorio a nuestro Source.list
</h3>

<pre><code>$ echo "deb http://davesteele.github.io/cloudprint-service/repo cloudprint-jessie main" | sudo tee /etc/apt/sources.list.d/cloudprint.list
$ wget -q -O - https://davesteele.github.io/key-366150CE.pub.txt | sudo apt-key add -
$ sudo apt-get update```

### Instalar el conector Google Print

`$ sudo apt-get -y install cloudprint-service`

**Hacer visible la impresora** para que el servicio de Cloud Print lo encuentre

</code></pre>

<p>
  $ sudo sed -i &#8216;s/Listen localhost:631/Listen *:631/&#8217; /etc/cups/cupsd.conf<br /> $ sudo sed -r -i &#8216;s/(Order allow,deny)/1n Allow all/&#8217; /etc/cups/cupsd.conf<br /> $ sudo usermod -a -G lpadmin pi<br /> $ sudo systemctl restart cups&#171;`
</p>

<h3 id="configurarimpresora">
  Configurar impresora
</h3>

<p>
  Ahora solo falta <strong>agregar la impresora</strong> en nuestro <a href="https://www.google.com/cloudprint#printers">Administrador de Impresoras de Google Print</a>. Para ello vamos a ejecutar un comando el cual nos pintará en la terminal una URL. <strong>Deberemos de acceder a esa url desde un navegador y darle los permisos necesarios.</strong>
</p>

<p>
  <code>$ sudo cps-auth</code>
</p>

<p>
  Un ejemplo de url puede ser algo parecido a esto:
</p>

<p>
  <code>https://goo.gl/printer/QWERTY</code>
</p>

<p>
  Así debería quedar:
</p>

<p>
  <img src="/content/images/2016/11/cups-raspberry-alejandroguerrero-es-2.png" alt="cups-raspberry-alejandroguerrero-es-2" />
</p>

<p>
  Ya podéis imprimir desde cualquier parte del mundo.
</p>

<p>
  Enjoy!
</p></p> 

<h2 id="bibliografa">
  Bibliografía
</h2>

<ul>
  <li>
    Drivers para la HP LJ 1020: <a href="http://foo2zjs.rkkda.com/">http://foo2zjs.rkkda.com/</a>
  </li>
  <li>
    Wiki Debian para instalar CUPS: <a href="https://wiki.debian.org/Instalar_HP_LaserJet_1020">https://wiki.debian.org/Instalar_HP_LaserJet_1020</a>
  </li>
  <li>
    Raspberry Pi Cloud Print: <a href="https://davesteele.github.io/raspberrypi/2016/04/23/raspberry-pi-cloudprint/">https://davesteele.github.io/raspberrypi/2016/04/23/raspberry-pi-cloudprint/</a>
  </li>
  <li>
    <a href="http://www.techradar.com/how-to/computing/how-to-turn-the-raspberry-pi-into-a-wireless-printer-server-1312717">http://www.techradar.com/how-to/computing/how-to-turn-the-raspberry-pi-into-a-wireless-printer-server-1312717</a>
  </li>
</ul>

<h2 id="fotosdelainstalacincilla">
  Fotos de la instalacióncilla
</h2><figure class="wp-caption aligncenter" id="attachment_1054" style="max-width: 4160px">![Raspberry Pi 2](/content/images/2016/11/cups-raspberry-alejandroguerrero-es-3.jpg)<figcaption class="wp-caption-text">Raspberry Pi 2</figcaption></figure> <figure class="wp-caption aligncenter" id="attachment_1055" style="max-width: 4160px">![HP LaserJet 1020](/content/images/2016/11/cups-raspberry-alejandroguerrero-es-4.jpg)<figcaption class="wp-caption-text">HP LaserJet 1020</figcaption></figure> <figure class="wp-caption aligncenter" id="attachment_1056" style="max-width: 4160px">![Impresión de pruebas](/content/images/2016/11/cups-raspberry-alejandroguerrero-es-5.jpg)<figcaption class="wp-caption-text">Impresión de pruebas</figcaption></figure>