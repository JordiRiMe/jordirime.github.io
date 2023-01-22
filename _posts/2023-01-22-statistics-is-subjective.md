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

Así, a bote pronto, podemos razonar: dado que el alfabeto español tiene 27 letras, la probabilidad de encontrarnos con un vehículo así sería de 1 entre $27^3$. Y el razonamiento podría darse por válido.

No obstante, al poco rato de pasear y leer algunas matrículas, observamos que la primera letra suele estar entre la A y la M. En ese mismo instante recuerdas que las matrículas se registran siguiendo el orden del alfabeto, variando las letras de derecha a izquierda. Es entonces cuando cambia tu perspectiva y actualizas tu creencia sobre el evento. En este caso, la probabilidad de encontrarte con esa matrícula sería de 1 entre $13\cdot27^2$ posibilidades.

A pesar de la cantidad de humo y el mal olor que hace, sigues con tu paseo, que al menos está siendo entretenido. Sigues leyendo matrículas y te das cuenta de que la gran mayoría de ellas se distribuyen entre las letras F y L. Es entonces cuando piensas que quizás hayan menos coches antiguos y nuevos en circulación. Y navegando por la red encuentras datos (ficticios) que muestran que la proporción de vehículos en circulación varía en función de la primera letra de la matrícula:

![Distribución de coches en circulación según la primera letra de la matrícula](/assets/img/distribucion_coches.jpg){:style="display:block; margin-left:auto; margin-right:auto"}

Entonces, tu creencia sobre la probabilidad de encontrarte con esa matrícula se vuelve a alterar, en particular, un $\displaystyle\frac{p_E}{\sum_{x\in \{A,\ldots,M\}} p_x}\cdot\frac{1}{27^2}$% de los automóviles (donde $p_x$ es la proporción de coches en circulación que tienen $x$ como la primera letra de la matrícula).

En fin, la idea está clara. Podríamos seguir con más razonamientos que puedan parecer lógicos, como por ejemplo considerar la proporción de matrículas con $x$ letra en la segunda posición sabiendo cuál es la primera, o que te tomes el problema como algo personal y encuentres la información de todas las matrículas de España, la geolocalización de las viviendas donde residen los conductores y estimes la probabilidad de que el vehículo con esa matrícula acabe circulando por tu lado en función de la distancia de donde resida el dueño. Sin embargo, los paseos no suelen dar para tanto.

Otras veces, cuando tienes que solucionar un problema serio, lo primero que se debería hacer es informarse sobre él. Y en este caso podemos encontrar que 
> El sistema actual de numeración de las matrículas utiliza el formato NNNN LLL, donde LLL son tres letras secuenciales desde BBB hasta ZZZ que se incrementan cuando el número llega a 9999. Las letras utilizadas son las consonantes.

Entonces no hay subjetividad ni nada que discutir, simplemente la matrícula DSE no existe.
