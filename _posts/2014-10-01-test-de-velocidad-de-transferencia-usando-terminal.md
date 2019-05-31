---
id: 44
title: Test de velocidad de transferencia usando terminal
date: 2014-10-01T23:10:34+00:00
author: aletsh
layout: post
guid: http://alejandroguerrero.es/2014/10/01/test-de-velocidad-de-transferencia-usando-terminal/
permalink: /test-de-velocidad-de-transferencia-usando-terminal/
categories:
  - Uncategorized
tags:
  - Linux
  - speedtest
  - terminal
---
Pues bien, actualmente existe ya una aplicación llamada speedtest-cli, el cuál, es un sencillo cliente CLI y escrito en Phyton el cuál mide el ancho de banda de manera bi-direccional usando la infraestructura de SpeedTest, vale reseñar que este cliente funciona tanto en las versiones 2.4 como en la 3.4 de Phyton.

Para realizar la instalación y comenzar a usar speedtest-cli debemos realizar los siguientes pasos vía terminal:

descargamos e instalamos la aplicación

wget <https://raw.github.com/sivel/speedtest-cli/master/speedtest_cli.py> -O /usr/bin/speedtest-cli chmod +x /usr/bin/speedtest-cli

Esto automáticamente nos localizará el servidor mas cercano de Speedtest y realizará las funciones de subida/descarga.

[![speedtest-cli-1](http://i0.wp.com/libuntu.com/content/images/2014/01/speedtest-cli-1.jpg?zoom=3&resize=568%2C244)](http://i0.wp.com/libuntu.com/content/images/2014/01/speedtest-cli-1.jpg)

Si deseamos obtener una imágenes para luego compartirla en la web, simplemente añadimos la opción –share despues del comando speedtest-cli.

[![speedtest-cli-2](http://i1.wp.com/libuntu.com/content/images/2014/01/speedtest-cli-2.jpg?zoom=3&resize=568%2C240)](http://i1.wp.com/libuntu.com/content/images/2014/01/speedtest-cli-2.jpg)

Si deseamos obtener resultados de un servidor distinto, debemos seleccionarlo manualmente, para ello agregamos la opción –list después del comando speedtest-cli (esto nos mostrara varios servidores ubicados geográficamente)

[![speedtest-cli-3](http://i2.wp.com/libuntu.com/content/images/2014/01/speedtest-cli-3.jpg?zoom=3&resize=640%2C253)](http://i2.wp.com/libuntu.com/content/images/2014/01/speedtest-cli-3.jpg)

Vale destacar que estos servidores tienen un ID, por lo cuál, una vez que hallemos el servidor deseado, simplemente colocamos la opción –server seguido del ID del servidor seleccionado después del comando speedtest-cli

[![speedtest-cli-4](http://i0.wp.com/libuntu.com/content/images/2014/01/speedtest-cli-4.jpg?zoom=3&resize=579%2C184)](http://i0.wp.com/libuntu.com/content/images/2014/01/speedtest-cli-4.jpg)

[Via: http://www.libuntu.com](http://libuntu.com)