---
layout: post
published: true
title: Instalar Ubuntu 20.04 en Macbook air (con dual boot)
subtitle: Sencillos pasos para instalar ubuntu 20.04 en el MacBook Air sin perder macOS
---
Lista de anotaciones para tener Ubuntu en el Macbook air:
1. Crear particiones necesarias
2. Crear USB de arranque e instalar Ubuntu 20.04
3. Teclado de mac en Ubuntu 20.04
4. Trackpad de mac en Ubuntu 20.04

## Crear particiones necesarias
Crear particion con el disk utility en macOS para `swap` de 10gb por lo menos si tienes 8GB de ram y crear particion para `/`, yo lo hice de 20 GB. Tarda bastante en aplicar.

Opcionalmente, puedes crear una particion para `/home`.

## Crear USB de arranque e instalar Ubuntu 20.04
Descargar Ubuntu 20.04 desde la web oficial.

* Descargar Ubuntu desde aqui: [https://ubuntu.com/](https://ubuntu.com/)
* Aqui os dejo las versiones de archivo: [https://releases.ubuntu.com/](https://releases.ubuntu.com/)

Crear usb de arranque con la aplicacion Etcher ([www.etcher.io](https://www.etcher.io)). Es necesario tener un pen drive de mas de 8GB.

Una vez tengamos el USB listo apagar macbook.

Encender macbook air y pulsar tecla "alt" o "option" y esperar a que aparezcan los discos de arranque.
Seleccionar EFI-BOOT. Si aparecen dos seleccionar el que este mas a la izquierda.

Esperar a que arranque Ubuntu e  inslatarlo con el asistente, no es difícil.

Decir que la particion que hemos particionado antes para `swap` va a ser para el intercambio y la otra particion para `/` y si pusiste una particion para `/home` seleccionarla tambien. Ambas en formato ext4.
Existe un video que explica bastante bien los puntos anteriores: [thttps://www.youtube.com/watch?v=o30qsxv1CsM](https://www.youtube.com/watch?v=o30qsxv1CsM)
<iframe width="560" height="315" src="https://www.youtube.com/embed/o30qsxv1CsM" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

## Instalar Webcam facetimehd en Ubuntu 20.04

```
$ cd /etc/local/src
$ git clone https://github.com/patjak/bcwc_pcie.git
$ cd bcwc_pcie/firmware
$ sudo make
$ sudo make install
$ cd ..
$ sudo make
$ sudo install
$ sudo depmod
$ sudo modprobe -r bdc_pci
$ sudo modprobe facetimehd
```

Existe un gran articulo aquí: [https://florisvanbreugel.wordpress.com/2018/04/10/accessing-mac-webcam-in-ros-running-ubuntu-on-the-mac/](https://florisvanbreugel.wordpress.com/2018/04/10/accessing-mac-webcam-in-ros-running-ubuntu-on-the-mac/)

Iré poniendo mas `hacks`...

## Teclado de mac en Ubuntu 20.04
La distribucion del teclado de Ubuntu 20.04 no esta nada mal pero si te gusta mantener las combinaciones de teclas como los que estamos acostumbrados a `cmd + c` para copiar y `cmd + v` para pegar puedes ver estos sencillos pasos. Yo lo hice para, copiar, pegar, cortar, deshacer.

Instalar `Autokey`: 

```sudo apt install autokey```

Tengo la siguiente configuración: 
![autokey-alejandroguerrero-es-01]({{site.baseurl}}/img/autokey-alejandroguerrero-es-01.png)

Como se puede observar en la imagen he duplicado para todos los comandos lo mismo.

Si alguien tiene una forma de tener la combinacion de mac en ubuntu más facil, que me lo diga por twitter (@aletsh), esta es la que encontré recientemente. Si encuentro una mejor la publico.

## Trackpad de mac en Ubuntu 20.04
Instalar tweak:
``` sudo apt install tweak ```

### Activar boton derecho del trackpad del macbook air en Ubuntu 20.04
Abrir `retoques`:
En el menu de la izquierda seleccionar la opcion Teclado y Raton.
A la derecha ir a la opcion `Emulación de la pulsación con el ratón`:
Seleccionar: Area.
![tweak-01-alejandroguerrero-es]({{site.baseurl}}/img/tweak-01-alejandroguerrero-es.png)

### Activar gestos naturales como en macOS en Ubuntu 20.04
`Todo: investigando... si sabeis como twiteame!!`
