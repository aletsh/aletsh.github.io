---
id: 48
title: 'Error 404 al pagar con Paypal en Prestashop [SOLUCIONADO]'
date: 2014-12-07T14:04:12+00:00
author: aletsh
layout: post
guid: http://alejandroguerrero.es/2014/12/07/error-404-al-pagar-con-paypal-en-prestashop-solucionado/
permalink: /error-404-al-pagar-con-paypal-en-prestashop-solucionado/
categories:
  - Uncategorized
tags:
  - "404"
  - error
  - paypal
---
En muchas ocasiones estuve “Googleando” sobre el mismo tema cada vez que construyo una pagina en Prestashop.

En este caso usaba la version 1.6.

El error se produce cuando quieres pagar mediante el método de pago Paypal y la siguiente pantalla que aparece es un error 404.

Para solventar esto se necesita:

  * Acceder al ftp del Hosting / VPS
  * Entrar en la carpeta “Modules”
  * Buscar “Paypal”
  * Cuando tengamos localizada la carpeta cambiarle los presimos por los siguientes: &#8211; Carpeta de Paypal: 755
  * Carpertas interiores: 755
  * Archivos: 644

Con esto se soluciona el problema y al pulsar sobre el pago “Paypal” redirecciona correctamente a la Web de Paypal.