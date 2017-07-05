---
layout: page
title: Chapters
use_math: true
category: "nav"
---

{% assign solutions = site.pages | where: "category", "solution" %}
{% assign sorted_solutions = solutions | sort:"chapter" %}
{% for page in sorted_solutions %}
<li class="nav-item">
    <a href="{{ site.url }}{{site.baseurl}}{{ page.url }}">{{ page.title }}</a>
</li>
{% endfor %}
