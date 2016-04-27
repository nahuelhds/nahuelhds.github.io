---
title:  "Problemas instalando Supersonic"
categories: mobile
tags: supersonic, steroids, appgyver, grunt, grunt-contrib
---

Este fin de semana estuve probando un poco de [Supersonic](http://www.appgyver.io/supersonic), el fork de [Ionic](http://ionicframework.com/) hecho por la gente de [AppGyver](http://www.appgyver.io/) para su hybrid apps tool [Steroids²](http://www.appgyver.io/steroids).

La realidad es que la instalación es más que sencilla y basta con seguir [el wizard que ellos mismos proveen](https://academy.appgyver.com/installwizard/steps).

El "problema" (tampoco es tan grave) ocurrió cuando estaba realizando el tutorial para generar la primer aplicación: [First mile: App on device in 5 minutes](http://docs.appgyver.com/supersonic/tutorial/first-mile/#overview). Luego de ejecutar `steroids create myProject` correctamente, al intentar conectar al proyecto mediante **steroids** se mostraron varios mensajes de errores por la inexistencia de dependecias.

El error en cuestión es el siguiente

```shell
            __   AppGyver           .__    .___
     ______/  |_  ___________  ____ |__| __| _/______ 2
    /  ___\   ___/ __ \_  __ \/  _ \|  |/ __ |/  ___/
    \___ \ |  | \  ___/|  | \(  <_> |  / /_/ |\___ \
   /____  >|__|  \___  |__|   \____/|__\____ /____  >
        \/           \/                     \/    \/

>> Local Npm module "grunt-contrib-sass" not found. Is it installed?
>> Local Npm module "grunt-extend-config" not found. Is it installed?

Running "steroids-make-fresh" task
>> Local Npm module "grunt-extend-config" not found. Is it installed?
>> Local Npm module "grunt-contrib-clean" not found. Is it installed?
>> Local Npm module "grunt-extend-config" not found. Is it installed?
>> Local Npm module "grunt-contrib-coffee" not found. Is it installed?
>> Local Npm module "grunt-extend-config" not found. Is it installed?
>> Local Npm module "grunt-extend-config" not found. Is it installed?
>> Local Npm module "grunt-contrib-sass" not found. Is it installed?
Loading "steroids-module-compile-default-native-styles.coffee" tasks...ERROR
>> TypeError: grunt.extendConfig is not a function
>> Local Npm module "grunt-extend-config" not found. Is it installed?
>> Local Npm module "grunt-contrib-coffee" not found. Is it installed?
Loading "steroids-module-compile-coffeescript.coffee" tasks...ERROR
>> TypeError: grunt.extendConfig is not a function
>> Local Npm module "grunt-extend-config" not found. Is it installed?
>> Local Npm module "grunt-contrib-concat" not found. Is it installed?
Loading "steroids-module-concat-javascript.coffee" tasks...ERROR
>> TypeError: grunt.extendConfig is not a function
>> Local Npm module "grunt-extend-config" not found. Is it installed?
>> Local Npm module "grunt-contrib-copy" not found. Is it installed?
Loading "steroids-module-copy-javascript.coffee" tasks...ERROR
>> TypeError: grunt.extendConfig is not a function
Loading "steroids-module-compile-scripts.coffee" tasks...ERROR
>> TypeError: grunt.extendConfig is not a function
>> Local Npm module "grunt-extend-config" not found. Is it installed?
Loading "steroids-module-compile-views.coffee" tasks...ERROR
>> TypeError: grunt.extendConfig is not a function
>> Local Npm module "grunt-extend-config" not found. Is it installed?
Loading "steroids-module-copy-assets.coffee" tasks...ERROR
>> TypeError: grunt.extendConfig is not a function
>> Local Npm module "grunt-extend-config" not found. Is it installed?
>> Local Npm module "grunt-contrib-copy" not found. Is it installed?
Loading "steroids-module-copy-default-native-styles.coffee" tasks...ERROR
>> TypeError: grunt.extendConfig is not a function
>> Local Npm module "grunt-contrib-copy" not found. Is it installed?
>> Local Npm module "grunt-extend-config" not found. Is it installed?
>> Local Npm module "grunt-contrib-copy" not found. Is it installed?
>> Local Npm module "grunt-extend-config" not found. Is it installed?
>> Local Npm module "grunt-contrib-copy" not found. Is it installed?
>> Local Npm module "grunt-extend-config" not found. Is it installed?
>> Local Npm module "grunt-extend-config" not found. Is it installed?
Loading "steroids-setup-cloud-resources.coffee" tasks...ERROR
>> TypeError: grunt.extendConfig is not a function
>> Local Npm module "grunt-extend-config" not found. Is it installed?
Loading "steroids-setup-features.coffee" tasks...ERROR
>> TypeError: grunt.extendConfig is not a function

Running "steroids-check-project" task
Warning: grunt.extendConfig is not a function Use --force to continue.

Aborted due to warnings.
```
El propio mensaje de error es bastante elocuente: "Is it installed?". No, no están instalados y esto es debido a que [grunt-contrib](https://github.com/gruntjs/grunt-contrib) está obsoleto (_This grunt-contrib plugins hoarder bundle is DEPRECATED_) y ya no instala el paquete con las funcionalidades habituales como antes hacía, por lo que hay que instalarlas manualmente por separado.

En nuestro caso lo que necesitamos es ejecutar lo siguiente:

```shell
npm install grunt grunt-extend-config grunt-contrib-clean grunt-contrib-coffee grunt-contrib-sass grunt-contrib-concat grunt-contrib-copy
```

Listo, ya está todo y instalado. Ahora sí podemos conectar normalmente al proyecto mediante `steroids connect` y continuar con el tutorial de [First mile: App on device in 5 minutes](http://docs.appgyver.com/supersonic/tutorial/first-mile/#overview).
