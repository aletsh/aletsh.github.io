---
id: 37
title: USB Booteable
date: 2014-06-04T23:20:05+00:00
author: aletsh
layout: post
guid: http://alejandroguerrero.es/2014/06/04/usb-booteable/
permalink: /usb-booteable/
categories:
  - Uncategorized
tags:
  - booteable
  - usb
---
En este tutorial os voy a explicar en muy cómodos pasos como hacer un USB (Pen Drive) Booteable, hablando en cristiano: “arrancable” desde la POST BIOS, mas en cristiano aún: Para poder instalar cualquier Sistema Operativo/utilidad desde un USB como por ejemplo:

  * Sistemas operativos de la marca Microsoft
  * Sistemas operativos “Live”
  * Sistemas de copias de seguridad/Imágenes/Clonado de discos
  * …

Materiales para empezar:

  * Tener la la imagen del DVD/CD ISO creada (p.e: mi\_sistema\_operativo_favorito.iso).
  * Un Pen Drive con mayor capacidad que el fichero ISO. (p.e: Si la ISO ocupa 600 MB con un Pen drive de 1GB bastaría).
  * Descargar el [Installer (ver 1.1)](http://www.themudcrab.com/downloads/grubinst-1.1-bin-w32-2008-01-01.zip) del GruBDos.
  * Descargar desde aqui el [Grub4DOS – ver. 4.4 2009-03-31 Official Release](http://www.themudcrab.com/downloads/grub4dos-0.4.4-2009-03-31_(official_release).zip)<span style="color: #000000;"> .</span>

Ya lo tenemos todo! Manos a la obra!

  1. **Arranca** como “**Administrador**” el **archivo** que está en el **Installer**: “**grubinst_gui.exe”.**
  2. En la parte de “**DISK”** dale a \*\*REFRESH \*\*y abre el **desplegable** donde aparecerá tu **Pen Drive**. **Seleccionalo**!
  3. En la parte de **“Part List**” dale a **REFRESH** y **selecciona** en el desplegable<span style="color: #000000;"> </span>**Whole disk (MBR).**
  4. Más **abajo** a la derecha **Selecciona** “**Don’t search floppy**“.
  5. Pulsa botón “**Install**“.
  6. Aparecerá una ventana negra de MS-DOS, **aprieta** la tencla “**ENTER**” y se cerrará la ventana negra.
  7. Abre la carpeta “grub4dos-0.4.4…”
  8. **Copia** y **Pega** el archivo “**grldr**” de la carpeta “**grub4dos-0.4.4…**” al “**Pen Drive**“.
  9. Crea dentro del Pen Drive el archivo “\*\*menu.lst” \*\*con el **siguiente\****contenido**:
 10. timeout 10 default 0 title Acronis True Image Home 2009 (9,615) map (hd0,0)/AQUI\_TU\_TITULO\_DE\_LA_ISO.iso (hd32) map &#8211;hook chainloader (hd32) boot title CommandLine commandline title Reboot reboot title Halt halt
 11. **Renombra\****en** el archivo “**menu.lst**” la parte donde pongo: “**AQUI\_TU\_TITULO\_DE\_LA_ISO.iso**” **por** el **nombre** real\*\* de tu\*\* archivo .**ISO**

Os pongo unsa imagenes para que sea mas intuitivo y no tan “lista de la compra”:<figure class="wp-caption aligncenter" id="attachment_774" style="max-width: 439px">\[![\](/content/images/2014/06/grub4dos01.jpg)](/content/images/2014/06/grub4dos01.jpg)<figcaption class="wp-caption-text">USB Booteable</figcaption></figure> 

\[![grub4dos02\](/content/images/2014/06/grub4dos02.jpg)](/content/images/2014/06/grub4dos02.jpg)

[![grub4dos03](/content/images/2014/06/grub4dos03.jpg)](/content/images/2014/06/grub4dos03.jpg)

[![grub4dos04](/content/images/2014/06/grub4dos04.jpg)](/content/images/2014/06/grub4dos04.jpg)

[![grub4dos05](/content/images/2014/06/grub4dos05.jpg)](/content/images/2014/06/grub4dos05.jpg)

[![grub4dos06](/content/images/2014/06/grub4dos06.jpg)](/content/images/2014/06/grub4dos06.jpg)

[![grub4dos07](/content/images/2014/06/grub4dos07.jpg)](/content/images/2014/06/grub4dos07.jpg)

[![grub4dos08](/content/images/2014/06/grub4dos08.jpg)](/content/images/2014/06/grub4dos08.jpg)

[![grub4dos09](/content/images/2014/06/grub4dos09.jpg)](/content/images/2014/06/grub4dos09.jpg)

[![grub4dos10](/content/images/2014/06/grub4dos10.jpg)](/content/images/2014/06/grub4dos10.jpg)

[![grub4dos12](/content/images/2014/06/grub4dos12.jpg)](/content/images/2014/06/grub4dos12.jpg)

[![grub4dos13](/content/images/2014/06/grub4dos13.jpg)](/content/images/2014/06/grub4dos13.jpg)</p> 

Listo!

**Si no eres experto sigue leyendo:**

Ahora te toca arrancar el ordenador desde el Pen Drive. Con alguna placas modernas no es necesario entrar en la BIOS y cambiar la configuración ya que se puede hacer apretando las teclas de funcion del teclado como por ejemplo el “F9” (para placas MSI) y aparecerá un listado con las opciones que permite la placa arrancar.

Recomendación: para que en el listado de arranca de la placa aparezca vuestro Pen drive teneis que reiniciar el ordenador con el Pen Drive insertado.</p> 

_Biografia de enlaces externos: <http://www.themudcrab.com/acronis_grub4dos.php#tagInstall>_</p> 

> No me hago responsable de un uso indebido del hardware o software