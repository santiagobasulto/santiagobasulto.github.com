---
layout: default
title: Santiago Basulto
---


# Bienvenido #

...a mi sitio personal.

Este blog ha mutado demasiado ya.

Lo importante es que este sitio me ayuda a mantener un lugar para esparcir mis pensamientos por internet y compartirlos publicamente. Podés ver más [acá](/archive.html)

**Importante: Soy encargado de la documentación en español del lenguaje de programación Scala, si estás interesado en participar podés escribir. **

{% assign first_post = site.posts.first %}

# Último Post: {{ first_post.title | truncatewords: 25 }} #

{{ first_post.content | truncatewords: 250 }}


[Leer más &raquo;]({{ first_post.url}})
