---
id: 32
title: Restaurar máquina virtual en Proxmox a partir de un Backup
date: 2014-05-12T00:24:41+00:00
author: aletsh
layout: post
guid: http://alejandroguerrero.es/2014/05/12/restaurar-maquina-virtual-en-proxmox-a-partir-de-un-backup/
permalink: /restaurar-maquina-virtual-en-proxmox-a-partir-de-un-backup/
categories:
  - Uncategorized
tags:
  - Linux
  - proxmox
  - restore
  - virtual machine
---
Los de sistemas ya sabéis y bien, si una cosa funciona no la actualicéis

_…<<Si funciona no lo toques>>…_

Pues bien, como soy un manazas he tenido un par de problemas con una maquina virtual ya que he actualizado un sistema operativo y dicha máquina estaba en producción.  
Y que ha ocurrido: Que ha fallado la actualización de nuestro amigo APT o eso creo yo!

Tras mucho “Guglear”, leer, postear en foros, perder el domingo entero, comer a las cinco de la tarde… emmm… bueno, los que se dedican a estas cosas no se si comen xD…

He decidido hacer un roll-back y quedarme mas tranquilo gracias a las super copias de seguridad que a veces por no decir casi siempre nos dan problemas.

Voy a poner una mini-guia que me ayudará para futuros Rool Back de máquinas virtuales.

Para realizar la restauración se necesita:

  * La copia de seguridad a la vista en el Proxmox Web GUI
  * Parar la maquina virtual a restaurar
  * Paz y ciencia xD

La maquina que voy a restaurar es:

  * Una VM Con 5GB de disco duro local
  * Sistema operativo: Open Media Vault
  * Un Disco duro de 1TB (VirtIO y en formato RAW)
  * 1 Socket de 2 cores

Comienzo:

  * Seleccionar el VM a restaurar de nuestro arbol de VM’s (parte izquierda)
  * Clic en la pestaña “Respaldo”
  * Seleccionar “bien bien” el nombre de la copia de seguridad (mirar el ID)
  * En el asistente seleccionar que hay que restaurarlo en “Local”
  * Restaurar
  * Esperar (comer, merendar, cenar, dormir…)

[![proxmox-restore-vm](/content/images/2014/05/proxmox-restore-vm.png)](/content/images/2014/05/proxmox-restore-vm.png)  
Una vez restaurada acceder a la VM por terminal y listar los discos duros:

# fdisk -l {#fdiskl}

No aparece el disco.  
A continuacion editar el archivo _/etc/pve/local/qemu-server/XXX.conf_ (en mi caso 104.conf):

# nano /etc/pve/local/qemu-server/104.conf {#nanoetcpvelocalqemuserver104conf}

Modificar esta linea:

# virtio0%3A NAS%3A101/vm-101-disk-2.raw,format=raw,backup=no,size=1000G" {#virtio03anas3a101vm101disk2rawformatrawbackupnosize1000g}

Por esta:

"virtio0: NAS:101/vm-101-disk-2.raw,format=raw,backup=no,size=1000G"

Reiniciar la VM

Despues reiniciar el nodo el disco duro de 1TB que era mi problema vuelve a funcionar a la perfección.

Una vez tengamos todas las instacias iniciadas o al menos la de nuestra VM accedemos al Open Media Vault desde Web.  
Reiniciar todos los servicios.

Y todo vuelve a funcionar a la perfeccion

Si se os ocurre alguna otra idea será bienvenida y publicada en este post.

> Atención:  Esta guia no hace referencia a la configuración que tengas tu en tu maquina y tampoco me hago responsable de la perdida de datos. Este blog/post es un ejemplo.