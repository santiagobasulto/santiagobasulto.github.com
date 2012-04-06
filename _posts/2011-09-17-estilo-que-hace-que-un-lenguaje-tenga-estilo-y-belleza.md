---
layout: post
title: Qué hace que un lenguaje tenga estilo y belleza
category: programacion
tags: lenguajes programacion estilo diseño
---

Hace un tiempo compré un excelente libro para aprender JavaScript a fondo. Todos los programadores web conocen y escriben a diario código javascript, pero muy pocos lo conocen y entienden a fondo. Yo era uno de esos. Me sorprendió de JavaScript que permite escribir código sin conocer el lenguaje, así que decidí investigar un poco más. Me encontré con una gran sorpresa. Es un gran lenguaje, con muchas características muy buenas. Ideas nuevas a las que no estaba acostumbrado y un acercamiento hacia el paradigma funcional que me sorprendió bastante. A continuación incluyo un fragmento [JavaScript: The Good Parts](http://www.amazon.com/JavaScript-Good-Parts-Douglas-Crockford/dp/0596517742/ref=sr_1_1?ie=UTF8&qid=1316235621&sr=8-1) de su autor, [Douglas Crockford](http://www.crockford.com/). Me parece importante compartir tan interesante punto de vista de la ciencia de la computación y programación. Espero lo disfruten:

Los programas de computadoras son las cosas más complejas que los humanos hacen. Los programas están hechos de una gran cantidad de partes, expresadas como funciones, sentencias, y expresiones que están dispuestas en secuencias que deben estar virtualmente libre de errores. El comportamiento en ejecución tiene poca similaridad con el programa que lo implementa. Generalmente se espera que el software sea modificado en el curso de su vida productiva. El proceso de convertir un programa correcto en otro programa correcto es extremadamente desafiante.

Los buenos programas tienen una estructura que anticipa (aunque no demasiado) las posibles modificaciones que serán requeridas en el futuro. Los buenos programas también tienen una presentación clara. Si un programa está bien expresado, entonces tenemos las mejores chances de poder entenderlo para así poder modificarlo o repararlo exitosamente.

Estas inquietudes se aplican a todos los lenguajes de programación, y en especial a JavaScript. El tipado débil y la excesiva permisividad ante errores proveen poca seguridad en tiempo de compilación de la calidad de nuestros programas, por lo tanto, para compensar, debemos escribir nuestro código con estricta disciplina.

JavaScript contiene un gran conjunto de características débiles o problemáticas que pueden socavar nuestros intentos de escribir buenos programas. Obviamente deberíamos evitar las peores características de JavaScript. Sorpresivamente tal vez, deberíamos también evitar las características que generalmente son útiles, pero ocasionalmente peligrosas. Tales características son atractivas molestias, y al evitarlas, una gran cantidad de errores son evitados.

El valor del software a largo plazo para una organización está en directa proporción a la calidad del código. A lo largo de su vida, un programa será manejado por múltiples pares de manos y ojos. Si un programa es capaz de comunicar claramente su estructura y características, es menos probable que se rompa cuando sea modificado en un futuro cercano.

El código JavaScript es generalmente mandado directamente al público. Debería ser siempre de calidad de publicación. La prolijidad cuenta. Al escribir en un estilo claro y consistente, tus progrmaas se vuelven más fáciles de leer.

Los programadores pueden debatir indefinidamente sobre qué constituye un “buen estilo”. La mayoría de los programadores están firmemente arraigados en a lo que están acostumbrados, tal como el dominante estilo  de su escuela, o su primer trabajo. Algunos tienen provechosas carreras con ningún sentido de estilo. ¿Es eso prueba de que el estilo no importa? Incluso si el estilo no importa, ¿no es un estilo tan bueno como otro?

Resulta que el estilo importa en la programación por la misma razón que importa en la escritura (N.T: referido a la literatura). Permite una mejor lectura.

Los programas algunas veces son pensados como un medio de “solo escritura”, por lo tanto importa poco como es escrito mientras funcione. Pero resulta que la provabilidad que un programa funcione mejora significativamente con nuestra habilidad de leerlo, lo que a su vez aumenta la probabilidad de que realmente funcione como se esperaba. Es la naturaleza del software ser extensivamente modificado a lo largo de su vida productiva. Si podemos leerlo y entenderlo, entonces podemos esperar modificarlo y mejorarlo.

Hasta ahí la cita a Crockford. Evidentemente algunos lenguajes pueden tener más estilo que otros…

{% highlight scala %}
/** Print prime numbers less than 100, very inefficiently. But very beautiful */
object primes extends Application {
  def isPrime(n: Int) = (2 until n) forall (n % _ != 0)
  for (i <- 1 to 100 if isPrime(i)) println(i)
}
{% endhighlight %}


