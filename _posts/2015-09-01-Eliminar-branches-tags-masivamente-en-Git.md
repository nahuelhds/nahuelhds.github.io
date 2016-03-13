---
layout: post
title:  "Eliminar branches/tags masivamente en Git"
categories: git
tags: git, branch, tag regexp
---

Siguiendo este tutorial ([http://blog.siyelo.com/how-to-bulk-delete-remote-git-tags/](http://blog.siyelo.com/how-to-bulk-delete-remote-git-tags/)) podemos ver cómo realizar una eliminación masiva de aquellos tags de nuestro proyecto que ya no necesitamos.

## El ejemplo

#### Supuestos
Sabemos que el comando para eliminar un tag es:

```shell
git push origin :refs/tags/<major>.<minor>.<fix>
```

Queremos eliminar todos los tags que pertenezcan a la *major version* 0.

Sabemos que `git ls-remote` nos da un *output* similar a lo siguiente:

```shell
d16aeb86430afc26fb17f182f567d39c8c732188 refs/tags/0.9
d16aeb86430afc26fb17f182f567d39c8c732188 refs/tags/0.9.6  
390c9a3251b813775ccdb96c375d50fed67d058f refs/tags/0.9.7
...
```

#### Eliminando
**Importante:** utilizar estos comandos con extrema precaución. Hagan backups y bla bla bla...

Con un poco de `regexp` podemos determinar que cada línea se compone de:

```
^(.*)  // El SHA al inicio de la línea (^)
(\s+)  // Algunos espacios
(.*)$  // La cadena de caracteres (no sólo texto) seguida del final de línea ($)
```

Ya tenemos la forma de nuestro `regexp`.

Pero antes de eliminar cualquier cosa, queremos ver qué vamos a eliminar. Ejecutamos lo siguiente:

```shell
git ls-remote --tags origin | awk '/^(.*)(\s+)(.*)$/ {print ":" $2}'
```

Si estamos contentos con el resultado, eliminamos...

```shell
git ls-remote --tags origin | awk '/^(.*)(\s+)(.*)$/ {print ":" $2}' | xargs git push origin
```

**Nota:** Si están en Windows, conviene utilizar GitBash para contar con los comandos tipo Linux.
