---
layout: post
title: "My Blog Home"
---

# Welcome to My Blog

### Recent Posts
{% for post in site.posts %}
* [{{ post.title }}]({{ post.url }}) — {{ post.date | date_to_string }}
{% endfor %}
