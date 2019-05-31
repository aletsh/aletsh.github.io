---
id: 42
title: PC de bajo coste para tu TV
date: 2014-09-18T22:00:33+00:00
author: aletsh
layout: post
guid: http://alejandroguerrero.es/2014/09/18/pc-de-bajo-coste-para-tu-tv/
permalink: /pc-de-bajo-coste-para-tu-tv/
categories:
  - Uncategorized
tags:
  - raspbmc
---
Pues si, el pc de bajo coste tal y como estas pensando es una Raspberry Pi. En mi caso es el modelo B+ que trae 4 puertos USB y no trae puerto VGA como su antecesora.

El experimento es instalar el Sistema Operativo para que nuestra Raspi parezca un media center con el sistema operativo XBMC.

En pocos pasos tendréis el XBMC dentro de la Raspi B+:

Para ello necesitareis:

  1. [Una Raspberry Pi Model B+](http://www.amazon.es/gp/product/B00LPESRUK/ref=oh_aui_detailpage_o01_s00?ie=UTF8&psc=1)
  2. [Una tarjeta micro-sd de 8GB](http://www.amazon.es/gp/product/B0085J1AOS/ref=oh_aui_detailpage_o00_s00?ie=UTF8&psc=1) (al ser posible con adaptador)
  3. [Un cable para conectar la Raspberry a la red electrica](http://www.amazon.es/gp/product/B008XI52BS/ref=oh_aui_detailpage_o00_s00?ie=UTF8&psc=1)

[La caja para la Raspberry](http://www.amazon.es/gp/product/B00LV9886W/ref=oh_aui_detailpage_o01_s01?ie=UTF8&psc=1) es recomendable si no quieres tener “eso” al aire libre.

Introduce la tarjeta SD (que dentro lleva la micro-sd de 8GB) en el equipo (en este caso será para Linux o OSX).

A continuación se indica los pasos a seguir según el sistema operativo que tengas en tu equipo.

## Si tienes un Linux: {#sitienesunlinux}

mkdir /var/tmp/raspi wget <http://svn.stmlabs.com/svn/raspbmc/release/installers/python/install.py> chmod +x install.py

sudo python install.py

Seguir asistente…

## Si tienes un OSX (<del>Apple</del>): {#sitienesunosxdelappledel}

mkdir Documents/raspi curl -O <http://svn.stmlabs.com/svn/raspbmc/release/installers/python/install.py> chmod +x install.py

sudo python install.py

Seguir asistente…

Una vez acabado, pon la micro-sd dentro de la raspi y espera hasta que la raspi haga su trabajo.

Tu tranquilo que cuando esté todo listo XBMC arrancará automaticamente.

Ahora os toca a vosotros configurar el XBMC a vuestro gusto y disfrutar de las peliculas / series / lo que sea en vuestro media center de bajo coste.</p> 

😉