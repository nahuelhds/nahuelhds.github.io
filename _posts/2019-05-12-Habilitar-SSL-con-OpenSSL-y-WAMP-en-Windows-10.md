---
lang: es
title: Habilitar SSL con OpenSSL y WAMP en Windows 10
excerpt: >-
  Si precisás habilitar SSL para algún proyecto local en Windows, seguramente ya
  sabés que puede ser un dolor de cabeza…
date: '2019-05-12T22:10:19.427Z'
categories: 
  - wamp
keywords:
  - ssl
  - windows10
  - openssl
  - wamp
---

![](img/0__HC__ouHIX5ypCpxsF.jpg)

Mi ambiente es el siguiente: Windows 10 x64, WampServer Version 3.0.4 64bits y Apache 2.4.18

### TL;DR

[Las instrucciones principales se encuentran en este post dentro del foro mismo de WampServer.](http://forum.wampserver.com/read.php?2,137505,137522#msg-137522)

Si Apache no levanta, seguramente haya algo mal. Los que me surgieron a mi los describo en la siguiente sección. Ustedes pueden ver sus errores explícitamente ejecutando `httpd` directamente, a través de **cmd**.

```
cd \\wamp\bin\apache\apachex.y.z\binhttpd -t
```

Eso va a dar el mensaje de error del archivo de configuración y en qué línea.

#### Importante

Es necesario utilizar una versión de **OpenSSL** que no sea la nativa de WAMP. Yo lo descargue de [la página de SourceForge](https://sourceforge.net/projects/openssl/). El archivo descargado fue [https://ufpr.dl.sourceforge.net/project/openssl/openssl-1.0.2j-fips-x86\_64/openssl-1.0.2j-fips-x86\_64.zip](https://ufpr.dl.sourceforge.net/project/openssl/openssl-1.0.2j-fips-x86_64/openssl-1.0.2j-fips-x86_64.zip).

### Errores que me surgieron

#### OpenSSL nativo en WAMP: “No se encuentra el ordinal (…)”

En _WampServer 64bits_, el ejecutable de **OpenSSL** no funciona en _Windows 10 64bits_, por lo que es necesario descargar una versión que sí lo haga.

El error que daba al ejecutarlo era “No se encuentra el ordinal 113 en la biblioteca de vínculos dinámicos”. La solución es instalar OpenSSL por cuenta propia.

#### WAMP httpd: “invalid command SSLCipherSuite”

Descomentar la línea del archivo de configuración `httpd.conf`.

```
LoadModule ssl_module modules/mod_ssl.so
```

Seguir instrucciones del artículo fuente.

**Fuente:** [http://impradeep.com/invalid-command-sslciphersuite-perhaps-misspelled-or-defined-by-a-module-not-included-in-the-server-configuration/](http://impradeep.com/invalid-command-sslciphersuite-perhaps-misspelled-or-defined-by-a-module-not-included-in-the-server-configuration/)

#### WAMP httpd: “Cannot load modules/mod\_ssl.so into server”

Dos posibles soluciones, de las cuales a **mi me funcionó la segunda**.

**Incluir DLL de OpenSSL en el directorio de Windows**

Hay que instalar una versión de OpenSSL distinta. Ver esta respuesta en StackOverlow y seguir dichas instrucciones: [http://stackoverflow.com/questions/40017498/cannot-load-modules-mod-ssl-so-into-server](http://stackoverflow.com/questions/40017498/cannot-load-modules-mod-ssl-so-into-server)

**Reemplazar libeay32.dll y ssleay32.dll en el directorio de Apache**

Por algún extraño motivo los archivos libeay32.dll y ssleay32.dll que vienen nativamente en WAMP 64 no funcionan con el módulo SSL. Es necesario descargar una versión de Apache 32bits y copiar y pegar esos mismos archivos en `\\wamp\bin\apache\apachex.y.z\bin`.

Yo tomé los archivos de [esta versión de Apache](https://www.apachelounge.com/download/win32/).

Explícitamente de este vínculo: [https://www.apachelounge.com/download/win32/binaries/httpd-2.2.32-win32.zip](https://www.apachelounge.com/download/win32/binaries/httpd-2.2.32-win32.zip).

**Fuente:** [http://serverfault.com/questions/477706/apache-ssl-on-64-bit-windows-not-a-valid-win32-application](http://serverfault.com/questions/477706/apache-ssl-on-64-bit-windows-not-a-valid-win32-application).
