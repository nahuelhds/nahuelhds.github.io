---
title:  'Solución a npm install ...killed'
categories: node 
tags: node, npm, server
---

Si alguna vez se encuentran frente a la situación de correr `npm install`
y el proceso termina con un "Killed" entre sus líneas, el problema está en la poca memoria
asignada para correr el proceso.  La solución está en utilizar un archivo bash conocido como `npm-f3-install.sh`

El mismo [se puede encontrar en este gist](https://gist.github.com/SuperPaintman/851b330c08b2363aea1c870f0cc1ea5a).

Lo descargan, lo sitúan donde necesitar realizar la instalación y simplemente lo ejecutan.
