---
layout: default
title: "Bienvenido a mi blog!"
---

{% assign first_post = site.posts.first %}

{% comment %}
# {{ first_post.title }}
{% endcomment %}

<br />

{{ first_post.content }}

[Leer más &raquo;]({{ first_post.url}})

[Todos los posts](/archive.html)
