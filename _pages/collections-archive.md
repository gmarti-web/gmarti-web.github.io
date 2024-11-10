---
layout: collection
title: "Collections"
permalink: /collections-archive/
author_profile: true
---

<div>
{% for collection in site.collections %}
  {% unless collection.output == false or collection.label == "posts" %}
    {% capture label %}{{ collection.title }}{% endcapture %}
    <h2 id="{{ label | slugify }}" class="archive__subtitle"><a href="/{{ label | slugify }}">{{ label }}</a></h2>
    {{ collection.description | strip }}
  {% endunless %}
{% endfor %}
</div>
