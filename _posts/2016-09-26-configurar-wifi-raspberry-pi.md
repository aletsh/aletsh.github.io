---
id: 65
title: Configurar Wifi Raspberry pi
date: 2016-09-26T19:34:29+00:00
author: aletsh
layout: post
guid: http://alejandroguerrero.es/2016/09/26/configurar-wifi-raspberry-pi/
permalink: /configurar-wifi-raspberry-pi/
categories:
  - Uncategorized
tags:
  - raspberry
  - wifi
  - wireless
---
Voy a poner el código necesario para que funcione correctamente una Raspberry Pi a la Wifi deseada. Son dos cómodos pasos.

Fichero:\*\* /etc/network/interfaces\*\*

Os recomiendo crear un backup primero del archivo:

cp /etc/network/interfaces interfaces.copy

Este será su contenido:

auto lo iface lo inet loopback iface eth0 inet manual allow-hotplug wlan0 iface wlan0 inet manual wpa-conf /etc/wpa\_supplicant/wpa\_supplicant.conf allow-hotplug wlan1 iface wlan1 inet manual wpa-conf /etc/wpa\_supplicant/wpa\_supplicant.conf

Fichero: **/etc/wpa\_supplicant/wpa\_supplicant.conf**

Si no tienes el fichero creado, hazlo!

touch **/etc/wpa\_supplicant/wpa\_supplicant.conf**

Editamos el archivo:

nano **/etc/wpa\_supplicant/wpa\_supplicant.conf**

Introducimos lo siguiente:

ctrl\_interface=DIR=/var/run/wpa\_supplicant GROUP=netdev update\_config=1 country=ES network={ ssid="{EL-NOMBRE-DE-TU-CONEXION-WIFI}" psk="{CONTRASEÑA}" key\_mgmt=WPA-PSK }

El valor de key_mgmt variará según la seguridad que tengas puesta en tu router.

Mas información aqui:

  * [Archilinux](https://wiki.archlinux.org/index.php/WPA_supplicant_(Espa%C3%B1ol))
  * Raspberrypi.org