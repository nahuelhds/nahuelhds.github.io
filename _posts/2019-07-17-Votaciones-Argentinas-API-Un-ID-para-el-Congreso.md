---
lang: es
title: "API de Votaciones Argentinas 🇦🇷"
description: >-
  Ya se encuentra disponible una versión alpha para la consulta de las votaciones de Argentina.
date: "2019-06-19T13:49:59.026Z"
categories:
  - datos-abiertos
keywords:
  - opendata
  - votaciones
  - argentina
  - diputados
  - senadores
---

Acabo de publicar [Cómo Votó](https://www.comovoto.com.ar/). Por ahora es simplemente un API disponibilizado para consultas. No requiere autorización y [está documentado](https://www.comovoto.com.ar/docs/#general) lo suficiente como para que cualquier nerd que haya manejado APIs en algún momento de su vida, pueda interactuar con ella. 🤓

![Pantalla de bienvenida del proyecto](img/comovoto.com.ar.png)
Pantalla de bienvenida del proyecto
{: .img-caption }

**El proyecto está en estado alpha** por lo que es inestable y va a sufrir cambios; pero lo interesante es que ya puede utilizarse para generar consultas rápidas y hacer aplicaciones o clientes web con esta información. 🎉🎊🥳

## Sobre la calidad de los datos 🧐

En el proceso de armado, varios cracks de la ciencia de datos me fueron desasnando y alertando de la existencia de varios problemas comunes con estas fuentes de datos, es decir, los sitios oficiales de [Diputados](https://votaciones.hcdn.gob.ar/) y [Senadores](https://www.senado.gov.ar/votaciones/actas).

### Un ID para el Congreso #️⃣

El principal es que no hay un identificador único transversal a diputados y senadores -y cuando se pide la información publica de ello, ya ustedes saben. El problema no está tanto en las votaciones en sí, sino en la trazabilidad sobre los y las legisladores que las votan. Todo sería más fácil con un ID común. No sólo permitir este tipo de iniciativas sino también para análisis serios como muchos de los que se ven por la red.

Por suerte existen proyectos como [Cargografías](https://www.cargografias.org/) quienes se tomaron el trabajo de realizar la trazabilidad sobre las y los distintos representantes argentinos. Será cuestión de ver si es posible integrar esa información de algún modo a esta base de datos generada para este API.

### Consecuencias sobre la normalización y curación

Uno podría pensar:

-Bueno, seguro igual se puede normalizar y todo bien... 🤔

No contar con el DNI, CUIT o cualquier cosa que sirva como ID común entre ambas fuentes de datos es cuanto menos odios. Y depender de nombres y apellidos para la estructuración es por demás imperfecto, ya que según me mostraron y enseñaron gente que realmente trabaja de esto, existen de mínima gente que se llama igual (vaya obviedad, ¿no?) y otras cuestiones más problemáticas aún.
Por suerte, el dominio de datos del API se acota a lo digitalizado -del 93 a la actualidad, en el caso de Diputados y del 2010 a la fecha en el caso de Senadores. Eso reduce el margen de error, pero no lo elimina.

### ¿Y entonces qué se puede hacer? 🧙‍♂️

Por lo expuesto, la base de datos está sucia. Es mejorable, sí, pero mantiene un núcleo de "suciedad" en sus datos. El caso más común a priori es la duplicidad de legisladores: la misma persona votando en diputados y en senadores, figurando con mismo apellido y mismo nombre pero con una variante, lo que hace que a los efectos de la normalización sea considerado una persona distinta y por ende un ID distinto en el API.

Existen estrategias varias para solventar esta problemática. La más evidente es pensar en presentar esta información bajo una &&plataforma tipo wiki\*\*: algo donde cualquiera pueda editar, volver atrás un cambio, etc. Que comunitariamente sea posible alcanzar una curación con margen de error tendiente a 0.

De este modo, y siguiendo el ejemplo, la fuente de datos se mantiene intacta (el legislador sigue figurando dos veces) pero a nivel de la plataforma podemos marcar que esos dos registros refieren al mismo y en consecuencia, poder unificar sus acciones, votos, datos en una entidad superior que los una para luego presentarlo como la misma persona a nivel de API y a su vez, poder indicar qué fuente de datos se está viendo.

Así, a nivel de datos se alcanza la trazabilidad, a nivel de usuario se puede visualizar mejor esa información, y a nivel de fuente de datos se mantiene intacta la información de base, permitiendo el agregado de nuevos datos sin complejizar su carga.

## ¿Querés colaborar con el proyecto? 👨‍💻👩‍💻

Podés acceder al código en Github, levantar una issue, o forkear y jugar por tu cuenta.

<!-- markdownlint-disable MD033 -->
<div class="github-card" data-github="nahuelhds/votaciones-ar" data-width="100%" data-height="auto" data-theme="default"></div>
<script src="//cdn.jsdelivr.net/github-cards/latest/widget.js"></script>
<!-- markdownlint-enable MD033 -->

Si me querés contactar, mi cuenta de Twitter está en la firma de acá abajo. 👇
