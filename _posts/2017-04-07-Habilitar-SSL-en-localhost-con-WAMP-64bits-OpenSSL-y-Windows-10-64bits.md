---
title:  "Localhost - Habilitar SSL en Windows 10 64bits con WAMP 64bits y OpenSSL"
categories: ssl
tags: servidor, localhost, ssl, https, windows 10, wamp, openssl, wampserver, 64bits
published: true
---

Si precisás habilitar SSL para algún proyecto local en Windows, sabé que puede
ser un dolor de cabeza.

Mi ambiente es el siguiente:
- Windows 10 64bits.
- WampServer Version 3.0.4 64bit
- Apache 2.4.18

### Importante
Es necesario utilizar una versión de **OpenSSL** que no sea la nativa de WAMP.
Yo lo descargue de acá [https://sourceforge.net/projects/openssl/](). El archivo
descargado fue https://ufpr.dl.sourceforge.net/project/openssl/openssl-1.0.2j-fips-x86_64/openssl-1.0.2j-fips-x86_64.zip.

## TL;DR
Las instrucciones principales se encuentran en el propio foro de [WampServer](http://forum.wampserver.com/read.php?2,137505,137522#msg-137522)

Si Apache no levanta, seguramente haya algo mal. Los que me surgieron a mi los
menciono en el apartado que sigue.

Ustedes, pueden ver sus errores explícitamente ejecutando `httpd` directamente,
a través de `cmd`

```ssh
cd \\wamp\bin\apache\apachex.y.z\bin
httpd -t
```

Eso va a dar el mensaje de error del archivo de configuración y en qué línea.

## Errores que me surgieron en el proceso

### OpenSSL nativo en WAMP: "No se encuentra el ordinal (...)"

En *WampServer 64bits*, el ejecutable de **OpenSSL** no funciona
en *Windows 10 64bits*, por lo que es necesario descargar una versión que sí lo haga.

El error que daba al ejecutarlo era "No se encuentra el ordinal 113 en la
biblioteca de vínculos dinámicos". La solución es instalar OpenSSL por cuenta propia.

### WAMP httpd: "invalid command SSLCipherSuite"

Descomentar la línea del archivo de configuración `httpd.conf`.

```apache
LoadModule ssl_module modules/mod_ssl.so
```

Seguir instrucciones del artículo fuente.

**Fuente:** http://impradeep.com/invalid-command-sslciphersuite-perhaps-misspelled-or-defined-by-a-module-not-included-in-the-server-configuration/

### WAMP httpd: "Cannot load modules/mod_ssl.so into server"

Dos posibles soluciones, de las cuales a **mi me funcionó la segunda**.

#### Incluir DLL de OpenSSL en el directorio de Windows
Hay que instalar una versión de OpenSSL distinta. Ver esta respuesta en StackOverlow y seguir dichas instrucciones: http://stackoverflow.com/questions/40017498/cannot-load-modules-mod-ssl-so-into-server

#### Reemplazar libeay32.dll y ssleay32.dll en el directorio de Apache
Por algún extraño motivo los archivos libeay32.dll y ssleay32.dll que vienen
nativamente en WAMP 64 no funcionan con el módulo SSL. Es necesario descargar
una versión de Apache 32bits y copiar y pegar esos mismos archivos en
`\\wamp\bin\apache\apachex.y.z\bin`.

Yo tomé los archivos de esta versión de Apache: https://www.apachelounge.com/download/win32/. Explícitamente de este vínculo: https://www.apachelounge.com/download/win32/binaries/httpd-2.2.32-win32.zip.

**Fuente:** http://serverfault.com/questions/477706/apache-ssl-on-64-bit-windows-not-a-valid-win32-application.
