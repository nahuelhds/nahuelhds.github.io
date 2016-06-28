---
title:  "Instalar Imagick en Wamp 2.5"
categories: wamp
tags: wamp, imagick
---

Estaba queriendo instalar Imagick de manera local. Como no podía ser de otra manera, encontré la pista en [StackOverflow](http://stackoverflow.com/a/26265214).

### Importante
Como Wamp 2.5 viene con _PHP 5.5.12_, _VC11_ y es _ThreadSafe_, vamos utilizar los siguientes archivos:

* [ImageMagick-6.9.1-2-vc11-x86.zip](http://windows.php.net/downloads/pecl/deps/ImageMagick-6.9.1-2-vc11-x86.zip)
* [php_imagick-3.4.0rc4-5.5-ts-vc11-x86.zip](http://windows.php.net/downloads/pecl/releases/imagick/3.4.0rc4/php_imagick-3.4.0rc4-5.5-ts-vc11-x86.zip)

### Instrucciones
1. Extraer el contenido de la carpeta `bin` del zip **ImageMagick-6.9.1-2-vc11-x86.zip** en una nueva carpeta. Ej.: `D:/imagick`
1. Incluir la carpeta creada en el PATH de Windows.
1. Extraer el contenido de **php_imagick-3.4.0rc4-5.5-ts-vc11-x86.zip** dentro de la nueva carpeta, reemplazando los archivos existentes.
1. En el `php.ini` de Wamp, incluir el path absoluto al DLL. Ej.: `D:/imagick/php_imagick.dll`.
1. Reiniciar Wamp (no los servicios, sino el programa entero).
1. ¡Listo!
