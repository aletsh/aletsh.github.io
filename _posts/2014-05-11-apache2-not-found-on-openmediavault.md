---
id: 31
title: Apache2 not found on OpenMediaVault
date: 2014-05-11T23:23:51+00:00
author: aletsh
layout: post
guid: http://alejandroguerrero.es/2014/05/11/apache2-not-found-on-openmediavault/
permalink: /apache2-not-found-on-openmediavault/
categories:
  - Uncategorized
tags:
  - Apache
  - Linux
  - omv
  - OpenMediaVault
---
Me he dado cuenta que tenia todos los servicios arrancados pero la Web que administra de una forma mas visual dichos servicios no me funcionaba.  
He accedido por _terminal_ para intentar arreglarlo y esto es lo que he realizado:

He intentado arrancar el servicio Web (Apache2) con el siguiente error:

# service apache2 start Starting web server: apache2apache2: Syntax error on line 203 of /etc/apache2/apache2.conf: Could not open configuration file /etc/apache2/mods-enabled/authnz_external.load: No such file or directory Action &#8216;start&#8217; failed. The Apache error log may have more information. failed! {#serviceapache2startstartingwebserverapache2apache2syntaxerroronline203ofetcapache2apache2confcouldnotopenconfigurationfileetcapache2modsenabledauthnz_externalloadnosuchfileordirectoryactionstartfailedtheapacheerrorlogmayhavemoreinformationfailed}</p> 

Seguir estos pasos:

# a2dismod authnz_external #omv-mkconf apache2 # service apache2 start Starting web server: apache2Syntax error on line 1 of /etc/apache2/openmediavault-webgui.d/git.conf: Invalid command &#8216;AddExternalAuth&#8217;, perhaps misspelled or defined by a module not included in the server configuration Action &#8216;start&#8217; failed. The Apache error log may have more information. failed! {#a2dismodauthnz_externalomvmkconfapache2serviceapache2startstartingwebserverapache2syntaxerroronline1ofetcapache2openmediavaultwebguidgitconfinvalidcommandaddexternalauthperhapsmisspelledordefinedbyamodulenotincludedintheserverconfigurationactionstartfailedtheapacheerrorlogmayhavemoreinformationfailed}</p> 

Al dar el error del GIT (Si está instalado)

# cd /etc/apache2/openmediavault-webgui.d/ #mv git.conf git.conf.bak #service apache2 start Starting web server: apache2httpd (pid 2000) already running . {#cdetcapache2openmediavaultwebguidmvgitconfgitconfbakserviceapache2startstartingwebserverapache2httpdpid2000alreadyrunning}</p> 

Ahora al intentar acceder a la Web Gui funciona!