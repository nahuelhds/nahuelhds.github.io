---
layout: post
title:  "Dependencias de wkhtmltopdf 0.12 o superior"
categories: server
tags: wkhtmltopdf, centos
---

Con la versión 0.12 de [wkhtmltopdf](http://wkhtmltopdf.org/) es necesario instalar las librerías `libjpeg`.

Para ello, corremos lo siguiente:

```shell
yum install libjpeg libpng libXrender libXext fontconfig
```

Hecho.
