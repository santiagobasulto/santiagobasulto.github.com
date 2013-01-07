---
layout: post
title: "Modelo de branching para manejar proyectos grandes"
category: git
tags: programacion git branch proyecto
published: false
---

Athlete.com es ya un proyecto grande (según CLOC tenemos 50.000 líneas de python). No solo es grande por la cantidad de líneas o por la cantidad de empleados (somos 4 programadores + 1 QA), sino que tenemos ciertas responsabilidades de un proyecto grande. Invariablemente cuando hay dinero en el medio, uno debe profesionarlizar muchas cosas y dejar el "hacker" de lado.

Una de las cosas más importantes a la hora de profesionalizar un proyecto son los releases, es decir, las versiones del proyecto. Más allá de la metodología que se siga (nosotros usamos un Scrum mutante), es necesario mantener orden de las versiones de producción, de test, de integración y demás. Los objetivos generales son mantener orden entre los sprints, documentar qué se hace en cada uno, poder saber qué versiones se encuentran "deployadas" en cada servidor, entre otras cosas.

A continuación voy a describir cómo manejamos nuestros branches y nuestros releases. Vale aclarar que es un modelo conocido, no inventamos nada nuevo, simplemente tomamos un modelo estandar y lo adaptamos a nuestras necesidades.

Primero voy a comenzar describiendo qué tipo de "versiones" consideramos. A grandes rasgos podemos describir 3:
    * **Production**: El código vivo en athlete.com
    * **Staging**: Generalmente llamado integración
    * **Testing**: Mini-versiones de prueba.

Contado tipo cuento, este es el proceso:

Cuando comenzamos cada sprint definimos qué funcionalidades vamos a desarrollar para ese release. Una vez terminado el sprint armamos una versión de **staging** o "pre-producción". Esa versión contiene todos esas funcionalidades y la idea es hacer un testing fuerte para encontrar posibles bugs. Hacemos un deploy en nuestros servidores de staging y QA se encarga de tratar de romper todo. Esa versión solamente acepta bug-fixes, es decir, no agregamos ninguna funcionalidad nueva, solo se arreglan cosas. Una vez que esa versión está testeada pasa a **production**. En el medio, mientras uno va desarrollando puede crear diferentes versiones de **testing** y hacer deploys en los servidores de testing para probar, pero estas versiones son propias de los desarrolladores y no tienen mayor importancia para el proyecto.

Para mantener este esquema usamos varios branches y tenemos ciertas reglas de como manejarse. Si bien git es descentralizado, tenemos un repositorio centralizado con las versiones. Los branches mas importantes son:
    * master
    * develop
    * release-*
    * hotfix-*
    * feature-*

A grandes rasgos, este es un resumen de cada uno. Después los describo con más detalle.

`master` tiene el código de producción que está vivo en el sitio. Cualquier cosa que pase, si se hace un deploy de master en un server de producción tiene la última versión funcional del site. Es el branch más estable.

`develop` tiene lo último en lo que se está trabajando, es decir, dónde se produce el desarrollo día a día de nuevas funcionalidades. Es un branch sumamente inestable. Cualquier desarrollador puede pushear a ese branch en cualquier momento.

`release-*` son las versiones de staging. Cuando se cierra un sprint se hace crea un branch y se hace un deploy en staging. Si se encuentran bugs se arreglan sobre ese mismo branch.

`hotfix-*` se crean cuando se encuentra un bug en producción.
