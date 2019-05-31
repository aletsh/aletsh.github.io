---
id: 8
title: Crear/Modificar Partición, en Linux
date: 2013-06-10T21:28:21+00:00
author: aletsh
layout: post
guid: http://alejandroguerrero.es/2013/06/10/crear-modificar-particion-en-linux/
permalink: /crear-modificar-particion-en-linux/
categories:
  - Uncategorized
---
He ido a comprar un disco duro el cual quiero ponerlo en mi servidor que tiene el S.O Linux (Debian) (en otros post reflejare como lo monté).

Apago el servidor ya que no tengo sistema Hot Swap.

Una vez iniciada la sesión con un usuario (root) procedo a realizar lo siguiente:

<div class="csharpcode">
  # fdisk -l</p>
</div> Aparecen unos resultados del tipo (pero un poco distinto ya que este ejemplo es de un disco con la partición creada):</p> 

<div class="csharpcode">
  Disk /dev/sdb: 1000.2 GB, 1000204886016 bytes 
  
  <p>
    255 heads, 63 sectors/track, 121601 cylinders, total 1953525168 sectors
  </p>
  
  <p>
    Units = sectors of 1 * 512 = 512 bytes
  </p>
  
  <p>
    Sector size (logical/physical): 512 bytes / 4096 bytes
  </p>
  
  <p>
    I/O size (minimum/optimal): 4096 bytes / 4096 bytes
  </p>
  
  <p>
    Disk identifier: 0x00000000
  </p>
  
  <p>
    Device Boot Start End Blocks Id System
  </p>
  
  <p>
    /dev/sdb1 63 1953525167 976762552+ 83 Linux
  </p>
  
  <p>
    Partition 1 does not start on physical sector boundary.
  </p>
</div> A continuación realizamos lo siguiente (sabiendo que sdb1 es mi disco duro nuevo): 

<div class="csharpcode">
  # cfdisk /dev/sdb1
</div> Aparece un asistente el cual deberemos dar a: 

New Primary Write Exit

A continuación lo formateamos y lo montamos:

# mkfs.ext3 /dev/sdb1 # mount -t ext3 /dev/sdb1 /punto/de/montaje {#mkfsext3devsdb1mounttext3devsdb1puntodemontaje}

Para que sea permanente el punto de montaje deberemos insertar la siguiente linea en “/etc/fstab” mediante el comando “vi” o “nano”:

<span class="rem"># vi /etc/fstab</span> # /dev/sdb1 /nuestro/punto/de/montaje ext3 <span class="kwrd">default</span> 1 2

Listo calisto!</p>