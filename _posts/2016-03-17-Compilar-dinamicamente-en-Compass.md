---
layout: post
title:  "Compilar dinámicamente en Compass"
date:   2016-03-17 20:23 -03:00
published: false
categories: sass
tags: sass, scss, compass
---

## Situación
Tengo un proyecto donde los _assets_ no están centralizados en una misma carpeta. Para peor, la carpeta *scss* puede estar en cualquier lado.

## Objetivo
Compilar todas las carpetas *scss*, y que dentro de una carpeta *css* que esté a la misma altura se generen los _css_ compilados.
Visualmente la idea es la siguiente

```shell
- dir1
--- css   # Carpeta destino
--- scss  # Carpeta fuente
----- archivo.scss
- dir2
--- dir2.1
----- css   # Carpeta destino
----- scss  # Carpeta fuente
------- archivo2.scss
- dir3
--- dir3.1
--- dir3.2
----- dir3.2.1
------- css   # Carpeta destino
------- scss  # Carpeta fuente
--------- archivo2.scss
```

Así de _random_...

## Solución

Crear un script bash que haga uso de la función *find* para luego ejecutar *compass compile* brindándole la configuración mediante otro archivo *config.rb* creado para este fin.

## Paso a paso
