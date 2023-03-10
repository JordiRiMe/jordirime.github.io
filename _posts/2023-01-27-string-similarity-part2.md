---
author: Jordi Ripoll Melis
date: 2023-01-25 21:45:00+00:00
draft: false
title: Similaridad de cadenas - Parte 2
layout: post

url: https://jordirime.github.io
categories:
- ciencia de datos
tags:
- ciencia de datos
- nlp
- similaridad
- distancias
---

En la anterior [publicación](https://jordirime.github.io/2023-01-25-string-similarity-part1/) hemos visto cómo podemos hacer uso de las medidas de similiaridad para ver la semejanza entre cadenas. Con esto, podemos tomar una decisión a la hora de considerar si dos cadenas son parecidas o no.  Por ejemplo, se puede construir un simple modelo logístico que determine la probabilidad de que dos cadenas sean parecidas en función de su distancia ($$d$$) y establecer un límite maximizando el área bajo la curva ROC o el indicador que mejor se ajuste al caso particular de cada uno:

$$logit(p) = \beta_0 + \beta_1d$$

Hasta aquí todo parece normal y es un punto en el que podrías dar por hecho que todo está bien sin analizar más a fondo el asunto. Es entonces cuando pones en producción el modelo y te encuentras con algunos casos particulares. Veamos funciona el coeficiente de Sorensen-Dice en un par:

1. Comparamos las direcciones:

* 123 main street unit 4 scranton a1b 2c3,
* 123 main street scranton a1b 2c3,

y tenemos un distancia de 0.1.

2. Ahora analizamos las direcciones:

* rutherford house nottingham science & technology park, university blvd 59 71 river road  ng7 2pz nottingam united kingdom,
* unit 6 airedale business park, royd ings avenue wheelforge way trafford park m17 1eh manchester,

y obtenemos una distancia de 0.66.

A primera vista no parece haber nada extraño. No obstante, cuando empiezas a utilizar estos indicadores e intentas entender su significado, te preguntas: ¿un 0.66 de semejanza entre dos direcciones que no se parecen en nada y un 0.1 entre dos direcciones prácticamente iguales?. 

Intentas entender mejor cómo funcionan estos coeficientes y empiezas a probar con diferentes casos. Es entonces cuando decides realizar algunas simulaciones con cadenas aleatorias de diferente longitud y observas el siguiente comportamiento:

![Coeficiente de Sorensen-Dice en función de la longitud de las palabras](/assets/img/sorensen_dice_estimator.png){:style="display:block; margin-left:auto; margin-right:auto"}

Es decir, cuanto mayor sea la longitud de las cadenas que se comparen, siendo ambas aleatorias (diferentes), la distancia según este coeficiente decrece de manera significativa. Este efecto ocurre en este tipo de indicadores en general.

Esto es un problema si queremos establecer un límite a partir del cual determinar si dos secuencias de palabras son diferentes. Hay que ajustarlo para poder hacer esto de manera consistente.

Como nota adicional, si se estandariza el coeficiente mediante una estimación basada en simulaciones, no hay que tener en cuenta solo el idioma (relevante en la distribución de los bigramas que nos encontremos), ¡sino que también habrá que considerar el contexto! ¿Qué quieres comparar? ¿Direcciones? ¿Conversaciones? ¡La distribución de los bigramas será diferente también!
