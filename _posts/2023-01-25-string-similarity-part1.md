---
author: Jordi Ripoll Melis
date: 2023-01-25 21:45:00+00:00
draft: false
title: Similaridad de cadenas - Parte 1
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

En los siguientes dos posts, voy a escribir sobre medidas de similaridad entre cadenas de caracteres y algunos de los problemas con los que me he tenido que aventurar.

Supongamos que quiero extraer información de una empresa llamada 'Servicios Manolo S.L.'. Busco algo de información por la red y veo que he pescado datos (de manera automatizada) de una empresa llamada 'servicios de manoli S.L.' y de otra con el nombre 'SERVICIOS MANOLO'. ¿Con qué información me quedo y cuál descarto? La respuesta parece obvia, pero hay que trabajar un poco esta información para poder automatizar la tarea.

En primer lugar, para poder comparar dos cadenas de caracteres, tengo que definir una medida de similaridad, algo que me pueda indicar cuanto se parecen las palabras, cuantificar de alguna manera su semejanza. Generalmente, una distancia entre palabras es una función que devuelve un valor entre 0 y 1, reflejando semejanza con valores cercanos a 0 y diferencia con valores cercanos a 1. En mi caso particular, usualmente suelo utilizar la distancia de Leveshtein y el coeficiente de Sorensen-Dice.

La distancia de Levenshtein mide el número de modificaciones que hay que hacer para convertir una cadena en la otra. Usualmente, se estandariza por el número de letras de la cadena más larga para obtener un valor entre 0 y 1, y hacer que sea comparable entre otras comparaciones de cadenas de diferente longitud (aunque ahondaremos en este asunto en la segunda parte). Por ejemplo, entre las palabras 'casa' y 'cosa', la distancia de Levenshtein sería de un 0.25, ya que hay que modificar 1 de 4 letras para hacer que sean iguales.

En cuanto al coeficiente de Sorensen-Dice, mide la proporción de bigramas coincidentes entre ambas palabras (ya hablé un poco de los bigramas en [este](https://jordirime.github.io/2023-01-23-language-detector/) post). Aprovechando el caso anterior, tenemos los bigramas {'ca', 'as', 'sa'} y {'co', 'os', 'sa'} con lo que la distancia (con este coeficiente) entre estas es de 0.66 (no coinciden 2 de 3 bigramas).

Cada una de estas distancias tiene sus ventajas y sus inconvenientes. La distancia de Levenshtein es mejor midiendo la similaridad exacta, penalizando menos aquellas palabras con letras mal introducidas, mientras que el coeficiente de Sorensen-Dice penaliza menos las cadenas que contienen palabras permutadas y es mucho más eficiente computacionalmente. Por poner un par de ejemplos para entender estos puntos, las palabras 'servicios' y 'services' tienen distancias '0.22' y '0.33' respectivamente (una letra penaliza mucho el coeficiente de Sorensen-Dice), mientras que las palabras 'trabajos verticales' y 'verticales trabajos' tienen distancias '0.74', '0.05' respectivamente (la permutación de palabras repercute en la distancia de Levenshtein).

Bien, ya tenemos medidas de similaridad para diferentes situaciones. En el caso de la comparación de nombres de empresa, sería más adecuado utilizar la medida de similaridad de Levenshtein, ya que el orden de las palabras en un nombre es relevante. En cambio, si por ejemplo se desea comparar direcciones postales, el coeficiente de Sorensen-Dice puede ayudarnos a medir mejor situaciones como 'Polígono Industrial de Son Castelló' y 'Son Castelló (Polígono Industrial)'.

Y realmente esto solo acaba de empezar, pero el tema de estandarización es un tema más particular y aburrido.
