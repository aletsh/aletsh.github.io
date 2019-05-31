---
id: 20
title: Iniciar facturación en Prestashop 1.5.5.0
date: 2013-10-05T01:25:20+00:00
author: aletsh
layout: post
guid: http://alejandroguerrero.es/2013/10/05/iniciar-facturacion-en-prestashop-1-5-5-0/
permalink: /iniciar-facturacion-en-prestashop-1-5-5-0/
categories:
  - Uncategorized
tags:
  - Prestashop
---
Uno de los problemas que tuve hace un tiempo era el volver a resetear la numeración de las facturas que se generan con Prestashop ya que al realizar pruebas de pedidos, dichos pedidos eran ficticios y al Activar la tienda, la primera factura empezaba por #15.

He visto muchos tutoriales por la red pero el que mas me ha servido ha sido entrar directamente a la base de datos (Con el PMA) y realizar la acción SQL que a continuación os muestro:

Para los pedidos:

<div class="wlWriterEditableSmartContent" id="scid:812469c5-0cb0-4c63-8c15-c81123a09de7:4f879575-4db0-437a-927e-b3eda90110cc" style="margin: 0px; display: inline; float: none; padding: 0px;">
  TRUNCATE `ps_orders`; TRUNCATE `ps_order_detail`; TRUNCATE `ps_order_history`; TRUNCATE `ps_order_message`; TRUNCATE `ps_order_message_lang`; TRUNCATE `ps_order_slip`; TRUNCATE `ps_order_slip_detail`; TRUNCATE `ps_order_return` ; TRUNCATE `ps_order_return_detail` ; TRUNCATE `ps_message` ; TRUNCATE `ps_message_readed` ;
</div>

 

Para las facturas:

<div class="wlWriterEditableSmartContent" id="scid:812469c5-0cb0-4c63-8c15-c81123a09de7:e1c10e37-2732-4935-8bf7-b3d648cdfd18" style="margin: 0px; display: inline; float: none; padding: 0px;">
  TRUNCATE `ps_order_invoice`; TRUNCATE `ps_order_invoice_payment`; TRUNCATE `ps_order_invoice_tax`;
</div>

 

[alert type=”info” sc_id=”sc1380929618826″]No me hago responsable de las perdidas de datos ocasionadas.[/alert]

Ahora solo nos queda acceder a la parte de PEDIDOS –> Facturas y en OPCIONES DE FACTURA –> Siguiente numero de factura: Comprobar que al final de la explicación aparece un “…mantener numero actual: (#1).

Si aparece un #1 todo es correcto.

> Caso práctico: Si actualmente estamos en el año 2013 muchas de las tiendas realizan su facturación con ese prefijo. Pero cuando el año cambie a 2014, la factura no empieza desde 1 sino desde la ultima factura del 2013 mas 1.