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

Una vez alli seleciona la opcion de [Windows hosts](https://download.virtualbox.org/virtualbox/6.1.32/VirtualBox-6.1.32-149290-Win.exe)

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

un poco mas abajo nos pide la cantidad de memoria RAM que le queremos asignar a la máquina, esto va a gusto del consumidor, yo normalmente le pongo el máximo dentro de la franja verde

![](/assets/images/RAM.PNG)

En el apartado de disco duro, dejamos marcada la opción de "Crear un disco duro virtual ahora"

![](/assets/images/discoduroç.PNG)

Le damos a crear y nos pedirá que asignemos el tamaño del disco duro para la máquina, recomiendo dar en entre 20 GB y 30 GB

![](/assets/images/espaciodiscoduro.PNG)

Para finalizar estas configuraciones podemos darle a configuración o CTRL + S

En el apartado de Sistema, en la sesión de Procesador podemos aumentar la cantidad de CPU destinada a la máquina, la cantidad a seleccionar depende de tu procesador, recomiendo poner el máximo dentro de la franja verde.

![](/assets/images/CPU.PNG)

## Iniciar la máquina
