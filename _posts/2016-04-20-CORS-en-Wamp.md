---
lang: es
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

## Configuración
La configuración puede realizarse en un host virtual o directamente en el `htaccess`.

### Desde el virtual host
Siguiendo el ejemplo, ingresaríamos al archivo `D:\wamp\bin\apache\apache2.4.9\conf\extra\httpd-vhosts.conf`. Si quisieramos configurar CORS
para todos los dominios dentro de localhost, definiríamos:

```
<VirtualHost *:80>
    ServerAdmin webmaster@localhost
    DocumentRoot "D:\wamp\www"
    ErrorLog "logs/mysite.log"
    CustomLog "logs/mysite-access.log" common

    <Directory "D:\wamp\www">
        AllowOverride All
        Order allow,deny
        Allow from all

        # ... otras configuraciones ...

        # CORS
        Header set Access-Control-Allow-Origin: *
        # Permitimos requests ajax
        Header set Access-Control-Allow-Headers: X-Requested-With
    </Directory>
</VirtualHost>
```

### Desde htaccess
Si no es necesario habilitar CORS para todo el servidor local, y por el contrario
basta con activarlo para un solo dominio, basta con crear un `.htaccess` dentro
del directorio del proyecto e incluir las siguientes líneas:

```
# CORS
Header set Access-Control-Allow-Origin: *
# Permitimos requests ajax
Header set Access-Control-Allow-Headers: X-Requested-With
```
