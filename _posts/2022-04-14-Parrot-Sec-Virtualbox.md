---
layout: single
title: Instalación de Parrot SEC en virtualbox 
excerpt: "Aquí explico cuáles son los pasos a seguir para instalar Parrot Sec en una máquina virtual."
date: 14-04-2022
classes: wide
header:
  teaser: /assets/images/506px-Parrot_Logo.png 
  teaser_home_page: true
  icon: 
categories:


tags:


---

A continuación enseñaré de forma gráfica el proceso de instalación de Parrot Sec en virtualbox

Virtualbox es una aplicación que nos permite crear máquinas virtuales, es decir, podremos estar ejecutando dos sistemas operativos o más  a la vez, en este caso win10 como sistema operativo principal y Parrot Sec ejecutándose en la máquina virtual.

## Instalar Virtualbox
Para empezar necesitamos instalar el programa virtualbox, que será el que nos permitirá generar las máquinas virtuales.

Primero entra en la web de [Virtualbox](https://www.virtualbox.org/)

![](/assets/images/dfdfddse.PNG)

Ves al apartado de [descargas](https://www.virtualbox.org/wiki/Downloads)

![](/assets/images/downloads.PNG)

Una vez alli, selecciona la opción de [Windows hosts](https://download.virtualbox.org/virtualbox/6.1.32/VirtualBox-6.1.32-149290-Win.exe)

![](/assets/images/windowshost.PNG)

Se te descargará el instalador del programa, ejecútalo y sigue las instrucciones

![](/assets/images/Captura.PNG)

## Descargar la imagen de nuestro sistema operativo

Una vez instalado el programa de virtualización, necesitamos la imagen del sistema operativo que queremos instalar, en este caso parrot sec.

Para ello vamos a la [página de descarga](https://www.parrotsec.org/download/) de parrot, seleccionamos la opción de Security Edition y le damos al botón de download

![](/assets/images/sdfsdfsdf.PNG)
 
Con esto ya tenemos todo preparado para la virtualización

## Crear la máquina virtual

Lo siguiente que tenemos que hacer es abrir virtualbox y darle donde pone nueva (CTRL+N)

![](/assets/images/modoexperto.PNG)

seleccionamos el modo experto

![](/assets/images/modoguiado.PNG)

Primero nos pedirá un nombre para la máquina, el tipo de sistema operativo y la versión del mismo

Para el tipo y la version de SO que queremos virtualizar ponemos Linux y Ubuntu (64-bit)

![](/assets/images/tipoyversion.PNG)

un poco más abajo nos pide la cantidad de memoria RAM que le queremos asignar a la máquina, esto va a gusto del consumidor, yo normalmente le pongo el máximo dentro de la franja verde

![](/assets/images/RAM.PNG)

En el apartado de disco duro, dejamos marcada la opción de "Crear un disco duro virtual ahora"

![](/assets/images/discoduroç.PNG)

Le damos a crear y nos pedirá que asignemos el tamaño del disco duro para la máquina, recomiendo dar en entre 20 GB y 30 GB

![](/assets/images/espaciodiscoduro.PNG)

Para finalizar estas configuraciones podemos darle a configuración o CTRL + S

En el apartado de Sistema, en la sesión de Procesador podemos aumentar la cantidad de CPU destinada a la máquina, la cantidad a seleccionar depende de tu procesador, recomiendo poner el máximo dentro de la franja verde.

![](/assets/images/CPU.PNG)

con esto ya estaríamos listos, de todas formas esto se puede modificar después

## Iniciar la máquina

En el menú principal, le damos a iniciar, nos abrirá una ventana, donde nos pide que seleccionemos la imagen del SO que queremos arrancar

![](/assets/images/iso.PNG)

Iniciamos...

En el menú que se nos abrirá seleccionamos Try/Install

![](/assets/images/try.PNG)

Al arrancar vemos que el sistema operativo está preparado, pero aún lo hemos de instalar, ahora mismo ningún cambio que realizamos se guarda.

Abrimos el instalado y seleccionamos nuestras preferencias de idioma, teclado y zona horaria.

![](/assets/images/installll.PNG)

Nos preguntará como queremos gestionar las particiones, seleccionamos borrar disco

![](/assets/images/particiona.PNG)

Después de esto seguimos rellenando los datos que nos pide, le damos a next y comprobamos que todo este según queremos, confirmamos dándole a install

![](/assets/images/sdgesgs.PNG)

Una vez que la instalación haya acabado reiniciamos la máquina, cuando finalice de reiniciar la apagamos por completo

Entramos en configuración y vamos al la sección de almacenamiento

![](/assets/images/amacenamiento.PNG)

Tenemos que borrar el disco que está dentro del Controlador: IDE

![](/assets/images/Captura de pantalla 2022-04-18 210515.png)

Una vez hecho esto ya está todo listo para disfrutar del sistema operativo y sus tantas herramientas dedicadas a la ciberseguridad.


## Hasta aquí el post, espero que te haya gustado y te sea útil
Si te gusta el trabajo que estoy haciendo y te gustaría apoyarme puedes hacerlo con una donación en bitcoin 

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

