---
lang: es
title:  "Xdebug & Atom: php-debug no respeta los breakpoints"
categories: atom
tags: atom, xdebug, php-debug
---

Al intentar utilizar [Xdebug](https://xdebug.org/) mediante [php-debug](https://atom.io/packages/php-debug) en [Atom](https://atom.io/), me sucedía que el debugger abría todo archivo envuelto en el Stack del proceso, __no respetando en absoluto los *breakpoints* configurados__.

El problema fue resuelto luego de _desactivar todas las casillas de PHP Exceptions_ en la configuración del plugin.

__Fuente__: [https://github.com/gwomacks/php-debug/issues/144#issuecomment-197302609](https://github.com/gwomacks/php-debug/issues/144#issuecomment-197302609)
