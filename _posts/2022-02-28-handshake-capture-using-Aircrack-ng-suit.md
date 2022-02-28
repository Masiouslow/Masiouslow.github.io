---
layout: single
title: Handshake capture using Aircrack-ng suit 
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

Lo primero que necesitamos hacer es identificar nuestras interfaces, para ello utilizaremos el comando `iwconfig`

Lo primero que necesitamos hacer es identificar nuestras interfaces, para ello utilizaremos el comando 
``` 
iwconfig 
```
