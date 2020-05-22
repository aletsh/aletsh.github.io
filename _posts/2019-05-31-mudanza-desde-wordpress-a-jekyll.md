---
layout: post
published: true
title: Migrando de Wordpress a Jekyll
date: '2019-05-31'
subtitle: La manera mas fácil de hacer un blog
category:
  - blogging
tags:
  - wordpress
  - jekyll
  - migration
---
## ¿Porque?
Como algunos sabreis el blog "con telas de araña" esta en una maquina (freenas) en mi casa desplegado en un Docker administrado via Rancher OS... y un largo bla bla bla...

Para practicar es muy bonito, configurar el rancher, configurar los contenedores, desplegar los dockers e incluso hacer un balanceador de carga pero no llega a ser práctico.

Por esos y otros motivos decido realizar la migración de Wordpresss a Jekyll ya que carece de base de datos y de servidor php. Y para hacer un sitio Web con algunas páginas estáticas y otra más que le llamaremos blog, sobra ^^.

## Objetivos sobre la mudanza
* Quitar el blog de mi máquina.
* Simplificar la manera de hacer los posts.
* Estilo más sencillo.
* Añadir dominio propio para github pages

## Quitar el blog de mi maquina.
Para ello he tenido que instalar un plugin llamado [Jekyll Exporter](https://wordpress.org/plugins/jekyll-exporter/ "Jekyll Exporter"). Lo he instalado y al pulsar sobre el plugin en muy poco tiempo me ha exportado todos los posts con sus respectivos adjuntos en un paquete zip.

![wordpress-to-jekyll.png]({{site.baseurl}}/img/wordpress-to-jekyll.png)

Dentro del archivo comprimido te crea un directorio con el nombre de _posts_ el cual subi al repositorio _git_ previo _forkeado_ desde [https://github.com/daattali/beautiful-jekyll#readme](https://github.com/daattali/beautiful-jekyll#readme "Fork Jekyll Beautiful") los cuales ya se pueden leer.

Tardé, 2 minutos.



## Simplificar la manera de hacer los posts
Este mismo post lo estoy redactando con Prose ([https://prose.io](https://prose.io)) el cual te pide autorizacion para leer tu repositorio de _gitHub_.

Una vez accedido, te muestra un listado de todos los repositorios de guthub, he seleccionado el de aletsh.github.io el cual previamente hemos hecho un _fork_.

![mudanza-wordpress-jekyll.PNG]({{site.baseurl}}/img/mudanza-wordpress-jekyll.PNG)

El editor de textos _wyswyg_ es muy simple y te redacta en _markdown_.

Si quieres aprender markdown en 5 minutos existe un tutorial bastante gracioso para aprender, solo hay que acceder aquí:  [https://www.markdowntutorial.com/](https://www.markdowntutorial.com/)

## Estilo más sencillo.
El estilo de este theme está bastante bien tanto para leer desde un ordenador de escritorio o el movil. 

He averiguado que existen bastantes autores que están empleando este theme y al parecer está siendo actualizado por varios contribuyentes, asi que me gustó la idea de poder usarlo y migrar de forma definitiva.

## Añadir dominio propio para github pages
Primero hay que entrar en Github, ir al repositorio de vuestro blog pulsar en la opcion "settings" que esta a la derecha. Buscar la sección GitHub Pages y añadir el dominio.

Luego hay que ir al parking de dominios eliminar vuestro registro "A" y añadir los siguientes:
* 185.199.108.153
* 185.199.109.153
* 185.199.110.153
* 185.199.111.153

Dependiendo de la ISP este cambio puede tardar 24/48h. A mi me ha funcionado al momento.


Este blog, supongo que seguirá teniendo telas de araña pero la migración me servirá para poder; apagar el servidor y asi ahorrar electricidad o emplearlo para otros fines.

(:
