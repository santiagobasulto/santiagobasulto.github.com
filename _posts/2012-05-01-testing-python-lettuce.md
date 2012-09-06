---
layout: post
title: "Testing en Python con Lettuce"
category: python
tags: python testing tdd bdd programacion lettuce
---

En el último tiempo he estado realizando mucho testing para athlete.com. La cantidad de características y funcionalidades crecen todos los días, así que es necesario tener un buen *test coverage* para que al agregar nuevas cosas no se rompan otras.

Una vez que usamos concientemente TDD vemos como la vida se nos simplifica, y a la vez nos damos cuenta de que pueden existir cosas mejores. Al estar tan metido en Scala en el último año me di cuenta de que existe algo mejor que el simple TDD (Test Driven Development): el BDD (Behavior Driven Development).

### BDD (Behavior Driven Development)

El BDD (más o menos: Desarrollo basado en el comportamiento del software) es similar al TDD. La mayor diferencia es que en vez de escribir funciones aisladas que prueban pequeñas funcionalidades del código, lo que se hace es pensar más en el comportamiento en general de la aplicación. Una gran ventaja del BDD es que debe realizarse mediante *Lenguaje Natural*. O sea, en TDD tendríamos esto:

{% highlight python %}

    def test_factorial_de_uno_devuelve_uno(self):
        self.assertEquals(factorial(1), 1)

{% endhighlight %}

El problema del código anterior es que no es muy descriptivo. Primero para personas que no están involucradas con la programación (pensá cómo le explicarías a un programador de front-end o a un diseñador el código anterior). Segundo, para nosotros mismos. Cuando tenés mucho código, creeme que los tests se pueden empezar a complejizar.

En cambio, con BDD deberíamos tener algo así:

* Paso 1: Primero agarro el número 1 para probar
* Paso 2: LLamo a la función factorial con 1 como parámetro
* Paso 3: Compruebo que el resultado sea 1

Aunque no lo creas eso es hacer BDD. Esto sí se lee más fácil. Tanto para programadores como para personas no técnicas. Aparte genera una buena documentación, lo cual en proyectos grandes puede ser un gran beneficio.

El BDD se hace de forma más simple en lenguajes que tengan un buen soporte para DSL (Domain Specific Languages). Este no es el caso de Python, por lo que existen algunas librerías útiles para BDD con Python. Una de ellas es [Lettuce](http://packages.python.org/lettuce/index.html).

### Lettuce

Lettuce, simple y claramente, es una librería que nos ayuda a realizar BDD en python. O sea, describir el comportamiento de nuestro programa/aplicación primero y después escribir código que ayude a resolver esa problemática. No quiero seguir explayándome teóricamente, así que veamos un ejemplo.

#### Primera aplicación con Lettuce

Lo que vamos a tratar de hacer ahora es escribir una simple función que calcule el [Factorial](http://es.wikipedia.org/wiki/Factorial) de un número utilizando BDD. Como agregado extra, no vamos a tratar de escribir la típica función factorial, porque ya la conocemos todos, sino que la vamos a escribir utilizando [notación lambda](http://docs.python.org.ar/tutorial/controlflow.html#formas-con-lambda), concepto relacionado a la programación funcional. Si no sabés lo que son las *lambdas* te va a servir para aprender un poco, o al menos despertar tu curiosidad.

Primero vamos a instalar lettuce. Para ello hacemos:

{% highlight bash %}

    $ pip install lettuce

{% endhighlight %}

_Nota:_ Como siempre, es recomendable instalarlo en un virtualenv ( y mejor aún utilizando virtualenvwrapper). Si no utilizas un virtualenv tal vez tengas que usar `sudo pip install lettuce`.

Después vamos a crear el directorio donde vamos a armar la aplicación de prueba, y vamos a tener que crear algunas carpetas y archivos para hacer andar correctamente lettuce. El resultado final debe ser este (reemplazá el directorio inicial):

{% highlight bash %}

/home/santiago/projects/lettuce_test
     | tests
           | features
                - zero.feature
                - steps.py

{% endhighlight %}

Yo hice lo siguiente:

{% highlight bash %}

    $ mkdir lettuce_test
    $ cd lettuce_test
    $ mkdir -p tests/features
    $ touch tests/features/zero.feature && touch tests/features/steps.py

{% endhighlight %}

#### Describiendo comportamiento

Ahora empieza la parte donde realmente estamos utilizando lettuce para describir comportamiento. Lo primero que vamos a hacer es escribir el comportamiento que debería tener nuestra función `factorial`. Abrimos el archivo `features/zero.feature` y ponemos lo siguiente:

{% highlight python %}
# -*- coding: utf-8 -*-
# language: es

Funcionalidad: Computar el factorial de un número
  Estamos probando lettuce, así que
  Como principiantes
  Queremos implementar la función factorial
  Utilizando notación lambda

  Escenario: El factorial de 0
    Dado el número 0
    Cuando computamos el factorial
    Debo ver el número 1

{% endhighlight %}

Eso no parece código python. Sin embargo tiene unos comentarios raros al principio, lo que indica que no es un archivo común y corriente. Ese archivo es utilizado por Lettuce para entender el comportamiento de nuestra aplicación. Es por ahí donde debemos arrancar, primero escribiendo el comportamiento.

### Usando Lettuce

Al fin llegamos! Vamos a usar Lettuce después de tantas vueltas. Simplemente (parado en el directorio del proyecto), ejecutá la siguiente sentencia:

{% highlight bash %}

    $ lettuce test/

{% endhighlight %}

Eso es todo! Lettuce debería estar andando. Si algo falló, te recomiendo que vuelvas a reveer tus pasos de instalación. Ahora bien; ¿qué fue lo que hicimos? y ¿qué fue lo que pasó?

Lo que hicimos fue pedirle a lettuce que pruebe nuestro comportaminto y trate de ejecutar el código relacionado. Ya que el código para probar el comportamiento debe estar en steps.py, y steps.py (por ahora) está vacío, resulta evidente que el test falló. Seguramente viste una salida similar a esta:

![Salida de Lettuce](/img/posts/2012-05-01-testing-python-lettuce/lettuce-out-1.png)

Como ves, aparecen algunos test como "undefined" y te da un ejemplo de cómo podrías implementarlo. Vamos a seguir con esto.

### Escribiendo los tests

Ya utilizamos el archivo `.feature` para describir el comportamiento. Ahora debemos escribir los test (sí, los tests primero) y la función `factorial` que realizará la tarea deseada. Como esto es BDD comenzamos escribiendo los tests y la función vamos a hacer que retorne -1 (podríamos haberla dejado sin implementar). En el archivo `steps.py` escribimos lo siguiente:

{% highlight python %}

# -*- coding: utf-8 -*-

from lettuce import *

@step(u'Dado el número (\d+)')
def dado_el_numero(step, numero):
    world.numero = int(numero)

@step(u'Cuando computamos el factorial')
def computamos_el_factorial(step):
    world.numero = fact(world.numero)

@step(u'Debo ver el número (\d+)')
def debo_ver_numero(step, esperado):
    esperado = int(esperado)
    assert world.numero == esperado, \
        "Obtuve %d" % world.numero

fact = lambda n : -1 # No implementamos nada aún!!

{% endhighlight %}

Si ejecutamos lettuce (`$ lettuce tests/`) la salida resultante será algo similar a esta:

![Salida de Lettuce](/img/posts/2012-05-01-testing-python-lettuce/lettuce-out-2.png)

Como podés ver, el problema fue el tercer Test ("Debo ver el número 1"). Como todavía no tratamos de escribir nuestra función. La salida parece bastante clara, muchos rojos y verdes por todos lados. Es obvio que esto iba a fallar porque no implementamos la función (en realidad solo nos dispusimos a devolver "-1").

Ahora vamos a tratar de programar usando BDD. La idea es (al igual que con TDD) ir ejecutando pequeños pasos que resuelvan la funcionalidad necesaria. Para hacerlo pensamos en el primer escenario de nuestro problema:

> ¿Cuál es el factorial de 0?

El factorial de 0 es 1, así que podemos directamente cambiar nuestra función factorial por esto:

{% highlight python %}

	def factorial(n):
		return -1

{% endhighlight %}

Volvé a correr tus tests y vas a ver cómo pasan tranquilamente:

![Salida de Lettuce](/img/posts/2012-05-01-testing-python-lettuce/lettuce-out-3.png)

Ahora bien, ¿cuál es el problema acá? Obviamente el escenario que planteamos no es el único con el que podemos econtrarnos.
