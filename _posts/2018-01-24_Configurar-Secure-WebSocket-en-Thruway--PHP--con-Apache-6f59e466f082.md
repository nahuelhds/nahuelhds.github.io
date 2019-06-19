---
title: Configurar Secure WebSocket en Thruway (PHP) con Apache
description: >-
  Si tenés un servidor websocket funcionando con voryx/Thruway probablemente
  quieras configurarlo para trabar bajo protocolo de encriptación…
date: '2018-01-24T03:33:06.722Z'
categories: []
keywords: []
slug: /@nahuelhds/configurar-secure-websocket-en-thruway-php-con-apache-6f59e466f082
---

![](img/1__N08XZ82dODX22Nuw0H1J0w.jpeg)

Si tenés un servidor websocket funcionando con [voryx/Thruway](https://github.com/voryx/Thruway) probablemente quieras configurarlo para trabar bajo protocolo de encriptación segura en los navegadores (wss://).

**Es importante destacar que esta configuración no requiere modificar nada del servidor Wamp. Sólo se necesita modificar la configuración de Apache y la URL utilizada por el cliente Wamp que utilizará el protocolo seguro.**

Voy a compartir la configuración con la que logré hacerlo andar, pero básicamente la guía de por dónde conectar los cabos [la tomé de este issue de GitHub](https://github.com/voryx/Thruway/issues/66).

**Importante:** la comunicación entre Apache y Thruway no estará encriptada, pero sí lo estará entre el navegador y Apache.

### Un poco de contexto…

1.  Mi servidor Wamp trabaja en el puerto `9090` (escuchando`0.0.0.0`)
2.  Mi cliente AutobahnJS conecta bien a`ws://127.0.0.1:9090`
3.  Quiero utilizar el mismo puerto seguro 443 también para la conexión wss.

### Configuración de Apache

#### httpd.conf

Necesitás modificar el archivo`httpd.conf` agregando los siguientes módulos:

1.  mod\_proxy
2.  mod\_proxy\_wstunnel

#### httpd-vhost.conf

Luego, es necesario configurar el virtual host para la conexión HTTPS y la redirección WSS al WS mediante el proxy:

```
<VirtualHost *:443>  # Configuración SSL habitual  ServerName my-site.test
```

```
SSLEngine on  SSLCertificateFile "/usr/local/etc/httpd/server.crt"  SSLCertificateKeyFile "/usr/local/etc/httpd/server.key"
```

```
DocumentRoot "/Users/nahuelhds/Sites/my/site"  <Directory  "/Users/nahuelhds/Sites/my/site">    Options +Indexes +FollowSymLinks +MultiViews    AllowOverride All    Require local  </Directory>
```

```
  # Websocket proxy  # wss redirigie al ws funcionando de la manera habitual  ProxyPass /wss ws://127.0.0.1:9090 retry=0 keepalive=On   ProxyPassReverse /wss ws://127.0.0.1:9090 retry=0 </VirtualHost>
```

Reiniciar Apache para que los cambios sean impactados.

### WebSocket Client URL

Ya podés usar esta URL para el WebSocket Seguro: `wss://my-site.test/wss`

Para testear que funcione correctamente se puede utilizar la herramienta [http://www.websocket.org/echo.html](http://www.websocket.org/echo.html)