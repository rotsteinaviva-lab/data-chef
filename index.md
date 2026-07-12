---
layout: home
title: "Data Chef Blog Home"
---
### Browse Content by Topic

<div class="tag-cloud" style="margin: 20px 0; padding: 10px 0; display: flex; flex-wrap: wrap; gap: 10px;">
  {% assign sorted_tags = site.tags | sort %}
  {% for tag in sorted_tags %}
    {% assign tag_name = tag[0] %}
    {% assign tag_posts = tag[1] %}
    <a href="{{ '/tags/' | relative_url }}#{{ tag_name | downcase | slugify }}" class="btn btn--info" style="margin: 0; padding: 5px 12px; font-size: 0.85rem; border-radius: 20px;">
      {{ tag_name }} <span style="opacity: 0.6; font-size: 0.75rem; margin-left: 3px;">({{ tag_posts.size }})</span>
    </a>
  {% endfor %}
</div>