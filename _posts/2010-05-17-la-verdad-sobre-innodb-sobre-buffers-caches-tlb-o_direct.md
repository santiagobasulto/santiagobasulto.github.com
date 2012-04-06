---
layout: post
title: La verdad sobre InnoDB (sobre buffers, caches, tlb y O_DIRECT)
category: mysql
tags: mysql innodb buffer o_direct odirect tlb
---

Hay muchos comentarios al rededor de la web que rezan cómo resolver los problemas que enfrenta MySQL sobre ambientes Linux en base a las caches.

Para los que no están muy interiorizados, InnoDB maneja un buffer_pool que funciona a modo de cache de datos, índices y metadata. Es importante que el tamaño de este buffer sea lo más grande posible para poder almacenar la mayor cantidad de información posible en memoria y no tener que leer el disco (la velocidad de acceso a la RAM es varios órdenes de magnitud mayor). El problema es que MySQL, como tantos otros motores de bases de datos, sigue siendo una aplicación que corre sobre un Sistema Operativo. El SO, tiene propias políticas y métodos de lograr una buena respuesta al usuario. Una de ellas es lograr multiprocesamiento y, sobretodo, que eso sea visible para el usuario. Uno de los recursos que tiene el SO para lograr eso es cachear datos de las aplicaciones a disco. Aquí surge un problema importante. Si MySQL, en particular InnoDB está cacheando los datos del disco, ¿para qué va a cachear los datos también el SO? Otra cuestión importante, el SO cachea los datos y a su vez los “pagina”. El concepto de paginación (swap) es que envía los datos al disco para ahorrar memoria. Osea, en resumidas cuentas, estaría duplicando los datos cacheados, y encima, enviandolos a disco. Esto es inaceptable desde cualquier punto de vista.

Existen muchas soluciones a esto, muy variadas por cierto. Lo ideal es hacer distintas pruebas y fijarse qué funciona mejor para nuestro SO. En particular, sobre Linux (Debian, para ser más preciso) podemos ejecutar el comando “top” que muestra los datos de nuestra Swap.

Entre las posibles se encuentran:

* Hacer que el metodo de flush sea directo. Se consigue seteando la variable “innodb_flush_method” con el método (O_DIRECT). innodb_flush_method=O_DIRECT
* Usar Huge Pages. Otro concepto bastante atado a los SOs. Se puede encontrar vasta información en la web. En particular recomiendo el siguiente post:
[http://www.cyberciti.biz/tips/linux-hugetlbfs-and-mysql-performance.html](http://www.cyberciti.biz/tips/linux-hugetlbfs-and-mysql-performance.html)
* Utilizar swappiness = 0. Otra cuestión bastante atada al SO. Es un tanto peligroso porque el SO puede matar el motor cuando se quede sin memoria. Es otro tema importante a estudiar.

Como recomendaciones finales. Prueben! No hay nada mejor que hacer un propio benchmark. Pueden hacerlo con tablas BLACKHOLE
[http://dev.mysql.com/doc/refman/5.0/en/blackhole-storage-engine.html](http://dev.mysql.com/doc/refman/5.0/en/blackhole-storage-engine.html)
