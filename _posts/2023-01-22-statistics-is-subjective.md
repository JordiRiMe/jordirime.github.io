---
author: Jordi Ripoll Melis
date: 2023-01-22 08:13:31+00:00
draft: false
title: La subjetividad de la estadística
layout: post

url: https://jordirime.github.io
categories:
- estadística
tags:
- estadística
- subjetividad
- probabilidad
---
Muchas son las noticias que sueltan resultados probabilísticos sobre ciertos eventos y nos limitamos a tomar esos resultados como verdades universales. No obstante, es importante tener presente que detrás de un resultados basado en probabilidades, hay un modelo estadístico, y este se construye a partir de nuestras experiencias, observaciones y creencias.

Por poner un ejemplo, imaginemos que estamos dando un paseo por una ciudad (necesito un escenario con coches, con mucho humo, por ejemplo, Madrid) y nos cuestionamos, ¿cuál es la probabilidad de que el siguiente vehículo que pase por esta carretera de 8 carriles tenga las letras DSE?

Así, a bote pronto, podemos razonar: dado que el alfabeto español tiene 27 letras, la probabilidad de encontrarnos con un vehículo así sería de 1 entre $$27^3$$. Y el razonamiento podría darse por válido.

No obstante, al poco rato de pasear y leer algunas matrículas, observamos que la primera letra suele estar entre la A y la M. En ese mismo instante recuerdas que las matrículas se registran siguiendo el orden del alfabeto, variando las letras de derecha a izquierda. Es entonces cuando cambia tu perspectiva y actualizas tu creencia sobre el evento. En este caso, la probabilidad de encontrarte con esa matrícula sería de 1 entre \(13\cdot24^2\) posibilidades.

A pesar de la cantidad de humo y el mal olor que hace, sigues con tu paseo, que al menos está siendo entretenido. Sigues leyendo matrículas y te das cuenta de que la gran mayoría de ellas se distribuyen entre las letras D y H. Es entonces cuando piensas, quizás la hayan menos coches antiguos y nuevos en circulación. Y buscando entre fuentes encuentras la siguiente información (ficticia):

![Distribución de coches en circulación según la primera letra de la matrícula](/assets/img/distribucion_coches.jpg){:style="display:block; margin-left:auto; margin-right:auto"}

<!-- Cuando me enfrento a un nuevo problema, me gusta recordar las palabras de George Box, quien citó que "todos los modelos son erróneos, pero algunos son útiles".  -->
