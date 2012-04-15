---
layout: post
title: "Scala: Orientación a expresiones y pattern matching"
category: scala
tags: scala programming pattern matching expresiones
---

Este es un post bastante colgado, ya que no he escrito mucho sobre Scala más allá del [Tutorial de Scala para programadores Java](/2011-11-20-scala-para-refugiados-de-java-resumen.html). Lo que quiero comentar aquí son dos características muy útiles que resultan sorprendentes y que hacen a Scala uno de los lenguajes más *concisos* que conozco. Un comentario aparte de esto es que, en mi opinión, Scala rompe con el paradigma de que los lenguajes de tipado estático son poco concisos y que requieren mucho código redundante. Veamos por qué.

Supongamos que estamos utilizando Scala para construir una Calculadora básica (saco el ejemplo de la [Scala School de Twitter](http://twitter.github.com/scala_school/). Para escribir nuestra calculadora vamos a pedir que en el constructor se especifique la marca. A su vez, de acuerdo a la marca vamos a asignar un color específico (muy subjetivo). Este ejemplo no tiene mucha utilidad, pero seguramente te has topado con algo así en tu vida de programador y sabés a lo que me refiero.

Entonces, la forma normal de hacerlo en un lenguaje de programación de los que estamos acostumbrados (Java, Python, PHP, javascript) sería así:

{% highlight scala%}
class Calculadora(marca: String) {
  // Este código suelto es el constructor!
  var color: String = ""
  if (marca == "Casio"){
    color = "Azul"
  }else if (marca == "HP"){
    color = "Rosa"
  }else if (marca == "Apple"){
    color = "Blanco"
  }else{
    color = "Negro"
  }

  def sumar(m: Int, n: Int): Int = m + n
}
{% endhighlight%}

Si no entendiste mucho del ejemplo anterior podés comenzar con el [Tutorial básico de Scala](/2011-11-20-scala-para-refugiados-de-java-resumen.html).

El código anterior aparte de ser feo, sufre de problemas de **legibilidad**, **falta de brevedad**, y sobretodo se torna **inmantenible**. Otra falencia importante es que no podemos utilizar los tan bien ponderados `val`s de Scala, o sea, valores inmutables. Por ejemplo, otro gran problema: escribimos `color` 5 veces!!! Eso es sin lugar a dudas código redundante. Como todo, cuantas más veces se repita algo, mayor es la probabilidad de cometer un error. En alguna de las 5 veces que escribimos `color` nos pudimos haber equivocado.

Una mejora que podemos hacer es mediante la utilización de la **orientación a expresiones** de Scala. Voy a explicar un poco más esto. En Scala, practicamente todo es una expresión. Esta es la definición de **Expresión** según wikipedia:

> Una expresión en un lenguaje de programación es una combinación de valores explícitos, constantes, variables, operadores y funciones que son interpretados de acuerdo a reglas particulares (...), lo cual al ser computado produce otro valor.

Es decír, la definición simple sería:

> Una expresión es algo que devuelve un valor

En Java, por ejemplo, un `if-else` no es una expresión, porque no devuelve ningún valor. En cambio en Scala, los `if-else` son expresiones, y podemos tomar ventaja de esto. Veamos cómo cambia nuestro ejemplo:

{% highlight scala%}
class Calculadora(marca: String) {
  val color: String = if (marca == "Casio"){
    "Azul"
  }else if (marca == "HP"){
    "Rosa"
  }else if (marca == "Apple"){
    "Blanco"
  }else{
    "Negro"
  }

  def sumar(m: Int, n: Int): Int = m + n
}
{% endhighlight%}

Primero que nada notá el `val` que precede a `color`. Eso indica que `color` será una variable inmutable, una constante, un valor. Es decir que no va a cambiar su valor a lo largo de la vida del objeto. Esto tiene mucho sentido, nosotros creamos una calculadora Casio y va a ser siempre azul, salvo que la pintemos, en cuyo caso crearíamos otra calculadora nueva. Si la inmutabilidad no te convence, creeme que en ambientes concurrentes donde múltiples hilos acceden a tus objetos, se vuelve una característica muy valiosa.

Lo segundo interesante ahora es que de alguna forma asignamos el resultado del `if-else` al valor de `color`. Esto es así, literalmenete se produce la asignación del resultado del la sentencia condicional `if-else`. Esta es una de las cosas que hacen a Scala orientado a las expresiones.

Esto significó una gran mejora de nuestro código. Primero porque pudimos utilizar variables inmutables, segundo porque hace nuestro código más legible, y tercero porque no va a haber lugar a errores. 

De todas maneras existe una mejora más que podemos realizar. Como en el primer ejemplo, donde repetimos 5 veces **color**, en el anterior repetimos 3 veces **marca**. Para conseguir simplificar esto podemos utilizar el **pattern matching** o reconocimiento de patrones. Podemos  Si querés leer más podes dirigirte al [Tour de Scala](http://docs.scala-lang.org/es/tutorials/tour/pattern-matching.html) (y de paso si encontrás algún error en la traducción me contás).

El ejemplo va a ser más que explicativo.

{% highlight scala%}
class Calculadora(marca: String) {

  val color: String = marca match{
    case "Casio" => "Azul"
    case "HP" => "Rosa"
    case "Apple" => "Blanco"
    case _ => "Negro"
  }
  def sumar(m: Int, n: Int): Int = m + n
}
{% endhighlight%}

Lo que hicimos es "machear" la variable `marca` con alguno de los patrones definidos mediante el `case`. Es decir, si `marca` es "Casio" devuelve "Azul", si es "HP", devuelve "Rosa" y así siguiendo. Lo único medio raro es el guión bajo (_) que aparece al final. Ese es el caso `default`, es decir que si marca no cumple ninguno de los criteros superiores, se devuelve "Negro". No es sorprendente que `match` sea una expresión, al igual que el `if-else`, que devuelve un valor.

Este es el final. Es increíble ver la potencia que tiene Scala sin resignar legibilidad ni concisión (sustantivo de conciso, aunque no lo crean). Si te interesa esto, podés continuar leyendo algo sobre las [Clases Case](http://docs.scala-lang.org/es/tutorials/tour/case-classes.html)
