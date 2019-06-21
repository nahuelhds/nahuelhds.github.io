---
lang: es
title:  "Instalar Compass en CentOS"
categories: sass
tags: centos, sass, compass, ruby
---

Para instalar Ruby, recomiendo [leer un post elaborado el año pasado al respecto](2016-03-17-Actualizar-Ruby2-en-CentOS.md).

Particularmente, Compass da error si se instala Ruby 2.5.x Entonces es necesario
instalar la versión 2.4.x. Dicho esto, basta con correr los siguientes comandos:

```shell
gem install --no-rdoc --no-ri sass -v 3.4.22
gem install --no-rdoc --no-ri compass
```
**Fuente**: [https://stackoverflow.com/a/39452453/1588525](https://stackoverflow.com/a/39452453/1588525)
