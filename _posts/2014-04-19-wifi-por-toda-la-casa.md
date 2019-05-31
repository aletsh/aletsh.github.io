---
id: 26
title: Wifi por toda la casa!
date: 2014-04-19T22:30:05+00:00
author: aletsh
layout: post
guid: http://alejandroguerrero.es/2014/04/19/wifi-por-toda-la-casa/
permalink: /wifi-por-toda-la-casa/
categories:
  - Uncategorized
tags:
  - client-bridge
  - dd-wrt
  - wifi
  - wifi-bridge
  - wrt160nl
---
Veo últimamente que tenéis problemas con vuestra cobertura Wifi o que básicamente queréis tener wifi en el “jardín”. _Digo Jardín como podría decir otra cosa._

Lo complicado no es tener wifi ya que el propio operador te da un trasto con wifi, lo complicado es que llegue a todas partes por igual.

Os voy a proponer algo bastante sencillo y económico, gratis no puede ser ya que necesitamos comprar un aparato para ampliar la Wifi de nuestra casa/oficina. Bueno, empezamos!

## Materiales {#materiales}

  * El Router de vuestra operadora. _Da igual cual sea, todos son malos_.
  * Un Router o un Acces Point (en un futuro llamado AP) viejo o nuevo.
  * Cable de red para configurar el Router/AP
  * Software para crear vuestro MAPA WIFI &#8211; Heat Mapper: <http://www.ekahau.com/wifidesign/ekahau-heatmapper>
  * Tamo Graph: <http://www.tamos.com/download/main/tg.php>
  * AirMagnet APP: <http://es.flukenetworks.com/enterprise-network/wireless-network/AirMagnet-AirMapper>
  * AeroHive: <http://www.aerohive.com/planner>

## Router/AP {#routerap}

Tenemos que saber que nuestro aparato es compatible con DD-WRT para ello accederemos a la [Web](http://www.dd-wrt.com/site/support/router-database "Base de Datos DD-WRT") la cual tiene una base de datos con todos los equipos compatibles.

Buscamos el modelo de nuestro aparato, por ejemplo: WRT-160NL. (Si no lo encontráis no sigas leyendo este tutorial).

Una vez encontrado el Firmware  vemos que existen unas columnas las cuales nos indica si esta soportado y si necesita una activación post instalación. En mi casi es soportado y no necesita activación.

Enchufamos el router a la electricidad y enchufamos un cable de red en la toma que querais menos en la que pone WAN, o Internet… enchufarla en la 1, 2… 32. Y a vuestro PC. Teneis que entrar en la configuración del mismo desde vuestro navegador preferido. En la barra de direcciones teneis que poner la IP del router que puede ser: 192.168.1.1, 192.168.2.1 en mi caso es la 172.17.10.1.

Teneis que navegar hasta la opcion de firware (antención: cada router es un mundo) y cargar el firmware DD-WRT que os habéis descargado previamente. Una vez le deis a cargar firmware no desenchuféis nada, no toquéis nada, no respiréis y sobretodo no enchuféis 20.000 Wat !!! Si se va la luz, mala suerte, tendréis que ir de paseo a comprar otro cacharro.

## Configuración DD-WRT {#configuracinddwrt}

A continuación para no torrarla más mirad el siguiente vídeo y seguid los pasos. Os recomiendo que vayáis parando el vídeo porque el tipo va súper rápido.

Este es el video: <https://www.youtube.com/watch?v=Ud-Hq3kgvk4>

## Mapa WIFI {#mapawifi}

Hasta aquí todo correcto ¿no?

Ahora tenemos que saber en que punto es mas optimo de nuestra casa/oficina para poner nuestro router ya configuradito y listo para que se caliente mas que un volcán.

Yo he decidido emplear <span style="color: #222222;">Aerohive (la url la tenéis mas arriba) os registráis y os mandaran las credenciales (usuario y contraseña) por mail.</span>

Una vez accedido os pedirá donde queréis poner vuestra oficina/casa y tenéis que crear el plano. Es muy fácil es a lo tipo Paint. Lo que mas me ha costado a sido poner los metros en el plano para que las coberturas de los AP’s sean mas o menos reales.

Al final así es mi plano a quedado así con un AP:

[![Wifi en casa](http://alejandroguerrero.es/content/images/2014/04/zona-acces-point1-1024x525.jpg)](/content/images/2014/04/zona-acces-point1.jpg)

Al añadir otro AP con las especificaciones reales del mismo se que lo tengo que poner en una estantería del salón para dar casi un 100% de cobertura. Así quedaría con el segundo AP:

[![Aumentar Wifi](http://alejandroguerrero.es/content/images/2014/04/zona-acces-point2-1024x503.jpg)](/content/images/2014/04/zona-acces-point2.jpg)

Id jugando vosotros donde poner los AP para que tengáis una conexión Wifi Optima.

Comentad dudas, si teneis un software para crear mapas que queráis compartir, experiencias con DD-WRT, experiencias con otros routers, antenas, Ubiquitis, Antena Patatillas Pringles, lo que sea, será bienvenido.

Espero ayudar un poco más con este mini-tutorial.

Saludos!

😉

### Fuentes externas: {#fuentesexternas}

_Vídeo_* para crear 2 Wifis, Personal y Privada con QoS:[ https://www.youtube.com/watch?v=d1Dpyin-99M](%20https://www.youtube.com/watch?v=d1Dpyin-99M)*

_DD-WRT (firmware para el router): <http://www.dd-wrt.com/site/support/router-database>_

_Otro: [http://foro.seguridadwireless.net/dd-wrt/es-posible-habilitar-yo-utilizar-el-modo-repetidor-en-router-linksys-wrt160nl/](%20http://foro.seguridadwireless.net/dd-wrt/es-posible-habilitar-yo-utilizar-el-modo-repetidor-en-router-linksys-wrt160nl/)_

_Otro: [https://www.youtube.com/watch?v=Ud-Hq3kgvk4](%20http://foro.seguridadwireless.net/dd-wrt/es-posible-habilitar-yo-utilizar-el-modo-repetidor-en-router-linksys-wrt160nl/)_</p>