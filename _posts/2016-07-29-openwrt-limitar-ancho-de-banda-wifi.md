---
id: 63
title: 'OpenWrt &#8211; Limitar Ancho de Banda Wifi'
date: 2016-07-29T19:17:32+00:00
author: aletsh
layout: post
guid: http://alejandroguerrero.es/2016/07/29/openwrt-limitar-ancho-de-banda-wifi/
permalink: /openwrt-limitar-ancho-de-banda-wifi/
categories:
  - Uncategorized
tags:
  - ancho de banda
  - bandwith
  - internet
  - limit
  - limitar
  - openwrt
  - qos
  - sqm
  - wifi
  - wireless
---
## Pre-requisitos {#prerequisitos}

  * Tener instalado OpenWrt
  * Tener configurada una Wifi con o sin contraseña

## Instrucciones {#instrucciones}

Descargar desde el gestor de paquetes de OpenWrt –> “sqm”.

  1. **System** –> **Software**
  2. En filter ponemos: **sqm**
  3. Pulsamos en la pestaña: **Available packages**
  4. Buscamos “**luci-app-sqm**“
  5. Pulsamos en “**install**“

Una vez instado **refrescar el navegador** y/o re-entramos en la configuración de OpenWrt.

Ahora aparece un nuevo menu en la opción del menu superior “**Network**” llamada **SQM QoS**.

Para añadir una nueva regla debemos de **saber primero que Wifi** limitarle el ancho de banda.

Para saber que wifi es si la wlan0-1 o wlan1-1 hay que ir a la configuración del Wifi y darle al botón editar del mismo. Ahi aparecerá:

[![openwrt - limit bandwith - 1](/content/images/2016/07/openwrt-limit-bandwith-1.png)](/openwrt-limitar-ancho-de-banda-wifi/openwrt-limit-bandwith-1/)

En mi caso la Wifi a limitar es la wlan0-1 por lo tanto en el menu **Network** –> **SQM QoS** voy a poner la interfaz: wlan0-1.

Adjunto pantallazo para limitar la wlan0-1 a 1 MB simétrico (1 de upstream 1 de downstream):

[![openwrt - limit bandwith - 2](/content/images/2016/07/openwrt-limit-bandwith-2.png)](/openwrt-limitar-ancho-de-banda-wifi/openwrt-limit-bandwith-2/)

Una vez guardada la configuración solo es necesario probarla.

## Conexión {#conexin}

Para ello existen un montón de páginas web las cuales nos hacen un test de velocidad.

Primeramente nos conectamos a la Wifi configurada y podemos hacer los tests en estas paginas:

  * <http://ovh.net/files/> –> Enlace SpeedTest
  * <http://www.speedtest.net/>

## Resultados {#resultados}

OVH Speed Test

[![openwrt - limit bandwith - 3](/content/images/2016/07/openwrt-limit-bandwith-3.png)](/openwrt-limitar-ancho-de-banda-wifi/openwrt-limit-bandwith-3/)

Speed Test.net

![](http://www.speedtest.net/result/5513393944.png)