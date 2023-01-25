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

Supongamos que quiero extraer información de una empresa llamada 'Servicios Manolo S.L.'. Busco algo de información por la red y veo que he pescado datos (de manera automatizada) de la empresa 'servicios de manoli S.L.' y de otra que se llama 'SERVICIOS MANOLO'. ¿Con qué información me quedo y cuál descarto?

La respuesta parece obvia, pero hay que trabajar un poco esta información para poder automatizar la tarea.

En primer lugar, para poder comparar dos cadenas de caracteres, tengo que definir una medida de similaridad, algo que me pueda medir la "distancia" entre estas. En general, se pueden definir diferentes medidas de similaridad que toman un valor entre 0 y 1, reflejando semejanza con valores cercanos a 0 y diferencia con valores cercanos a 1. En particular, suelo utilizar las medidas de distancia de Leveshtein y el coeficiente de Sorensen-Dice.

La distancia de Levenshtein mide el número de modificaciones que hay que hacer para convertir una cadena en la otra. Usualmente, se estandariza por el número de letras de la cadena más larga para estandarizarlo y hacer que sea comparable entre comparaciones de cadenas de diferente longitud (aunque ahondaremos en este punto más adelante). Por ejemplo, entre las palabras 'casa' y 'cosa', la distancia de Levenshtein sería de un 0.25, ya que hay que modificar 1 de 4 letras para hacer que sean iguales.

En cuanto al coeficiente de Sorensen-Dice, mide la proporción de bigramas coincidentes entre ambas palabras. Aprovechando el caso anterior, tendríamos los bigramas {'ca', 'as', 'sa'} y {'co', 'os', 'sa'} con lo que la distancia entre ellas es de 0.66 (no coinciden 2 de 3 bigramas).

Cada una de estas distancias tiene sus ventajas y sus inconvenientes. La distancia de Levenshtein es mejor midiendo la similaridad exacta, penalizando menos algunas palabras con letras mal escritas (bueno para controlar errores de entrada de datos), mientras que el coeficiente de Sorensen-Dice penaliza menos las cadenas que contienen palabras permutadas y es mucho más eficiente computacionalmente. Por poner un par de ejemplos para entender estos puntos, las palabras 'servicios' y 'services' tienen distancias '0.22' y '0.33' respectivamente (una letra penaliza mucho el coeficiente de Sorensen-Dice), mientras que las palabras 'trabajos verticales' y 'verticales trabajos' tienen distancias '0.74', '0.05' respectivamente (la permutación de palabras perjudica la distancia de Levenshtein).

Bien, ya tenemos medidas de similaridad para diferentes situaciones. Por ejemplo, para comparar nombres de empresa, sería más adecuado utilizar la medida de similaridad de Levenshtein, ya que el orden de las palabras en un nombre es relevante. Por otro lado, si por ejemplo se desea comparar direcciones postales, el coeficiente de Sorensen-Dice puede ayudarnos a medir mejor situaciones como 'Polígono Industrial de Son Castelló' y 'Son Castelló (Polígono Industrial).

Y realmente esto solo acaba de empezar, pero el tema de estandarización, que es lo que seguiría, es demasiado aburrido para leer.
