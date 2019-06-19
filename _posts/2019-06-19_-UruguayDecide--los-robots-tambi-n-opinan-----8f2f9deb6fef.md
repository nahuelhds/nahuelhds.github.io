---
title: "#UruguayDecide: los robots también opinan… `\U0001F916`"
description: >-
  Análisis de datos automatizado sobre el texto completo del debate entre entre
  Óscar Andrade y Ernesto Talvi, mediante técnicas de…
date: '2019-06-19T13:49:59.026Z'
categories: []
keywords: []
slug: /@nahuelhds/uruguaydecide-los-robots-tambi%C3%A9n-opinan-8f2f9deb6fef
---

En esta publicación vamos a ver cómo con un robot analizamos el #UruguayDecide que el pasado Jueves 13 de Junio tuvo a buena parte de la población expectante. 🇺🇾🇺🇾🇺🇾

![Así vería un robot a Óscar Andrade y a Ernesto Talvi respectivamente, luego de todo lo que dijeron durante el debate.](img/1__TwaO6HcPoAFWbXjgElX1pg.jpeg)
Así vería un robot a Óscar Andrade y a Ernesto Talvi respectivamente, luego de todo lo que dijeron durante el debate.

### ¿Un robot sacando conclusiones? 🤔

Bueno, quizás no sea tan así. Lo que es real es que a partir de algunos algoritmos y técnicas, las máquinas pueden realizar análisis de textos y a partir de allí brindarnos datos jugosos e interesantes.

A ese conjunto de algoritmos y técnicas se lo conoce como [**Procesamiento de Lenguaje Natural**](https://en.wikipedia.org/wiki/Natural_language_processing) (PLN o **NLP** por sus siglas en inglés). Para el análisis de este debate, programé un “bot” (un conjunto de algoritmos) donde se aplicó NLP sobre el debate de #UruguayDecide entre Andrade y Talvi.

El código de fue hecho en Python, utilizando las librerías [NLTK](https://www.nltk.org/) y [word\_cloud](https://amueller.github.io/word_cloud/). Por si hay algún **nerd** en la sala, les dejo el código del proyecto en Github para que lo puedan revisar en detalle.

[**nahuelhds/simple-text-analysis-nlp**  
_Algoritmos hechos en Python para analizar textos, tokenizarlos y generar nubes de palabras de forma simple. …_github.com](https://github.com/nahuelhds/simple-text-analysis-nlp "https://github.com/nahuelhds/simple-text-analysis-nlp")[](https://github.com/nahuelhds/simple-text-analysis-nlp)

Todo el material crudo que se produjo para esta publicación, [se encuentra en la carpeta de ejemplos](https://github.com/nahuelhds/rob-el-robot-nlp/tree/master/examples/andrade-vs-talvi).

### Así lo vio el bot 🤖

Para el análisis de texto que realiza el bot, a mayor cantidad de repeticiones _más grande es la palabra que se verá en la nube generada._

#### Óscar Andrade en anteojos computarizados 😎

En base a lo anterior, si le damos al bot todos los fragmentos de texto pronunciados por Óscar Andrade y le pedimos que nos muestre como él lo ve, la silueta/nube de palabras del precandidato sería la siguiente.

![](img/1__N9gDeNpjd4aVGNbk48Pp6g.jpeg)

Como somos medio cuadrados, y además nos gustan los numeritos, también generé en forma de gráfico de barras, donde además se compara: a misma palabra, cuántas veces la dijo su adversario durante el debate.

![](img/1__ihTeVmT__EAnlkDvuKr7JMw.png)

#### Ahora le toca a Ernesto Talvi 🧐

Aplicando las mismas acciones, al precandidato colorado lo veríamos del siguiente modo.

![](img/1__Nkahth1RG6LU3nXiNZbmyA.jpeg)

En cuanto a la _data dura_ de las palabras pronunciadas y en comparación a su adversario.

![](img/1__ynZaizHLjOB3LsS8tfxsbQ.png)

### Un robot sensible 🥺

Como para variar, también contamos con la posibilidad de detectar sentimientos en las frases que se pronuncian. Por lo que podríamos determinar si el debate fue una fiesta de flores y alegría, o un horror apocalíptico donde todos vamos a morir.

![Según el bot, el debate estuvo dominado por frases de carácter neutral.](img/1__Lsf__8FkPcIS1sX0tU77aBQ.png)
Según el bot, el debate estuvo dominado por frases de carácter neutral.

Como se puede apreciar, el debate no fue muy Disney que digamos, aunque tampoco el horror personificado. Por el contrario, **el debate** tuvo momentos de frases consideradas negativas y más que nada **se vistió de neutralidad en el discurso** lo cual -agrego yo- es esperable para un debate de caracter institucional y democrático.

🇺🇾🇺🇾🇺🇾¡Uruguay nomá! 🇺🇾🇺🇾🇺🇾

#### Las frases más “negativas”

Es importante destacar que esta categorización de “frases negativas” no necesariamente es porque éstas sean hirientes, insultos, o cosas del estilo; sino más bien que apunta a su concepto general.

Veamos…

> “Creo que es un mérito. Es algo que nos convocaban las juventudes de todos los partidos políticos cuando, en el aniversario del Río de Libertad, pedían por una campaña sin enchastre. Por una campaña sin descalificación. Por una campaña sin provocaciones y ojalá sostengamos hasta el último domingo de Octubre que el debate sea de esta manera: sea sobre la base de ideas y pudiendo darnos la mano al final del debate” — Óscar Andrade

> “En el año 2004 el Uruguay de 2002 a 2004 vivió la peor crisis de su historia como país independiente. No por errores de gestión sino porque sufrimos un contagio severo de la aftosa y una crisis bancaria que heredamos de la Argentina.” — Ernesto Talvi

Esas son las frases más “negativas” de cada precandidato.

Sin riesgo a equivocarme, se puede apreciar que no son comentarios horribles en sí sino que _la idea general de la frase alude a cuestiones de ese tono:_ las campañas de golpes-bajos, por un lado, y la crisis de 2002, por el otro.

### Un robot muy atento 🤩

Siguiendo con el análisis, utilizamos estos algoritmos para determinar el _universo lingüístico_ de cada persona a la que escucha.

No es que estemos hablando de algún término netamente técnico, pero básicamente entendemos por universo lingüístico a la _cantidad y diversidad en el vocabulario que una persona expresa al hablar_. Este análisis es más certero cuanto más texto tenemos de una persona. La realidad es que un debate no es mucho tiempo, por lo que los datos que nos provee para este caso son superficiales, pero sirven para tomar referencias (y divertirnos, claro).

![](img/0__JSIVFJkqlelDcV31.jpg)

Sobre el eje Y, vemos la _cantidad de repeticiones_. Sobre el eje X la _diversidad en el vocabulario_. Sabiendo esto, lo que podemos observar es que Andrade tuvo durante sus intervenciones una diversidad levemente mayor en palabras, aunque las pronunció menos veces. Por su parte, Talvi lo contrario: apenas menos diversidad, y más repeticiones.

Un corolario es que al ser tan parejas las tendencias, las cantidades y las repeticiones podríamos concluir que efectivamente **las intervenciones fueron parejas para cada uno en el tiempo** (lo que es esperable de un debate con espacios pautados y cronometrado, ¿no?).

Punto para Daniel Castro y su moderación 🥳

### Un robot muy zen 💆‍♂️

Si bien el bot es capaz de procesar muchísima información a la vez, también es posible hacer uso de su gran capacidad de resumen: es capaz de tomar todo un discurso y resumirlo a sus ideas centrales, representadas en dos o tres frases. Parece demasiado fantástico pero es sorprendentemente acertado en cuanto a los resultados con textos grandes.

Según el bot, estas fueron las tres ideas/conceptos de cada precandidato en todas sus intervenciones.

#### Lo fundamental de Óscar Andrade

![Óscar Andrade en el acto 48 aniversario del Frente Amplio. Foto: Darwin Borrelli](img/0__C67MqLcQFndI6I1C.jpg)
Óscar Andrade en el acto 48 aniversario del Frente Amplio. Foto: Darwin Borrelli

La primera frase, _la que resume todo_, fue pronunciada en el contexto del cuarto eje del debate, sobre el rol del Estado en la economía y en la vida, y en referencia a los docentes, la educación y la investigación.

> “Cuando tenían sueldos de miseria lo que tenían que investigar era cómo diablos hacían para llegar a fin de mes.”

La segunda, durante el eje sobre propuestas para el próximo gobierno (quinto eje).

> “Creemos q hay q aplicar de manera inmediata la duplicación de la inversión y el presupuesto en materia de vivienda porque, dentro de la inversión en infraestructura, es la inversión en vivienda la que más puestos de trabajo genera en relación a cada peso q se invierte”

Y la última, la dijo mientras le agradecía a Talvi el debate durante el mensaje final de los precandidatos.

> “Creo que es un mérito. Es algo que nos convocaban las juventudes de todos los partidos políticos cuando, en el aniversario del Río de Libertad, pedían por una campaña sin enchastre. Por una campaña sin descalificación. Por una campaña sin provocaciones y ojalá sostengamos hasta el último domingo de Octubre que el debate sea de esta manera: sea sobre la base de ideas y pudiendo darnos la mano al final del debate.”

Adicionalmente, observen que esta última frase, considerada como tercera en cuanto a núcleo de las intervenciones, fue además también marcada como una frase de emoción negativa. #DatosNoOpinión 🧐

#### Lo fundamental de Ernesto Talvi

![Foto: [www.teledoce.com](http://www.teledoce.com)](img/0__H2ALEcjPM5nSL0RB.jpg)
Foto: [www.teledoce.com](http://www.teledoce.com)

La primera frase, la fundamental, _la que resume al precandidato colorado,_ fue dicha en el primer eje que fue sobre el balance del gobierno del Frente Amplio.

> “Este es el país que el Frente Amplio va a dejar: primero, la producción nacional contra las cuerdas. Empresas que cierran, se achican. Problemas financieros que dejan trabajadores cesantes. 60.000 empleos se perdieron en los últimos cuatro años.”

La segunda, en el segundo eje relacionado a la inserción de Uruguay en el mundo y en particular, criticando la postura diplomática tomada por el Frente Amplio frente al conflicto sucedido en Venezuela.

> “Yo creo que este hecho nos ha colocado en una situación. que nos ha dado vergüenza a nivel internacional, haciéndonos cómplices de una dictadura militar que viola todos los derechos habidos y por haber; y alejándonos flagrantemente de lo que han sido las tradiciones uruguayas más queridas por la enorme mayoría de la población, que es el respeto por la democracia y por los derechos humanos.”

Y la tercera frase, en el contexto de las propuesta para un próximo gobierno colorado, durante el quinto eje.

> “(…) el foco que vamos a poner en la primera infancia: en los primeros tres años de vida de un chiquilín se juega buena parte de su destino. Esto no quiere decir como muchos erróneamente creen que no son recuperables en etapas más tardías. Simplemente cuesta muchísimo más recuperarlos. Vamos a darle una enorme importancia para fortalecer a los centros CAIF y, un programa que yo le reconozco al Frente Amplio como bueno que es, Uruguay Crece Contigo.”

### Gracias bot, qué haríamos sin vos 🤖

Hasta acá el análisis que nos proveyó el bot para este #UruguayDebate.

*   ¿Se podrían hacer más cosas? Seguramente sí. Por ejemplo realizar un análisis similar al de esta publicación pero por cada uno de los seis ejes. Hay algunas técnicas NLP que quedaron fuera de este análisis y que también podrían ser incluidas. El proyecto está ahí para que cualquiera que tenga ganas pueda hacerlo 😉
*   La idea original fue de [@GastoDuffour](http://twitter.com/GastoDuffour), quien estaba interesado en ver qué datos podía arrojar este tipo de análisis. Sabe que me cuelgo con estas cosas, y de hecho así sucedió.
*   La transcripción de los discursos la hice con [Sonix](https://sonix.ai) y los videos del debate los descargué de Youtube.
*   Más allá de todo ese trabajo que me ahorró la transcripción automatizada, hice una revisión general para pulir el texto -aunque no fui muy exigente, debo admitir- y separar los fragmentos de moderación, de cada precandidato, etc. Esto para poder procesarlos individualmente con los algoritmos.
*   El texto completo de la transcripción del #UruguayDebate está [disponible en este documento de Google](https://docs.google.com/document/d/1tYyYXfoejbwbRKXUsofSOd0uXfEBc2G7yiRol_sVDPc/edit?usp=sharing).
*   Los gráficos incluidos en esta publicación, [se pueden ver en este Google Sheet](https://docs.google.com/spreadsheets/u/1/d/1lWCehkTTS1Cm4WxiIB2AzhMrHrISYHTZRRoe3p2vIKw/edit?usp=sharing), donde también están las tablas de datos utilizadas que fueron generadas por los algoritmos del proyecto.

### Nada más por acá

Si llegaste hasta acá, sólo me queda decir gracias. Si te gustó, compartilo por ahí que quizás a alguien más le puede colgar.

Si te gusta lo que hago, podés:

*   [Seguir mi actividad en Twitter.](https://twitter.com/nahuelhds)
*   [Comprarme un café.](https://ko-fi.com/C0C5XC3Z)
*   [Contribuir conmigo en Patreon.](https://www.patreon.com/nahuelhds)
