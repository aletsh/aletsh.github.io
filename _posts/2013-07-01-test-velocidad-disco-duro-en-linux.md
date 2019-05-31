---
id: 13
title: Test velocidad Disco Duro en Linux
date: 2013-07-01T12:23:41+00:00
author: aletsh
layout: post
guid: http://alejandroguerrero.es/2013/07/01/test-velocidad-disco-duro-en-linux/
permalink: /test-velocidad-disco-duro-en-linux/
categories:
  - Uncategorized
---
Esta entrada viene relacionada por varios motivos:

  * <span style="line-height: 13px;">Mucha demora al realizar una copia de seguridad en un disco duro externo conectado por USB.</span>
  * Error I/O al acceder a la ruta donde esta montado el disco duro por USB.
  * Que a [David](http://facebook.com/djdavidalexa "David Carrizo Alexa") (Colaborador de este blog) no pueda acceder a sus archivos de OwnCloud porque en la pantalla de Login le aparece un error xD.

Como tengo una mini-lista de casos, explicaré breve mente lo que he realizado para solventar el problema.

  1. <span style="line-height: 13px;">Reiniciar el sistema. En mi caso un 100% de veces se ha solucionado.</span>
  2. Si aún así va lento el proceso de copia de seguridad, instalar el “hdparm” para realizar un test de velocidad del disco duro:&#171;\` 
    </br></li> </ol> 
    
    # apt-get install hdparm  
    </br> {#aptgetinstallhdparmbrbr}
    
    # hdparm -tT /dev/sdaX  
    </br> {#hdparmttdevsdaxbrbr}
    
    Mostrará algo parecido a esto:  
    </br>  
    /dev/sda:  
    </br>  
    Timing cached reads: 29084 MB in 2.00 seconds = 14574.71 MB/sec  
    </br>  
    Timing buffered disk reads: 308 MB in 3.01 seconds = 102.36 MB/sec  
    </br>`3. Reiniciar los USB’s de la placa base:`
    
    </br>  
    $ cc usbreset.c -o usbreset  
    </br>  
    $ lsusb  
    </br>  
    Bus 002 Device 003: ID 0fe9:9010 DVICO  
    </br>  
    $ chmod +x usbreset  
    </br>  
    $ sudo ./usbreset /dev/bus/usb/002/003  
    </br>&#171;\`
    
    Con estas 3 soluciones he podido resolver los problemas.
    
    Si en un futuro veo mas soluciones para solventar este tipo de problemas iré editando la entrada.