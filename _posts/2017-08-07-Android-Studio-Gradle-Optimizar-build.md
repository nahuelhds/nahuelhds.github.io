---
title:  'Android Studio - Optimizar tiempo de build de Gradle'
categories: android 
tags: android, gradle, build
---

En mi caso, tengo un proyecto que demoraba aproximadamente 1 minuto en realizar el build inicial
y un tiempo similar por cada vez que quería volver a correrlo en el emulador, mientra iba desarrollando
modificaciones en el código.

Para acelerar el proceso de build se requiere de dos pasos:

1. Activar la opción de build paralelos modificando el archivo activando primero la opción `parallel`
1. Aumentar el tamaño de RAM dedicada al proceso de build paralelo (el famoso `heap size`)

Lo primero se logra modificando el `/gradle.properties` en la raíz del proyecto, incluyendo la siguiente línea:

```java
org.gradle.parallel=true
```

Lo segundo, se logra modificando el mismo archivo. De todos modos, para saber qué cantidad nos recomienda el proceso
debemos correr el build y prestar atención al siguiente mensaje:

```bash
To run dex in process, the Gradle daemon needs a larger heap.
# It currently has 1024 MB.
# For faster builds, increase the maximum heap size for the Gradle daemon to at least 4608 MB (based on the dexOptions.javaMaxHeapSize = 4g).
# To do this set org.gradle.jvmargs=-Xmx4608M in the project gradle.properties.
# For more information see https://docs.gradle
```

Como se ve, en mi caso el heap size era de 1024m y me recomendaba levantarlo a 4g, por lo que en `gradle.properties`
agregué la siguiente línea:

```java
org.gradle.jvmargs=-Xmx4608M 
```

Con estas dos modificaciones, el tiempo del primero build pasó de 1 min a 30 seg y los siguientes builds pasaron de 1 min a 10 seg.
Tiempos considerables, realmente.
