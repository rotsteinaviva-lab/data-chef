---
layout: home
title: "Data Chef Blog Home"
---
<html>
<div class="tag-cloud">
  {% assign tags = site.tags | sort %}
  {% for tag in tags %}
    {% assign tag_name = tag[0] %}
    {% assign posts = tag[1] %}
    <a href="/tags/{{ tag_name | slugify }}/" class="tag-item" style="font-size: {{ posts.size | times: 2 | plus: 12 }}px;">
      {{ tag_name }} ({{ posts.size }})
    </a>
  {% endfor %}
</div>
</html>
