---
title:  "Git & Bitbucket: sobreescribir la historia de master/develop en Bitbucket"
categories: git bitbucket
tags: git, bitbucket, push, force
---

## TL;DR
Si estás seguro que querés sobreescribir la historia en la rama `develop` con un `git push -f` en un proyecto alojado en **Bitbucket** asegurate de sacar esta rama de:

1. Settings
1. Branch management
1. [Prevent history re-writes (rebase) on these branches](https://confluence.atlassian.com/bitbucket/branch-management-385912271.html#Branchmanagement-Preventhistoryre-writes(Gitonly))

De otro modo vas a recibir el siguiente mensaje:

```shell
$ git push -f
Total 0 (delta 0), reused 0 (delta 0)
remote: permission denied to force push branch develop
To https://xxxxxx@bitbucket.org/yyyyyy/zzzzzz.git
 ! [remote rejected] develop -> develop (pre-receive hook declined)
error: failed to push some refs to 'https://xxxxxx@bitbucket.org/yyyyyy/zzzzzz.git'
```

**Importante:** Sobreescribir la historia no es recomendado. Asegurate que nadie esté trabajando en esa rama mientras vos cometés este [acto criminal perverso](https://www.youtube.com/watch?v=AwRuXkpTP0Q).

**Importante 2:** Luego de sobreescribir la historia, volvé a incluir la rama en las opciones de Bitbucket para prevenir que algún otro criminal intente sobreescribir la historia.

## La historia completa que a nadie le importa

El otro día quería hacer _revert_ de un merge que _ya estaba pusheado en **origin**_ en el branch __develop__. El merge que había hecho no resultó como yo esperaba: resolví muy mal los conflictos. En un ataque de demencia, hice lo siguiente:

1. Descarte todo archivo no conflictuado.
1. Resolví el único archivo en conflicto.
1. Commiteé.
1. Luego volví a mergear _esperando que el proceso modifique los archivos que descarté inicialmente_.
1. [WTF!!!](https://media.giphy.com/media/deURfFYxgQEQ8/giphy.gif)

### 1er. intento: deshacer el merge
Lógicamente, pensé que con deshacer el merge era suficiente. Para ello seguí el querido tutorial [Undoing Merges](https://git-scm.com/blog/2010/03/02/undoing-merges.html). Pero claro, no era eso lo yo necesitaba. Yo quería mergear los archivos que descarté. ¿Por qué? Porque luego de deshacer el merge correctamente e intentar volver a mergear el branch a develop, Git inteligentemente intuía que debía descartar los archivos porque yo los descarté en el merge inicial. Hacer revert del revert del merge sólo me daría el archivo en conflicto. Desastre absoluto.

**Nota mental.** _Git is never wrong_.

![Git is never wrong](http://33.media.tumblr.com/166d05c49766a68d39b902c03e299cc2/tumblr_n54myile9s1tv2sd2o1_400.gif)

### 2do. intento: push force
Resignado, debía hacer algo totalmente en contra de cualquier recomendación: hacer un revert al commit previo al merge, y forzar un push al branch remoto.

_Suerte para mí: soy quién gestiona el proyecto. Podía romper el historial -con mucho cuidado- porque soy yo quién integra las características (de todos modos avisé que nadie toque nada en develo por las dudas)._

Mi historia había quedado muy sucia y por varios motivos, prefería destruir esa historia totalmente, para poder volver a realizar el merge como quería hacerlo originalmente.

En otras palabras: quería deshacer un historial sucio mediante una acción más sucia aún.

_Nasty._

![Nasty](https://media0.giphy.com/media/l2JJnuO6aYod49plK/200.gif)

Lo intenté. No funcionó. El error recibido era el siguiente.

```shell
$ git push -f
Total 0 (delta 0), reused 0 (delta 0)
remote: permission denied to force push branch develop
To https://xxxxxx@bitbucket.org/yyyyyy/zzzzzz.git
 ! [remote rejected] develop -> develop (pre-receive hook declined)
error: failed to push some refs to 'https://xxxxxx@bitbucket.org/yyyyyy/zzzzzz.git'
```

Lo raro era que hice esto varias veces (sí, no tengo miedo al decirlo) y no había recibido este error.

Luego de investigar por la web, encontré que esto era por una **medida de seguridad que Bitbucket tiene por defecto para los branches _master_ y _develop_**.

## La solución
Ingresás a tu proyecto en Bitbucket y luego vas a:

1. Settings
1. Branch management
1. Sacar la rama _develop o master_ de [Prevent history re-writes (rebase) on these branches](https://confluence.atlassian.com/bitbucket/branch-management-385912271.html#Branchmanagement-Preventhistoryre-writes(Gitonly))

![Prevent history re-writes (rebase) on these branches](https://confluence.atlassian.com/bitbucket/files/385912271/403505298/1/1379375652632/prevent-rewrites.png)

Luego de esto, podrás hacer `git push -f` sin recibir este error.

No olvidés volver a incluir la rama en **esta característica de seguridad** al terminar de realizar este [acto criminal](https://www.youtube.com/watch?v=AwRuXkpTP0Q).
