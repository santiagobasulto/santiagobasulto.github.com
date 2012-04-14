---
layout: post
title: "Scala para refugiados de Java - Parte 1: main(String[])"
category: scala
tags: scala java programming tutorial
---

>Este es un tutorial de Scala para gente con conocimientos de Java. Es una traducción literal de las series homónimas de [Daniel Spiewak](http://twitter.com/#!/djspiewak), con expresa autorización del autor. Accedé al [contenido original](http://www.codecommit.com/blog/scala/scala-for-java-refugees-part-1).

Vos sabés quién sos. Sos el desarrollador que eligió Java unos años atras, tal vez como un segundo lenguaje y una mejor alternativa a C++, tal vez como el primer lenguaje al ingresar a la industria. Estás cómodo con Java, conocés sus entradas y salidas, sus formas. Es como una vieja novia; tal vez no sentís la vibración de siempre, pero sabes cómo acariciarla para que sonría. En resumen, sos un artesano y Java es tu animal de carga, tu caballo de batalla.

De todas maneras estás empezando a ser un poco más pragmático a la hora de decidir por un lenguaje. Para decirlo gentilmente, la luna de miel de Java se terminó. Todavía es difícil encontrar las suficientes fallas en el lenguaje para dejarlo del todo, pero estás abierto a considerar otras alternativas. Has escuchado de esta moda llamada Ruby – cómo no escucharlo, dado el nivel de ruido producido por sus seguidores. Estás impresionado por la simpleza de sus construcciones y el poder de su sintaxis, pero no compras eso de utilizar un lenguaje de scripting para construir una aplicación empresarial. El tipado dinámico y TextMate son muy buenos, pero para el desafío del mundo real vas a necesitar algo con un poco más de solidez. Como buen pragmático, te quedas con la herramienta que funciona: Java.

La buena noticia es que hay una luz al final del tunel. Un nuevo lenguaje entró en escena que está llamando la atención del mundo del desarrollo. Scala parece ofrecer todo lo que estuviste buscando en un lenguaje: tipado dinámico, compilado a bytecode (para poder ejecutarlo en todos esos servidores de antaño que soportan Java), una sintaxis breve y expresiva. Has visto algunos ejemplos que realmente te han cautivado. Parece la viva imagen de Java, pero con la mitad de las construcciones inútiles de este. No hay punto y coma, ni “public static void” para anotar métodos; hasta parece tener algún tipo de mecanismo inferencia de tipado dinámico.

El único problema que tenés es darte cuenta cómo comenzar. Trataste mirando el sitio web de Scala, pero lo que encontraste te detuvo. Todo es tan… funcional. Lambdas, funciones de alto nivel, inmutabilidad, recursión. De repente las cosas parecen tan prometedoras.

No tengas miedo, refugiado de Java EE, no todo está perdido. Es verdad, Scala es un lenguaje funcional, pero también es imperativo y orientado a objetos. ¿Qué significa esto? Esto significa que no es necesario escribir código con el único propósito de agradar a Haskell Curry. Podés escribir código que sea realmente posible leer una semana después. Hasta te será posible mostrarle el código a tus conocidos amantes de Java y que les sea posible entenderlo. No tenés que aplicar curry para todas las funciones y evitar bucles a cualquier costo. Podés escribir tus aplicaciones Java en Scala. Lo único que necesitás es la introducción correcta.

## Introducción

Si vos sos como yo y te podes identificar con lo anterior, entonces estas series son para vos. He leido muchos artículos y tutoriales sobre Scala (las series de Alex Blewitt son altamente recomendables, especialmente si estás interesado en un lado más funcional de la vida), pero pocos de estos tutoriales han sido escritos para hacerle más fácil la transición al desarrollador Java común y corriente. Yo personalmente tengo muy poca experiencia con PF (Programación Funcional), por lo tanto no creo que pueda escribir un artículo acerca de como transformar código en Scheme a Scala incluso aunque así lo quisiera. En su lugar, esta serie de tutoriales se enfocarán en cómo Scala es tan similar a Java, aunque mejor.

¿Mencióne las series introductorias de Alex? Realmente, es un gran tutorial y también una buena introducción a Scala. Una vez que hayas terminado de leer mis pensamientos, deberías seguir con cosas más coherentes. Cuantos más mejor.

## Manos a la obra

{% highlight scala %}
object HelloWorld extends Application {
  println("Hello, World!")
}
{% endhighlight %}

Nada mejor que empezar con un poco de código. Notá lo refrescante de no tener que incluir puntos y coma obligatoriamente. Es posible usarlos si queremos, pero no son necesarios salvo que necesitemos múltiples sentencias en una sola linea. Este código hace exactamente lo que parece, define una aplicación la cual (cuando se ejecuta mediante el intérprete de Scala) imprimirá “Hello, World!” a stdout (la salida del intérprete). Si ponés este código en un archivo con la extensión .scala, después podés compilarlo usando el compilador scalac. El resultado será un solo archivo .class. Tecnicamente sería posible ejecutar el archivo .class usando el intérprete de Java, pero sería necesario hacer algunos arreglos al classpath. Lo más fácil es usar el comando scala de la siguiente manera:

{% highlight bash %}
scalac hello.scala
scala HelloWorld
{% endhighlight %}

¿Notás el nombre del archivo en cuestión? A diferencia de Java, Scala no nos fuerza a definir todas las clases públicas individualmente en archivos con el mismo nombre. De hecho, Scala te deja definir tantas clases como quieras por archivo (como en C++ o Ruby). De todas maneras sigue siendo una buena práctica seguir las convenciones de nombres de Java, por lo tanto siendo buenos programadores guardaremos nuestro ejemplo HelloWorld en un archivo llamado HelloWorld.scala.

## Editores

Es momento para una breve nota acerca de tus primeros momentos con Scala: usar el editor correcto es la clave. Como seguramente has aprendido de todos tus años en el mundo Java, los IDEs son tus amigos. Siendo Scala un lenguaje mucho más joven no cuenta con un soporte de IDEs tan bueno. Es un lenguaje estático de propósito general como Java, por lo que un IDE estará disponible. Sin embargo, por el momento estás limitado a un conjunto muy limitado de opciones.

* Eclipse (usando uno de los dos inestables plugins)
* Emacs
* IntelliJ (basicamente cuenta con coloreado de sintaxis)
* TextMate
* VIM
* jEdit

Hay algunas otras opciones disponibles, pero estas son las más conocidas (para una lista completa ver el directorio misc/scala-tool-support/ bajo la instalación de Scala). Mi recomendación personal es usar jEdit o TextMate, aunque si te sentís aventurado sos libre para probar alguno de los plugins de Eclipse.

El soporte para Scala en Eclipse tiene la ventaja (por lo menos con el plugin beta) de contar con características como resaltado semántico, completación de código (para Scala y clases importadas de Java) y otras características similares. En mi experiencia, de todas formas, ambos plugins de Eclipse eran inestables hasta el punto de ser inutilizables como tales, no vale la pena los problemas que generan. Scala es un lenguaje mucho más claro que Java, por lo tanto no es realmente necesario un IDE super potente. Sería agradable tenerlo, sin dudas, pero no esencial.

## Más Hello World

{% highlight scala %}
object HelloWorld2 {
  def main(args:Array[String]) = {
    var greeting = ""
    for (i <- 0 until args.length) {
      greeting += (args(i) + " ")
    }
    if (args.length > 0) greeting = greeting.substring(0, greeting.length - 1)

    println(greeting)
  }
}
{% endhighlight %}

Guardá esto en un archivo nuevo (lo llamaremos “HelloWorld2.scala”), compilalo y ejecutalo utilizando los siguientes comandos:

{% highlight bash %}
scalac HelloWorld2.scala
scala HelloWorld2
{% endhighlight %}

Una vez más se imprime “Hello, World!” a stdout. De todas maneras esta vez hicimos las cosas un tanto diferentes. Ahora incluímos argumentos de la consola de comando en nuestra aplicación. Definimos una variable de tipo String, iteramos sobre un array y hacemos un poco de manipulación de String. Bastante sencillo, pero definitivamente más complejo que el primer ejemplo. (Nota: Los expertos en Scala sin dudas sugerirán el uso de Array#deepMkString(String) (similar al método Array::join de Ruby) en lugar de iterar sobre el array. Este es el enfoque correcto, pero quería ilustrar un poco más del lenguaje que solo características oscuras de la API).

La primera cosa para notar de este ejemplo es que esta vez definimos un método main. En el primer ejemplo, solamente extendimos Application y declaramos todo en el constructor por defecto. Eso es simple y conciso, pero tiene dos problemas. Primero, nos es imposible parsear los argumentos de la consola de esa forma. Segundo, los ejemplos así son tremendamente confusos para los que se están iniciando en Scala ya que parece algo meramente mágico. No te preocupes, explicaré la magia detras de nuestro primer ejemplo a su tiempo, pero por ahora solamente confiá.

En el ejemplo, definimos un método principal (main) que es similar al viejo conocido de Java, public static void main. De hecho, es casi exactamente el análogo en Scala a la signatura del método de Java. Con esto en mente, a un desarrollador experimentado le será posible entender algunas cosas del lenguaje solo con una leída.

En primer lugar, parece que tódos los métodos son implicitamente públicos. Esto es correcto. Los métodos en Scala son públicos por defecto, lo que significa que no existe un modificador de acceso para anotar a un método como publico (es decir, no existe el public de Java), sin embargo sí existen los modificadores private y protected. También parece que los métodos de Scala son estáticos por defecto. Esto, de todas maneras, no es exactamente correcto.

Scala en realidad no tiene el concepto de métodos (ni atributos) estáticos (static en Java). Cuanto antes te des cuenta de eso, más fácil te resultará el lenguaje. En su lugar cuenta con una sintaxis especial la cual permite fácilmente definir y utilizar clases singleton (o instancia única); eso es precisamente lo que object significa en nuestro ejemplo. Lo que realmente hemos declarado es una clase singleton con un método de instancia main. Me ocuparé de esto con más detalle después, pero por ahora solo pensá en un object como una clase con un único miembro estático.

Mediante una inspección más profunda de nuestro ejemplo, vamos a comprender un poco mejor tanto la sintaxis de arrays de Scala, comom también la idea de cómo podemos especificar explicitamente tipos variables.

{% highlight scala %}
def main(args:Array[String]) = {
{% endhighlight %}

En este caso, args es un parámetro del método del tipo Array[String]. Por lo tanto podemos decir que args es un array de Strings (un vector o arreglo que contiene cadenas de caracteres). En Scala, Array es realmente una clase (a diferencia de los arrays de Java) que toma un parámetro de tipo para definir el tipo de sus elementos. La sintaxis de Java equivalente (asumiendo que Java tuviera una clase Array) sería algo como:

{% highlight java %}
public static void main(Array<String> args) {
{% endhighlight %}

En Scala, el tipo de una variable es especificado con la sintaxis variable:Tipo. Así, si quisera declarar una variable explicitamente del tipo Int, lo haría de la siguiente manera:

{% highlight scala %}
var myInteger:Int
{% endhighlight %}

Si mirás el ejemplo, de hecho declaramos una variable de tipo String. Sin embargo, no especificamos explicitamente ningún tipo. Esto es así porque estamos aprovechando el mecanismo de inferencia de tipos de Scala. Estas dos declaraciones son semanticamente equivalentes:

{% highlight scala %}
var greeting = ""

var greeting:String = ""
{% endhighlight %}

En la primer declaración es obvio para nosotros que greeting es un String, por lo tanto el compilador es capaz de inferirlo por nosotros. Ambas variables greeting son chequeadas estaticamente, la primera es solamente 7 caracteres más corta.

Programadores observadores también se daran cuenta de que no hemos declarado el tipo de retorno para nuestro método main. Es así porque Scala puede inferir esto también. Si realmente quisiéramos decir algo explicitamente, podríamos realizar una declaración como la siguiente:

{% highlight scala %}
def main(args:Array[String]):Unit = {
{% endhighlight %}

Una vez más, el tipo está por delante del elemento, delimitado por el caracter dos puntos. Un comentario, en Scala, Unit es un tipo para situaciones tipo no-me-importa-qué-retorno. Podés pensarlo como Object y void de Java juntos en una sola estructura.

## Iterando sobre un Array
{% highlight scala %}
var greeting = ""
for (i <- 0 until args.length) {
  greeting += (args(i) + " ")
}
{% endhighlight %}

Por cierto, no vale la pena notar por el momento que la convención para identar en Scala es dos espacios, a diferencia de los tabs o cuatro espacios tan comunes en Java. La identación no es significante, por lo tanto podés hacer las cosas como más te gusten, pero las otras cuatro mil millones, noventa y nueve millones, novecientos noventa y nueve mil, novecientos noventa y nueve personas en el mundo usan dos espacios como convencion, por lo tanto tal vez es una buena idea empezar a usarlos.La lógica detras de esta convención es que las estructuras profundamente anidadas no son un mal signo en Scala, como lo son en Java, por eso este tipo de identación puede ser más acorde.

Este ejemplo de código es un poco menos obvio que los anteriores. Primero comenzamos declarando una variable, greeting la cual es de tipo String (inferido). Nada difícil por ahora. La segunda linea está usando el raramente visto bucle for de Scala, un poco más de inferencia de tipos, una invocación de un método sobre una primitiva y una instancia de Range. Desarrolladores con experiencia en Ruby reconocerán esta sintaxis equivalente:

{% highlight ruby %}
for i in 0..(args.size - 1)
      greeting += args[i] + " "
    end
{% endhighlight %}

La clave del bucle for en Scala es la instancia de Range creada por el método RichInt#until. Podemos partir esta sintaxis en diferentes sentencias así:

{% highlight scala %}
val range = 0.until(args.length)
for (i <- range) {}
{% endhighlight %}

Ah, el usar val en lugar de var no es un error de tipeo. Cuando usamos val estamos declarando la variable range como una constante (en el sentido de Java, no de C/C++). Pensalo como una forma más corta del modificador final de Java.

Scala hace posible el invocar métodos usando diferentes sintaxis. En este caso, estamos viendo la forma valor nombreMetodo parametro, la cual es literalmente equivalente a valor.nombreMetodo(parametro). Otra importante acción que sucede aquí es la conversión implícita de un literal Int (0) a una instancia de scala.runtime.RichInt. Cómo sucede esto no es importante ahora, solo es importante saber que RichInt es la clase que declara el método until, el cual retorna la instancia de Range.

Una vez que tenemos la instancia de Range (más alla de cómo es creada), le pasamos el valor a la mágica sintaxis del for. En la declaración del for, estamos definiendo una nueva variable i del tipo inferido Int. Esta bariable contiene el valor actual mientras iteramos a avanzamos a través de range [0, args.length] (incluyendo el límite inferior, pero no el superior).

En resumen, el for mostrado es casi, pero no completamente equivalente al siguiente código Java:

{% highlight java %}
for (int i = 0; i < args.length; i++) {
{% endhighlight %}

Obviamente la sintaxis Java está definiendo explicitamente la evaluación del rango sobre el cual itera, en vez de usar algún tipo de objeto Range, pero el punto sigue siendo válido. Afortunadamente, no vas a tener que usar mucho esta sintaxis de bucles en Scala, como veremos en un momento.

El cuerpo del bucle es último pedazo interesante de código de nuestro ejemplo. Obviamente estamos agregando al final de nuestro String greeting el valor. Lo que seguramente te causó gracia (tanto como a mi) es el hecho de que el acceso a los arrays en Scala es a mediante paréntesis, no corchetes. Supongo tiene sentido ya que los parámetros de tipo en Scala son especificados usando corchetes (en vez de signos mayor, menor < >), pero sigue siendo un poco raro.

Para resumir, el ejemplo superior en Scala es logicamente equivalente al inferior en Java:

{% highlight scala %}
var greeting = ""
for (i <- 0 until args.length) {
  greeting += (args(i) + " ")
}

String greeting = "";
for (int i = 0; i < args.length; i++) {
    greeting += args[i] + " ";
}
{% endhighlight %}

## Una mejor forma para iterar

En Java 5 vimos la introducción del llamado bucle for/each. Por lo tanto en Java podemos hacer algo así:

{% highlight java %}
for (String arg : args) {
    greeting += arg + " ";
}
{% endhighlight %}

Mucho más conciso. Scala tiene una sintaxis similar definida como una función de alto nivel (una función la cual toma otra función como parámetro). Hablaré más sobre esto en un rato, pero por el momento podés considerarlo más polvo mágico de hadas:

{% highlight scala %}
args.foreach { arg =>
  greeting += (arg + " ")
}
{% endhighlight %}

Aquí vemos que foreach es un método de la clase Array que toma una closure (una función anónima) como parámetro. El método foreach después invoca esa closure una vez por cada elemento, pasando el elemento como un parámetro para esa closure (arg). El parámetro arg tiene un tipo inferido String porque estamos iterando sobre un array de Strings.

Como vimos antes, los métodos en Scala pueden ser invocados de diversas formas. En este caso estamos llamando a foreach omitiendo los paréntesis por claridad. También podríamos haber escrito el ejemplo así:

{% highlight scala %}
args.foreach(arg => {
  greeting += (arg + " ")
})
{% endhighlight %}

Scala de hecho define una forma aun más concisa para definir closure en una linea. Podemos omitir todas las llaves al mover la instrucción a la invocación del método

{% highlight scala %}
args.foreach(arg => greeting += (arg + " "))
{% endhighlight %}

Nada mal! Entonces, nuestro ejemplo completamente re escrito queda así:

{% highlight scala %}
object HelloWorld2 {
  def main(args:Array[String]) = {
    var greeting = ""
    args.foreach(arg => greeting += (arg + " "))
    if (args.length > 0)
      greeting = greeting.substring(0, greeting.length - 1)
    println(greeting)
  }
}
{% endhighlight %}

La sintaxis luce genial, pero ¿qué es lo que realmente está haciendo? No se vos, pero yo odio usar APIs que no se cómo implementarlas yo mismo. Con un poco de trabajo, podemos comprender el método foreach de Scala con un póco de código puro de Java. Asumamos por un momento que Java tiene una clase Array. En esa clase, pretendamos que existe un mètodo foreach el cual recibe una sola instancia como parámetro. En código queda algo así:

{% highlight java %}
public interface Callback<T> {
    public void operate(T element);
}

public class Array<T> {
    // ...
    public void foreach(Callback<T> callback) {
        for (T e : contents) {   // our data structure is called "contents"
            callback.operate(e);
        }
    }
}
{% endhighlight %}

Podría haber definido el foreach de forma recursiva (como está definido en Scala), pero acordate que estoy tratando de mantener estas explicaciones libres de las complicaciones de la programación funcional.

Manteniendo nuestro objetivo de ver un análogo al foreach de Scala, aquí muestro cómo podemos usar la API de arriba en Java:

{% highlight java %}
public class HelloWorld2 {
    public static void main(Array<String> args) {
    final StringBuilder greeting = new StringBuilder();
    args.foreach(new Callback<String>() {
        public void operate(String element) {
            greeting.append(element).append(' ');
        }
    });
    if (args.length() > 0) {
        greeting.setLength(greeting.length() - 1);
    }

    System.out.println(greeting.toString());
    }
}
{% endhighlight %}

¿Comenzás a ver por qué Scala es realmente atractivo? Si sos como yo, querés que Scala sea más conciso que Java. En este caso es exactamente lo que conseguimos. Nada de funcional, ni inmutabilidad. Solo código sólido y trabajado.

# Unas palabras sobre tipos primitivos
Dado que Scala está construido sobre la JVM, hereda muchas de sus API directamente de Java. Esto significa que podés interactuar con las API de Java. Más aun, significa que cualquier código que escribis en Scala está usando las API y funciones de Java. Por ejemplo, nuestro ejemplo HelloWorld2 está usando la variable greeting de tipo String. Esta variable es literalmente del tipo java.lang.String. Cuando declaras una variable entera (tipo Int) el compilador la convierte a la primitiva int de Java.

Es importante notar que hay algunas de conversiones implícitas incluidas (como la de Int a RichInt que vimos antes con la creación de Range). Por ejemplo, el Array[String] de Scala será implicitamente convertido a String[] de Java cuando sea pasado a un método que acepte esos valores. Incluso los parámetros de tipo de Scala están disponibles y son interoperables con las generics (genéricos) de Java (a partir de la versión 2.6.2). En resumen, cuando usas Scala, realmente lo estás usando Java, solo que con una sintaxis diferente.

## Conclusión
Scala no tiene por qué ser complejo, necesariamente académico o requerir un master en Computer Science. Scala puede ser el lenguaje para el hombre común, el desarrollador de 9-5 que está trabajando en la próxima aplicación web empresarial. Tiene el potencial real de proveer la sintaxis clara que Java nunca tuvo sin renunciar al poder y estabilidad de un lenguaje confiable de primer nivel. ¿Convencido?

A continuación, clases, métodos y propiedades: todo lo que necesitas saber para empezar con la programación orientada a objetos en Scala.
