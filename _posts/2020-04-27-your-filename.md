---
layout: post
published: true
title: Instalar Ubuntu 20.04 en Macbook air (con dual boot)
subtitle: Sencillos pasos para instalar ubuntu 20.04 en el MacBook Air sin perder macOS
---
Lista de la compra:
1. Crear particiones necesarias
2. Crear USB de arranque e instalar Ubuntu 20.04
3. Instalar Webcam facetimehd en Ubuntu 20.04
4. Combinacion de teclas mac en Ubuntu 20.04

## Crear particiones necesarias
Crear particion con el disk utility en macOS para `swap` de 10gb por lo menos si tienes 8GB de ram y crear particion para "/", yo lo hice de 20 GB. Tarda bastante en aplicar.
Opcionalmente, puedes crear una particion para /home.

## Crear USB de arranque e instalar Ubuntu 20.04
Descargar ubuntu 20.04 desde la web oficial.
Crear usb de arranque con la aplicacion Etcher (www.etcher.io). Es necesario tener un pen drive de mas de 8GB.
Una vez tengamos el USB listo apagar macbook.
Encender macbook air y pulsar tecla "alt" o "option" y esperar a que aparezcan los discos de arranque.
Seleccionar EFI-BOOT. Si aparecen dos seleccionar el que este mas a la izquierda.
Esperar a que arranque Ubuntu.
Inslatar ubuntu con el asistente, no tiene mas misterio.
Decir que la particion que hemos particionado antes para `swap` va a ser para el intercambio y la otra particion para `/` y si pusiste una particion para /home seleccionarla tambien. Ambas en formato ext4.
Existe un video que explica bastante bien los puntos anteriores: https://www.youtube.com/watch?v=o30qsxv1CsM

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

Iré poniendo mas `hacks`...

## Teclado de mac en Ubuntu 20.04
La distribucion del teclado de Ubuntu 20.04 no esta nada mal pero si te gusta mantener las combinaciones de teclas como los que estamos acostumbrados a `cmd + c` para copiar y `cmd + v` para pegar puedes ver estos sencillos pasos. Yo lo hice para, copiar, pegar, cortar, deshacer.

Instalar `Autokey`: 
```sudo apt install autokey```

