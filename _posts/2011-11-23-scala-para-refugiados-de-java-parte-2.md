---
layout: post
title: "Scala para refugiados de Java - Parte 2: POO básica"
category: scala
tags: scala java programming tutorial
---


>Este es un tutorial de Scala para gente con conocimientos de Java. Es una traducción literal de las series homónimas de [Daniel Spiewak](http://twitter.com/#!/djspiewak), con expresa autorización del autor. Accedé al [contenido original](http://www.codecommit.com/blog/scala/scala-for-java-refugees-part-2).

<br />

> Este tutorial es el segundo de una serie. Podés acceder al anterior mediante el siguiente [link](/scala/2011/11/22/scala-para-refugiados-de-java-parte-1.html)

En el artículo anterior vimos lo básico de la sintaxis de Scala y brindamos algunas explicaciones simples de los conceptos. Obviamente hay mucho más de este lenguaje de lo que puedo presentar en un único (aunque bastante largo) artículo. En este post vamos a examinar la orientación a objetos de Scala y sus construcciones (clases, objetos, métodos, etc) y cómo se comparan con Java.

Un ejemplo más complejo
------------------------
<pre lang='scala'>
	package com.codecommit.examples
	 
	import java.awt.{Color, Graphics}
	 
	abstract class Shape {
	  var fillColor:Color = null
	 
	  def draw(g:Graphics):Unit
	  def area:Double
	}
	 
	class Circle(var radius:Int) extends Shape {
	  def draw(g:Graphics):Unit = {
	    if (fillColor == null) {
	      g.drawOval(0, 0, radius / 2, radius / 2)
	    } else {
	      g.setColor(fillColor);
	      g.fillOval(0, 0, radius / 2, radius / 2)
	    }
	  }
	 
	  def area:Double = {
	    var back = Math.Pi * radius 
	    back * radius
	  }
	}
	 
	class Square(var width:Int) extends Shape {
	  def draw(g:Graphics):Unit = {
	    if (fillColor == null) {
	      g.drawRect(0, 0, width, width)
	    } else {
	      g.setColor(fillColor)
	      g.fillRect(0, 0, width, width)
	    }
	  }
	 
	  def area:Double = width * width
	}
</pre>

Acordate que en Scala no es necesario que cada clase pública sea declarada en un archivo con el mismo nombre. De hecho, ni siquiera requiere que cada clase sea declarada en un archivo separado. Organizativamente, tiene sentido para todas esas clases triviales estar contenidas en en un mismo archivo. Con eso en mente, podemos copiar y pegar el código anterior en un nuevo archivo llamado “shapes.scala”.

La primer cosa que deberías notar sobre el fragmento es la declaración del paquete. Todas estas clases son están declaradas dentro del paquete “com.codecommit.examples”. Si esto fuese Java, hubiese sido necesario crear una nueva jerarquía de directorios que se correspondiera (com/codecommit/examples). Afortunadamente, Scala nos simplifica el trabajo para esto también. Simplemente podemos almacenar este archivo en el directorio base de nuestro proyecto y compilarlo en el lugar, sin dificultades.

Dicho esto, sigue siendo una buena práctica separar tus paquetes en sus correspondientes directorios. Esta organización hace más simple encontrar las cosas y simplifica la carga para vos (el desarrollador) a largo plazo. Aparte, ¿no es eso lo que estamos tratando al utilizar Scala en primer lugar?

Para compilar estas clases, vamos a usar el comando `fsc` (abreviatura de `Fast Scala Compiler`, Compilador rápido de Scala). `fsc` es una de esas brillantes mejoras de Scala que proveen compilación repetitiva de archivos Scala casi sin latencia. `fsc` elimina casi completamente el tiempo de inicialización del compilador debido al hecho de que el compilador de Scala se ejecuta sobre la JVM. Hace esto mediante el "precalentamiento" del compilador, manteniendo el proceso persistente de fondo. Efectivamente, es un demonio del compilador, establecido en el fondo y casi sin usar recursos hasta ser llamado. La sintaxis para ejecutarlo es idéntica al comando `scalac`:

<pre lang='bash'>
	fsc -d bin src/com/codecommit/examples/*.scala
</pre>

Este comando compilará todos los archivos .scala dentro del directorio src/com/codecommit/examples/ y ubicará los .class resultantes en /bin. Los desarrolladores de Java experimentados conocerán el valor de esta convención, especialmente en un proyecto más grande. Otra vez, Scala no intenta hechar por tierra todas las buenas prácticas y convenciones establecidas por décadas. En su lugar, su propósito es hacer más simple tu trabajo al mantenerse fuera del camino.

Primeras impresiones
--------------------

Of course, compiling an example doesn’t do us much good if we don’t understand what it means.  Starting from the top, we declare the package for all of the classes within the same file.  Immediately following is a single statement which imports the java.awt.Color and java.awt.Graphics classes.  Notice Scala’s powerful import syntax which allows for greater control over individual imports.  If we wanted to import the entire java.awt package, the statement would look like this:

Por supuesto, compilar un ejemplo no nos favorece mucho si no entendemos qué significa. Comenzando desde el principio, declaramos el paquete para todas las clases dentro del mismo archivo. Inmediatamente siguiendo, hay una única sentencia la cual importa las clases java.awt.Color y java.awt.Graphics. Nótese la potencia de la sintaxis de importación de Scala la cual permite más control sobre importaciones individuales. Si quisieramos importar el paquete entero java.awt, la declaración sería así:

<pre lang='scala'>
	import java.awt._
</pre>

En Scala, el caracter _ es un "comodín" (un caracter especial). En el caso de una importación (mediante el `import`) significa precisamente lo mismo que el caracter * en Java:

<pre lang='scala'>
	import java.awt.*;
</pre>

Scala es más consistente que Java en que el caracter _ también sirve como comodín en otras áreas, como en parámetros de tipos y en reconocimiento de patrones. Pero me estoy desviando...

Siguiendo con el ejemplo, la primer declaración es la clase abstracta `Shape`. Es importante notar que el orden de las declaraciones en un archivo no guarda ninguna significancia. Así, `Shape` podría simplemente ser declarada bajo `Circle` y `Rectangle` sin cambiar el significado del código. Esto es completamente opuesto a la sintaxis de Ruby, la cual puede derivar en raros escenarios como errores debido a clases referenciando otras clases las cuales no han sido declaradas aun. El orden es también insignificante para las declaraciones de los métodos. Como en Java, un método puede llamar otro método incluso si este es declarado sobre el segundo.

<pre lang='scala'>
	class Person {
	  def name() = firstName() + ' ' + lastName()
	 
	  def firstName() = "Daniel"
	  def lastName() = "Spiewak"
	}
</pre>

Propiedades
------------

Volviendo a nuestro primer ejemplo, la primer cosa que observamos en la clase `Shape` es la variable `color`. Esta es una variable pública (acordate que los elementos en Scala son públicos por defecto) del tipo `Color` con el valor por defecto `null`. Ahora bien, si sos un desarrollador Java con algo de experiencia, el canto de sirenas te está alertando a la vista de una variable pública. En Java (como en otros lenguajes orientados a objetos), las buenas prácticas dicen que es recomendable declarar todos los campos privados y proveer accessors (métodos de acceso, setters y getters). Esto es para promover la encapsulación, un concepto critico en el diseño orientado a objetos.

Scala también soporta encapsulación, peru su sintaxis es considerablemente más compacta que la de Java. Efectivamente, todos las variables publicas se convierten en atributos de instancia. Podés pensar en esto como si existieran setters y getters autogenerados para cada variable. Es como si estos dos fragmentos de Java fueran equivalentes (el análogo no es preciso, sirve para ilustrar la idea):

<pre lang='scala'>
    public class Person {
	    public String name;
	}

	public class Person {
	    private String name;
	 
	    public String getName() {
		return name;
	    }
	 
	    public void setName(String name) {
		this.name = name;
	    }
	}
</pre>

En realidad no es tan así, pero se entiende el punto del ejemplo. Lo que realmente está sucediendo es que estamos aprovechándonos del hecho de que en Scala las variables son realmente funciones. Es un concepto un poco raro para incorporar viniendo de un ambiente imperativo, por lo tanto probablemente es más simple seguir pensando en variables como variables.

Imaginemos que tenemos nuestra clase `Shape` y su variable pública `fillColor`. Mientras tanto decidimos que necesitamos agregar una comprobación al método que modifica el `fillColor` para asegurarnos de que el color nunca sea rojo (por qué, no estoy seguro, pero sigamos así). En Java, esto sería imposible porque la variable es pública y el forzar el uso del método de acceso cambiaría la interfaz pública de la clase.  Afortunadamente, Scala nos permite reescribir fácilemente esa porción de la clase sin afectar la interfaz de la clase ni cualquier otro código que esté utilizando nuestra clase:

<pre lang='scala'>
	abstract class Shape {
	  private var theFillColor:Color = null
	 
	  def fillColor = theFillColor
	 
	  def fillColor_=(fillColor:Color) = {
	    if (!fillColor.equals(Color.RED)) {
	      theFillColor = fillColor
	    } else {
	      throw new IllegalArgumentException("Color cannot be red")
	    }
	  }
	}
	 
	var shape = ...
	shape.fillColor = Color.BLUE
	var color = shape.fillColor
	 
	shape.fillColor = Color.RED  // lanza una IllegalArgumentException
</pre>

Como podés ver, el método sufijo `_=` usa un poco de sintaxis mágica la cual nos permite redefinir el operador de asignación (efectivamente) para una variable. Notá que desde la perspectiva del código que usa `Shape` aun parece como si fuera un atributo público. El fragmento de código que usa `Shape` seguirá andando con ambas versiones de la clase. Pensalo bien, no más get* ni set*... Ahora podés usar atributos públicos con impunidad y sin miedo de casticos de diseño a futuro.

Solo para asegurar que esto está realmente claro, aquí está el análogo con sintaxis de Ruby:

<pre lang='ruby'>
	class Shape
	  def initialize
	    @fill_color = nil
	  end
	 
	  def fill_color
	    @fill_color
	  end
	 
	  def fill_color=(color)
	    raise "Color cannot be red" if color == Color::RED
	 
	    @fill_color = color
	  end
	end
</pre>

La diferencia obvia es que el ejemplo en Scala tendrá comprobación de tipo por el compilador, mientras en Ruby no. Esta es una de las muchas áreas donde Scala demuestra la flexibilidad de la sintaxis de Ruby junto con la potencia y seguridad de Java

Métodos abstractos
------------------

Una de las características importantes de la clase `Shape` en el ejemplo es que está declarada como `abstract`. Las clases abstractas son muy importantes en el diseño orientado a objetos, y Scala no sería muy orientado a objetos si no las soportara. De todas maneras, al mirar la definición de la clase, no parece haber métodos abstractos definidos. Por supuesto, tal como en Java esto es perfectamente legal (declarar una clase abstracta sin miembros abstractos), solo que no parece tan útil.

De hecho, hay dos métodos abstractos en la clase `Shape`. Te darás cuenta que ni el método `draw` ni `area` estan realmente definidos (no tienen cuerpo). Scala detecta esto e implicitamente los hace métodos abstractos. Esto es muy similar a la sintaxis de C++ para declarar métodos abstractos:

<pre lang='scala'>
	class Shape {
	public:
	    virtual void draw(Graphics *g2) = 0;
	    virtual double area() const = 0;
	 
	    Color *fillColor;
	};
</pre>

Doy gracias a Dios que esta es el final de las similaridades de Scala con C++ en el área de los tipos abstractos. En C++ si una clase hereda de una clase abstracta y no implementa todos los métodos abstractos heredados, la clase derivada implicitamente se convierte en clase abstracta. Si una situación así ocurre en Scala, el compilador dispara un error informando al desarrollador (como en Java). La única excepción a esta regla está en las clases `Case`, que son demasiado raras como para comenzar a mencionarlas y requerirán mayor explicación más adelante.

Constructores
--------------

A pesar de los mejores esfuerzos de Josh Bloch, los constructores perduran en las arquitecturas orientadas a objetos modernas. Personalmente no puedo imaginarme escribiendo una clase no trivial la cual carezca de este elemento virtualmente esencial. Ahora, puede no ser inmediatamente obvio, pero todas las clases mostradas en este ejemplo tienen un constructor. De hecho, cada clase (y objetos) tiene por lo menos un constructor. No solo uno que podes pensar como generado por el compilador por defecto, sino declarado en tu código. Los constructores en Scala son un poco diferentes que los de Java, que en realidad son métodos especiales nombrados en base a la clase que los contiene.

<pre lang='java'>
	public class Person {
	    public Person(int age) {
		if (age > 21) {
		    System.out.println("Over drinking age in the US");
		} 
	    }
	 
	    public void dance() { ... }
	}
 
	Person p = new Person(26);   // prints notice that person is overage
</pre>

En Scala, las cosas se hacen un poco diferente. El constructor no es un método sintacticamente especial, en realidad es el cuerpo de la clase en sí mismo. El ejemplo de arriba es equivalente al siguiente fragmento de Scala:

<pre lang='scala'>
	class Person(age:Int) {
	  if (age > 21) {
	    println("Over drinking age in the US")
	  }
	 
	  def dance() = { ... }
	}
 
	var p = new Person(26)   // prints notice that person is over-age
</pre>

¿Te acordás del primer ejemplo de Scala que mostré en estas series? (el HelloWorld de tres lineas). En ese código el cuerpo del método `main` es implementado como un constructor en el objeto `HelloWorld`. Veamos:

	object HelloWorld extends Application {
	  println("Hello, World!")
	}

La sentencia `println` no está incluida en un método `main` de ningún tipo, en realidad es parte del constructor del objeto `HelloWorld` (más acerca de objetos `object` en el siguiente post). Cualquier sentencia declarada a nivel de clase es considerada parte del constructor por defecto. Las escepciones a esto son las declaraciones de métodos, que son partes de la clase en sí misma. Esto es para permitir la referencia a estos métodos.

<pre lang='scala'>
	class ChiefCallingMethod {
	  private var i = 1
	 
	  if (i < 5) {
	    lessFive(i)
	  }
	 
	  def lessFive(value:Int) = println(value + " is less than 5")
	}
 
	var chief = new ChiefCallingMethod()
</pre>

El código anterior se ejecutará y determinará satisfactoriamente que 1 es menor a 5, provando nuevamente la veracidad de las matemáticas.

This constructor syntax seems very strange to those of us accustomed to Java.  If you’re like me, the first thought which comes into your head is: how do I overload constructors?  Well, Scala does allow this, with a few caveats:

La sintaxis de este constructor parece bastante extraña aquellos que estamos acostumbrados a Java. Si vos sos como yo, el primer pensamiento que se te viene a la cabeza es: ¿cómo sobrecargo los constructores?

<pre lang='scala'>
	class Person(age:Int) {
	  if (age > 21) {
	    println("Over drinking age in the US")
	  }
	 
	  def this() = {
	    this(18)
	    println("Created an 18 year old by default")
	  }
	 
	  def dance() = { ... }
	}
</pre>

Esta versión mejorada de `Person` tiene ahora dos constructores, uno el cual recibe un `Int` como parámetro y uno que no recibe ninguno. La mayor salvedad aquí es que todos los constructores sobrecargados deben delegar al constructor por defecto (el que es declarado como parte de la clase). Así que no es posible sobrecargar un constructor para realizar operaciones completamente diferentes que el constructor por defecto. Esto tiene sentido desde un punto de vista de diseño (de todas maneras, ¿cuándo fue la última vez que declaraste un constructor así?) pero sigue siendo un poco restrictivo.

Propiedades de Constructores
--------------------------------

Entonces entendés los constructores en Scala y estás empezando a acostumbrarte a los atributos de instancia públicos, ahora es tiempo de combinar los dos conceptos mediante propiedades de constructores. ¿Qué es esto? La respuesta tiene que ver con una aparente trivialidad sintáctica de Scala, la cual establece que todos los parámetros de los constructores se convierten en variables de instancia privadas y constantes (variables `val`). Es posible, por lo tanto, acceder los parámetros pasados al constructor desde los métodos de instancia:

<pre lang='scala'>
	class Person(age:Int) {
	  def isOverAge = age > 21
	}
</pre>

Este código se compila y corre exactamente como es esperado. Es importante recordar que `age` no es realmente una variable (es un valor) y por lo tanto no puede ser reasignada en ninguna parte de la clase. De todas maneras, podría tener sentido cambiar la edad de una persona. Después de todo, las personas (desafortunadamente) crecen. Dar soporte a esto es realmente muy fácil:

<pre lang='scala'>
	class Person(var age:Int) {     // nota el modificador var
	  def isOverAge = age > 21
	 
	  def grow() = {
	    age += 1
	  }
	}
</pre>

En este código, `age` dejó de ser solamente un valor privado, es ahora una variable pública (como el ejemplo de `fillColor` en `Shape` que vimos lineas arriba). Podrás apreciar cuán extremadamente potente es esta sintaxis cuando se trata de simples clases `beans`:

<pre lang='scala'>
	class Complex(var a:Int, var b:Int)
	 
	// ...
	val number = new Complex(1, 0)
	number.b = 12
</pre>

Omitir las llaves es una sintacticamente válido para las clases que no requieran de un cuerpo. Esto es similar a cuando Java permite omitir las llaves para sentencias condicionales `if` de una sola linea. El código equivalente en Java sería más o menos así:

<pre lang='scala'>
	public class Complex {
	    private int a, b;
	 
	    public Complex(int a, int b) {
		this.a = a;
		this.b = b;
	    }
	 
	    public int getA() {
		return a;
	    }
	 
	    public void setA(int a) {
		this.a = a;
	    }
	 
	    public int getB() {
		return b;
	    }
	 
	    public void setB(int b) {
		this.b = b;
	    }
	}
	 
	// ...
	final Complex number = new Complex(1, 0);
	number.setB(12);
</pre>

Mucho más largo, mucho menos intuitivo, y menos mantenible aun. Con el ejemplo en Scala, agregar otra propiedad es tan simple como agregar otro parámetro al constructor. En Java, debemos agreagar otro atributo privado, otro getter, el setter y después finalmente el parámetro extra al constructor con el correspondiente código para inicializar el atributo. ¿Comenzás a ver cuánto código puede ahorrarte esto?

En nuestro ejemplo al principio de la página, `Circle` declara una propiedad, radio (la cual es una variable, y por lo tanto puede ser cambiada por el código que use la clase). De forma similar, `Square` tiene una propiedad, `width`. Estas son propiedades del constructor, y son una de los recursos más útiles a la hora de ahorrarnos trabajo en Scala. Es realmente increíble cuán útiles son estas cosas.

Conclusión
-----------

Realmente solo arañamos la superficie de todo lo que Scala es capaz de hacer en el campo de la orientación a objetos. La potencia de sus construcciones y la elegancia de su sintaxis nos permite mucha más productividad, especialmente cuando lidiamos con un proyecto mayor. Por otro lado, las capacidades de orientación a objetos en Scala prueban que este no es solo un lenguaje funcional interesante para académicos, sino un lenguaje poderoso, expresivo y práctico, indicado para casi cualquier aplicación del mundo real.

A continuación: más sobre métodos (incluyendo la sobreescritura) y alternativas a métodos estáticos.
