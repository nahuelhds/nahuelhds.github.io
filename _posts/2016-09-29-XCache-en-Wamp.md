---
lang: es
title:  "Instalar XCache en Wamp (Windows)"
categories: wamp
tags: xcache, windows, php, wamp
published: true
---

Instalación en Wamp: http://stackoverflow.com/questions/36233341/how-do-i-install-xcache-in-wamp-in-window
Habilitar Administración: https://xcache.lighttpd.net/wiki/InstallAdministration

En PrestaShop se activa XCache directamente desde el archivo config\settings.inc.php cambiando las variables por...

```
define('_PS_CACHING_SYSTEM_', 'CacheXcache');
define('_PS_CACHE_ENABLED_', '1');
```

Esto es debido a que al intentar configurarlo desde ps me daba error para sobreescribir el archivos settings
con mi amigo xdebug vi que el cambio eran esas dos variables
haciendo eso agarra vuelo
