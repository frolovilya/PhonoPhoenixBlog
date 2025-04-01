---
layout: post
title: "Tags"
permalink: /blog/tags
---

<div class="post-tags all-tags">
    {%- for tag in site.tags -%}
    <div><a href="/blog/tags/{{ tag[0] | slugify }}">#{{ tag[0] | escape }}</a></div>
    {%- endfor -%}
</div>