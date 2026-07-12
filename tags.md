---
title: "Posts by Topic"
layout: single
permalink: /tags/
author_profile: true
---

Select a topic below to jump directly to its matching articles:

<!-- 1. The Sub-Navigation Filter Cloud -->
<div class="tag-cloud" style="margin: 20px 0; display: flex; flex-wrap: wrap; gap: 10px;">
  {% assign sorted_tags = site.tags | sort %}
  {% for tag in sorted_tags %}
    {% assign tag_name = tag.first %}
    {% assign tag_posts = tag.last %}
    
    <a href="#{{ tag_name | downcase | slugify }}" class="btn btn--info" style="margin: 0; padding: 6px 16px; font-size: 0.8rem; border-radius: 20px;">
      {{ tag_name }} <span style="opacity: 0.6; font-size: 0.9rem; margin-left: 3px;">({{ tag_posts.size }})</span>
    </a>
  {% endfor %}
</div>

<hr style="margin: 40px 0;">

<!-- 2. The Actual Post Lists -->
<div class="tags-lists">
  {% for tag in sorted_tags %}
    {% assign tag_name = tag.first %}
    {% assign tag_posts = tag.last %}
    
    <div id="{{ tag_name | downcase | slugify }}" style="margin-bottom: 45px; scroll-margin-top: 30px;">
      <!-- Increased font-size to 2rem to make category tag headings bigger -->
      <h4 style="border-bottom: 2px solid #7a8288; padding-bottom: 8px; color: #6b90b4; font-size: 0.8rem;">
        📁 {{ tag_name }}
      </h4>
      <ul style="list-style-type: square; padding-left: 20px;">
        {% for post in tag_posts %}
          <li style="margin-bottom: 10px;">
            <a href="{{ post.url | relative_url }}" style="font-weight: bold; text-decoration: none; font-size: 0.95rem;">
              {{ post.title }}
            </a>
            <span style="color: #888; font-size: 0.75rem; margin-left: 10px;">
              — {{ post.date | date: "%B %d, %Y" }}
            </span>
          </li>
        {% endfor %}
      </ul>
    </div>
  {% endfor %}
</div>