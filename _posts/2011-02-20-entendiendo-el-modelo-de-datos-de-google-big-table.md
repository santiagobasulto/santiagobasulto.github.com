---
layout: post
title: Entendiendo el Modelo de Datos de Google Big Table
category: data
tags: google big table big-table datamodel distributed schemaless
---

Google Big Table es un motor de base de datos distribuído, construido por la empresa Google que ha pisado fuerte en el sector desde la publicación del paper original. Este artículo no intenta ser una introducción a Big Table, sino una forma de entender el modelo de datos (datamodel) que plantea. Es por eso que no voy a entrar en detalles como Arquitectura, Ventajas, Desventajas, FileSystem, etc. Simplemente debo mencionar, que a la hora de construir este motor, la gente de Google se puso un objetivo en claro: construir un sistema distribuido que acepte datos semi-estructurados para una gran variedad de aplicaciones (y por lo tanto dominios). A qué se refiere esto: necesitamos un motor, que podamos distribuir geográficamente, y que nos sirva para todos los proyectos que emprendamos (el buscador, google maps, blogger, orkut, buzz, etc). Como verán, es una tarea muy difícil, ya que los requerimientos de distintos proyectos cambian mucho (los datos almacenados para el buscador son muy distintos a los de Google Maps). También entra en juego la escalabilidad y el presupuesto.

En la sección 2 del paper de BigTable, aparece una descripción (no muy detallada) del modelo de datos del motor. Empieza haciendo una descripción muy específica y rica:

> BigTable es un mapa multidimensional ordenado, disperso, distribuido y persistente.

Cuántas definiciones importantes en una sola linea. Voy a arrancar descomponiendo la oración.

Primero que nada arranca con la “base” de la estructura de datos que utiliza: el “Mapa”, que los hispanohablantes también llamamos “Vector asociativo”. La idea de esta estructura de datos es simple. Se tiene un conjunto de tuplas, indexadas por una clave. Algo muy conocido como “clave,valor”. En PHP es un array normal:

{% highlight php %}
$map = array( "key" => "value" );
{% endhighlight %}

en Python se llaman “Diccionarios”:

{% highlight python %}
map = { 'key' : 'value' }
{% endhighlight %}

y en javascript son “Objetos” (Literal Object, para ser preciso):

{% highlight javascript %}
var map = { 'key' : 'value' }
{% endhighlight %}

En fin, son estructuras de datos por demás conocidas, que han estado en el rubro desde la invención de la memoria. El problema, es que no se estudian lo suficientemente bien, y empiezan los problemas cuando se agregan “dimensiones”. Es un concepto básico, pero que cuesta entenderlo. Recordemos de Algebra Lineal, que los vectores pueden tener múltiples dimensiones, no solamente 1, 2 o 3. El problema es que nuestra mente no puede hacerse la idea de más de 3 dimensiones. Veamos:

1 dimension, un vector R en 1, puede ser un “array” computacional básico:

{% highlight javascript %}
{"f1" : "naranja", "f2" : "pera", "f3" : "manzana"}
{% endhighlight %}

En 2 dimensiones, podemos pensar en una matríz, o una simple tabla de una hoja de cálculo. Nuestro vector quedaría así:

{% highlight javascript %}
{
    'colores_calidos':{
        'rojo',
        'amarillo',
        'naranja'
    } ,
    'colores_frios':{
        'azul',
        'verde'
    }
}
{% endhighlight %}

En 3 dimensiones, podemos (con un poco más de esfuerzo) pensar en un cubo. Es una representación un poco más complicada, pero realizable igual. Ya más dimensiones (algo totalmente posible en la computación actual) es muy difícil de entender, y representar. Es en este momento donde nos interesa hacer una apreciación especial. BigTable es un “mapa multidimensional”. O sea, vamos a estar tratando con las representaciones anteriores.

Con respecto a las otras definiciones tenemos:

**Ordenado**: Simplemente las “filas” de nuestro mapa o vector van a estar ordenadas por un cierto criterio (lexicográficamente por la clave).

**Distribuido**: Si pensamos en un mapa con 100 “tuplas”, podríamos tener la mitad de un mapa en un servidor, y la otra mitad en otro.

**Disperso**: Se puede entender como “poco denso” también, puede darnos la sensación de tener pedazos de distintos mapas juntos.

**Persistente**: Simple, los datos se persisten a una unidad física (discos). O sea, se corta la luz y no perdemos nada.

Después de esa definición, el paper da la nomenclatura básica para referirse al modelo de datos:

>El mapa es indexado por una clave de fila, clave de columna, y un timestamp (no me parece bueno traducirlo, es algo así como una “marca temporal”). Cada valor en el mapa es un conjunto de bytes no interpretados (pensemos en strings).

Para entender mejor esto utilizaremos el ejemplo del paper. Cómo mencioné anteriormente, el motor fue pensado para una amplia variedad de utilizaciones; una en particular era el motor de búsqueda. El motor debe indexar todas los sitios webs y guardar contenido referido a ellos, como por ejemplo la URL, el contenido en sí (el código HTML), el idioma, el país, etc. Podemos pensar entonces, que se decide crear una “tabla” para este propósito. La tabla es llamada “Webtable”.

La tabla tendrá varias “tuplas” que serán conformadas por cada URL encontrada. Es decir, que la URL va a ser la “clave de fila”. Tendremos varias claves, por ejemplo com.google.www, com.cnn.www (están al revés por motivos de eficiencia de índices y otras consideraciones, no es importante de todas formas). Por cada fila tendremos algún contenido. En BigTable se llaman “familias de columnas”. Yendo al ejemplo, nuestra tabla (un mapa, recuerden) quedaría así:

{% highlight javascript %}
"com.cnn.www" : { //la clave de fila
// Familias de Columnas
}
{% endhighlight %}

Ahora bien. El mapa es multidimensional. Por lo tanto, cada familia de columnas puede tener varios valores, cada uno indexado a su vez por una clave propia. En nuestro ejemplo, guardamos la home page de CNN. Veamos qué datos son interesantes guardar. Algo interesante sería guardar todos los links que contiene esa web. O sea, el codigo HTML <a href=’…’>link</a> de todos los links presentes. Nuestro mapa quedaría algo así:

{% highlight javascript %}
"com.cnn.www" : {
    'links': {
        "<a href="http://itunes.apple.com/us/app/cnn-app-for-ipad/id407824176?mt=8">", "</a><a id="nav-world" title="World News International Headlines Stories and Video from CNN.com" href="/WORLD/">World</a>",
    }
}
{% endhighlight %}

Como dije antes, el mapa es multidimensional, y cada familia de columnas puede tener muchos valores. Los cuales también pueden estar indexados. Pensemos en el siguiente ejemplo. ¿Cómo conseguimos todos los links dentro de esa URL (el home de CNN) que NO apunten a CNN.com? O sea, todos los links “externos”. Bueno, tendríamos que conseguir el mapa con los links, e ir recorriendo cada elemento, utilizando regexp ir cortándolos y demás. Parece un trabajo complicado. Pero retrocedamos un segundo. Nuevamente repito. BigTable es un Mapa Multidimensional! Entonces podemos utilizar más mapas! Podríamos por ejemplo guardar los links, con una clave especial, por ejemplo, el sitio al que apuntan. Quedaría algo así:

{% highlight javascript %}
"com.cnn.www" : {
    'links': {
            "apple.com" : "<a href="http://itunes.apple.com/us/app/cnn-app-for-ipad/id407824176?mt=8">itunes</a>",
            "cnn.com" : "<a id="nav-world" title="World News International Headlines Stories and Video from CNN.com" href="/WORLD/">World</a>",
    }
}
{% endhighlight %}

Eso está mejor. Ahora es mucho más facil acceder a nuestro contenido. Incluyamos otra familia de columnas más: el contenido del sito. Esto es, el código HTML de cada URL indexada. Para CNN tendríamos:

{% highlight javascript %}
"com.cnn.www" : {
    "contenido":"<html><head> ..."
}
{% endhighlight %}

Acá veremos una variante más del modelo. Previamente, utilizamos la el sitio base del link como clave para guardar todo el contenido (apple.com apuntaba al sitio de itunes). Ahora, BigTable nos presenta una variante más, que no es introducida por nosotros. Dentro de cada celda (el contenido, por ejemplo) van a existir varias “versiones” de lo que guardamos, cada una indexada por un timestamp. Esto es, una marca temporal. Veamos cómo quedaría:

{% highlight javascript %}
"com.cnn.www" : {
    "contenido":{
        "1298222849":"HBase, una proyecto OpenSource que provee un motor similar a BigTable sobre Hadoop
{% endhighlight %}
