---
title: Tutorials
layout: page
date: 2024-11-04
last_modified_date: 2024-11-04
---

<div>
{%- for tutorial in site.data.tutorial-list -%}
    <h2><a href="{{ tutorial.url }}">{{ tutorial.title }}</a></h2>
    {{ tutorial.description }}
{%- endfor -%}
</div>
