---
title: Categories
layout: page
---
<ul class="tag_box inline">
{% for cat in site.categories %}
<a href="#{{ cat[0] }}" title="{{ cat[0] }}" rel="{{ cat[1].size }}">{{ cat[0] | join: "/"}}<span> ({{ cat[1].size }})</span></a>
{% endfor %}
</ul>
<ul class="listing-item">
{% for cat in site.categories %}
<li class="listing-seperator" id="{{ cat[0] }}">{{ cat[0]}}</li>
 {% for post in cat[1] %}
  <time datetime="{{ post.date | date:"%Y-%m-%d" }}">{{ post.date | date:"%Y-%m-%d" }}</time>
  <a href="{{ site.url }}{{ post.url }}" title="{{ post.title }}">{{ post.title }}</a><br />
{% endfor %}
{% endfor %}
</ul>

