---
layout: default
title: Santiago Basulto
---

{% assign first_post = site.posts.first %}

# {{ first_post.title | truncatewords: 25 }}

{{ first_post.content | truncatewords: 250 }}

[Leer más &raquo;]({{ first_post.url}})

[Todos los posts](/archive.html)