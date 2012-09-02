---
layout: default
title: "Bienvenido a mi blog!"
---

Mi nombre es Santiago, y este es mi blog donde escribo sobre programación, tecnología, emprendedorismo y otras cosas <span style='text-decoration:line-through'>interesantes</span> desvariantes.

_Últimos posts:_

<ul class="post-list">
{% for post in site.posts %}
  <li><a href="{{ post.url }}">{{ post.title }}</a> <span class="date">( {{ post.date | date: "%b %Y" }} )</span></li>
{% endfor %}
</ul>
{% comment %}
{% for post in site.posts %}
{% endfor %}
{% assign first_post = site.posts.first %}


# {{ first_post.title }}


<br />

{{ first_post.content }}

[Leer más &raquo;]({{ first_post.url}})

[Todos los posts](/archivo.html)
{% endcomment %}
