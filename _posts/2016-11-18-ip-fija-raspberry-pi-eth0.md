---
id: 68
title: Ip fija Raspberry Pi (eth0)
date: 2016-11-18T22:00:25+00:00
author: aletsh
layout: post
guid: http://alejandroguerrero.es/2016/11/18/ip-fija-raspberry-pi-eth0/
permalink: /ip-fija-raspberry-pi-eth0/
categories:
  - Uncategorized
tags:
  - eth0
  - fija
  - ip
  - raspberry
  - raspberry pi
  - raspbian
  - static
---
Hay que **editar** el siguiente \*\*archivo \*\*

<span class="s1">/etc/network/interfaces</span>

Haced una copia antes, por si se rompe algo…

<span class="s1">cp /etc/network/interfaces /etc/network/interfaces_old vi /etc/network/interfaces</span>

<span class="s1">#Contenido del archivo auto eth0</span><span class="s1">iface lo inet loopback</span><span class="s1">iface eth0 inet static</span> <span class="s1">address rasp.berry.pi.ip</span> <span class="s1">netmask net.mask.rasp.berry</span> <span class="s1">gateway gate.way.rasp.berry</span><span class="s1">allow-hotplug wlan0</span><span class="s1">iface wlan0 inet manual</span><span class="s1"><span class="Apple-converted-space">    </span>wpa-conf /etc/wpa_supplicant/wpa_supplicant.conf</span><span class="s1">allow-hotplug wlan1</span><span class="s1">iface wlan1 inet manual</span><span class="s1"><span class="Apple-converted-space">    </span>wpa-conf /etc/wpa_supplicant/wpa_supplicant.conf</span>

Guardar, Reiniciar y vovler a conectar vía SSH (a la nueva IP) .