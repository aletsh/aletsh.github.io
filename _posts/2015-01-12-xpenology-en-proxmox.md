---
id: 50
title: XPenology en Proxmox
date: 2015-01-12T20:34:30+00:00
author: aletsh
layout: post
guid: http://alejandroguerrero.es/2015/01/12/xpenology-en-proxmox/
permalink: /xpenology-en-proxmox/
categories:
  - Uncategorized
tags:
  - proxmox
  - xpenlogy
---
Buenas a todos,  
actualmente estuve gugleando como instalar una maquina virtual con el SSOO que esta muy de moda: [XPenology](http://www.xpenology.nl/ "XPenology").

A continuación pondré la configuración que emplee yo para crear dicha instancia en Proxmox 3.3.1:

  * Memoria RAM: 512mb (escalable hasta 1gb on demmand)
  * CPU: 1 core (core2duo)
  * HDD: 2 TB (SATA)
  * RED: rtl8139 bridge(vmbr0)

La iso que cargué en el VM es la siguiente: [Nanoboot-5.0.2.4 **DSM 5.0-4528**](http://www.xpenology.nl/xpenology-downloads/?myvar=1531 "Nanoboot-5.0.2.4 DSM 5.0-4528 X86 by XPEnology.nl")

  1. La primera  vez que se ejecute la ISO en el VM hay que seleccionar la 2ª opcion que aparece en el menu azul (Install/Update).
  2. Cuando cargue todo (letras grises) aparecerá la IP que te asigno tu router DHCP en mi caso 10.0.0.254, si la IP que te asigno no es la correcta, reinicia.
  3. Cuando sepas la ip accede al navegador e introduce la IP en la barra de direcciones ej: <http://10.0.0.254:5000> o emplea el software Synology Assistant.
  4. A continuación aparecerá un asistente muy bonito en el cual deberemos cargar el siguiente DSM:[DSM 5.0-4528](http://www.xpenology.nl/dsm-software-download/?myvar=1449 "DSM 5.0-4528 (DS214play)")

Esperamos unos 5 minutos, ya se que pone 10 pero es mentira. Y wala! Ya tenemos un Synology en una instancia.

[![XPenology-alejandroguerrero-es](http://alejandroguerrero.es/content/images/2015/01/Captura-de-pantalla-2015-01-12-a-las-20.41.09-1024x332.png)](/content/images/2015/01/Captura-de-pantalla-2015-01-12-a-las-20.41.09.png)

Algunos enlaces de interes:

  * <http://www.mundonas.com/>
  * <http://xpenology.com/forum/>
  * <http://xpenology.nl/>

Listado de SOURCES que empleo en mi XPenology

  * <https://synocommunity.com/packages>

😉