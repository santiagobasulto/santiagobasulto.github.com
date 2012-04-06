---
layout: post
title: String, StringBuffer, StringBuilder… Conclusiones sobre la ciclotimia de Java
category: java
tags: java string stringbuffer stringbuilder architecture design
---

Hace unos días estuvimos en una charla sobre TDD y Pair Programming (algo que merecerá algún post en algún momento).
La consigna era resolver un problema dado mediante un gran grupo de 10 personas aplicando TDD, y metodologías ágiles, como PP.

En un momento, mientras discutíamos cierta funcionalidad, surgió una duda. Había que concatenar una cierta cantidad de Strings. Existen tres opciones: la primera, y más simple, es simplemente utilizar el operador de concatenación de Java, algo similar a esto:

{% highlight java%}
String result = "";
for(int i=0;i>10;i++){
    result += String.valueOf(i);
}
{% endhighlight %}

El problema de esto es que es ineficiente. La explicación es que los Strings en Java son objetos inmutables. ¿Qué quiere decir esto? Que cada vez que uno llama a un método de un objeto de la clase String, que generaría un cambio en el estado interno del objeto, lo que sucede en realidad es que no cambia el objeto original, sino que nos devuelve otra instancia.

Por ejemplo, el siguiente código ilustra el concepto:

{% highlight java%}
String cadena = "Hola Mundo";
cadena.toUpperCase();
System.out.println(cadena);
{% endhighlight %}

La impresión de ese código devuelve: “Hola Mundo”, aún cuando el sentido común hubiera indicado que devuelve “HOLA MUNDO”. El objeto “cadena” no va a cambiar a lo largo del ciclo de vida del programa. Nace y muere “Hola Mundo”.
La inmutabilidad es una propiedad muy deseable en los programas. Es algo que se da mucho en lenguajes que siguen el paradigma funcional, y hace que la programación concurrente sea más simple y menos tendiente a errores.
Volviendo a la concatenación. Cada vez que uno hace una concatenación con el operador “+”, se crea un nuevo objeto, algo que es costoso a nivel performance. Entonces, el código del principio del post generará 11 objetos (el “result” original y los otros 10 generados en el bucle).

Para eso nació la clase [StringBuffer](http://download.oracle.com/javase/1.5.0/docs/api/java/lang/StringBuffer.html). Introducida en la versión 1.0 del JDK, es (citando la documentación oficial).

> una secuencia mutable de caracteres segura en cuanto a concurrencia (thread-safe)

El objetivo es tener una clase que sea mutable, en la que se puedan concatenar cadenas sin sufrir en performance. El siguiente código lo ilustra.

{% highlight java%}
StringBuffer cadena = new StringBuffer("Hola");
cadena.append(" Mundo");
System.out.println(cadena);
{% endhighlight %}

Si prestaste atención a la documentación, dice que es una clase “thread-safe”, o sea, que puede ser usada en programas concurrentes sin que ocurran [condiciones de carrera](http://es.wikipedia.org/wiki/Condici%C3%B3n_de_carrera). Por si no lo sabes, para generar esa “seguridad” en programas concurrentes es necesario utilizar mecanismos de sincronización como Locks, Mutex, Semáforos, etc. Algo que va a ser degradante en performance. Por lo tanto, para los programas que no utilizan múltiples hilos de ejecución se creó otra clase, a saber, StringBuilder. En este caso, la documentación dice que es:

> una secuencia mutable de caracteres

Provee la misma interfaz que StringBuffer, y funciona de forma muy similar.

###Resumen

La clase StringBuilder es un poco más eficiente a la hora de la “mutación” de Strings, que la clase StringBuffer, pero no es “thread-safe”, o sea que puede derivar en comportamientos indeseados en programas concurrentes. La clase StringBuffer es “thread-safe” y es más eficiente que la “cruda” concatenación de Strings que vimos al principio del post.

###Recomendaciones

Si bien a después de esta sección voy a exponer una conclusión más personal, más alejada de cuestiones técnicas, debo transmitir las intenciones de la comunidad Java. Leyendo la documentación se puede llegar a las siguientes “reglas útiles”:

1. Si vas a utilizar Strings sin que cambien a lo largo del programa, utilizá simplemente la clase String.
2. Si tus Strings van a cambiar (se van a agregar o cambiar caracteres) tenés dos opciones:

    i. Si utilizas varios hilos en tu programa, los cuales pueden acceder a esos Strings, utilizá la clase StringBuffer.
    
    ii. Si tu programa no utiliza hilos, utilizá la clase StringBuilder.
    
###Conclusiones

Más allá de las cuestiones técnicas expuestas hasta ahora, me gustaría remarcar la rareza de estos cambios en Java.

Evidentemente, la inmutabilidad de la clase String original no fue un accidente. Hacer que nuestras clases sean inmutables es una propiedad excelente, con innumerables ventajas, y que se ha estudiado con mucho detenimiento en las ciencias de la computación. En resumen, es algo MUY bueno que tiene la clase String. Pero “el pueblo” aparentemente no estaba conforme, por lo que se creó la clase StringBuffer, que provee seguridad en programas concurrentes, pero con medios menos “naturales” (locks, a través de la palabra reservada synchronized). En definitiva crearon una clase más compleja, para realizar las mismas operaciones un poco más eficientes. Como todo eso no fue suficiente crearon la clase StringBuilder, ya que algunos programadores no querían pagar el precio de la creación de objetos ni de la sincronización cuando sus programas no utilizaban hilos. Seguramente esos programadores van a tener un gran dolor de cabeza si algún día quieren que su programa sea concurrente, cambiando todas las apariciones de StringBuilder por StringBuffer (o debuggeando horas y atendiendo a sus clientes muy enojados porque el programa “últimamente no está andando bien como debería”).

Existe, realmente una gran diferencia de performance entre la concatenación de Strings y la utilización de StringBuffer. En promedio (un script simple corrido unas 100 veces) concatenar 10000 Strings toma cerca de 300 milisegundos, mientras que haciendo “append” con un objeto StringBuffer toma 30 milisegundos. Encima la performance se degrada exponencialmente, los resultados de la concatenación de 100.000 Strings dan cerca de 40 segundos (40.000 milis!), mientras que StringBuffer se mantiene por debajo de los 100 milisegundos. La diferencia entre StringBuffer y StringBuilder no llega a ser nunca mayor a 10% del tiempo de ejecución, algo que personalmente no considero relevante. Les dejo a ustedes que saquen sus propias conclusiones, lo único que quiero dejar en claro es que tengan cuidado a la hora de decidir qué método utilizarán para utilizar sus Strings.
