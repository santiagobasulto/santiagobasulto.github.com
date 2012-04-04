---
layout: default
title: Santiago Basulto
---


# Bienvenido #

...a mi sitio personal.

Este blog ha mutado demasiado ya.

Lo importante es que este sitio me ayuda mantener mi blog, un lugar para esparcir mis pensamientos por internet y compartirlos publicamente. Podés verlo [acá](/archive.html)

**Importante: Si querés participar en el desarrollo de la documentación oficial de Scala en español escribime. **

{% assign first_post = site.posts.first %}

<h1><small>Último Post</small></h1>
# {{ first_post.title | truncatewords: 25 }}

{{ first_post.content | truncatewords: 250 }}


[Leer más &raquo;]({{ first_post.url}})
