---
lang: es
title: Accedé a las votaciones de Diputados Argentina de forma sistematizada
description: Todas las votaciones desde 1993 en formato SQL y CSV
date: '2019-04-20T23:21:52.120Z'
categories:
  - datasets 
keywords:
  - data-science
  - conjunto-de-datos
  - diputados-argentina
  - votaciones
  - votos
  - actividad-parlamentaria
  - datos-abiertos
  - gobierno-abierto
  - open-data
  - open-gov
---

Pueden encontrar esta información en la repo GitHub que creé al respecto

<!-- markdownlint-disable MD033 -->
<div class="github-card" data-github="nahuelhds/votaciones-ar-datasets" data-width="100%" data-height="auto" data-theme="default"></div>
<script src="//cdn.jsdelivr.net/github-cards/latest/widget.js"></script>
<!-- markdownlint-enable MD033 -->

Desde hace unas semanas, andaba con ganas de cruzar datos de formas absurdas y divertidas, por fuera de los habituales análisis de datos de las consultoras políticas.

Busqué por la web a ver si ya existía esa información de forma abierta y sistematizada, cosa de poder empezar con eso sin más. No tuve suerte.

Si bien la Cámara de Diputados tiene el acceso a la información en la web, no se encuentra la misma de forma **programática** Partiendo de esta base, decidí programar un bot para descargar toda la información disponible en el sitio de la Cámara de Diputados de Argentina sobre las votaciones. Gracias a éste descargué toda la data disponible en el sitio en un par de horas (luego de algunos días de programación, claro).

A partir de allí, pude tomar esa información, construir una base de datos normalizada que me permite empezar a jugar con esos datos realizando consultas SQL.

Pura diversión nerd.

![](https://i.embed.ly/1/image?url=https%3A%2F%2Fi.giphy.com%2Fmedia%2FOMK7LRBedcnhm%2F200.gif&key=a19fcc184b9711e1b4764040d3dc5c07){: .img-responsive }

Si todo sale bien, en pocos días tendré disponibilizado un API para que cualquiera pueda consultar esta misma información a través de sus algoritmos.

Mientras tanto, los archivos de la base de datos en formato MySQL, así como los archivos CSV normalizados, se encuentran en la repo que compartí más arriba.
