---
title:  "Ferozo - Habilitar acceso remoto MySQL"
categories: servidor
tags: servidor, ferozo, mysql, remote
published: true
---

Quien haya trabajado con DonWeb, sabe que utiliza Ferozo para la gestión de los
servidores dedicados, y que por ende realizar acciones que son triviales con CPanel
suelen ser bastante tediosas. Este es uno de esos casos.

En este caso, habilitar acceso remoto a una base de datos MySQL se hace por SSH únicamente.
Habiendo accedido al home del usuario **root**, se ejecuta...

```
./habilita-acceso.sh NOMBRE-BASE-DATOS USUARIO PASSWORD
```

Fuente: http://donwebayuda.com/como-habilitar-el-acceso-remoto-a-mis-bases-de-datos/
