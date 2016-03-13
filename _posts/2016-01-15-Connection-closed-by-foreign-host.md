---
layout: post
title:  "Connection closed by foreign host"
categories: server
tags: wamp2.5, wamp, imagick
---

Al hacer deploy con *ant* de manera remota se me moría la conexión en cualquier lugar de la ejecución con el siguiente error

```shell
Connection closed by foreign host
```

Para solucionarlo, encontré el siguiente enlace: [http://www.hypertable.com/documentation/misc/ssh_maxstartups/](http://www.hypertable.com/documentation/misc/ssh_maxstartups/).

Allí se indica que algunos servidores, por defecto, permiten hasta 10 conexiones simultáneas a nivel SSH, lo cual es configurado mediante la variable `MaxStartups`. Por tal motivo, es necesario modificar esta propiedad que se encuenta en `/etc/sshd_config` o `/etc/ssh/sshd_config`.

```shell
MaxStartups 100
```

Luego es necesario reiniciar el servicio `sshd`.

```shell
service sshd restart
```

Hecho esto, el deploy funcionó sin problemas.
