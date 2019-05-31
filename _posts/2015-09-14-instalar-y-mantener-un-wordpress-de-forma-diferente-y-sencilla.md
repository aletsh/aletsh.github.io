---
id: 55
title: Instalar y mantener un WordPress de forma diferente y sencilla
date: 2015-09-14T21:54:16+00:00
author: aletsh
layout: post
guid: http://alejandroguerrero.es/2015/09/14/instalar-y-mantener-un-wordpress-de-forma-diferente-y-sencilla/
permalink: /instalar-y-mantener-un-wordpress-de-forma-diferente-y-sencilla/
categories:
  - Uncategorized
tags:
  - grunt
  - node.js
  - wordpress
  - yeoman
---
Hace unos días llevo recopilando información para hacer una mini guía de instalación y mantenimiento de una página WordPress de una forma distinta o mejor dicho, de una forma “mas moderna”.

Actualmente estamos administrando nuestras páginas Web de WordPress cambiando datos en nuestro ordenador y subiéndolos por FTP y/o haciendo los cambios directamente en el servidor (en producción, cosa que está mal). Mas de uno se ha llevado las manos a la cabeza al realizar un cambio sea estético o instalar alguna actualización tanto oficial como si no y ha roto WordPress y le ha aparecido la temida pagina Blanca del horror/maldición ¿Verdad?

¿Y ahora que hago? ¿¡Por favor házmelo _te pago lo que quieras_!?

Luego te llaman para poder resolverlo y… o que pena! hay que restaurar un backup de la empresa del Hosting, y si el hosting es sencillo hay que empezar de nuevo y te enteras que la Web la hizo _el primo_ (casi nunca es el caso ¿¡a que no!?).

Bien, hasta aquí creo que mas de uno se identifica y admitirá que hacer primero los cambios en vuestro ordenador, ver que funciona correctamente, que no se ha roto nada y luego modificar el servidor es buena solución. Si no pensáis eso, cierra ya la página y si os entra curiosidad de como hacerlo de una forma mas profesional; ¡quédate!

Para empezar hablaré un poco de los requisitos que necesitamos tener, tanto instalados y de teoría básica se encargará el Sr. Google de ofrecerosla.

  1. Tener instalado [Node.js](https://nodejs.org/en/)
  2. Tener instalado [Yeoman.js](http://yeoman.io/)
  3. Y [Grunt.js](http://gruntjs.com/)
  4. Servidor MAMP, Xamp y derivados (Apache, phpMyadmin, MySQL, php etc)

# Crear nuevo proyecto WordPress {#crearnuevoproyectowordpress}

Para crear el proyecto necesitaremos albergar los archivos como bien sabeis en un directorio dentro de la carpeta “htdocs” o la carpeta que empleis vosotros, otra opcion seria en la “www”…

Una vez creada la carpeta entrad en ella mediante la terminal (yo para este tutorial he empleado el S.O de apple).

Si tenéis instalado Node ahora tenéis que instalar el generador de Yeoman que te baja todo lo necesario para tener la pagina a punto de WordPress: Te baja la ultima version, te dice si quieres algún Theme en especial, si quieres cambiarle los prefijos a las tablas de la base de datos, si quieres cambiar el nombre de la estructura de directorios (muy util por seguridad) y un montón de cosas que el Wizard te ayudará. Os mostrare un ejemplo mas abajo.

En la pagina de <http://yeoman.io/generators/> existen infinidad de generadores para cualquier proyecto que queramos hacer, claro, hoy en día esta muy de moda el desarrollo ágil de proyectos, esto, es una forma de instalar “agilmente” nuestro Worpdress.

En la pagina buscaremos wordpress-generator (Yeopress) podeis encontrar la forma de instalarlo desde aqui: <https://github.com/wesleytodd/YeoPress>.

Estamos aun con la terminal abierta en el directorio donde queremos instalar el WordPress verdad?

Pues en la terminal únicamente hay que introducir el comando “yo” y “> wordpress” y nos aparecerá esta pantalla:

yo

[![yo](/content/images/2015/09/Captura-de-pantalla-2015-09-12-a-las-10.38.03.png)](/content/images/2015/09/Captura-de-pantalla-2015-09-12-a-las-10.38.03.png)

[![yo-2](/content/images/2015/09/yo-21.png)](/content/images/2015/09/yo-21.png)</p> 

Seguiremos el asistente según nos convenga con las credenciales de la base de datos etc … y WALA!

¡Ya tenemos Worpdress instalado! Que fácil ¿Verdad?

A partir de ahora te toca trabajar en el proyecto y hacer los cambios que desees.

# Instalar WordPress en el servidor {#instalarwordpressenelservidor}

Requisitos del servidor:

  1. Que tenga conexión mediante SSH (si no lo tiene tu hosting no es muy bueno)
  2. Compatible con rSync
  3. Que tenga instalado el MySQLDump

Existe un “tasker” de grunt que se basa en subir a un servidor de pruebas o al servidor final nuestro proyecto WordPress sin necesidad de realizar la famosa “migración” de subirlo todo por ftp y cambiar unas columnas en la base de datos etc…

Ese tasker es: [grunt-wordpress-deploy-2](https://www.npmjs.com/package/grunt-wordpress-deploy-2).

Con grunt-wordpress-deploy-2 podremos deplegar nuestro proyecto en un servidor de prueba y en un servidor de producción o configurarlo a nuestro gusto. Solo es necesario ir rellenando los campos que nos indica el “howto”.

Una vez tengamos el gruntfile configurado podemos por ejemplo desplegar el proyecto (en mi caso) en el servidor de pruebas o el de producción.

Espero que con estos sencillos pasos podamos mantener nuestros “Wordpreses” de una forma un poco mas ágil y moderna.

😉</p>