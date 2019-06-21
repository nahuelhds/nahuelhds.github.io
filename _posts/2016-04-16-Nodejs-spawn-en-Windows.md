---
lang: es
title:  "Node.js - Utilizar método Spawn en Windows"
categories: nodejs
tags: nodejs, spawn, windows
---

El otro día en [_node_](https://nodejs.org/en/) intenté utilizar [spawn](https://nodejs.org/api/child_process.html#child_process_child_process_spawn_command_args_options) por la utilidad de poder brindar feedback en tiempo real sobre la ejecución del proceso. Estando en Windows, me encontré con que falla al intentar utilizarla sin más. [Un verdadero problema](https://www.youtube.com/watch?v=gOW_azQbOjw).

## La solución
Instalar [cross-spawn-async](https://www.npmjs.com/package/cross-spawn-async).

```shell
npm install --save-dev cross-spawn-async
```

Luego en el archivo se utiliza como el método ya conocido, ya que éste es un [_drop in replacement_](https://en.wikipedia.org/wiki/Drop-in_replacement):

```shell
var spawn = require('cross-spawn-async')

spawn(command[, args][, options])
```

### Workaround
Si por alguna razón lo anterior no te resulta convincente, un _workaround_ podría ser lo siguiente.

```
require('child_process').spawn('cmd', ['/s', '/c', '"C:\\util\\mycmd.bat"'], {
  windowsVerbatimArguments: true
});
```

De todos modos, y como puede verse, esto no es ni de cerca [código multiplataforma](https://en.wikipedia.org/wiki/Cross-platform).
