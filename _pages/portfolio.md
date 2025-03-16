---
title: Portfolio
permalink: /portfolio/
layout: collection
---

<div>
{% for collection in site.portfolio %}
    {% capture label %}{{ collection.title }}{% endcapture %}
    <h2 id="{{ label | slugify }}" class="archive__subtitle"><a href="{{ label | slugify }}">{{ label }}</a></h2>
    {{ collection.description | strip }}
{% endfor %}
</div>

[What is a hub-and-spoke network architecture?](what-is-a-hub-and-spoke-topology/)
