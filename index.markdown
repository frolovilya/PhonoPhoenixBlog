---
layout: home
---

<div>
  {%- if site.posts.size > 0 -%}
  <ul class="post-list">
    {%- for post in site.posts -%}
    {% include blog-post-li.html %}
    {%- endfor -%}
  </ul>
  {%- endif -%}
</div>