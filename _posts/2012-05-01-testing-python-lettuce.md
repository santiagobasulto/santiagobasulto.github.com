---
layout: post
title: Testing en Python con Lettuce
category: python
---

En el último tiempo he estado realizando mucho testing para athlete.com. La cantidad de características y funcionalidades crecen todos los días, así que es necesario tener un buen *test coverage* para que al agregar nuevas cosas no se rompan otras.

Una vez que usamos concientemente TDD vemos como la vida se nos simplifica, y a la vez nos damos cuenta de que pueden existir cosas mejores. Al estar tan metido en Scala en el último año me di cuenta de que existe algo mejor que el simple TDD (Test Driven Development) y es el BDD (Behavior Driven Development).

El BDD es similar al TDD. La mayor diferencia es que en vez de escribir funciones aisladas que prueban pequeñas funcionalidades del código, lo que se hace es pensar más en el comportamiento en general de la aplicación. Una gran ventaja del BDD es que debe realizarse mediante *Lenguaje Natural*. O sea, en TDD tendríamos esto:

{% highlight python %}

    def test_factorial_de_uno_devuelve_uno(self):
        self.assertEquals(factorial(1),1)

{% endhighlight %}

El problema del código anterior es que no es muy descriptivo. Primero para personas que no están involucradas con la programación (pensá cómo le explicarías a un programador de front-end o a un diseñador el código anterior). Segundo, para nosotros mismos. Cuando tenés mucho código, creeme que los test se pueden empezar a complejizar.

En cambio, con BDD deberíamos tener algo así:

* Paso 1: Primero agarro el número 1 para probar
* Paso 2: LLamo a la función factorial con 1 como parámetro
* Paso 3: Compruebo que el resultado sea 1

Aunque no lo creas eso es hacer BDD. Esto sí se lee más fácil. Tanto para programadores como para personas no técnicas.

El BDD se hace de forma más simple en lenguajes que tengan un buen soporte para DSL (Domain Specific Languages). Este no es el caso de Python, por lo que existen algunas librerías útiles para BDD con Python. Una de ellas es [Lettuce](http://packages.python.org/lettuce/index.html).


