---
id: 21
title: 'Raspberry Pi &#8211; Ten tu propio NAS de bajo coste'
date: 2018-09-18T15:13:36+00:00
author: aletsh
layout: post
guid: http://alejandroguerrero.es/2018/09/18/raspberry-pi-4-nas-bajo-coste/
permalink: /raspberry-pi-4-nas-bajo-coste/
categories:
  - Uncategorized
tags:
  - nas
  - raspberry
  - raspbian
  - raspi
---
## Introducción {#introduccin}

En este tutorial os enseñaré a montar un NAS, esto es un disco duro compartido en red, para por ejemplo tener un disco duro desde el que poder acceder desde todos los ordenadores conectados a la red de tu casa. Es una idea inteligente tenerlo montado en nuestra raspi, ya que si lo necesitamos tenerlo todo el día encendido, al no consumir mucha energía nos ahorramos mucho dinero, por lo cual tendremos una solución NAS muy económica.

## ¿Qué necesitamos? {#qunecesitamos}

– Un disco duro externo de 3.5 o 2.5 pulgadas

– Un hub usb por si no tenemos puertos libres (con toma de corriente si tenemos un disco de 2.5″, ya que por los usb’s de la raspberry solo salen 100mA, y no bastan). Yo personalmente uso éste:&nbsp;<http://www.conceptronic.net/es/product.php?id=15&linkid=16>

## Preparando el disco {#preparandoeldisco}

Primero necesitaremos formatear nuestro disco con el formato que más nos guste. Yo personalmente prefiero ext4 por su rapidez de acceso (tranquilos que luego los podremos usar en cualquier linux, mac o windows a través de la red sin necesidad de ningún programa o extensión).

Si os habéis decantado por NTFS deberéis primero instalar el soporte para dicho formato:

`sudo apt-get install ntfs-3g`

Luego miraremos a qué letra corresponde nuestro disco:

`sudo fdisk -l`

Los dos primeros discos que empiezan por “mmc” son las 2 particiones que tiene vuestra sd:

![](http://cdn.howtogeek.com/content/images/2013/02/2013-02-28_110924.jpg "2013-02-28_110924") 

En este caso hay 2 discos externos con una partición cada una correspondientes a sda1 y sdb1

Primero tendremos que crear la carpeta donde se montarán (se mostrará el contenido de) los discos:

`sudo mkdir /media/USBHDD1`

Montamos nuestro disco en el punto de montaje anteriormente creado:

`sudo mount -t auto /dev/sda1 /media/USBHDD1`

## Configurando samba {#configurandosamba}

Ahora instalaremos samba, que nos permitirá visualizar el disco en nuestra red:

`sudo apt-get install samba samba-common-bin`

Hacemos una copia de nuestro fichero de configuración de samba por si las moscas:

`sudo cp /etc/samba/smb.conf /etc/samba/smb.conf.old`

Editamos el fichero de configuración:

`sudo nano /etc/samba/smb.conf`

Esto abrirá el editor de textos nano con ese fichero:

![](http://cdn.howtogeek.com/content/images/2013/02/2013-02-28_121208.jpg "2013-02-28_121208") 

Te encontrarás con un montón de configuraciones, pero solo nos interesan unas pocas.

La primera es el identificador del grupo de trabajo, por defecto workgroup = WORKGROUP. Si usas otro nombre de grupo de trabajo, aquí es donde tienes que cambiarlo, si usas el por defecto déjalo como está.

Ahora habilitaremos la autenticación mediante usuario, bajamos en el fichero hasta encontrarnos con ésta linea:

![](http://cdn.howtogeek.com/content/images/2013/02/2013-02-28_122716.jpg "2013-02-28_122716") 

Quitamos el símbolo # para habilitar la autenticación mediante usuario/contraseña al servidor samba.

Ahora bajamos hasta el final de todo e introducimos las siguientes lineas de texto. Esto nos creará una carpeta (en este caso todo nuestro disco duro externo) compartida en nuestra red :

    [Backup]<br></br>
    comment = Backup Folder<br></br>
    path = /media/USBHDD1<br></br>
    valid users = @users<br></br>
    force group = users<br></br>
    create mask = 0660<br></br>
    directory mask = 0771<br></br>
    read only = no
    

El nombre entre corchetes será el nombre de la carpeta compartida que aparecerá en los otros ordenadores de la red. Con el parámetro path indicamos qué ruta se compartirá en esa carpeta.

Con CTRL+X salimos y presionamos Y para guardar. Reiniciamos el servidor samba:

`sudo /etc/init.d/samba restart`

Creamos un usuario para el servidor samba dentro del grupo users, y con passwd le añadimos una contraseña:

`sudo useradd backups -m -G users`

`sudo passwd backups`

Luego añadimos el usuario creado anteriormente a los usuarios de samba:

`sudo smbpasswd -a backups`

Podemos observar el resultado en cualquier máquina que soporte samba, por ejemplo en windows:

![](http://cdn.howtogeek.com/content/images/2013/02/2013-02-28_130015.jpg "2013-02-28_130015") 

Donde nos pedirá el usuario y contraseña que hemos creado anteriormente al entrar en la carpeta.

Podemos probar de crear un fichero desde windows:

![](http://cdn.howtogeek.com/content/images/2013/02/2013-02-28_130916.jpg "2013-02-28_130916") 

Y verificamos que efectivamente se ha creado en nuestro disco duro compartido:

`cd /media/USBHDD1/shares`  
`ls`

![](http://cdn.howtogeek.com/content/images/2013/02/2013-02-28_131328.jpg "2013-02-28_131328") 

## Automontado de discos {#automontadodediscos}

Una vez comprobado que todo funciona como toca, hay que configurar el fstab para que nos monte automáticamente el disco al arranque de la raspi:

`sudo nano /etc/fstab`

Añadimos la siguiente línea al fichero:

`/dev/sda1 /media/USBHDD1 auto noatime 0 0`

Y guardamos. Listo! Ya tenemos nuestro NAS configurado!!

## Reinicio automático del sistema {#reinicioautomticodelsistema}

Os parecerá raro, pero en la raspberry hay un error muy común, por el cual pasado un tiempo de inactividad del disco duro, por alguna extraña razón, la raspi desmonta y vuelve a montar nuestro disco en un punto distindo (de sda, pasa a estar en sdb). A mi me ha llegado a durar como algo más de 2 días sin que se me desmonte el disco. En otras páginas echan la culpa al disco duro, o al hub, pero no son causas muy convincentes. Una solución chapuzera pero efectiva es reiniciar la raspi cada día, a una hora a la que estemos seguros de que no la estaremos utilizando, por ejemplo a las 4.00 de la mañana (si sois muy frikis y a esas horas la estáis usando, pensad en una hora en la que normalmente estéis durmiendo 😉 ). Para eso programaremos un reinicio automático del sistema mediante el crontab.

Editamos el crontab

`sudo crontab -e`

Debajo del todo insertaremos la siguiente línea

`0 4 * * * /sbin/shutdown -r +5`

Con el &#171;+5&#187; avisariamos a posibles usuarios activos que en 5 minutos está programado un reinicio automático del sistema.

Enjoy!

#### Bibliografía {#bibliografa}

Imagen de este post: <https://www.youtube.com/watch?v=B7HXX6HGUJA>