---
layout: post
title: "HATEOAS: ¿qué y por qué?"
category: rest
tags: programacion rest api hateoas

---

Hace un tiempo di una charla en el PyDay de Córdoba sobre cómo construir [APIs REST usando Tastypie](http://www.slideshare.net/santiagobasulto1/restful-apis-con-tastypie). En uno de los slides menciono que una de las características de una API para ser considerada RESTful (que no es lo mismo que REST) debe ser HATEOAS.

### La R de REST es de "Recurso"

Primero pensemos en qué es REST. REST es un "estilo de arquitectura". La clave de REST es que es "orientado a recursos" en vez de ser "orientado a acciones" como lo es, por ejemplo, SOA. Es decir, nosotros cuando construimos algo "REST" estamos concentrándonos en los recursos (en las "cosas"). Esto es fundamental, porque esto guía la construcción de la API.

Veamos un ejemplo para entender todo esto. Supongamos que estamos construyendo una API para nuestro sitio de e-commerce. Esta es la forma de pensar en acciones (no sería RESTful). Primero pongo la descripción y después el método:

> "A través de nuestra API podés **comprar** un **producto** de la siguiente manera:

    POST /productos/?accion=comprar&cantidad=2

Horrible, ¿no? ¿Cuál es el problema? El problema anterior es concentrarse en las acciones en vez de concentrarse en los recursos. Primero pensamos que se **compra** (una acción) y después en el recurso **producto** sobre el cual se realiza la acción.

Para hacer que nuestra API sea RESTful debemos concentrarnos en el recurso. En este caso, me pregunto, ¿cuáles son los recursos involucrados? Esta es una aproximación.

> "Para comprar **productos** es necesario crear **transacciones**, del tipo compra indicando la cantidad."

    POST /transaccion/?producto_id=20&cantidad=2&tipo=compra

O más fácil:

    POST /compra/?producto_id=20&cantidad=2

En este caso nos concentramos en el producto. Lo interesante es que la acción apareció sola, de forma natural. La acción en este caso es *crear* que se corresponde directamente con el verbo POST de HTTP. ¿Qué verbo HTTP se correspondía con la acción *comprar*? Ninguno, por eso tuvimos que elegir cualquiera (usamos POST, pero tranquilamente podría haber sido GET o PUT).

### ¿Qué ventajas tiene la orientación a recursos?

Primero que nada hace que nuestra API sea más clara al aumentar su "trazabilidad". En el ejemplo de crear (POST) el recurso compra, lo bueno es que ese recurso va a quedar creado en la API y vamos a poder verlo en el futuro. En el primer ejemplo, ¿cómo veríamos las compras? Tal vez como un atributo dentro de productos, pero realmente no estoy seguro, dependería del creador de la API.

Por otro lado hace que nuestra API cumpla con el concepto de "round-trippable", que significa algo así como "ida y vuelta". Si yo pude crear el recurso compra, debo poder obtenerlo (y tal vez modificarlo, eliminarlo, etc).

    POST /compra/?producto_id=20&cantidad=2
    <<< Location: /compra/115/

    GET /compra/115/

### ¿Qué tiene todo esto que ver con HATEOAS?

HATEOAS (Hypermedia as the Engine of Application State) significa: "Hipermedia como el motor de estado de la aplicación". El principio detras de HATEOAS es que la API debe poder ser "recorrida" enteramente sin documentación. Es decir, dado algún punto de entrada de alto nivel (/api/, /api/schema/) deberíamos poder acceder a todos los rincones de la API sin problema. Puede entenderse como que cada recurso, que tenga a su vez algún recurso asociado, debe proveer hypermedia para acceder dichos recursos asociados.

Aunque no lo creas esto es de gran ayuda. Imaginate las representaciones del recurso Producto en los anteriores ejemplos. Para el (mal-)ejemplo de la API orientada a acciones tendríamos seguramente algo así:

    GET /productos/1/
    {
        'id': 1,
        'nombre': 'Macbook PRO',
        'stock': '10'
        'compras': ???
        ...
    }

¿Dónde aparece la información de las compras? No está siquiera en el recurso. Y de estarlo, seguramente sería un valor entero, o algo por el estilo.

Con nuestro ejemplo orientado a recursos podríamos tener:

    GET /productos/1/
    {
        'id': 1,
        'nombre': 'Macbook PRO',
        'stock': '10'
        'compras': [
            {
                'id': 1,
                'user': /api/v1/user/29/
                'cantidad': 2,
                'fecha': '12/12/12'
            },
        ]
        ...
    }

De esa manera, para cada producto sabemos qué compras tiene, o cómo acceder a las compras. Tal vez no queremos listar todas las compras en el recurso, entonces en vez de proveer esa lista podemos proveer la URI para dicho recurso:

    'compras': /api/v1/compras/?producto_id=1

### ¿Es HATEOAS realmente importante?

Sí, muy importante. Además de escribir APIs, también soy un usuario de ellas (como lo es cualquier persona que utiliza internet). Te muestro un ejemplo. Cuando accedo a mi perfil de facebook a través de su API obtengo algo similar a esto:

    GET https://graph.facebook.com/santiago.basulto
    {
       "id": "605471098",
       "name": "Santiago Basulto",
       "first_name": "Santiago",
       "last_name": "Basulto",
       "link": "https://www.facebook.com/santiago.basulto",
       "username": "santiago.basulto",
       "location": {
          "id": "116532501690915",
          "name": "La Plata, Buenos Aires"
       }
    ...
    }

"Location" en el ejemplo anterior es claramente un recurso (tiene un id asociado). ¿Cómo obtenes los datos de ese recurso? Bueno, si peleaste alguna vez con la API de facebook seguramente sabés que el ID representa un recurso dentro del "grafo" de facebook, o sea que para obtener su info tenés que hacer la siguiente llamada:

    GET https://graph.facebook.com/116532501690915 <-- El ID de Location

¿No sería más fácil incluir esa URI dentro del recurso "persona" cuando hice la request a mi información? ¿Por qué debo andar adivinando o leyendo documentación para el simple hecho de conocer más información acerca del recurso que originalmente quiero ver (/santiago.basulto)?

La idea sería que uno pueda "recorrer" o "navegar" la API sin andar adivinando o leyendo muchas cosas. Si la API devolviese lo siguiente, todo sería más fácil:

    GET https://graph.facebook.com/santiago.basulto
    {
       "id": "605471098",
       "name": "Santiago Basulto",
       "first_name": "Santiago",
       "last_name": "Basulto",
       "link": "https://www.facebook.com/santiago.basulto",
       "username": "santiago.basulto",
       "location": {
          "id": "116532501690915",
          "name": "La Plata, Buenos Aires",
		  "uri": "https://graph.facebook.com/116532501690915"
       }
    ...
    }

¿Ves el atributo **uri** dentro de **location**? Eso es HATEOAS. Proveer URIs (links, URLs, como quieras llamarlo) en los recursos asociados para que estos puedan ser consultados sin mayor esfuerzo.

### Otro ejemplo, la API de MercadoLibre

No es solamente Facebook el que muestra estas deficiencias. MercadoLibre también hace caso omiso a HATEOAS. Un ejemplo, esto devuelve una llamada al punto de entrada:

	curl -XGET "https://api.mercadolibre.com/sites/MLA"
	{
		"id" : "MLA",
		"name" : "Argentina",
		"country_id": "AR",
		"default_currency_id" : "ARS"
		...
	}

El resultado contiene dos recursos asociados (**country** y **default\_currency**). Nos damos cuenta porque son IDs. ¿Ahora te pregunto, cómo harías para obtener la moneda (**default\_currency**)? Esta es la llamada que deberías hacer:

	curl -XGET "https://api.mercadolibre.com/currencies/ARS"
	{
		"id": "ARS",
		"description": "Peso argentino",
		"symbol": "$",
		"decimal_places": 2,
	}

Eso no es explícito, está implícito en la API y debe ser usada la documentación para conocerlo.

Debo decir en favor de MercadoLibre que tienen una interfaz web para explorar la API muy buena y que cuenta con una especie de "HATEOAS" implícito. Además, la API es bastante intuitiva. Pero, no es HATEOAS.


### HATEOAS en Tastypie, brevemente

En algún momento debo escribir un post entero de Tastypie, pero por ahora te cuento que Tastypie por defecto soporta HATEOAS. Cada vez que relacionas recursos dentro de tu API esos recursos conocen inteligentemente como proveer las URIs para relacionarse, lo cual es muy útil.


### Conclusión final

REST es un estilo de arquitectura orientado a la simpleza. ¿Por qué utilizamos REST y no SOAP? Por la simplicidad de uso. SOAP es un protocolo excelente, muy robusto y extensible. Pero no es simple. Lamentablemente no tenemos tiempo para leer miles de lineas de WSDLs para recién poder comenzar a interactuar con la API. Eso es lo que nos provee REST. Tomás una URI y en 5 segundos usando `curl` o el mismo browser podés comenzar a recorrer la API y a interactuar con ella. No hace falta leer cientos de páginas de manuales (pienso en la API de AFIP automaticamente) para crear un post en Facebook, o ver un artículo en MercadoLibre.

Entonces, si REST está orientado a la simplicidad, ¿por qué no tenemos como objetivo tratar de hacerlo lo más simple posible? Sinceramente no lo se. Tanto Facebook como MercadoLibre son empresas enormes, con desarrolladores brillantes, así que me queda solamente pensar que es una cuestión "cultural". Es nuestro deber como desarrolladores fomentar el buen uso de REST a través de HATEOAS. Espero que así sea.
