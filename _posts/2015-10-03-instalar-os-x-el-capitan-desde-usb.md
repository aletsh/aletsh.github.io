---
id: 57
title: Instalar OS X El Capitan desde USB
date: 2015-10-03T21:18:43+00:00
author: aletsh
layout: post
guid: http://alejandroguerrero.es/2015/10/03/instalar-os-x-el-capitan-desde-usb/
permalink: /instalar-os-x-el-capitan-desde-usb/
categories:
  - Uncategorized
tags:
  - apple
  - el capitan
  - os x
  - os x el capitan
---
Si, has leído bien. Esta entrada servirá para que instales OS X El Capitan en tu equipo desde 0, limpiamente, desde un USB.

[![macosx-el-capitan](/content/images/2015/10/macosx-el-capitan.png)](/content/images/2015/10/macosx-el-capitan.png)

##  {#}

Pre-requisitos

  1. USB de más de 8GB
  2. Descargar la app que actualiza el sistema
  3. Cambiarle el nombre al USB
  4. Crear imagen USB con OS X El Capitan

### Descargar OS X El Capitan {#descargarosxelcapitan}

Para descargarlo es bien fácil, si no lo tienes instalado como si lo tienes, desde la APP Store puedes bajártelo de forma totalmente gratuita:

[Desde aquí (enlace oficial)](https://itunes.apple.com/es/app/os-x-el-capitan/id1018109117?mt=12)

[![app-store-alejandroguerrero-es](/content/images/2015/10/app-store-alejandroguerrero-es-1024x69.png)](/content/images/2015/10/app-store-alejandroguerrero-es.png)

[![osx-el-capitan-alejandroguerrero-es-4](/content/images/2015/10/osx-el-capitan-alejandroguerrero-es-4.png)](/content/images/2015/10/osx-el-capitan-alejandroguerrero-es-4.png)

Una vez lo tengas descargado no sigas el asistente, no es necesario que lo cierres, si lo que quieres es instalarlo desde 0, si lo que quieres es migrar, sí, sigue el asistente.

### Cambiarle el nombre al USB {#cambiarleelnombrealusb}

Si al poner el usb en el equipo no os detecta bien tenéis que emplear la utilidad de discos para borrar vuestro USB ya que lo borrais podéis ponerle el nombre de: **ElCapInstaller.**

Si os lo detecta bien, cambiadle el nombre tal como sabéis hacer, pero tenéis que ponerle el nombre de ElCapInstaller porque lo necesitarás mas adelante.

### Crear imagen USB con OS X El Capitan {#crearimagenusbconosxelcapitan}

Ahora viene lo complicado, lo duro, lo que os da miedo, si un comando por la terminal, seguro que hay mas formas de hacerlo pero… por terminal mola más y punto!

Ya tenéis descargado el OS X El Capitan, ya esta listo el USB ahora toca abrir la terminal en ella introducid:

sudo /Applications/Install OS X El Capitan.app/Contents/Resources/createinstallmedia &#8211;volume /Volumes/ElCapInstaller &#8211;applicationpath /Applications/Install OS X El Capitan.app/ &#8211;nointeraction

Si tenéis problemas podéis ir escribiendo poco a poco el texto en la terminal ayudando os con la tecla tabulador que os auto-completa o auto-sugiere palabras.

[![osx-el-capitan-alejandroguerrero-es-2](/content/images/2015/10/osx-el-capitan-alejandroguerrero-es-2.png)](/content/images/2015/10/osx-el-capitan-alejandroguerrero-es-2.png)

El proceso al pulsar la tecla intro es el siguiente:

“Erasing Disk: 0%… 10%… 20%… 30%…100%… Copying installer files to disk… Copy complete. Making disk bootable… Copying boot files… Copy complete. Done.”

Una vez haya finalizado podéis restaurar vuestro equipo con OS X El Capitan y tener un nuevo principio en vuestra vida xD.