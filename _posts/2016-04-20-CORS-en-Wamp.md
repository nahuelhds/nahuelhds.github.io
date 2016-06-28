---
title:  "Implementar CORS en WampServer"
categories: wamp
tags: cors, wamp, wampserver, apache, htaccess
---

Si por esas casualidades necesitás activar CORS para trabajar localmente, podés
hacerlo de la siguiente manera.

## Activar módulo headers de Apache

### Desde WampServer
Primero que nada es necesario tener el módulo Apache "headers" activado. Para ello
utilizamos el menu propio de WampServer que resulta por demás cómodo para estas activaciones.

![Apache headers_module](http://i.imgur.com/cYTgIad.png)

### Desde httpd.conf
Opcionalmente, podemos abrir el archivo de configuración de Apache `httpd.conf`,
ubicado en, por ejemplo, `D:\wamp\bin\apache\apache2.4.9\conf\httpd.conf`.
Dentro del archivo, buscamos y reemplazamos:

```
#LoadModule headers_module modules/mod_headers.so
LoadModule headers_module modules/mod_headers.so
```
