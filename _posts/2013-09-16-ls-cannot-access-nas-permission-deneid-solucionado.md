---
id: 19
title: 'ls: cannot access NAS: Permission deneid [SOLUCIONADO]'
date: 2013-09-16T20:23:07+00:00
author: aletsh
layout: post
guid: http://alejandroguerrero.es/2013/09/16/ls-cannot-access-nas-permission-deneid-solucionado/
permalink: /ls-cannot-access-nas-permission-deneid-solucionado/
categories:
  - Uncategorized
---
Hacia ya unos meses que tenia el [servidor en marcha](http://alejandroguerrero.es/presentacion-hp-proliant-microserver-n40l/ "Presentación HP Proliant Microserver N40L") y nunca me había pasado algo igual.

Tengo un NAS, un disco duro externo pero en vez de enchufarlo por USB a un equipo se enchufa con un cable de red RJ45 al router/switch/tarjeta de red.

Lo empleo para guardar una copia de seguridad incremental mediante imágenes del servidor.

Explicare brevemente lo que es una imagen de disco; en vez de guardar todos los archivos por separado se crea uno solo. Dicho archivo necesita de un software para ser generado, hay un montón en el mercado. Vale, tu empleas el WinRaR (con licencia xD) y el 7z, y guardas todos tus archivos importantes en uno único archivo… si! Ok! Pero aparte de que una imagen tenga varias ventajas, la mejor es la que llevo haciendo desde hace muchos años: Imagen completa separada en archivos de 4GB, y no explicare el porque, tal vez en un futuro, solo os diré una pista;

> Disco 1 cargado satisfactoriamente, Inserte el disco 2 y pulse Aceptar para continuar…

Pues después de todo este royo, el NAS tiene un directorio que lo comparto en NFS (no explicare lo que es, bueno os diré una pista: Wiki).

Volviendo al error, cuyo error me enteré por un mail que me mando el servidor (proxmox, muy moderno todo xD):

<div class="wlWriterEditableSmartContent" id="scid:812469c5-0cb0-4c63-8c15-c81123a09de7:93ed639a-b1d4-4ca7-8c12-1f931ef66d35" style="margin: 0px; display: inline; float: none; padding: 0px;">
  Asunto: ***** &#8211;quiet 1 &#8211;mode snapshot &#8211;mailto info@alejandroguerrero.es &#8211;node *NODE* &#8211;compress gzip &#8211;storage NAS Texto: unable to activate storage &#8216;NAS&#8217; &#8211; directory &#8216;/mnt/XXX/NAS&#8217; does not exist
</div>

Por algún motivo he tenido algún error que no se cual es y que en la consola del servidor al realizar un:

<div class="wlWriterEditableSmartContent" id="scid:812469c5-0cb0-4c63-8c15-c81123a09de7:9d62cef1-0306-4af4-b310-c14bc37b5eba" style="margin: 0px; display: inline; float: none; padding: 0px;">
  ls
</div>

en el directorio donde estaba montado mi NAS me aparecían interrogantes. Una cosa bastante rara.

También comprobé que el NAS funcionaba xD.

He reiniciado el servidor, lamentablemente es el TRUNK y no uno virtual:

<div class="wlWriterEditableSmartContent" id="scid:812469c5-0cb0-4c63-8c15-c81123a09de7:e407468d-77de-490f-bf19-dec35b2a2f75" style="margin: 0px; display: inline; float: none; padding: 0px;">
  shutdown -r now
</div>

Después de reiniciar (1 minuto) ya me aparecía bien los permisos del directorio y ya empezó ha realizar la copia de seguridad.

> Que sudores frios!