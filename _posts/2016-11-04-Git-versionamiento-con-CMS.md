---
title:  "Git. Versionamiento con CMS"
categories: git
tags: contrinuous integration, ci, git, cms, joomla, wordpress
published: true
---

Lo siguiente es una idea de cómo versionar cambios en proyectos de tipo CMS,
donde es necesario tener control de los cambios en el código de parte de los
devs, así como también cambios que pueda realizar el cliente desde la
administración del CMS.

Más que nada, es necesario que cada cambio introducido no pise lo hecho por el
cliente.

# Antes de empezar
Tener a mano el título del **hotfix** para copiar y pegar fácilmente.
Si existe previamente un **hotfix**, eliminarlo con

```shell
git branch -d "hotfix/$cliente/$titulo"
```

## Publicando los cambios en la repo
Ingresar al servidor e ir a la repo, y luego ejecutamos los siguientes comandos

```shell
git checkout master
git status
```

Si hay cambios, primero stasheamos para no perder nada durante el proceso de creación del hotfix que integrará todo tanto en **master** como en **develop**.

```shell
git stash save "tmp"
git flow hotfix start "CODIGO-999-Integracion"
git stash pop
```

Ahora, ya tenemos los cambios replicados pero en el hotfix, entonces los commiteamos para luego publicar el hotfix y finalmente integrar todo de forma local, ya que en caso de conflicto es más cómodo trabajar desde allí

```shell
git add .
git commit -m "Integración YYYY.mm.dd"
git flow hotfix publish "CODIGO-999-Integracion"
```

## Finalizando la integración localmente

1. Hacemos pull de los cambios.
1. Checkout al hotfix nuevo.
1. Verificamos que no hayan archivos no deseados o bien algunos ajustes que sean requeridos (en general ninguno, pero nunca se sabe).
1. Finalizar el hotfix para que mergee a master y develop.
1. Si surgen conflictos, resolverlos.
1. Pushear todo.

## Limpiando la repo remota
Volvemos al servidor, movemos la repo a master, hacemos pull, eliminamos el hotfix publicado y finalmente dejamos los permisos al usuario correspondiente.

```shell
git checkout master
git pull
git branch -d "hotfix/$cliente/CODIGO-999-Integracion"
chown -R cpaneluser: *
```
