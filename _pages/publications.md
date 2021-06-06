---
layout: page
permalink: /publications/
title: Publications
description: publications by categories in reversed chronological order.
years: [2021, 2019, 2018]
nav: true
summary: Research papers by categories in reversed chronological order
---

<div class="publications">

{% for y in page.years %}
  <h2 class="year">{{y}}</h2>
  {% bibliography -f papers -q @*[year={{y}}]* %}
{% endfor %}

</div>
