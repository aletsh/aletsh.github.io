---
layout: post
published: true
title: Wifi para invitados en OpenWrt
subtitle: Configuracion para habilitar una red Wifi para invitados en 3 comodos pasos.
---
## Ingredientes
- El router de conejillo de indias, yo uso un TP-Link TL-WR841N/ND v9
- El router TL-WR841N/ND v9 esta conectado mediante cable a otro router que es el que da acceso a internet.
- OpenWrt instalado en tu router, actualmente yo lo tengo con OpenWrt Chaos Calmer 15.05.1 

## Elaboración
### Crear red Wifi
Acceder a Network --> Wifi --> Add

- Channel: El que querais yo puse el 11
- ESSID: El nombre que querais yo puse: Guest_Wifi
- Mode: Access Point
- Network; "Create" con el nombre de public
- WMM Mode: Habilitado

Seguridad: En la pestaña Wireless Security poner la contraseña que querais.

![wifi_guest_1.PNG]({{site.baseurl}}/img/wifi_guest_1.PNG)

### Modificar la interfaz de red Public
Acceder a Network --> Interfaces
Editar la red Public

- Protocol: Static Address
- IPv4: 10.0.0.1 (O la que querais)
- IPv4 Netmask: 255.255.255.0
- Use custom DNS servers: 8.8.8.8, 8.8.4.4 (o los que querais)

Guardar los cambios y volver a editar la interfaz public

- DHCP Server;
- Deshabilitamos la opcion "Disable DHCP for this interface"
- Start: 50
- Limit: 10
- Leasetime: 1h

En el tab "Firewall Settings" crear la nueva llamada "Public"

![wifi_guest_2.PNG]({{site.baseurl}}/img/wifi_guest_2.PNG)

![wifi_guest_2_1.PNG]({{site.baseurl}}/img/wifi_guest_2_1.PNG)

### Modificar el Firewall de red Public
Acceder a Network --> Firewall

Dejar estas opciones de la siguiente manera:
- Enable SYN-Flood protection: Habilitado
- Input: accept
- Output: accept
- Forward: reject

**Zones:**
Public-input: accept
Public-output: accept
Public-forward: reject

![wifi_guest_3.PNG]({{site.baseurl}}/img/wifi_guest_3.PNG)

**Modificar la zona "Public" pulsando en "Edit":**
En la parte de Inter-Zone Forwarding:
- Allow forward to destination: en LAN
- Allow forward from source zones: LAN

Acceder a la opcion **Traffic Rules**

Crear estas dos rules nuevas:
![wifi_guest_3_2.PNG]({{site.baseurl}}/img/wifi_guest_3_2.PNG)

Crear  rule **allow2gw** con esta configuracin:
![wifi_guest_3_3.PNG]({{site.baseurl}}/img/wifi_guest_3_3.PNG)

Crear rule **drop2lan** con esta configuración:
![wifi_guest_3_4.PNG]({{site.baseurl}}/img/wifi_guest_3_4.PNG)

**Source NAT**
Crear una source nat llamada **pub2lan**:
![wifi_guest_3_5.PNG]({{site.baseurl}}/img/wifi_guest_3_5.PNG)



Reiniciar el router.

Enjoy!

:)




