---
id: 15
title: 'No puedo actualizar wordpress [SOLUCIONADO] &#8211; Descarga fallida.: La carpeta de destino para cargar el archivo no existe o no tiene permisos de escritura'
date: 2013-07-15T20:02:26+00:00
author: aletsh
layout: post
guid: http://alejandroguerrero.es/2013/07/15/no-puedo-actualizar-wordpress-solucionado/
permalink: /no-puedo-actualizar-wordpress-solucionado/
categories:
  - Uncategorized
tags:
  - wordpress
---
Me acaba de ocurrir un error que seguro que a muchos de vosotros os ha podido pasar y lo quiero compartir para futuros <span style="text-decoration: line-through;">no-dolores</span> de cabeza.

Tras intentar actualizar una Web realizada con el CMS WordPress previamente migrado de un proveedor a otro distinto me daba el siguiente error:

`Descarga fallida.: La carpeta de destino para cargar el archivo no existe o no tiene permisos de escritura.`

En mi caso:

  * La carpeta si existe.
  * Y la carpeta destino tiene los permisos correctamente puestos.

Lo que ocurría es que el directorio “wp-content” no tiene la misma ruta en el proveedor-2 que del proveedor-1.

No entendéis nada ¿¡A que no!? Os lo detallo un poco más abajo;

El proveedor-1 administrado con cPanel tenia la ruta “/home/mi-user/public_html/content/images” y el proveedor-2 tiene la ruta /var/www/virtual/mi-user/htdocs/content/images”.

Esta ruta está detallada en el archivo “wp-config.php” alojado en la raiz del WordPress.

Tenéis que buscar la línea con el texto (en mi caso esta en la línea #46):

`define('WP_TEMP_DIR',...)`

Cuando identifiquéis la línea modificad la parte de la ruta. En mi caso quedaría así:

`define('WP_TEMP_DIR', '/var/www/virtual/miweb.org/htdocs/content/images');`

Repito: Verificad bien la ruta si no os continuará dando el maravilloso error.

Una vez editado el archivo “wp-config.php” guardadlo y reemplazarlo por el que teneis en la raiz.

Edito la entrada pese a los comentarios de algunos usuarios les ha ido genial lo que nos ha comentado nuestro compañero @pauloconde que comenta que podemos definir la linea de WP\_TEMP\_DIR de la siguiente forma:

`define('WP_TEMP_DIR', ABSPATH . 'content/images');`

Gracias @pauloconde por compartirlo.

Suerte a todos