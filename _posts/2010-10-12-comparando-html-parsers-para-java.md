---
layout: post
title: Comparando HTML parsers para Java
category: java
tags: java html parser regex
---

Hace un tiempo comencé a construir un WebCrawler (que proximamente tendrá su entrada en este blog) como proyecto personal. Una vez definida la arquitectura, y empezando a refinar un poco el código me encontré con una clase que podría presentar problemas. Se llama URLFinder. Como podrán imaginar sirve para obtener URLs a partir de un documento HTML.

Cuando empecé a construir el Crawler usé regex, ya que era la forma más simple de hacer el testeo (de arquitectura). Una vez hecho eso necesitaba dar un paso más en cuanto a performance. Regex, no es la mejor opción para parsear un Documento HTML, y está poco recomendado por varias cuestiones. Entre ellas podemos encontrar algunas muy fuertes de performance, aunque también podemos citar en cuanto a escalabilidad, y facilidad de uso.

Es por eso que existen varios Parsers de HTML. A continuación los listo con una breve reseña de cada uno:

###El parser de Swing
[Link](http://java.sun.com/products/jfc/tsc/articles/bookmarks/)

El que finalmente elegí. Resultó ser el más rápido (vean los tiempos a continuación) y más simple de usar. Toma los streams directamente y hace un uso muy eficiente de todos los recursos. Como todas las librerías oficiales está muy bien documentado.

###HTMLParser:
[Link](http://htmlparser.sourceforge.net/)

He leído muchos buenos comentarios. No me pareció simple, sí bueno en cuanto a performance. La documentación deja mucho que desear. De todas maneras vale aclarar que no la usé “correctamente” (usé solamente los componentes básicos). Tal vez puede ser optimizado un poco. Si es así actualizaré el post a su debido tiempo.

###JSoup
[Link](http://jsoup.org/)

Excelente librería. Acepta todo tipo de documentos. No tiene muchos problemas con HTMLs mal formateados. Muy buena documentación. PARSEA JQUERY Y DEJA UTILIZAR SELECTORES! Pero no es tan buena a nivel performance

##TagSoup
[Link](http://home.ccil.org/~cowan/XML/tagsoup/)

No la utilicé mucho. No es muy buena a nivel performance. Aunque si recupera bien los documentos mal formateados.

Como han podido observar hay dos grandes candidatos HTMLEditorKit de Swing y JSoup. Me tiré por la primera por su gran performance y por la extensibilidad (se pueden declarar DTD personalizados). Ambas se manejan en base a Documents. Ahora sí, les comento los tiempos.

La prueba la realicé sobre un Core 2 Duo E8600. Con 1 Gb de RAM y 1Mbit de conexión. Utilicé un solo hilo (para esta prueba, el Crawler es multihilo).
En extraer todos los links de la siguiente URL (la elegí por la gran cantidad de links) “http://news.google.com.ar/nwshp?hl=es&tab=wn” tardaron (en promedio 10 pruebas realizadas):

* **HTMLEditorKit:** 2182 milisegundos
* **HTMLParser:** 2882 milisegundos
* **JSoup:** 3988 milisegundos
* **TagSoup:** 2988 milisegundos

#####Eso es todo. Recomendaciones entonces: HTMLEditorKit y JSoup.
