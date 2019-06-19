---
title: Accedé a las votaciones de Diputados Argentina de forma sistematizada
description: Todas las votaciones desde 1993 en formato SQL y CSV
date: '2019-04-20T23:21:52.120Z'
categories: []
keywords: []
slug: >-
  /@nahuelhds/acced%C3%A9-a-las-votaciones-de-diputados-argentina-de-forma-sistematizada-8028b0040e14
---

Pueden encontrar esta información en la repo GitHub que creé al respecto

[**nahuelhds/votaciones-ar-datasets**  
_Información sistematizada y normalizada de las votaciones de las Cámaras de Diputados y de Senadores de Argentina …_github.com](https://github.com/nahuelhds/votaciones-ar-datasets "https://github.com/nahuelhds/votaciones-ar-datasets")[](https://github.com/nahuelhds/votaciones-ar-datasets)

Desde hace unas semanas, andaba con ganas de cruzar datos de formas absurdas y divertidas, por fuera de los habituales análisis de datos de las consultoras políticas.

Busqué por la web a ver si ya existía esa información de forma abierta y sistematizada, cosa de poder empezar con eso sin más. No tuve suerte.

Si bien la Cámara de Diputados tiene el acceso a la información en la web, no se encuentra la misma de forma **programática** Partiendo de esta base, decidí programar un bot para descargar toda la información disponible en el sitio de la Cámara de Diputados de Argentina sobre las votaciones. Gracias a éste descargué toda la data disponible en el sitio en un par de horas (luego de algunos días de programación, claro).

A partir de allí, pude tomar esa información, construir una base de datos normalizada que me permite empezar a jugar con esos datos realizando consultas SQL.

Pura diversión nerd.

Si todo sale bien, en pocos días tendré disponibilizado un API para que cualquiera pueda consultar esta misma información a través de sus algoritmos.

Mientras tanto, los archivos de la base de datos en formato MySQL, así como los archivos CSV normalizados, se encuentran en la repo que compartí más arriba.