---
layout: post
title: "Scala para refugiados de Java - Parte 3: Métodos y miembros estáticos"
category: scala
tags: scala java programming tutorial
---

>Este es un tutorial de Scala para gente con conocimientos de Java. Es una traducción literal de las series homónimas de [Daniel Spiewak](http://twitter.com/#!/djspiewak), con expresa autorización del autor. Accedé al [contenido original](http://www.codecommit.com/blog/scala/scala-for-java-refugees-part-1).


<br />

> Este tutorial es el tercero de una serie. Podés acceder al anterior mediante el siguiente [link](/scala/2011/11/23/scala-para-refugiados-de-java-parte-2.html)

En esta serie de tutoriales, ya hemos inspeccionado los fundamentos de la [sintaxis de Scala](/scala/2011/11/22/scala-para-refugiados-de-java-parte-1.html) como también una aproximación de cómo funciona la [orientación a objetos](/scala/2011/11/23/scala-para-refugiados-de-java-parte-2.html). De todas maneras, no hemos visto ninguno de estos temas en mayor profundidad. La mayoría de nuestros esfuerzos se han concentrado en vistazos a un nivel muy alto para obtener una noción general del lenguaje. Este post tratará de profundizar más en cuanto a la sintaxis de métodos, considerar algo de alcances y tratar de cubrir cómo funcionan los miembros estáticos en Scala. También veremos algunas trampas para "manejar" la falta de instrucciónes imperativas.

Más sobre métodos
-----------------

A Scala no se lo llama un "lenguaje funcional" solo porque sea [Turing completo](http://es.wikipedia.org/wiki/Turing_completo). Scala tiene una sintaxis muy poderosa y flexible a lo que se refiere a métodos, tanto para declaraciones como para invocaciones. Ya hemos visto algunos ejemplos básicos:

<pre lang='scala'>
class Person {
  def firstName() = {
    var back:String = ...   // leido desde la base de datos
    back
  }
}
</pre>

Suficientemente simple. Pero esto no te ilustra el panorama completo. En Java, por ejemplo, podés crear métodos con diferentes tipos de visibilidad, modificadores y (suficientemente raros) tipos de dato de retorno. ¿Soporta Scala toda esta flexibilidad?

La respuesta es "Sí". Scala permite diferentes visibilidades no solo para métodos, sino para todo tipo de miembros. Por ejemplo:

<pre lang='scala'>
class Person {
  private var name = "Daniel Spiewak"
  val ssn = 1234567890    // campo constante público

  def firstName() = splitName()(0)   // método público

  private def splitName() = name.split(" ")    // método privado

  protected def guessAge() = {
    import Math._
    round(random * 20)
  }
}
</pre>

Bajo el riesgo de irme por las ramas, es importante notar la (aparente) sentencia de importación dentro del método `guessAge()`. En el primer post mencioné que los imports de Scala son bastante más poderosos que los de Java. Uno de sus muchos encantos es poder trasnferir el poder de importar en un alcance específico. La sentencia de importación dentro de `guessAge()` es muy parecida a una sentencia de importación estática de Java que solo provee acceso a los miembros de `Math` dentro del método `guessAge()`. Por lo tanto no podríamos haber hecho una llamada a `round()` dentro del método `splitName()`. Los que están familiarizados con Ruby pueden pensar en esto como las inclusiones sin todos esos dolores de cabeza (de hecho no está incluyendo, está importando, por lo tanto se elimina la necesidad de utilizar los nombres completos).

Los modificadores de acceso de Scala también son un poco más poderosos que los de Java. Por ejemplo, `protected` por defecto limita el acceso solo a subclases, a diferencia de Java que también permite el acceso a otras clases en el mismo paquete. De todas maneras, lo más importante es que Scala permite al desarrollador especificar más explicitamente el alcance del modificador de acceso. Esto se logra utilizando la notación `modificador[paquete]`. Por ejemplo:

<pre lang='scala'>
package com.codecommit.mypackage

class MyClass {
  private[mypackage] def myMethod = "test"
}
</pre>

En este ejemplo, el acceso a `myMethod` está restringido a ambos, la clase que lo contiene y el paquete que contiene dicha clase. Esencialmente, esta es la manera de emular el modificador a nivel de paquete de Java utilizando Scala. El modificador `protected` también permite estos calificadores de visibilidad. La única restricción acá es que el paquete especificado debe ser el paquete que contiene a la definición. En el ejemplo anterior, el especificar `private[com.codecommit.mypackage]` es perfectamente válido, pero especificar `private[scala.collection.immutable]` no sería correcto.

Por lo tanto, a excepción del modificador a nivel de paquete, la visibilidad en Scala funciona bastante parecido a la de Java, tanto a nivel sintáctico como en funcionamiento. Los modificadores son los que empiezan a poner las cosas más interesantes. Scala tiene menos modificadores de métodos que los que tiene Java, principalmente porque no necesita tantos. Por ejemplo, Scala soporta el modificador `final`, pero no soporta `abstract`, `native`, o `synchronized`:

<pre lang='scala'>
abstract class Person {
  private var age = 0

  def firstName():String
  final def lastName() = "Spiewak"

  def incrementAge() = {
    synchronized {
      age += 1
    }
  }

  @native
  def hardDriveName():String
}
</pre>

En Java hubiésemos escrito el código anterior así:

<pre lang='java'>
public abstract class Person {
    private int age = 0;

    public abstract String firstName();

    public final String lastName() {
        return "Spiewak";
    }

    public synchronized void incrementAge() {
        age += 1;
    }

    public native String hardDriveAge();
}
</pre>

Sí, ya se que es más acorde a Scala utilizar actores que `synchronized()`, pero vamos paso a paso.

¿Ves como Scala continúa con su filosofía de hacer las cosas comunes más concisas? Pensalo, casi todos los métodos que declarás son públicos, entonces ¿por qué deberías especificar eso explicitamente? De forma similar, también tiene sentido que los métodos sin un cuerpo deberían ser implicitamente abstractos (salvo que sean nativos).

Una cosa muy importante a la hora de ahorrar en tipeo que deberías ver del ejemplo anterior es que Scala no te fuerza a que declares el tipo de retorno de tus métodos. Otra vez, el mecanismo de inferencia de tipos juega su papel y el tipo de retorno es inferido. La excepción a esto existe si el método puede retornar en diferentes momentos del flujo de ejecución distintos tipos (ahí necesita la sentencia de retorno obligatoriamente). En este caso, Scala te obliga a especificar el tipo de retorno para asegurarse un comportamiento no ambiguo.

También deberías notar que ninguno de los métodos en Scala incluyen una cláusula `return`. Obviamente esto parece raro, a juzgar por la traducción a Java, `lastName()` debería retornar un String. Resulta que Scala tiene un atajo muy útil para el retorno en los métodos: la última sentencia en una expresión, estando en el alcance adecuado, una closure, o un método, es el valor que se retorna. Esta convención existe también en lenguajes como Ruby y Haskell. Miremos el siguiente ejemplo que ilustra lo dicho:

<pre lang='scala'>
    def nombre() = {
      val nombre = new StringBuilder("Daniel")
      nombre.append(" Spiewak");
      nombre.toString()
    }

    val s = nombre()
    println(s)    // imprime "Daniel Spiewak"
</pre>

De nuevo, en este ejemplo el tipo del valor de retorno del método es inferido (como un String). Tranquilamente podríamos haber escrito el método `nombre()` de la siguiente manera, solamente que sería menos conciso.

<pre lang='scala'>
    def nombre():String = {
      val nombre = new StringBuilder("Daniel")
      nombre.append(" Spiewak");
      return nombre.toString()
    }
</pre>

Esta forma de "no-return" resulta realmente importante cuando se trata de métodos (o funciones) anónimos, también llamados closures. Obviamente una closure no va a "retornar" nada, sino que producirá valores para ser usados dentro de otro método o función, de todas maneras el principio es el mismo. Ya que las closures generalmente son usadas para reducir la cantidad de código y hacer algunos algoritmos más concisos, solo tiene sentido si su sintaxis (incluído el retorno de valores) sea lo más compacto posible:

<pre lang='scala'>
    val arr = Array(1, 2, 3, 4, 5)
    val sum = arr.reduceLeft((a:Int, b:Int) => a + b)

    println(sum)    // 15
</pre>

En este ejemplo le estamos pasando una función anónima al método `reduceLeft()`de `Array`. Este método solamente llama a la función pasada como parámetro repetidamente para cada par de valores, pasándo estos valores como los parámetros `a` y `b`. El quid de la cuestión reside en que nuestra función anónima suma ambos parámetros y produce un valor que es pasado nuevamente al método `reduceLeft()`. Nuevamente, no existe ninguna cláusula `return` (de hecho, como se trata de una closure debería ser `yield`). Además, no especificamos explicitamente el tipo de retorno para la closure, ya que es inferido de nuestra última (en este caso única) sentencia.

Sobreescribiendo métodos
------------------------

A very important concept in object-oriented programming is method overriding, where a subclass redefines a method declared in a superclass.  Java’s syntax looks like this:

Un concepto muy importante en la programación orientada a objetos es la sobreescritura de métodos, donde una subclase redefine un método declarado en una superclase. La sintaxis de Java es algo así:

<pre lang='java'>
    public class Fruta {
        public int getPrecio() {
            return 5;
        }
    }

    public class Manzana extends Fruta {
        @Override
        public int getPrecio() {
            return 1;
        }
    }
</pre>

Técnicamente, la anotación `@Override` es opcional, pero es una buena práctica usarla. Te da en tiempo de compilación la seguridad de que realmente estás sobreescribiendo el método de una superclase. En principio, un método declarado en una subclase sobreescribe cualquier método en la superclase declarado de la misma forma (exactamente la misma signatura). En un principio, parece genial, ¿menos sintaxis, o no?. El problema está cuando empezás a manejar APIs cuando no estás seguro si la signatura del método sobreescrito es correcta. Simplemente pudiste haber sobrecargado el método en vez de sobreescribirlo, resultando en una funcionalidad totalmente distinta y a veces en errores (bugs) difícil de encontrar. Para estos casos es donde se ve la utilidad de `@Override`.

Scala tiene un problema mayor con la sobreescritura de métodos que solo la verificación de la signatura: herencia múltiple. La herencia múltiple es cuando una clase hereda de más de una superclase. C++ ya contaba con esta característica hace muchos años, demostrando efectivamente cuán horrible puede llegar a ser. Cuando James Gosling diagramó la especificación inicial de Java, la herencia múltiple fue una de las cosas que evitó especificamente. Esto es bueno por simplicidad, pero a veces restringe demasiado. Las interfaces son muy buenas, pero algunas veces realmente no alcanzan.

La clave para evitar ambiguedades en la jerarquía de herencia es especificar explicitamente que un método debe sobreescribir un método de una superclase. Si ese método tiene la misma signatura que el método de la superclase pero no se dice especificamente que lo sobreescribe, se lanza un error de compilación. Agregale a eso un orden significativo a las cláusulas `extend/with` y terminás con un esquema de herencia múltiple bastante funcional. Pero me estoy adelantando un poco...

Este es el ejemplo de la Fruta escrito en Scala:

<pre lang='scala'>
    class Fruta {
      def precio() = 5
    }

    class Manzana extends Fruta {
      override def precio() = 1
    }
</pre>

Notá que en Scala, `override` es una palabra reservada. Es un modificador obligatorio para cualquier método con una signatura que entre en conflicto con otro método en una superclase. Por consiguiente, sobreescribir métodos en escala no es implícito (como en Java, Ruby, C++, etc), sino explicitamente declarado. Este pequeño agregado resuelve por completo el problema asociado con herencia múltiple en Scala. Veremos traits y herencia múltiple con más detalle en un artículo futuro.

Generalmente cuando sobreescribis un método, necesitás hacer una llamada al método de la superclase. Un buen ejemplo de esto sería extender un componente de Swing:

<pre lang='scala'>
    class StrikeLabel(text:String) extends JLabel(text) {
      def this() = this("")

      override def paintComponent(g:Graphics):Unit = {
        super.paintComponent(g)

        g.setColor(Color.RED)
        g.drawLine(1, getHeight() / 2, getWidth() - 1, getHeight() / 2)
      }
    }
</pre>

Este componente es un JLabel común y corriente con una linea roja dibujada en el medio. No es un componente muy útil, pero demuestra un patrón que vemos mucho en Java: delegar la implementación a la superclase. En realidad no queremos implementar toda la lógica necesaria para dibujar el texto en el contexto `Graphic` con el fondo apropiado y demás. Ese trabajo ya está hecho por nosotros en JLabel. Por lo tanto le decimos a JLabel que se pinte a sí mismo y después dibujamos lo que queremos arriba.

Como ves en el ejemplo, la sintaxis para realizar esta delegación a las superclases es prácticamente la misma que en Java. Efecticamente `super` es un valor especial privado (similar a `this`) que contiene una instancia interna de la superclase. Podemos usar dicho valor tal como `super` en Java para acceder a métodos y valores directamente en la superclase.

That little bit of extra syntax in the extends clause is how you call to a superclass constructor.  In this case, we’re taking the text parameter passed to the default constructor of the StrikeLabel class and passing it on to the constructor in JLabel.  In Java you do the same thing like this:

Ese poco de código extra en la cláusula `extends` es lo que llamamos el *constructor de la superclase*. En este caso, tomamos el parámetro `text` pasado al constructor por defecto de la clase `StrikeLabel` y se lo pasamos al constructor en `JLabel`. En Java hacemos lo mismo así:

<pre lang='java'>
    public class StrikeLabel extends JLabel {
        public StrikeLabel(String text) {
            super(text);
        }

        public StrikeLabel() {
            this("");
        }
    }
</pre>

Esto puede parecer un poco raro al principio, pero realmente provee una forma sintáctica agradable de asegurarnos que la llamada al constructor de la superclase es siempre la primer sentencia en nuestro constructor. En java, por su puesto que esto es chequeado en tiempo de compilación, pero no existe nada intuitivamente obvio en la sintaxis que te prevenga de hacer la llamada al constructor de la superclase algunas lineas más abajo. En Scala, llamar al constructor de la superclase y llamar un método de una superclase son operaciones totalmente distintas, sintacticamente. Esto representa una manera más intuitiva para entender por qué uno puede ser llamado arbitrariamente y el otro debe ser llamado antes que cualquier otra cosa.

Miembros estáticos de Scala
---------------------------

Scala is a very interesting language in that it eschews many of the syntax constructs that developers from a Java background might find essential.  This ranges from little things like flexible constructor overloading, to more complex things like a complete lack of static member support.

Scala es un lenguaje muy interesante en el sentido que este elude muchas de las construcciones sintácticas que los desarrolladores con un transfondo en Java encontrarían esenciales. Esto varía desde pequelas cosas como sobrecarga flexible de constructores, a cosas más complejas como la completa carencia de soporte para miembros estáticos (métodos, variables, etc).

En Java, los miembros estáticos son miembros normales de clases con un modificador diferente. Son accedidos desde afuera del contexto de la instancia usando el nombre de la clase como calificador:

<pre lang='java'>
    public class Utilities {
        public static final String APP_NAME = "Test App";

        public static void loadImages() {
            // ...
        }

        public static EntityManager createManager() {
            // ...
        }
    }

    System.out.println(Utilities.APP_NAME);

    Utilities.loadImages();
    EntityManager manager = Utilities.createManager();
</pre>

Scala does support this type of syntax, but under the surface it is quite a bit different.  For one thing, you don’t use the static modifier.  Instead, you declare all of the “static” members within a special type of class which acts as an only-static container.  This type of class is called object.

Scala soporta este tipo de sintaxis, pero bajo la superficie es bastante diferente. Primero, no se utiliza el modificador `static`. En su lugar, declaras todos tus miembros estáticos dentro de un tipo especial de clase que actua como un contenedor solo-para-estáticos. Este tipo de clase es llamada Objeto (mediante la palabra reservada `object`).

<pre lang='scala'>
    object Utilities {
      val APP_NAME = "Test App"

      def loadImages() = {
        // ...
      }

      def createManager():EntityManager = {
        // ...
      }
    }

    println(Utilities.APP_NAME)

    Utilities.loadImages()
    val manager = Utilities.createManager()
</pre>

The syntax to use these “statics” is the same, but things are quite a bit different in the implementation.  It turns out that object actually represents a singleton class.  Utilities is in fact both the classname and the value name to access this singleton instance.  Nothing in the example above is static, it just seems like it is due to the way the syntax works.  If we port the above class directly to Java, this is what it might look like:

La sintaxis para usar estos "estáticos" es la misma, pero las cosas son un poco distintas en la implementación. Resulta que un objeto representa una clase singleton. `Utilities` es de hecho tanto el nombre de la clase y el nombre del valor para acceder a esa instancia singleton. Nada en el ejemplo anterior es estático, solamente parece que fuera así, por la forma en que funciona la sintaxis. Si portara la clase de arriba a Java, sería algo similar a esto:

<pre lang='java'>
    public class Utilities {
        private static Utilities instance;

        public final String APP_NAME = "Test App";

        private Utilities() {}

        public void loadImages() {
            // ...
        }

        public EntityManager createManager() {
            // ...
        }

        public static synchronized Utilities getInstance() {
            if (instance == null) {
                instance = new Utilities();
            }

            return instance;
        }
    }
</pre>

Entonces, Scala nos provee una sintaxis especial que basicamente nos provee la posibilidad de utilizar singleton sin necesidad de toda esa sintaxis loca necesaria para su declaración en otros lenguajes. Esta es una solución realmente elegante a los problemas que requieran el uso de estáticos. Ya que Scala no tiene miembros estáticos, no es necesario preocuparse por mezclar los alcances, los calificadores de acceso, etc. Simplemente anda todo bien.

Pero, ¿qué hay de mezclar los miembros estáticos y de instancia? Java nos permite realizar esto de forma muy sencilla ya que los miembros estáticos están en la misma clase (con el calificador `static`), pero Scala requiere que los miembros estáticos sean declarados en una clase especial singleton. En Java podemos hacer lo siguiente:

<pre lang='java'>
public class Person {
    public String getName() {
        return "Daniel";
    }

    public static Person createPerson() {
        return new Person();
    }
}
</pre>

The solution in Scala is to declare both an object and a class of the same name, placing the “static” members in the object and the instance members in the class.  To be honest, this seems extremely strange to me and is really the only downside to Scala’s singleton syntax:

La solución en Scala es declarar ambos, el objeto y la clase con el mismo nombre y ubicar los miembros estáticos en el objeto y los miembros de instancia en la clase.

> En este punto el autor sostiene que esto es una de las desventajas de Scala, por ser algo confuso. Mi opinión es diametralmente opuesta, ya que pienso que es la mejor forma existente para mantener una orientación a objetos pura. Recordemos que el concepto de estáticos, o "miembros de clase" (como lo llaman autores reconocidos en el área como Timothy Budd) son una característica necesaria pero que rompe con la orientación a objetos, ya que la POO establece que "todo debe ser un objeto". Siguiendo con ese razonamiento, un miembro estático no estaría ligado a un "objeto", estaría ligado a una estructura extraña, una clase, no sabemos bien. En Scala se resuelve esto creando un único objeto, y siendo este el contenedor de estos miembros estáticos.

<pre lang='scala'>
object Persona {
  def crearPersona() = new Persona()
}

class Persona {
  def nombre() = "Daniel"
}
</pre>

La sintaxis para utilizar esta combinación `object/class` es exactamente la misma que resultaría en Java al mezclar los miembros estáticos y de instancia. El compilador de Scala es capaz de distinguir entre referencias al objeto Persona y referencias a la clase Persona (a una instancia de ella en realidad). Por ejemplo, el compilador sabe que no podemos crear una nueva instancia de un objeto, ya que es un singleton. Por lo tanto en el método `crearPersona()` nos estamos refiriendo a la clase persona. De forma similar, si una llamada fuese hecha a `Persona.crearPersona()` el compilador es capaz de deducir que debe ser una referencia al objeto Persona ya que no hay forma de acceder al método directamente desde la clase. Todo esto es perfectamente lógico y consistente, solo te va a parecer un poco raro las primeras veces que lo mires.

Conclusión
----------

Y de esta manera termina nuestro tutorial sobre métodos y miembros estáticos. Existen por supuesto trivialidades que no hemos cubierto, pero te van a resultar lo suficientemente simple ahora que contás con el conocimiento básico. La sintaxis más interesante está por venir. Recién hemos arañado la superficie de todas las cosas que podés hacer con los métodos. No es llamado un "lenguaje funcional" por nada! Pero al tratar de mantenernos en nuestro objetivo de representar el lado imperativo de Scala, eso vamos a guardarlo para después.

En el próximo artículo, veremos algo de reconocimiento de patrones y manejo de excepciones, dos conceptos (sorprendentemente) relacionados.
