---
lang: es
title:  "Atom - Plugins y configuraciones"
categories: atom
tags: atom
---

Este post es más bien para registor propio, pero... nunca está de más compartir:

## Plugins

#### git-plus
[https://atom.io/packages/git-plus](https://atom.io/packages/git-plus)

## Configuraciones

#### Auto indentación del código
[http://stackoverflow.com/questions/22611377/auto-indent-code-in-atom-editor](http://stackoverflow.com/questions/22611377/auto-indent-code-in-atom-editor)

#### Posibilitar el ingreso del arroba (@)
En el archivo `keymap.cson`...

```
'atom-text-editor':
  'ctrl-alt-q': 'unset!'
```

#### Auto-indent
```
'atom-text-editor':
  'alt-shift-f': 'editor:auto-indent'
```
