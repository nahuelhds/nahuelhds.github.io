---
lang: es
title:  "Instalando Websocket PHP en CentOS 7"
categories: websocket
tags: centos7, centos, websocket, voryx, thruway, systemd
---

Instrucciones para instalar de forma efectiva la implementación de Websocket para PHP mediante [Voryx/Thruway](https://github.com/voryx/Thruway)

### Abrir el puerto 9090
Se requiere el puerto 9090 abierto para que javascript pueda conectarse desde el sitio. Entonces es necesario ingresar a WHM
1. ConfigServer Security & Firewall
1. Firewall Configuration
1. TCP_IN: agregar puerto 9090 al final del string
1. TCP_OUT: agregar puerto 9090 al final del string
1. Change

### Instalación y configuración del Websocket
Teniendo el proyecto instalado, movemos la implementación a un lugar compartido del servidor. En nuestro caso, utilizamos la carpeta `/opt`

```shell
cp -R <websocket_dir> /opt/<websocket_dir>
```

En mi caso, utilizo la ejecución del servidor Websocket con un cliente añadido, el archivo es el siguiente:

```php
<?php
// /opt/<websocket_dir>/serverWithClient.php

$dir = __DIR__;
require $dir . '/vendor/autoload.php';
require $dir . '/config.php';

use Thruway\Peer\Router;
use Thruway\Transport\InternalClientTransportProvider;
use Thruway\Transport\RatchetTransportProvider;
use WampPost\WampPost;

$router = new Router();

//////// WampPost part
// The WampPost client
// create an HTTP server on port 8181 - notice that we have to
// send in the same loop that the router is running on
$wp = new WampPost(WS_REALM, $router->getLoop(), WS_CLIENT, WS_CLIENT_PORT);

// add a transport to connect to the WAMP router
$router->addTransportProvider(new InternalClientTransportProvider($wp));
//////////////////////

// The websocket transport provider for the router
$transportProvider = new RatchetTransportProvider(WS_SERVER, WS_SERVER_PORT);
$router->addTransportProvider($transportProvider);
$router->start();
```

Como habrán visto se utilizan algunas constantes para la definición del cliente, puerto y servidor. Dichas constantes se definen en un archivo de configuración que incluyo a continuación:

```php
<?php
// /opt/<websocket_dir>/config.php

define ('WS_REALM'          , 'example.realm1');
define ('WS_CLIENT'         , '127.0.0.1');
define ('WS_CLIENT_PORT'    , 8181);
define ('WS_SERVER'         , '0.0.0.0');   // Importante
define ('WS_SERVER_PORT'    , 9090);
```

**Importante:** La definición del puerto del servidor como `0.0.0.0` es fundamental. De hecho, fue EL problema que me llevó horas descubrir. Para ser justo, tuve que pedirle ayuda a la gente de Voryx -mediante Github- quienes rápidamente me ayudaron a resolverlo.

Básicamente, esa definición significa *recibir cualquier petición que provenga de cualquier IP*. Lógicamente, esto se complementa con la apertura del puerto 9090 para efectivamente permitir que cualquier IP envíe peticiones al servidor WS.

### Creación y configuración del daemon
Crear el archivo `websocket.service` en la repo de `systemd` del usuario del servidor

```shell
vi /usr/lib/systemd/system/websocket.service
```

Pegar el contenido

```shell
[Unit]
Description=Websocket Server Daemon

[Service]
Type=simple
ExecStart=/usr/bin/php /opt/ws/serverWithClient.php
Restart=always

[Install]
WantedBy=multi-user.target
```

Para que este programa inicie cuando inica el Sistema operativo, ejecutamos el comando `enable` de systemd

```shell
systemctl enable websocket
```

Finalmente, damos inicio de forma manual al daemon que creamos y configuramos mediante el comando `start`.

```shell
systemctl start websocket
```

Para verificar el estado de la ejecución podemos utilizar el comando `status`.

```shell
systemctl status websocket
```

Ejemplo de respuesta OK (debe decir `Active: active (running)`).

```shell
websocket.service - Websocket Server Daemon
Loaded: loaded (/usr/lib/systemd/system/websocket.service; disabled; vendor preset: disabled)
Active: active (running) since Tue 2016-02-02 12:14:18 EST; 6min ago
Main PID: 10048 (php)
CGroup: /system.slice/websocket.service
└─10048 /usr/bin/php /opt/ws/serverWithClient.php
...
```

### Comprobar funcionamiento
Ingresar a [http://www.websocket.org/echo.html](http://www.websocket.org/echo.html) y probar la dirección del websocket `ws://<url>:9090`.

El resultado debe ser *"this browser supports WebSocket"*.

¡Listo!
