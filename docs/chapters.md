---
layout: page
title: Chapters
use_math: true
category: "nav"
---

{% for page in site.pages %} {% if page.category == "solution" %}
<li class="nav-item">
    <a href="{{ site.url }}{{site.baseurl}}{{ page.url }}">{{ page.title }}</a>
</li>
{% endif %} {% endfor %}
