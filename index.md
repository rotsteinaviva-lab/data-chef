---
layout: home
title: "Data Chef: Recipes for data wrangling, visualization, & more (sample step-by-step projects)"
---
### Browse Content by Topic

<div class="tag-cloud" style="margin: 20px 0; padding: 10px 0; display: flex; flex-wrap: wrap; gap: 10px;">
  {% assign sorted_tags = site.tags | sort %}
  {% for tag in sorted_tags %}
    {% assign tag_name = tag.first %}
    {% assign tag_posts = tag.last %}
    <a href="{{ '/tags/' | relative_url }}#{{ tag_name | downcase | slugify }}" class="btn btn--info" style="margin: 0; padding: 5px 12px; font-size: 0.85rem; border-radius: 20px;">
      {{ tag_name }} <span style="opacity: 0.6; font-size: 0.75rem; margin-left: 3px;">({{ tag_posts.size }})</span>
    </a>
  {% endfor %}
</div>

***Did you attempt any projects?*** *[Take the Data Chef survey](https://qualtricsxmmz3zzqb9x.qualtrics.com/jfe/form/SV_72Fa2DomIssjpn8) to help improve the learning tool.*
