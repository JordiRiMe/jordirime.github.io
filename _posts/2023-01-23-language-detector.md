---
author: Jordi Ripoll Melis
date: 2023-01-22 08:13:31+00:00
draft: false
title: Cómo detectar el idioma de un texto
layout: post

url: https://jordirime.github.io
categories:
- estadística
tags:
- ciencia de datos
- nlp
- probabilidad
---

Necesito urgentemente poder detectar el idioma de muuuchos documentos de texto diferentes, con el menor coste posible y mediante un algoritmo lo más rápido y efiiente que se pueda, sin necesidad de depender de APIs ni nada. Puedo construir algo que sea capaz de esto?

A raíz de un post en el que vi cómo desencriptar mensajes con letras permutadas, me vino la inspiración.

La idea consiste en trabajar con los bigramas de las palabras de los textos, es decir, cada par de letras. Por ejemplo, la palabra 'patata' tendría los bigramas $$\{' p', 'pa', 'at', 'ta', 'at', 'ta', 'a '\}$$. Un detalle importante a considerar, que se me pasó al principio, es considerar el primer y último bigrama, ya que indican el inicio y el final de una palabra.

Esta información se puede explotar para construir una matriz de probabilidades de encontrar cierto bigrama, la cual, por ejemplo, puede representar en las filas la primera letra del bigrama y en las columnas la segunda letra. Para construir esa matriz, tendría que tener en cuenta todas las letras de los idiomas que quiero considerar, más el espacio ' '. En mi caso particular, necesito detectar si un texto está escrito en catalán, castellano, inglés, francés o alemán. Por lo tanto, tendre que considerar todas las letras del alfabeto español, la 'ç' y la 'ß'. Podría considerar tildes, diéresis, pero para evitar errores ortográficos y otras cosas salvajes que puedan surgir en los textos, me limitaré a texto sin carácteres especiales de ese estilo.

Una vez que tengo en cuenta esto, leo un texto (cuanto más largo mejor) de cada idioma y calculo la probabilidad $$p_{xy}$$ de encontrar un bigrama $$xy$$ en el documento (esto sería calcular $$n_{xy}/N$$ donde N es el número de bigramas totales del texto y $$n_{xy}$$ el número de bigramas $$xy$$ que encuentre). Para ser más precisos, realmente estimo $$\hat{p_{xy}}$$ como $$\displaystyle\frac{n_{xy}+1}{N + n_L}$$ por un pequeño detalle que veremos más adelante, donde $$n_L$$ es el número de letras diferentes que estoy considerando más 1 (por el espacio).

Ahora bien, dado un texto, cómo detecto con esto qué idioma es más verosímil que represente el texto? 

Con esta matriz (o vector de probabilidades) hemos construido una distribución de probabilidades para cada idioma, es decir $$p(xy\|Idioma)$$. El sistema es muy sencillo, considera que los bigramas son independientes entre sí (cosa que no es verdad), pero no funciona nada mal. Es más, funciona mejor cuanto más largo sea un texto.

Al tener un texto, obtenemos todos los bigramas de este $$\{x_1y_1,\ldots,x_ny_n\}$$ y calculamos la verosimilitud de los bigramas en cada idioma para luego simplemente ver cuál es mayor,

$$p(x1y1,\ldots,x_ny_n|Idioma) = p(x1y1|Idioma)\cdots p(x_ny_n|Idioma).$$

Por este motivo, antes hemos sumado 1 en la estimación de las probabilidades, porque, por ejemplo, en la lengua española puede que no observemos el bigrama 'th'. Pero podríamos pillar un texto español con este error ortográfico y entonces el algorítmo detectaría que el idioma del texto es el inglés, ya que el producto anterior se volvería 0.
