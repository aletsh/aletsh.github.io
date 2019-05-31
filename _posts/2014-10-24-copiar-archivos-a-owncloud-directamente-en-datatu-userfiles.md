---
id: 47
title: 'Copiar archivos a Owncloud (directamente en /data/{tu-user}/files/)'
date: 2014-10-24T00:26:42+00:00
author: aletsh
layout: post
guid: http://alejandroguerrero.es/2014/10/24/copiar-archivos-a-owncloud-directamente-en-datatu-userfiles/
permalink: /copiar-archivos-a-owncloud-directamente-en-datatu-userfiles/
categories:
  - Uncategorized
tags:
  - Linux
  - owncloud
  - rsync
  - ubuntu
---
Es posbile copiar archivos de un servidor a otro empleando por ejemplo el famoso comando “scp” o “rsync”.

Cuando se emplea estos comandos Owncloud no sabe que hemos introducir esos archivos en su arbol de ficheros por lo tanto si no vemos los archivos que hemos copiado en la web de OwnCloud no os preocupeis es normal –> tenemos que eliminar la cache de la base de datos. Tarea fácil ya vereis

  1. Copia los archivos deseados desde la propia maquina OwnCloud (usb, discoduro), desde servidor remoto dentro de: /tu/raiz/de/archivos/owncloud/data/{tu-usuario}/files
  2. Cambia los permisos de ese directorio y subdirectorios: chown -R www-data:www-data /tu/nuevo/directorio
  3. Ahora toca Trunca la tabla de la base de datos (busca por ahi que significa truncar tabla base de datos… ;-)): mysql -u {tu-user} -p &#8211;>password: \***** mysql> show database; mysql> use owncloud-data-base; mysql> TRUNCATE Table oc_filecache; mysql> exit;
  4. Cierra sesion de OwnCloud y vuelve a acceder.
  5. Ahora podrás ver los archivos que has copiado recientemente

Si vais a copiar muchos archivos habitualmente posiblemente deberiais montar una carpeta dedicada para ello en vuesta maquina linux de origen;

Crea un montaje desde OwnCloud protocolo WebDav:

mkdir /media/{nombre-carpeta}:archivos-de-owncloud mount -t davfs <https://ip-servidor/owncloud/files/webdav.php> /media/archivos-de-owncloud/ rsync -ravz &#8211;progress /tu/directorio/local/ /media/archivos-de-owncloud/

Espero que con esto os ayude.

> No me hago responsable de ningun borrado/modificado/maltrato de vuestros sistemas/archivos