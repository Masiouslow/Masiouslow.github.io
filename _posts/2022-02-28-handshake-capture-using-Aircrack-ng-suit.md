---
layout: single
title: Captura de Handshake usando la suit de Aircrack-ng 
excerpt: "En este post te enseñaré a capturar un handshake de una red wifi utilizando la suite Aircrak-ng."
date: 28-02-2022
classes: wide
header:
  teaser: /assets/images/handshake capture_01/47-477852_this-free-icons-png-design-of-handshake-002-PhotoRoom.png
  teaser_home_page: true
  icon: 
categories:


tags:


---

En este post te enseñaré a capturar un handshake de una red wifi utilizando la suite Aircrak-ng.


## Antes de empezar

Para la captura del handshake, es necesario tener un adaptador wifi que permita habilitar el modo monitor, esto es necesario para poner nuestro adaptador en modo escucha.
En este caso yo estoy utilizando un adaptador de la marca Alfa, modelo AWUS1900, para más información sobre adaptadores puedes consultar las recomendaciones de la página de [aircrack-ng](https://www.aircrack-ng.org/doku.php?id=faq) o el listado de [kalitut](https://kalitut.com/usb-wi-fi-adapters-supporting-monitor/)

[![](/assets/images/handshake capture_01/antena_pwq.png)](https://www.amazon.es/Alfa-Network-AWUS1900-802-11ac-adapter/dp/B01MZD7Z76/ref=sr_1_1?__mk_es_ES=%C3%85M%C3%85%C5%BD%C3%95%C3%91&crid=2Z3VD0ZAFT97J&keywords=awus+1900&qid=1646076976&sprefix=awus+1900%2Caps%2C950&sr=8-1)


## Punto de inicio

Lo primero que necesitamos hacer es identificar nuestras interfaces, para ello utilizaremos el comando `iwconfig`:

```
┌[parrot]─[00:00-00/00]─[/home/masiouslow]
└╼masiouslow$iwconfig       
lo        no wireless extensions.

eth0      no wireless extensions.

wlan0     IEEE 802.11  ESSID:"Hello_world"  
          Mode:Managed  Frequency:5.24 GHz  Access Point: 50:77:B3:EE:65:33   
          Bit Rate=292.5 Mb/s   Tx-Power=17 dBm   
          Retry short limit:7   RTS thr:off   Fragment thr:off
          Power Management:on
          Link Quality=52/70  Signal level=-58 dBm  
          Rx invalid nwid:0  Rx invalid crypt:0  Rx invalid frag:0
          Tx excessive retries:0  Invalid misc:0   Missed beacon:0

wlx00c0caab5835  unassociated  Nickname:"WIFI@RTL8814AU"
          Mode:Managed  Frequency=2.412 GHz  Access Point: Not-Associated   
          Sensitivity:0/0  
          Retry:off   RTS thr:off   Fragment thr:off
          Power Management:off
          Link Quality=0/100  Signal level=0 dBm  Noise level=0 dBm
          Rx invalid nwid:0  Rx invalid crypt:0  Rx invalid frag:0
          Tx excessive retries:0  Invalid misc:0   Missed beacon:0

```
Esto nos sirve para identificar cuál es el adaptador con el que trabajaremos, en mi caso es: `wlx00c0caab5835` también podemos ver en que estado se encuentra: `Mode:Managed`


## Modo monitor y matar los procesos que interfieren

El siguiente paso consiste en matar los procesos que interfieren con la suite de Aircrak-ng, podrían causar un mal funcionamiento, para ello ejecutamos el siguiente comando: `sudo airmon-ng check kill`

```
┌[parrot]─[00:00-00/00]─[/home/masiouslow]
└╼masiouslow$sudo airmon-ng check kill
[sudo] password for masiouslow: 

Killing these processes:

    PID Name
    798 wpa_supplicant


```
