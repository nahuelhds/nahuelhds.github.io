---
lang: es
title: Debugging React Native + Expo con Nuclide en Windows
description: La experiencia que pudo ser y no fue…
date: '2017-07-24T11:18:38.083Z'
categories: []
keywords: []
slug: /@nahuelhds/debugging-react-native-expo-con-nuclide-en-windows-dbe6fc4e154f
---

### TL;DR

Para una mejor experiencia de desarrollo de React Native en Windows, recomiendo fuertemente utilizar [VS Code](https://code.visualstudio.com/). Con dicho editor pude hacer debugging React Native tanto en Genymotion para Android así como **desde mi dispositivo remoto para iOS**.

### Mi experiencia

Nuclide puede que sea la mejor experiencia para debugging web. Pero cuando se trata de desarrollo mobile -y especialmente en dispositivos iOS siendo un usuario Windows- tiene varios faltantes que deben ser resueltos con algunos programas externos que logran cubrir dichos huecos -aunque no todos.

Luché literalmente un par de semanas para tener una buena configuración general hasta que logré codificar React Native con Flow y ESLint. A nivel codificación propiamente dicho funcionó excelente -especialmente en relación a la inteligencia del código. Estaba muy entusiasmado.

#### Intentando debugguear

Entrados varios días de desarrollo, tuve la necesidad de comenzar a debuguear la app. Y ahí es donde, como usuario de Windows, empecé a sufrir sentir la ausencia de soporte oficial (Facebook enfoca Nuclide específicamente al desarrollo en Mac). De todos modos, encontré algunas soluciones en cuanto a lo que debugging respecta.

Mi caso específico de entorno y herramientas de desarrollo es:

*   Windows 10 64 bits
*   Atom + [Nuclide](https://nuclide.io/)
*   [React Native](https://facebook.github.io/react-native/)
*   [Expo.io](https://expo.io/)

Lo complicado de toda la investigación era encontrar referencias cruzadas entre [CRNA (React Native Create App)](https://github.com/react-community/create-react-native-app), Expo y [React Native Cli](https://www.npmjs.com/package/react-native-cli). En todos los casos, el problema con [Nuclide Inspector](https://nuclide.io/docs/platforms/react-native/#element-inspector) es que:

1.  El packager que utiliza difiere del que utiliza Expo para lanzar la app.
2.  Al momento de conectar con el packager, lo hace buscando la conexión en un **puerto fijo que no se puede configurar de ningún modo** y se debe intentar hacerlo modificando archivos en los módulos instalados como dependencias del proyecto.

Adicionalmente, casi todos los casos de éxito de remote debugging en dispositivos iOS eran tutoriales de _desarrolladores Mac_. A medida que avanzaba en mi investigación mi frustación y decepción crecián: el único modo de debuggear hasta ahora era:

1.  Levantar el “Start remote JS debugging”.
2.  Utilizar la Chrome Dev Tools
3.  Incluir “debugger;” en donde quisiera que el código realice un breakpoint.

De ese modo podría ver el estado de las variables. Ahora bien, si quería realizar modificaciones en el código tendría que volver a Atom sin poder realizar las modificaciones allí mismo (como cuando realizamos js debugging en web).

#### React Native Debugger

Si bien nunca llegué a tener la mejor de las experiencias con el debugging, [React Native Debugger](https://github.com/jhen0409/react-native-debugger) me permitió obtener la posibilidad de incluir breakpoints en su programa (basado en [Electron](https://electron.atom.io/)). Comprende mejor el sourcemap de los archivos. Aunque es lo máximo que pude avanzar. No logré en ningún momento [modificar el archivo local tal como suelo hacer con las Chrome Dev Tools](https://developers.google.com/web/updates/2015/05/local-modifications).

### Conclusión

En el contexto de Windows, Nuclide es un gran avance en términos de codificación de nuevas tecnologías. Pero tal como advierten en su propio sitio web **no tiene aún compatibilidad oficial con Windows** y esa frase se hizo real cuando de debuguear se trata.

¿La solución? Utilizar [VS Code](https://code.visualstudio.com/).
