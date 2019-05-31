---
id: 14
title: Comando FTP en Linux
date: 2013-07-04T18:41:02+00:00
author: aletsh
layout: post
guid: http://alejandroguerrero.es/2013/07/04/comando-ftp-en-linux/
permalink: /comando-ftp-en-linux/
categories:
  - Uncategorized
---
Hay veces que necesitamos conectarnos desde la terminal a un servidor FTP. Os pongo un caso practico que estuve haciendo hace unos instantes.

Necesitaba descargar el Windows Server 2008 R2 para instalarlo en un Proxmox (de forma virtualizada).

Lo que no quería hacer es:

  * Bajar el Windows a mi equipo.
  * Subirlo vía web al proxmox

Así que dije, como el equipo que se lo bajo es un virtualizado del proxmox, lo quiero pasar de máquina virtual a otra maquina virtual. Así que lo haré en la misma máquina.

Vamos a ello!

Os pondré un ejemplo de lo que tengo montado:

  * Máquina física con el ProxMox instalado: 10.30.100.100
  * Maquina virtual con FTP: 10.30.100.101

En este caso me conecto desde x.x.x.100 al x.x.x.101 por FTP:

<div class="wlWriterEditableSmartContent" id="scid:812469c5-0cb0-4c63-8c15-c81123a09de7:8ebb47d8-4fb3-499a-bae0-728a84aceb6c" style="margin: 0px; display: inline; float: none; padding: 0px;">
  # ftp 10.30.100.101 # Connected to 10.30.100.101 220 ProFTPD 1.3.3a Server (ftp) [::ffff:10.30.100.101] Name (10.30.100.101:root): {USUARIO} 331 Password required for {USUARIO} Password: <PASSWORD DE "USUARIO" /> 230-Welcome user USUARIO}@::ffff:10.30.100.100 to 127.0.1.1 FTP server. 230-The local time is: Thu Jul 04 18:22:52 2013 230 User {USUARIO} logged in Remote system type is UNIX. Using binary mode to transfer files.
</div>

Ya estamos conectados!

Lista de comandos:

  * “ls”: listar archivos
  * “cd”: cambiar de directorio
  * “get archivo-a-descargar.zip el-nombre-que-yo-quiera.zip”: Se descarga el archivo en el directorio donde insertamos el comando “ftp ip [puerto]”
  * “mget”: Descargar multiples archivos &#8211; Ej. para descargar todas las imagenes que acaben en “iso”: <div class="wlWriterEditableSmartContent" id="scid:812469c5-0cb0-4c63-8c15-c81123a09de7:a33847e4-a820-45e1-bd68-781345311e28" style="margin: 0px; display: inline; float: none; padding: 0px;">
      ftp> mget *iso</li> </ul>
    </div>
    
    &#8211; “put”: Subir un archivo  
    &#8211; “mput”: Subir multiples archivos  
    &#8211; “lcd”: Cambiar directorio local.  
    &#8211; “lpwd”: Muestra por pantalla el directorio donde nos encontramos localemnte.  
    &#8211; “quit” o “bye”: Cierra la sesion ftp.
    
    Espero que este comando os sea de gran utilidad.
    
    salu2
    
    😉
    
    Mas información:
    
      * <http://www.faqs.org/docs/Linux-mini/FTP.html>
      * <http://www.cyberciti.biz/faq/linux-unix-ftp-commands/>