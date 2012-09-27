---
layout: post
title: "HATEOAS: ¿qué y por qué?"
category: rest
tags: programacion rest api hateoas
published: false
---

Hace un tiempo di una charla en el PyDay de Córdoba sobre cómo construir [APIs REST usando Tastypie](http://www.slideshare.net/santiagobasulto1/restful-apis-con-tastypie). En uno de los slides menciono que una de las características de una API para ser considerada RESTful (que no es lo mismo que REST) debe ser HATEOAS.

### La R de REST es de "Recurso"

Primero pensemos en qué es REST. REST es un "estilo de arquitectura". La clave de REST es que es "orientado a recursos" en vez de ser "orientado a acciones" como lo es, por ejemplo, SOA. Es decir, nosotros cuando construimos algo "REST" estamos concentrándonos en los recursos. Esto es fundamental, porque esto guía la construcción de la API.

Veamos un ejemplo para entender todo esto. Supongamos que estamos construyendo una API para nuestro sitio de e-commerce. Esta es la forma de pensar en acciones (esto no sería RESTful). Primero pongo la descripción y después el método:

> "A través de nuestra API podés **comprar** un **producto** de la siguiente manera:

    POST /productos/?accion=comprar&cantidad=2

Horrible, ¿no? ¿Cuál es el problema? El problema anterior es concentrarse en las acciones en vez de concentrarse en los recursos. Primero pensamos que se **compra** (una acción) y después en el recurso **producto** sobre el cual se realiza la acción.

Para hacer que nuestra API sea RESTful debemos concentrarnos en el recurso. En este caso, me pregunto, ¿cuáles son los recursos involucrados? Esta es una aproximación.

> "Para comprar **productos** es necesario crear **transacciones**, del tipo compra indicando la cantidad."

    POST /transaccion/?producto_id=20&cantidad=2&tipo=compra

O más fácil:

    POST /compra/?producto_id=20&cantidad=2

En este caso nos concentramos en el producto. Lo interesante es que la acción apareció sola, como naturalmente. La acción en este caso es *crear* que se corresponde directamente con el verbo POST de HTTP. ¿Qué verbo HTTP se correspondía con la acción *comprar*? Ninguno, por eso tuvimos que elegir cualquiera (usamos POST, pero tranquilamente podría haber sido GET o PUT).

### ¿Qué ventajas tiene la orientación a recursos?
