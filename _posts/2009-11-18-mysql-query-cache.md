---
layout: post
title: MySQL query cache
category: mysql
tags: mysql query cache database optimization
---

Hace un tiempo enfrentando un par de problemas de performance en uno de los sitios que administro me topé con algo raro. Tenía que mejorar el acceso algunas partes del sitio y ya estaba hecho todo lo “básico” en cuanto a tunning y las respuestas no parecían llegar. Obviamente como cualquier DBA haría, me concentré en la Cache. Al analizarla vi que todo parecía normal. El hit-rate estaba por encima de lo esperado y todavía le quedaba espacio libre para seguir cacheando. Cómo optimizar más entonces?
Bien, buscando un poco econtré el siguiente artículo del Sr. Robin Schumascher: http://dev.mysql.com/tech-resources/articles/mysql-query-cache.html
Si alguien no conoce mucho de la cache de consultas (query cache) de MySQL se lo recomiendo. Dice algunas cosas básicas y explica distintas estrategias. No quiero pasar a explicar qué es la “query cache” de MySQL, ya que en artículo de Robin está muy bien explicado y en el manual de MySQL también. Simplemente voy a dar unos conceptos básicos para poder seguir con el artículo.

La “cache de consultas” (query cache) de MySQL mantiene una copia de los resultados arrojados por consultas ejecutadas en la base de datos. Por ejemplo, si realizamos una consulta a una base de datos de un foro, pidiendole usuarios (SELECT * FROM users) una vez devuelto el resultado se almacena en memoria. La proxima vez que ejecutemos la misma consulta, en vez de preguntarle a la BD y ejecutar las operaciones respectivas, nos arrojará el resultado cacheado.
Bien, esto no siempre es así. Existen algunas limitaciones, las cuales Robin comenta, y es muy importante tenerlas en cuenta.
Por ejemplo, si cambiamos las mayúsculas de la consulta anterior y consultamos lo siguiente: select * from users. esa consulta NO es igual a la anterior, por lo tanto no va a resolverse a través de la cache.
Otra limitación importante es que, si algún dato del conjunto cacheado se actualiza, la cache se invalida totalmente. Osea que si ejecutamos cualquier sentencia DML (por ejemplo un UPDATE o INSERT), la cache de usuarios se borra y la próxima vez que ejecutemos un SELECT el motor no va a poder utilizar la cache. De ahora en más me voy a concentrar en dicha limitación.
Cómo podemos entonces evitar que cada vez que se ejecute una sentencia DML se nos borre la cache? Bueno, la única forma es NO ejecutando dicha sentencia DML. Pero qué sucede si tenemos que ejecutar dicha consulta sí o sí? Bueno, entonces vamos a tener que tenerlo en cuenta a la hora del diseño. Para clarificar todo un poco más voy a plantear un ejemplo práctico.
Supongamos que estamos creando una BD de un foro. Tenemos varias tablas, y entre ellas tenemos la tabla “users”. Es probable que la tabla users contenga datos similares a estos: user_id,username, password, avatar, firma, etc. Si queremos que nuestro foro tenga un buen control y deseamos obtener datos más precisos sobre los usuarios podemos tener un campo con el numero de IP con la que se conecto dicho usuario por última vez. Aclaro que es un ejemplo muy simplificado para poder ilustrar el tema. Entonces, la tabla nos quedaría algo así:

——————
| USERS |
| #* user_id |
| * username |
| * password |
| * avatar |
| * firma |
| * ultima_IP |
——————
Cada vez que un usuario se loguea se actualiza el campo “ultima_IP” con la dirección actual. Imaginando el comportamiento básico de un foro, podemos conjeturar que cada vez que se consulta un Post, se pide a la Base de Datos información del usuario, como la firma, la imagen “avatar”, etc. Lo mas coherente sería que se cacheen estos datos, con el objetivo de no sobrecargar a la BD con información relativamente estática.

Supongamos ahora que nuestro foro funciona de la siguiente manera. Cuando se pide leer un post se obtiene una lista con TODOS los usuarios del foro. Una vez obtenido el registro completo buscamos los usuarios que realizaron entradas en dicho post dentro de la aplicación mediante un bucle. Esto no es lo recomendado, pero nuevamente aclaro, está simplificado para ilustrar el concepto. Recapitulando, cada vez que queremos ver un post realizamos la siguiente consulta: SELECT * FROM users. Acto seguido mediante un bucle obtenemos los usuarios que nos interesan y mostramos la información necesaria.
Supuestamente, cada vez que se accede a un Post, la información va a ser obtenida a través de la cache ya que siempre realizamos la misma consulta, cualquiera sea el Post. Qué sucede cuando un usuario se loguea? Como dije anteriormente, cada vez que se loguea el usuario se actualiza su campo “ultima_IP” con el valor correspondiente mediante una consulta similar a esta: “UPDATE users SET ultima_IP = X WHERE user_id = Y”. Dicha consulta va a invalidar la cache que estabámos utilizando antes y cuando se quiera acceder nuevamente a un Post la consulta no va a poder ser satisfecha por dicha cache, sino que va a tener que resolverse mediante las estrategias comunes. Pareciera que no podemos realizar ninguna mejora a este comportamiento. Por un lado, es un requerimiento necesario mostrar la información de usuarios en los Posts, y por otro, por cuestiones de seguridad debemos tener la IP de todos los usuarios. Qué soluciones existen para mejorar entonces?
Deben existir muchas, a mi se me ocurrió la siguiente:
Dividimos la tabla users en dos. Por un lado almacenamos la información relativamente “estática” como el nombre de usuario, el avatar, la firma, etc. Digo estática, porque esta información cambia con menos frecuencia que “ultima_ip” que cambia cada vez que el usuario se loguea. Siguiendo, creamos otra tabla conteniendo la información dinámica, por ejemplo la tabla “users_ip_addr” que contendrá simplemente dos campos, el id de usuario (user_id), que a la vez será la PK y la dirección IP correspondiente. Tendríamos entonces el siguiente esquema:
—————— ———————-
| USERS | | USERS_IP_ADDR |
| #* user_id | | #* user_id |
| * username | ——— | * ultima_IP |
| * password | ————————-
| * avatar |
| * firma |
——————
Ahora, cada vez que un usuario se loguea, la consulta será algo similar a: “UPDATE users_ip_addr SET ultima_IP = X WHERE user_id = Y”. Vemos que la tabla USERS no entró en juego, por lo tanto la cache no será invalidada. Bajo este esquema y dado el funcionamiento explicado anteriormente, podemos decir que las consultas para obtener usuarios podrán ser satisfechas mediante la cache un número mayor de veces.
Es importante remarcar que esto es una solución relativamente “casera” y que no se aplica en todos los casos. Está basada en la Query Cache de MySQL que cachea el conjunto de datos, si quisiéramos usarla en otro motor que no lo hiciera no tendría sentido. Simplemente trato de ilustrar las variantes que podemos encontrar a la hora de realizar la optimización de un sitio, más allá del tunning “básico” de la BD.
Otra cosa importante es, obviamente, tener consultas de buena calidad. No es una noticia y en el comienzo del articulo de Robin también está mencionado.
