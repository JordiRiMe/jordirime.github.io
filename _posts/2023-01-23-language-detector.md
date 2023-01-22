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

Necesito urgentemente ser capaz de detectar el idioma de muuuchos documentos de texto diferentes, al menor coste y mediante un algoritmo lo más rápido y eficiente posible, sin necesidad de depender de ninguna API. ¿Es posible construir algo semejante?

A raíz de un post que me mostró cómo desencriptar mensajes con letras permutadas, me vino la inspiración.

La idea consiste en trabajar con los bigramas, que no son más que los pares de letras de las palabras que componen un texto. Por ejemplo, la palabra 'patata' tendría los bigramas $$\{' p', 'pa', 'at', 'ta', 'at', 'ta', 'a '\}$$. Un detalle importante a considerar, y que se me pasó en un primer momento, es considerar el primer y último bigrama (en este caso ' p' y 'a '), ya que indican el inicio y el final de una palabra.

Es posible explotar esta información construyendo una distribución que indique la probabilidad de encontrar cierto bigrama dado un idioma. Para construir dicha distribución de probabilidad, habría que tener en cuenta todas las letras de aquellos idiomas que se consideren, más el espacio ' '. En mi caso particular, necesito detectar si un texto está escrito en catalán, castellano, inglés, francés o alemán. Por lo tanto, tendré que considerar todas las letras del alfabeto español, incluyendo además la 'ç' (que aparece en el catalán y francés) y la 'ß' (en textos alemanes). Podría considerar tildes, diéresis, etc., pero para evitar posibles errores ortográficos en el texto y otras cosas imprevisibles que puedan surgir en los textos, me limitaré a texto sin caracteres especiales de ese estilo.

Una vez que tengo en cuenta esto, leo un texto (cuanto más largo mejor) de cada idioma y calculo la probabilidad $$p_{xy}$$ de encontrar un bigrama $$xy$$ en el documento (esto sería calcular $$n_{xy}/N$$ donde N es el número de bigramas totales del texto y $$n_{xy}$$ el número de bigramas $$xy$$ que encuentre). Para ser más precisos, realmente estimo $$\hat{p_{xy}}$$ como $$\displaystyle\frac{n_{xy}+1}{N + n_L^2}$$ por un pequeño detalle que veremos más adelante, donde $$n_L$$ es el número de letras diferentes que estoy considerando más 1 (por el espacio).

Ahora bien, dado un texto, y teniendo en cuenta todo lo anterior, ¿cómo detecto con esto qué idioma es más verosímil que represente dicho texto? 

Hemos creado una distribución de probabilidad estimada para cada idioma, es decir $$p(xy\vert Idioma)$$. A partir de esto, podemos asumir que los bigramas son independientes entre sí, cosa que sabemos que no es cierta, pero simplifica mucho el problema y no funciona nada mal. Es más, funciona mejor cuanto más largo sea un texto.

Dado un texto, obtenemos todos los bigramas de este $$\{x_1y_1,\ldots,x_ny_n\}$$ y calculamos la verosimilitud de los bigramas en cada idioma para luego simplemente ver cuál es mayor, es decir:

$$p(x_1y_1,\ldots,x_ny_n|Idioma) = p(x_1y_1|Idioma)\cdots p(x_ny_n|Idioma).$$

He aquí el motivo por el que antes hemos sumado 1 y ajustado el divisor en la estimación de las probabilidades. Tomando como ejemplo la lengua española, puede que no observemos el bigrama 'th', pero podríamos dar con un texto en castellano con este error ortográfico; en ese caso, la estimación indicaría que es más verosímil que el texto esté escrito en inglés, ya que el producto anterior se volvería 0.

Es en este punto cuando intentas buscar cosas que se te puedan escapar, le das un par de vueltas y piensas, ¿qué pasaría si mi texto es una URL o un conjunto de carácteres aleatorios?. La respuesta es sencilla, detectaremos un idioma de los que estamos intentando buscar. 

Enconces, ¿cómo detecto por ejemplo un texto random como puede ser la letra de una canción de Bad Bunny? Pues construyendo justamente eso, una distribución de probabilidad aleatoria $$p(xy\vert Random)=\displaystyle\frac{1}{n_L^2}$$.

Con esto, lo tendríamos todo listo. Solo faltaría aplicar la regla del gran Bayes para calcular la probabilidad de que el texto sea de cierto idioma:

$$p(Idioma_i|x_1y_1,\ldots,x_ny_n) = \displaystyle\frac{p(x_1y_1,\ldots,x_ny_n|Idioma_i)}{\sum_{i}p(x_1y_1,\ldots,x_ny_n|Idioma_i)}$$

Veamos algunos ejemplos:
