---
layout: post
id: 59
title: DNS Dinámica con Cloudflare (ddclient)
date: 'Wed Jan 06 2016 21:33:39 GMT+0100 (hora estándar de Europa central)'
author: aletsh
guid: 'http://alejandroguerrero.es/2016/01/06/ddclient-cloudflare/'
permalink: /ddclient-cloudflare/
categories:
  - Uncategorized
tags:
  - cloudflare
  - ddclient
  - dinamic
  - dns
  - dyndns
  - namecheap
  - no-ip
published: true
---
Si eres de esos que tiene algún servicio de red en casa el cual quieres mantener desde fuera, seguramente habrás empleado un nombre de dominio ya que la IP de tu casa va cambiando bastante a menudo.

Bien para eso se inventó las DNS Dinamicas que ya sabréis; no-ip.org, dyndns etc. Lo malo de estas es que si no quieres pagar te dan un nombre de dominio propio que a veces es un poco engorroso pero a la vez cómodo.

Como la mayoría de nosotros ya tenemos un nombre de dominio alojado en algún lugar os propongo una solución para que vuestro dominio apunte a la ip de vuestra casa / oficina siempre y no pensar más en cambiar la ip manualmente desde el panel de DNS.

Yo he empleado el servicio que ofrece Namecheap pero se que se puede hacer algo parecido con OVH.

No voy a postear un tutorial solo un listado de cosas que hacer ya que el tutorial está muy bien explicado en la web.

Para proceder necesitaremos crearnos una cuenta en namecheap.com y comprar o que nos transfieran un dominio, en su lugar algun amiguete que tenga vuestro dominio os puede dar permisos para poder administrarlo y que pague él 😉

## Instalar DDClient {#instalarddclient}

`apt-get update && apt-get install ddclient`

## Parar DDClient {#pararddclient}

`service ddclient stop # /etc/init.d/ddclient stop`

## Ejecutar DDClient {#ejecutarddclient}

`service ddclient start # /etc/init.d/ddclient start`

## Reiniciar DDClient {#reiniciarddclient}

`service ddclient restart {forze-restart} # /etc/init.d/ddclient restart {forze-restart}`

## Uso de Logs

Para ver que DDClient a funcionado correctamente podemos ver el log de esta manera:

`cat /var/log/daemon.log`

`tail -f /var/log/daemon.log | grep ddclient`

Para hacer una prueba cambiaremos desde el panel de DNS la IP. Le podemos poner cualquier numero entre 0 y 255 😉

Una vez cambiado vamos a proceder a ejecutar ddclient y ver si la configuración es correcta.

1. Paramos el servicio service:
`ddclient stop`

2. Borramos la cache de DDClient 
`rm /var/cache/ddclient/ddclient.cache` 
3. Arrancamos el servicio de nuevo
`service ddclient start`

Podemos tener en un terminal el $tail ejecutandose y realizar la operacion anterior y veremos algo parecido a este log:

`Jan 6 20:08:38 px ddclient[378481]: SUCCESS: updating www: good: IP address set to tu.ip.aparecera.aqui`

De lo contrario aparecerá de esta manera (ejemplo de mal host):

`Jan 6 20:08:05 px ddclient[324059]: FAILED: updating @: Invalid reply.`

Para realizar pruebas siempre recomiendo borrar la cache de ddclient y emplear la ejecucion manual:

`rm /var/cache/ddclient.cache ddclient -daemon=0 -debug -verbose -noquiet</p>`

# ddclient para CloudFlare {#ddclientparacloudflare}

Vamos a configurar ddclient para actualizar la ip tal y como si fuese un DDNS pero esta vez para cloudflare.

Si ya tienes una cuenta en CloudFlare continua leyendo 😉

Si no tienes _ddclient_ instalado, instálalo;

`apt-get update && apt-get install ddclient`

Mira si existe algún cache en el directorio `_/var/cache/ddclient_` si es así bórralo.

`rm /var/cache/ddclient.cache`

Hay que instalar un parche para que el parámetro ‘_protocol_‘ que va dentro del _ddclient.conf_ acepte ‘_cloudflare_‘ como valor.

Para ello hay que descargarse un parche y aplicarlo:

`sudo apt-get install curl libjson-any-perl libio-socket-ssl-perl curl -O <http://blog.peter-r.co.uk/uploads/ddclient-3.8.0-cloudflare-22-6-2014.patch> sudo patch /usr/sbin/ddclient < ddclient-3.8.0-cloudflare-22-6-2014.patch`

Editar el archivo de configuración ‘_/etc/ddclient.conf’_:

`nano /etc/ddclient.conf
ssl=yes 
use=web, 
web=dyndns 
protocol=cloudflare, 
server=www.cloudflare.com, 
zone=tudominio.com, 
login=TUEMAIL@foo.com
password=TU-API-DE-CLOUDFLARE TU-SUPER-DOMINIO.com`

Para saber la API de cloudflare tendremos que acceder a nuestro perfil de cloudflare y bajar la pagina hasta que encontremos la generacion de la API KEY.

Para probar nuestra configuración lo que voy hacer va a ser editar mi IP de cloudflare, lo pondré apuntando a 99.99.99.99

Ahora ejecutaremos nuestro `ddclient` de forma manual, mas abajo se describe como ponerlo en modo automático (demonio o daemon):

`ddclient -daemon=0 -debug -verbose -noquiet`

La respuesta final tiene que ser algo parecido a esto:

`SUCCESS: alejandroguerrero.es Updated Successfully to bla.bla.bla.206`

Ahora toca poner ddclient en modo demonio.

## Crear demonio para DDClient {#creardemonioparaddclient}

Editamos y guardamos el archivo /etc/default/ddclient

`nano /etc/default/ddclient` 

`daemon_interval="600"`

Comprobamos que el servicio funciona:

`service ddclient start # /etc/init.d/ddclient start`

## Bibliografía: {#bibliografa}

  * <http://sourceforge.net/p/ddclient/wiki/Home/>
  * <https://www.namecheap.com/support/knowledgebase/article.aspx/583/11/how-do-i-configure-ddclient>
  * <https://www.cloudflare.com/resources-downloads/>
  * <http://www.ubuntugeek.com/how-to-use-cloudflare-as-a-ddclient-provider-under-ubuntu.html>

Enjoy!

😉

PD: Gracias por la idea a Jose @Scero

> No me hago responsable de los daños que puedan ser causados a partir de esta entrada de blog
