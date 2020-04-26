---
lang: es
title: "Bots de Twitter y diarios de Uruguay 🇺🇾"
excerpt: >-
  Un repaso sobre cómo llegué a crear bots de Twitter para el seguimiento y registro de artículos de distintos diarios uruguayos🇾
categories:
    - bots
keywords:
    - twitter
    - bots
    - python
    - diffengine
    - rss
---

Bueno, hace unos días hice públicos unos bots que armé para monitorear las noticias que publican algunos medios de prensa uruguayos 🇺🇾

El país
- 📰 [@elpaisuy](https://twitter.com/elpaisuy)
- 🤖 [@ep_diff](https://twitter.com/ep_diff)

El observador
- 📰 [@ObservadorUY](https://twitter.com/ObservadorUY)
- 🤖 [@ob_diff](https://twitter.com/ob_diff)

La diaria
- 📰 [@ladiaria](https://twitter.com/ladiaria)
- 🤖 [@ld_diff](https://twitter.com/ld_diff)

Montevideo portal
- 📰 [@portalmvd](https://twitter.com/portalmvd)
- 🤖 [@mp_diff](https://twitter.com/mp_diff)

Semanario Brecha
- 📰 [@SemanarioBrecha](https://twitter.com/SemanarioBrecha)
- 🤖 [@sb_diff](https://twitter.com/sb_diff)

## Les cuento un poco más 👇

Primero que nada, pueden verlos a todos juntos funcionando en [esta lista](https://twitter.com/i/lists/1251295778045378561). Por supuesto, la idea es sumar más medios (LaRed21, La República, etc), así que si tienen alguno para sugerir, ¡me avisan! ☝️

### ¿Para qué? 🤔
Para ver cómo los distintos medios van moldeando la redacción de la noticia, desde que nace la noticia hasta que pasa el editor y le pone el “toque editorial”. ✍️

### ¿Cómo funciona? 🧐
Los bots leen la fuente RSS de cada medio cada hora. Si hay una diferencia respecto de la lectura anterior (sea URL, título o contenido), simplemente lo tuitean en un hilo.

Si detectan nuevas diferencias, continúan publicando sobre el mismo hilo. 🤖

Tiene varias ajustes para hacer aún. Por ejemplo, [@portalmvd](https://twitter.com/portalmvd) tiene problemas de acentos y todo el tiempo se detectan cambios por eso. Tengo que hacer que omita este tipo de cosas. No aportan a las diferencias que me gustaría destacar. Es un monitoreo editorial, no de redacción.

Otro caso de ejemplo es que [@ladiaria](https://twitter.com/ladiaria) cada tanto pone que se llegó al límite de consultas (la querida suscripción). Tendría que poder detectar que eso en realidad no es un cambio en la noticia.

Detalles que iré mejorando.

### ¿Cómo lo hice? 👨‍💻

Investigué lo que hizo [@j_e_d](https://twitter.com/j_e_d) con sus bots, que hacen lo mismo que acá pero sobre medios argentinos como Clarín o La Nación y encontré varias cuestiones interesantísimas...

Del proyecto este, nacen dos que toman caminos distintos para hacer lo mismo: leer fuentes RSS para realizar el monitoreo.

Uno armado por [@xuv](https://twitter.com/xuv), que es sobre el cual se basa por ejemplo el laburo hecho por [@cuasiperfecto](https://twitter.com/cuasiperfecto) en su bot [@canillita_uy](https://twitter.com/canillita_uy) que hace lo mismo que estos bots que publico hoy, pero todo en la misma cuenta-bot de TW (desarrollado casi a la vez que esto, apenas unas semanas antes jaja).

Y otro armado por [@edsu](https://twitter.com/edsu), que se llama “diffengine” (DE) y es sobre el cual partí yo. Me gustó más este porque además de publicar las diferencias en TW, las guarda en [@internetarchive](https://twitter.com/internetarchive) que, como ya sabemos, guarda para siempre lo que le pidamos.

De todos modos, a diffengine le hice algunos agregados, ya que por ejemplo publicaba todo, sí, pero de forma aislada y no como hilo. Así que mi primer mejora fue esa: que se publique en forma de hilo aquellas noticias sobre las que encuentran diferencias en el tiempo.

Hubieron otros agregados más técnicos:
- el cambio de motor de gecko a chrome,
- el paso de sqlite a postgresql,
- la posibilidad de generar una URL de autorización para las cuentas bots que quiero que usen este motor
- y finalmente, poder guardar datos sensibles a nivel de variables de entorno. Esto último para poder compartir el código del proyecto pero sin compartir datos sensibles.

Estas mejoras técnicas se hicieron para poder subir todo esto a servicios como Heroku, cosa de que quede corriendo en la nube y que no precise de mi máquina local para vivir.

Así que bueno, los que quieran chismear el código de diffengine + agregados, lo pueden hacer en la repo que tengo forkeada. 👇

<!-- markdownlint-disable MD033 -->
<div class="github-card" data-github="nahuelhds/diffengine" data-width="100%" data-height="auto" data-theme="default"></div>
<script src="//cdn.jsdelivr.net/github-cards/latest/widget.js"></script>
<!-- markdownlint-enable MD033 -->

Por otro lado, dejo también el proyecto que conecta los bots con este motor, acá 👇

<!-- markdownlint-disable MD033 -->
<div class="github-card" data-github="nahuelhds/diffbots" data-width="100%" data-height="auto" data-theme="default"></div>
<script src="//cdn.jsdelivr.net/github-cards/latest/widget.js"></script>
<!-- markdownlint-enable MD033 -->

Cualquier idea o mejora sobre esto, ¡me avisan!