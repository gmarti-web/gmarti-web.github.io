---
title: Tutorials
layout: single
permalink: /tutorials/
date: 2024-11-04
classes: wide
last_modified_at: 2024-11-09
---

<div class="tutorial-list">
{%- for tutorial in site.data.tutorial-list -%}
    <div class="tutorial-list-item">
        <h2><a href="{{ tutorial.url }}">{{ tutorial.title }}</a></h2>
        {{ tutorial.description }}
    </div>
{%- endfor -%}
</div>
