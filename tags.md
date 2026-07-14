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
    <a href="#{{ tag.first | slugify }}" class="btn btn--info" style="margin: 0; padding: 5px 12px; font-size: 0.85rem; border-radius: 20px;">
      {{ tag.first }} <span style="opacity: 0.6; font-size: 0.75rem; margin-left: 3px;">({{ tag.last.size }})</span>
    </a>
  {% endfor %}
</div>

<hr style="margin: 40px 0;">

<!-- 2. The Actual Post Lists -->
<div class="tags-lists">
  {% for tag in sorted_tags %}
    <div id="{{ tag.first | slugify }}" style="margin-bottom: 45px; scroll-margin-top: 50px;">
      
      <!-- Heading font size strictly scaled down to a normal 1.2rem -->
      <h4 style="border-bottom: 1px solid #7a8288; padding-bottom: 8px; color: #b6bcd1; font-size: 1.2rem; margin-top: 0; margin-bottom: 15px;">
        {{ tag.first }}
      </h4>
      
      <ul style="list-style-type: square; padding-left: 20px; margin-top: 0;">
        {% for post in tag.last %}
          <li style="margin-bottom: 8px; line-height: 1.4;">
              <!-- Fluid font floor forces a highly legible minimum text size on mobile screens -->
            <a href="{{ post.url | relative_url }}" style="text-decoration: none; font-size: clamp(1rem, 2.5vw, 1.1rem); font-weight: normal;">
              {{ post.title }}
            </a>
            <span style="color: #888; font-size: 0.8rem; margin-left: 8px; display: inline-block;">
              — {{ post.date | date: "%B %d, %Y" }}
            </span>
          </li>
        {% endfor %}
      </ul>
      
    </div>
  {% endfor %}
</div>