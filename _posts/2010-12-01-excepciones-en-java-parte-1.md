---
layout: post
title: Excepciones en Java – Parte 1
category: java
tags: java excepciones tutorial
---

Generalmente suelo tener, una mirada muy pesimista sobre el género humano. Todas las desgracias a las que nos enfrentamos son, en total o parcial medida, responsabilidad nuestra. Lo mismo sucede con nuestros programas. Si un programa falla, la probabilidad de que sea por un factor humano es la más alta. Obviamente que puede no ser responsabilidad nuestra. Pudimos haber escrito un código perfecto, sin ningún error. Simplemente el usuario se sentó y accedió una letra en un campo donde debería haber accedido un número. Sin embargo eso es un error humano. Y para ser aún más pesimista, es un error nuestro.

Este post está pensado con dos grandes objetivos. Primero introducir un poco el manejo de excepciones en el lenguaje de programación Java y por otro lado, contar un poco de mi experiencia personal. Antes de arrancar con las cuestiones técnicas, quiero explayar un concepto que siempre me ha servido mucho a la hora de escribir mis programas:

_“Siempre pensá que tus usuarios son idiotas con el cerebro de un niño de 5 años, y si es posible, que nunca se han sentado frente a una PC”_

Ahora sí, qué son las excepciones y cómo se manejan en Java.

##Concepto

No voy a ahondar mucho en esto. La idea es tener un enfoque práctico. Las Excepciones, a grandes rasgos, son errores que pueden suceder en nuestro programa. Pueden ser generado debido a errores en el código (llamar un método a un objeto null), de recursos del SO (quedarse sin memoria o red), de recursos del programa (no poder acceder a un archivo), etc. Existen definiciones más precisas, como una que aparece en Wikipedia:

_“Excepcion es la ocurrencia de una condición especial que altera el flujo normal de un programa en ejecución”_

O sea, el programa está leyendo datos de usuarios y en el lugar donde debía leer la “edad”, leyó el caracter “a”. En ese caso hay dos opciones posibles. Derivará en un error del programa, y la ejecución de este se verá repentinamente finalizada (seguramente perdiendo todos los datos ingresados hasta el momento, y llevando consecuentemente a que el usuario no vuelva a usar nunca más nuestro software) o a lo que se llama “manejo de la excepción”. Esto es, manejar esa “condición especial” de tal forma que el programa ni el usuario se vean afectados.

##Excepciones en Java

En Java, un objeto de tipo “excepción” es siempre una subclase que deriva de Throwable. Existe una gran jerarquía de excepciones, y nosotros podemos agregar excepciones propias. A continuación se muestra una imagen con la jerarquía (incompleta) de clases de la librería estándar de Java.

![Jerarquía de Excepciones en Java](/resources/img/exceptions-throwable.gif)

Como mencioné anteriormente, todas derivan de Throwable. En el nivel siguiente, existen solamente dos clases, estas son: [Error](http://download.oracle.com/javase/1.5.0/docs/api/java/lang/Error.html) y [Exception](http://download.oracle.com/javase/1.5.0/docs/api/java/lang/Exception.html). La clase Error, y todas sus subclases describen errores internos y agotamiento de recursos dentro del sistema de ejecución de Java. O sea, todos los errores relacionados con la JVM y el Sistema Operativo anfitrión. No es recomendable lanzar  este tipo de excepciones. Generalmente, si lidiamos con este tipo de excepciones, poco nos queda por hacer. Ha ocurrido un error ajeno a nuestro programa y (probablemente) a nuestros usuarios. La buena noticia es que estas situaciones son poco frecuentes.

Yendo hacia la otra rama, encontramos la clase Exception. La más útil y en la que concentraremos nuestros esfuerzos. A su vez, podemos decir que de Exception descienden dos ramas, a saber: la clase [RuntimeException](http://download.oracle.com/javase/1.5.0/docs/api/java/lang/RuntimeException.html) y todas las demás. En este caso, y a modo de ejemplo yo marqué la clase [IOException](http://download.oracle.com/javase/1.5.0/docs/api/java/io/IOException.html), pero existen bastantes clases más. En la siguiente sección trataremos más a fondo esos temas.

##Excepciones Comprobadas vs Excepciones no Comprobadas

Como mencioné anteriormente, de Exception extienden dos ramas. En una, vemos a la clase RuntimeException (en color celeste). En la otra, se ve (solamente) la clase IOException (color rojo). En realidad, junto a IOException existen otras clases, pero no las muestro por motivos de claridad. Cuál es la diferencia entre ellas? Ese es el motivo de esta sección.

Las excepciones derivadas de RuntimeException son, generalmente, errores nuestros como programadores. Estas excepciones se producen cuando se producen llamadas a métodos sobre objetos null, cuando se trata de acceder a un array más allá de sus límites, y cosas similares. Podríamos decir que son cosas que podríamos haber evitado codificando con cuidado. Subclases de RuntimeException, por ejemplo, son: IndexOutOfBoundsException, NullPointerException, y más. RuntimeException, y todas sus clases derivadas son **Excepciones no Comprobadas**.

Todas las otras clases que extiendan de Exception, como por ejemplo, IOException, SQLException son:  **Excepciones Comprobadas**.

Esto qué quiere decir: Todas las Excepciones Comprobadas deben ser manejadas, especificamente, por nostoros. O sea, el compilador se asegura de que nos dimos cuenta que, debido a “esa” instrucción en particular, algo puede salir mal y una Excepción va a ser lanzada. En cambio, para las Excepciones No Comprobadas, el compilador no nos exige ningún esfuerzo extra, solamente pueden llegar a ocurrir, y deberíamos ser capaces de evitarlas.

Esta denominación es bastante útil. Imaginate el tormento que sería tener que manejar una excepción cada vez que haces una llamada a un método, porque el objeto que recibe esa llamada podría ser null.

##Manejo de Excepciones (Exception Handling)

Pocas lineas atrás me referí a las Excepciones Comprobadas, y dije que debían ser siempre manejadas. Ahora voy a ahondar en esto, en particular especificar a qué me refiero con manejar esas excepciones.
Existen, a grandes rasgos, dos maneras de manejar excepciones no comprobadas. Una de ellas es declarar específicamente que un método puede lanzar una excepción. Por ejemplo, echemos un vistazo al método close() de la clase FileInputStream. El método comienza con la siguiente definición:

{% highlight java %}
public void close() throws IOException
{% endhighlight %}

Después de todos los modificadores que ya conocemos (el modificador de visibilidad public, el de tipo void, etc) se encuentra la palabra reservada throws, y a continuación el nombre de una clase, en particular IOException. Lo que quiere decir esto, es que la el método close, debido a alguna acción que realice en su interior, se puede topar con una excepción, por lo tanto, lo avisa. Si se produjera este error, el compilador alteraría el flujo normal del método close, para encontrar un manejador de excepción adecuado. Empezará a recorrer linealmente, y en dirección superior al grafo de ejecución el método que lo llamó, y a su vez el (o los) que accedieron a este último, y así siguiendo. Esto hasta que encuentre un método que maneje correctamente la excepción, si no terminará el programa de forma abrupta. Si en nuestro código llamáramos al método close() de dicha clase, podríamos también agregar la declaración de lanzamiento de excepción, algo similar a esto:

{% highlight java %}
/* Un método nuestro que lee de un archivo */
public void leerUnArchivo(String nombreDelArchivo) throws IOException
{% endhighlight %}

De esa forma, el compilador no se quejaría y nuestro programa se compilaría sin ningún tipo de problema.

Ahora bien, como dije anteriormente, si surge una excepción, esta empezará a subir niveles de llamadas a métodos hasta que alguien la maneje correctamente. Con lo expuesto anteriormente, lo único que hacemos es tirarle la responsabilidad a otro, despreocupándonos del correcto manejo del error. Yendo a la semántica del problema, esa excepción seguramente se generó porque el nombre del archivo que nos indicaron no era correcto, o porque no teníamos suficientes permisos, o algo por el estilo. Quiere decir que en algún punto, ese error debe ser comunicado a quien tiene la responsabilidad de indicar el nombre del arhivo. Vamos a suponer que existe una clase que se comunica con el usuario y le pide que ingrese el nombre de un archivo. Esa clase (podría ser una ventana de GUI) después instancia el método leerUnArchivo() para ejecutar los pasos deseados, por ejemplo, contar la cantidad de lineas del archivo. Qué sucedería en ese momento? Vamos por un ejemplo:

{% highlight java %}
/* Un método de nuestra clase Ventana */
public int contarCantidadDeLineasDelArchivo()
{% endhighlight %}

Dentro de ese método, tendríamos de alguna manera que pedir al usuario que ingrese el nombre del archivo, y con ese nombre ejecutar el método leerUnArchivo(), algo así:

{% highlight java %}
public int contarCantidadDeLineasDelArchivo(){
    //obtenemos el nombre del archivo en una variable
     String nombreArchivo = ...
     //llamamos al método leerUnArchivo con el parámetro leído anteriormente
     leerUnArchivo(nombreArchivo);
}
{% endhighlight %}

Qué sucede si el usuario ingresa un nombre equivocado? No sería correcto que el programa finalizase de forma poco agradable, como lo realiza en Java. Lo ideal sería comunicarle que la opción que ingresó es erronea y ejecutar otra acción consecuentemente (bien puede ser pedir nuevamente el nombre, o finalizar el programa, pero de forma fortuita).

Para hacer esto disponemos del segundo método de manejo de excepciones, la cláusula try – catch. Con ella podemos especificar que estamos tratando de ejecutar sentencias que pueden llevar a un error, a saber, una excepción controlada, y por lo tanto debemos especificar una forma de manejar, agraciadamente, ese error. Un ejemplo:

{% highlight java %}
public int contarCantidadDeLineasDelArchivo(){
     //obtenemos el nombre del archivo en una variable
     String nombreArchivo = ...
     try{   // Trato de ...
          //llamamos al método leerUnArchivo con el parámetro leído anteriormente
     leerUnArchivo(nombreArchivo);
     }catch(IOException e){  // Ocurrió un error y capturé (catch) la excepción en un objeto, en este caso "e"
          // Informo del error y procedo
     }
}
{% endhighlight %}

De esta forma, si se produjera la IOException por un mal nombre de archivo, la ejecución se cortaría y se saltaría a la primer línea del bloque catch, permitiéndonos ejecutar otro código alternativo. Podríamos por ejemplo, loguear el error e informárselo al usuario, o pedirle un nuevo nombre, etc.

El procedimiento descripto anteriormente es bastante directo e intuitivo. El sistema trata de hacer lo que está dentro del bloque try y si no puede irá al catch. Es interesante notar que a catch le pasamos como parámetro un nombre de una clase con un nombre de parámetro. Quiere decir que, de producirse el error, dentro del objeto ese (en este caso “e”) tendremos la excepción (de tipo IOException) que causó el problema. Podemos inspeccionarla libremente para saber, por ejemplo, si fue producida por un nombre equivocado, una falta de permisos, o algo más. Es obvio que el tipo de clase de excepción proporcionado en el bloque catch tiene que estar en concordancia con la excepción tirada por el código del bloque try. Esto es, si nuestro código pude lanzar una excepción del tipo IOException, no deberíamos capturar una excepción NullPointerException, ya que el método que puede causar el problema definió explicitamente que la excepción era del tipo IOException. Si podemos, sin embargo, optar por una superclase de esta. De hecho, si recuerdan parrafos arriba mencioné que la clase IOException extiende de Exception, lo que quiere decir que “es una” Exception (por la regla “es un” de las jerarquías de clases).

Eso es todo por hoy, en el próximo post examinaremos algunos de los siguientes temas:

* Lanzar excepciones.
* Creación de nuestras propias clases de Excepciones
* La cláusula finally
* Captura de múltiples excepciones
* Más concejos…

Adios!
