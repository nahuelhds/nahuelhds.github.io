---
lang: es
title: Habilitar acceso remoto MySQL en Ferozo
description: "Quien haya trabajado con DonWeb \U0001F92E\U0001F92E\U0001F92E sabe que utiliza Ferozo para la gestión de los servidores dedicados, y que por ende realizar…"
date: '2019-05-14T11:19:15.795Z'
categories: 
  - server
keywords:
  - ferozo
  - acceso-remoto
  - mysql
---

Quien haya trabajado con DonWeb 🤮🤮🤮 sabe que utiliza Ferozo para la gestión de los servidores dedicados, y que por ende _realizar acciones que son triviales con CPanel_ **suelen ser bastante tediosas**.

Este es uno de esos casos: el acceso remoto se habilita por SSH únicamente; por lo que habiendo accedido al home del usuario **root**, se ejecuta…

```sh
./habilita-acceso.sh NOMBRE-BASE-DATOS USUARIO PASSWORD
```

**Fuente:** [http://donwebayuda.com/como-habilitar-el-acceso-remoto-a-mis-bases-de-datos/](http://donwebayuda.com/como-habilitar-el-acceso-remoto-a-mis-bases-de-datos/)
