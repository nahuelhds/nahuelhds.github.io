---
layout: post
title:  "Guardando las credenciales Git"
date:   2016-03-03 12:00:00 -0300
categories: git
---

¿Querés evitar que Git pregunte todo el tiempo por tu usuario y contraseña en tu proyecto? Segun, [la documentación de Git](http://git-scm.com/docs/git-credential-store) basta con configurar el proyecto con el siguiente comando:

```shell
git config credential.helper 'store'
```

Es importante tener en cuenta que el archivo donde Git guarda las credenciales es accesible en `~/.git-credentials` (salvo que se especifique otra ruta mediante `--file=<path>`). Por lo que quien tenga acceso mediante el mismo usuario shell, podrá ver tu contraseña Git ya que la misma se guarda en formato plano (`usuario:contraseña@dominio.com`).

Por este motivo, es recomendable utilizar un usuario shell al que ninguna otra persona tenga acceso -o que sea de confianza-, ya que de otro modo, accediendo mediante el mismo usuario shell podrá acceder al archivo  `~/.git-credentials` y ver las contraseñas para los usuarios Git allí guardados. En otras palabras, y a modo de regla general: *para cada usuario Git debe existir un usuario shell diferente*.

Si trabajamos de forma local, nada de esto debe preocuparnos -¿o sí?.
