---
layout: page
title: Blog Archive
---

{% assign sorted_tags = site.tags | sort %}

{% for tag in sorted_tags %}
  {% if tag[0] contains "math" %}
    <h3>{{ tag[0] | replace: "-", " → " }}</h3>
    <ul>
      {% for post in tag[1] %}
        <li>
          <a href="{{ post.url }}">
            {{ post.date | date: "%B %Y" }} – {{ post.title }}
          </a>
        </li>
      {% endfor %}
    </ul>
  {% endif %}
{% endfor %}
