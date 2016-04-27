---
title:  "Debug mobile en Windows con Weinre"
categories: mobile
tags: mobile, ios, weinre, debug
---

**Nota:** El ejemplo está hecho pensado en debuggear iOS pero, como dice el título, aplica para cualquier dispositivo.

El tutorial es

[https://www.smashingmagazine.com/2014/09/testing-mobile-emulators-simulators-remote-debugging/2/](http://www.smashingmagazine.com/2014/09/03/testing-mobile-emulators-simulators-remote-debugging/2/)

### Instalando Weinre

Instalás weinre con node:

```shell
npm install -g weinre
```

Después lo inicializamos en el shell para que escuche todas las conexiones

```shell
weinre --boundHost -all-
```

Desde el navegador, ingresamos a la **página de debugging** [http://localhost:8080/client/#anonymous](http://localhost:8080/client/#anonymous)

### Iniciando el debugging
En la página que se quiere debuggear, y suponiendo que la computadora está en la red en la IP `192.168.1.47`, incluir el siguiente script:

```html
<script type="text/javascript" src="http://192.168.1.47:8080/miProyecto/target-script-min.js#anonymous"></script>
```

Hecho eso, se ingresa a la página desde el dispositivo iOS `http://192.168.1.47/miProyecto/`. Ahora, si vamos a la **página de debugging** veremos que un dispositivo se conectó (nuestro celular). En esa página estarán disponibles las herramientas de desarrollador.

¡Magia!
