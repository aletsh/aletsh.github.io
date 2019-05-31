---
id: 28
title: Agregar Provincias Españolas en Prestashop 1.5
date: 2014-04-24T00:00:39+00:00
author: aletsh
layout: post
guid: http://alejandroguerrero.es/2014/04/24/prestashop-1-5-agregar-provincias-espanolas/
permalink: /prestashop-1-5-agregar-provincias-espanolas/
categories:
  - Uncategorized
tags:
  - Prestashop
---
Otro aporte más, esta vez de Prestashop.

Estoy ayudando a un colega hacer su comercio electrónico y haciendo las primeras pruebas no aparecía el método de envío. ¡QUE RARO!

Eso pasa porque Prestashop (la versión que estoy empleando es la 1.5, ya se que esta la nueva…) no tiene nada configurado para que nos hagan la factura a una dirección de España.

Para que tengamos todos los territorios, provincias y ciudades de España hay que insertarlas. Y para insertarlas de una manera mas rápida os lo compartiré en un SQL el cual deberéis:

  1. Entrar en vuestro gestor de base de datos como por ejemplo “PhpMyAdmin” comunmente “PMA”.
  2. Seleccionar la base de datos donde teneis alojada todas las tablas del Prestashop
  3. Darle al editor de SQL
  4. Pegar el contenido que esta más abajo.

Contenido SQL:

/\* Agregamos las zonas de España\*/ INSERT INTO `ps_zone` (`id_zone`, `name`, `active`) VALUES (9, &#8216;Peninsula&#8217;, 1), (10, &#8216;Canarias&#8217;, 1), (11, &#8216;Baleares&#8217;, 1), (12, &#8216;Ceuta y Melilla&#8217;, 1); /* Preparamos el campo ISO_CODE para aceptar 5 caracteres _/ ALTER TABLE `ps_state` MODIFY `iso_code` char(5) NOT NULL; /_ Agregamos las provincias y asignamos su zona _/ INSERT INTO `ps_state` (`id_state`,`id_country`, `id_zone`, `name`, `iso_code`, `tax_behavior`, `active`) VALUES (313, 6, 9, &#8216;La Coruña&#8217;, &#8216;C&#8217;, 0, 1), (314, 6, 9, &#8216;Álava&#8217;, &#8216;VI&#8217;, 0, 1), (315, 6, 9, &#8216;Albacete&#8217; ,&#8217;AB&#8217;, 0, 1), (316, 6, 9, &#8216;Alicante&#8217;, &#8216;A&#8217;, 0, 1), (317, 6, 9, &#8216;Almería&#8217;, &#8216;AL&#8217;, 0, 1), (318, 6, 9, &#8216;Asturias&#8217;, &#8216;O&#8217;, 0, 1), (319, 6, 9, &#8216;Ávila&#8217;, &#8216;AV&#8217;, 0, 1), (320, 6, 9, &#8216;Badajoz&#8217;, &#8216;BA&#8217;, 0, 1), (321, 6, 11, &#8216;Islas Baleares&#8217;, &#8216;PM&#8217;, 0, 1), (322, 6, 9, &#8216;Barcelona&#8217;, &#8216;B&#8217;, 0, 1), (323, 6, 9, &#8216;Burgos&#8217;, &#8216;BU&#8217;, 0, 1), (324, 6, 9, &#8216;Cáceres&#8217;, &#8216;CC&#8217;, 0, 1), (325, 6, 9, &#8216;Cádiz&#8217;, &#8216;CA&#8217;, 0, 1), (326, 6, 9, &#8216;Cantabria&#8217;, &#8216;S&#8217;, 0, 1), (327, 6, 9, &#8216;Castellón&#8217;, &#8216;CS&#8217;, 0, 1), (328, 6, 12, &#8216;Ceuta&#8217;, &#8216;CE&#8217;, 0, 1), (329, 6, 9, &#8216;Ciudad Real&#8217;, &#8216;CR&#8217;, 0, 1), (330, 6, 9, &#8216;Córdoba&#8217;, &#8216;CO&#8217;, 0, 1), (331, 6, 9, &#8216;Cuenca&#8217;, &#8216;CU&#8217;, 0, 1), (332, 6, 9, &#8216;Gerona&#8217;, &#8216;GI&#8217;, 0, 1), (333, 6, 9, &#8216;Granada&#8217;, &#8216;GR&#8217;, 0, 1), (334, 6, 9, &#8216;Guadalajara&#8217;, &#8216;GU&#8217;, 0, 1), (335, 6, 9, &#8216;Guipuzcoa&#8217;, &#8216;SS&#8217;, 0, 1), (336, 6, 9, &#8216;Huelva&#8217;, &#8216;H&#8217;, 0, 1), (337, 6, 9, &#8216;Huesca&#8217;, &#8216;HU&#8217;, 0, 1), (338, 6, 9, &#8216;Jaén&#8217;, &#8216;J&#8217;, 0, 1), (339, 6, 9, &#8216;La Rioja&#8217;, &#8216;LO&#8217;, 0, 1), (340, 6, 10, &#8216;Las Palmas&#8217;, &#8216;GC&#8217;, 0, 1), (341, 6, 9, &#8216;León&#8217;, &#8216;LE&#8217;, 0, 1), (342, 6, 9, &#8216;Lérida&#8217;, &#8216;L&#8217;, 0, 1), (343, 6, 9, &#8216;Lugo&#8217;, &#8216;LU&#8217;, 0, 1), (344, 6, 9, &#8216;Madrid&#8217;, &#8216;M&#8217;, 0, 1), (345, 6, 9, &#8216;Málaga&#8217;, &#8216;MA&#8217;, 0, 1), (346, 6, 12, &#8216;Melilla&#8217;, &#8216;ML&#8217;, 0, 1), (347, 6, 9, &#8216;Murcia&#8217;, &#8216;MU&#8217;, 0, 1), (348, 6, 9, &#8216;Navarra&#8217;, &#8216;NA&#8217;, 0, 1), (349, 6, 9, &#8216;Orense&#8217;, &#8216;OR&#8217;, 0, 1), (350, 6, 9, &#8216;Palencia&#8217;, &#8216;P&#8217;, 0, 1), (351, 6, 9, &#8216;Pontevedra&#8217;, &#8216;PO&#8217;, 0, 1), (352, 6, 9, &#8216;Salamanca&#8217;, &#8216;SA&#8217;, 0, 1), (353, 6, 10, &#8216;Santa Cruz de Tenerife&#8217;, &#8216;TF&#8217;, 0, 1), (354, 6, 9, &#8216;Segovia&#8217;, &#8216;SG&#8217;, 0, 1), (355, 6, 9, &#8216;Sevilla&#8217;, &#8216;SE&#8217;, 0, 1), (356, 6, 9, &#8216;Soria&#8217;, &#8216;SO&#8217;, 0, 1), (357, 6, 9, &#8216;Tarragona&#8217;, &#8216;T&#8217;, 0, 1), (358, 6, 9, &#8216;Teruel&#8217;, &#8216;TE&#8217;, 0, 1), (359, 6, 9, &#8216;Toledo&#8217;, &#8216;TO&#8217;, 0, 1), (360, 6, 9, &#8216;Valencia&#8217;, &#8216;V&#8217;, 0, 1), (361, 6, 9, &#8216;Valladolid&#8217;, &#8216;VA&#8217;, 0, 1), (362, 6, 9, &#8216;Vizcaya&#8217;, &#8216;BI&#8217;, 0, 1), (363, 6, 9, &#8216;Zamora&#8217;, &#8216;ZA&#8217;, 0, 1), (364, 6, 9, &#8216;Zaragoza&#8217;, &#8216;Z&#8217;, 0, 1); /_ Activamos los estados en España */ UPDATE `ps_country` SET `contains_states` = 1 WHERE `id_country` = 6;

> \* No me hago responsable de los desperfectos de vuestra Base de Datos\*</p> 

Fuentes:

  * <http://www.prestashop.com/forums/topic/189941-aporte-agregar-provincias-espanolas-en-version-15/>
  * <http://blog.ansystem.es/modulo-provincias-de-espana-para-prestashop/>