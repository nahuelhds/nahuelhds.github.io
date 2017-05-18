---
title:  "Levantar Websocket PHP manualmente"
categories: websocket
tags: server, centos, websocket, voryx, thruway
---

En post no muy lejano, expliqué [cómo instalar un servidor y cliente de Websocket PHP](2016-02-02-Instalando-Websocket-PHP-en-CentOS-7.md). En este caso vamos a ver
cómo levantarlo y matarlo manualmente en un servidor CentOS.

# ¿Cuándo intentar la implementación manual?
Hay casos donde no es posible configurar un daemon. Dada la situación, se podría
pensar en configurar al menos con [gulp](http://gulpjs.com/) una tarea para
levantar el ws manualmente a través del comando `nohup`

```shell
nohup php /opt/ws/serverWithClient.php > /opt/ws/ws_log 2>/opt/ws/error_log &
```

De este modo, todo el dump que genere el archivo será guardado en un **ws_log**
para poder tener un registro de lo que se va generando. Adicionalmente, el archivo
**error_log** contendrá cualquier error que pueda surgir con la ejecución del script.

**Fuente:** http://stackoverflow.com/questions/4797050/how-to-run-process-as-background-and-never-die

## Matar el proceso activo

Para el caso de un reinicio del proceso, se debe buscar el *PID* del proceso php que está corriendo el archivo. Luego, con ese dato matar el proceso en cuestión

```shell
ps aux | grep "/opt/ws/serverWithClient.php"
```

Esta ejecución brindará un resultado similar al siguiente
```
root      2613  0.0  0.2 264144 19972 pts/0    S    13:19   0:00 php /opt/ws/serverWithClient.php
root      3187  0.0  0.0 103460  1164 pts/0    S+   13:25   0:00 grep --color php /opt/ws/serverWithClient.php
```

**Importante:** la segunda fila refiere a la búsqueda que acabamos de hacer.
Nótese que el proceso es "grep" y no "php" como sucede en la primera. A nosotros nos interesa matar el
proceso "php" relacionado

Entonces, el PID es el número de la segunda columna. En nuestro caso, es "2613".
Con ese número luego se ejecuta:

```shell
kill 2613
```

Con el proceso finalizado, ahora podemos proceder con el reinicio del proceso websocket detallado en el apartado anterior.

## Comprobar funcionamiento
Ingresar a http://www.websocket.org/echo.html y probar la dirección del websocket
`ws://<url>:9090`. El resultado debe ser "this browser supports WebSocket".
