---
layout: default
title: "Bienvenido a mi blog!"
---

Mi nombre es Santiago, y este es mi blog donde escribo sobre programación, tecnología, emprendedorismo y otras cosas <span style='text-decoration:line-through'>interesantes</span> desvariantes.

Algunos posts destacados:

_Entrevistas:_

* [Angel "Java" Lopez](/entrevistas/2012/08/12/entrevista-angel-java-lopez.html)


_Posts sobre Scala:_

* [Scala: Orientación a expresiones y pattern matching](/scala/2012/02/12/scala-orientacion-a-expresiones-y-pattern-matching.html)
* [Scala para refugiados de Java - 3 partes](/scala/2011/11/20/scala-para-refugiados-de-java-resumen.html)

[Todos los posts](/archivo.html)
{% comment %}

<ul class="post-list">
{% for post in site.posts %}
  <li><a href="{{ post.url }}">{{ post.title }}</a> <span class="date">( {{ post.date | date: "%b %Y" }} )</span></li>
{% endfor %}
</ul>

{% for post in site.posts %}
{% endfor %}
{% assign first_post = site.posts.first %}


# {{ first_post.title }}


<br />

{{ first_post.content }}

[Leer más &raquo;]({{ first_post.url}})

[Todos los posts](/archivo.html)
{% endcomment %}
