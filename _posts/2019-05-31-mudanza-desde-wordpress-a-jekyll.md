---
layout: post
published: true
title: Mudanza desde Wordpress a Jekyll
date: '2019-05-31'
---
### ¿Porque?
Como algunos sabreis el blog "con telas de araña" esta en una maquina (freenas) en mi casa desplegado en un docker administrado via Rancher OS... Vamos, un poco royo.

Para practicar es muy bonito, configurar el rancher, configurar los contenedores, desplegar los dockers e incluso hacer un balanceador de carga...

### Objetivos sobre la mudanza
* Quitar el blog de mi maquina.
* Simplificar la manera de hacer los posts.
* Estilo mas sencillo.

## Quitar el blog de mi maquina.
Para ello he tenido que instalar un plugin llamado [Jekyll Exporter](https://wordpress.org/plugins/jekyll-exporter/ "Jekyll Exporter"). Lo he instalado y al pulsar sobre el plugin en muy poco tiempo me ha exportado todos los posts con sus respectivos adjuntos.

Dentro del archivo comprimido te crea un directorio con el nombre de _posts_ el cual subi al repositorio _git_ previo _forkeado_ desde [https://github.com/daattali/beautiful-jekyll#readme](https://github.com/daattali/beautiful-jekyll#readme "Fork Jekyll Beautiful") los cuales ya se pueden leer.

### Falta por hacer
* Redireccionar el dominio al blog

## Simplificar la manera de hacer los posts
Este mismo post lo estoy redactando con [https://prose.io](https://prose.io) el cual te pide autorizacion para leer tu repositorio de _gitHub_.

Una vez accedido a tu listado de repositorios he seleccionado el de aletsh.github.io.

## Estilo mas sencillo.
El estilo de este theme esta bastante bien tanto para escritorio como para leer los posts desde el movil. He averiguado que existen bastantes autores que estan empleando este theme y al parecer esta siendo actualizado por varios contribuyentes, asi que me gusto la idea de poder usarlo y migrar de forma definitiva.





