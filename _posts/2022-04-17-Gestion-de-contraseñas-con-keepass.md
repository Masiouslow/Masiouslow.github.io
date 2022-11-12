---
layout: single
title: Gestión de contraseñas con KeePass
excerpt: "Generar y almacenar contraseñas seguras para todas las plataformas con KeePass."
date: 17-04-2022
classes: wide
header:
  teaser: /assets/images/800px-KeePass_icon.svg.png 
  teaser_home_page: true
  icon: 
categories:


tags:


---
Hoy en día ya no basta con tener una contraseña segura, si reutilizamos las contraseñas en diferentes plataformas y una de ellas es vulnerada, quedaremos expuestos ante los atacantes. Por ello necesitamos tener una contraseña segura por cada plataforma, para hacer esto posible utilizaremos un gestor de contraseñas, en este caso [KeePass](https://keepass.info/download.html)

## Instalación de KeePass
En Windows podemos instalar [KeePass](https://sourceforge.net/projects/keepass/files/KeePass%201.x/1.40.1/KeePass-1.40.1-Setup.exe/download), en [linuxKeePassXC](https://keepassxc.org/) y para Android hay varias opciones, pero yo uso [KeePass2Android](https://play.google.com/store/apps/details?id=keepass2android.keepass2android), pero la elección del gestor es una decisión persona. Lo importante es que el gestor utilicé la extensión .kdbx

## Archivo .KDBX ![](/assets/images/KeePass/kdbx.png)
Los archivos .KDBX son bases datos con contraseñas generadas por los gestores de contraseñas. Almacenan una base de datos cifrada que solo se puede ver utilizando una contraseña maestra. Al momento de gestionar nuestras contraseñas es igual de importante guardar el archivo .kdbx como la contraseña maestra, porque las dos son imprescindibles para acceder a ellas.

![](/assets/images/KeePass/kdbx.png)









































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

