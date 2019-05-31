---
id: 9
title: Montar carpeta compartida (SMB), en Linux
date: 2013-06-11T20:41:20+00:00
author: aletsh
layout: post
guid: http://alejandroguerrero.es/2013/06/11/montar-carpeta-compartida-smb-en-linux/
permalink: /montar-carpeta-compartida-smb-en-linux/
categories:
  - Uncategorized
---
SMB, o SAMBA protocolo para compartir archivos con equipos que tengan el S.O de Microsoft a través de nuestras distribuciones Linux.

Ya! ya lo sé, SMB es anticuado y ahora es CIFS pero no entraré en detalle ahora.

Como en un [post anterior](http://alejandroguerrero.es/crear-modificar-particion-en-linux/) expliqué como montar una partición en nuestro Linux hoy toca saber como montar una carpeta compartida de otro equipo (NAS o PC) por si necesitamos hacer alguna copia de seguridad.

Primeramente necesitaremos saber **la IP** del recurso y el **nombre del directorio** compartido.

> En este ejemplo yo tengo un disco duro externo conectado por red (comúnmente llamado NAS) si, ya sé que en catalán es una parte de la cara pero dejemos las bromas a parte.

Vamos a ello:

Para la instalación necesitaremos ‘smbclient’ y ‘smbfs’:

# aptitude <span class="kwrd">update</span> # aptitude safe-<span class="kwrd">update</span> # aptitude install smbclient smbfs {#aptitudespanclasskwrdupdatespanaptitudesafespanclasskwrdupdatespanaptitudeinstallsmbclientsmbfs}

Ahora toca montar el disco:

# mount -t smbfs [//ip.del.recurso.compartido/nombre\_del\_directorio](//ip.del.recurso.compartido/nombre_del_directorio) /media/windows-pc -o <span class="kwrd">user</span>=tu-usuario-del-recurso-compartido # password: (mientras escribes la contraseña <span class="kwrd">no</span> se ven los caracteres) {#mounttsmbfsipdelrecursocompartidonombre_del_directoriomediawindowspcospanclasskwrduserspantuusuariodelrecursocompartidopasswordmientrasescribeslacontraseaspanclasskwrdnospansevenloscaracteres}

 

Para verificar que esta montada podemos hacer lo siguiente:

# cd /media/windows-pc # ls -l {#cdmediawindowspclsl}

O hacer lo siguiente:

# df -h {#dfh}

Listo calisto!