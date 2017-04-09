---
title: welcome
layout: default
---
## {{page.title}}
Thanks for visiting. The following post is the most recent:
<div>
	{% for item in site.nav %}
  {% if item.href contains 'http' %}
     <a href="{{ item.href }}">{{ item.title }}</a>
  {% else %}
     <a href="{{ item.href | relative_url }}">{{ item.title }}</a>
  {% endif %}
  {% if forloop.last %}  {% else %} • {% endif %}
{% endfor %}
</div>
<div id="nav">
{% for item in site.nav %}
  {% if item.href contains 'http' %}
     <a href="{{ item.href }}">{{ item.title }}</a>
  {% else %}
     <a href="{{ item.href | relative_url }}">{{ item.title }}</a>
  {% endif %}
  {% if forloop.last %}  {% else %} • {% endif %}
{% endfor %}
</div>