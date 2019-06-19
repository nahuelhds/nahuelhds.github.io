---
title: >-
  Cómo instalar múltiples versiones de PHP en Apache con Homebrew y no morir en
  el intento…
description: Actualización de Mayo de 2019
date: '2017-10-17T14:29:30.937Z'
categories: []
keywords: []
slug: >-
  /@nahuelhds/c%C3%B3mo-instalar-m%C3%BAltiples-versiones-de-php-en-apache-con-homebrew-y-no-morir-en-el-intento-9b4de6f1e327
---

![](img/1__ZDOzg6V661UtBKQiGRWVQw.png)

### Actualización de Mayo de 2019

Al momento en que creé este post, su contenido tenía sentido en relación a los problemas que encontré durante el proceso. Las cosas cambiaron bastante desde entonces, al punto tal que todos estos problemas ya no existen!

Así sólo puedo recomendarles [leer el post original](https://getgrav.org/blog/macos-sierra-apache-multiple-php-versions) del blog de Grav. Está siempre actualizado y contiene las mejores instrucciones.

¡Saludos!

### Contenido original (Octubre 2017)

Hace unos días estoy mudándome a MacOS.

Lógicamente, de las primeras cosas que necesité hacer fue instalar **MAMP** (**M**acOS, **A**pache, **M**ariaDB/**M**ySQL y **P**HP). La particularidad es que necesitaba PHP en distintas versiones por los distintos proyectos que tengo conviviendo en mi servidor local. Para ello, me recomendaron seguir [esta guía del blog de Grav, que consta de tres partes y que, realmente, es oro](https://getgrav.org/blog/macos-sierra-apache-multiple-php-versions).

De todos modos, hay algunos inconvenientes (menores la verdad) que me surgieron y que paso a detallar y que por las dudas incluyo en este post como para complementar dicha instalación.

### Extensiones PHP — Build from source

Es necesario instalar las extensiones de PHP con la opción `--build-from-source` ya que [de otro modo darán error](https://github.com/Homebrew/homebrew-php/issues/2475). Entonces, cuando en el tuto diga de instalar las extensiones, esos comandos quedan así:

brew install php{xy}-{extension} --build-from-source

Donde:

*   xy: version de php: 55, 56, 70 o 71.
*   extension: módulo a integrar: apcu, opcache, yaml o xdebug

Si ya se instaló y da error, entonces correr `brew reinstall`

### Certificado SSL

La guía olvida mencionar que en Apache hay que agregar el comando `Listen 443` inmediatamente luego de la linea `Listen 80`

### Soporte MySQL en PHP5.5 y PHP5.6

Esta me tuvo todo el fin de semana y no era nada complicado al final…

![](img/1__9pqxqRnUXF09vIcHX__BY0g.png)

La extensión mysql no viene pre-instalada en Homebrew PHP (como sí sucede con mysqli). Para colmo al intentar hacerlo con la opción`--with-libmysql` da error al no encontrar unas librerías en el directorio `/usr/local/bin`. [Por suerte existe Github](https://github.com/Homebrew/homebrew-php/issues/4501#issuecomment-337139957).

En resumen, primero hay que instalar MySQL:

brew install mysql

Luego, parar el servicio MariaDB y desmontarlo para luego montar MySQL.

brew services stop mariadb  
brew unlink mariadb  
brew link mysql

Una vez hecho esto, hay que ir a`/usr/local/lib` y duplicar y renombrar los siguientes dos archivos

```
libmysqlclient.a     -> libmysqlclient_r.alibmysqlclient.dylib -> libmysqlclient_r.dylib
```

Ahora sí se puede (re)instalar php56 con la vieja librería mysql:

brew install php55 --with-httpd --with-libmysql  
brew install php56 --with-httpd --with-libmysql

Si ya instalaste php56, reemplazá `install` por `reinstall`.

### ¡Listo!

A codear se ha dicho.

![](img/1__o0RaJxltpHX03VGW9F__vrg.png)
