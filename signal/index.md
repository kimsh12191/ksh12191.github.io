---
layout: page
title: SIGNAL
excerpt: "An archive of blog posts sorted by date."
search_omit: true
---

<ul class="taxonomy-index">
  {% assign tags_max = 0 %}
  {% for tag in site.tags %}
    {% if tag[1].size > tags_max %}
      {% assign tags_max = tag[1].size %}
    {% endif %}
  {% endfor %}
  {% for i in (1..tags_max) reversed %}
    {% for tag in site.tags %}
      {% if tag[1].size == i %}
        <li>
          <a href="#{{ tag[0] | slugify }}">
            <strong>{{ tag[0] }}</strong> <span class="taxonomy-count">{{ i }}</span>
          </a>
        </li>
      {% endif %}
    {% endfor %}
  {% endfor %}
</ul>


<ul class="post-list">
{% for post in site.categories.signal %}
  <li><article><a href="{{ site.url }}{{ post.url }}">{{ post.title }} <span class="entry-date"><time datetime="{{ post.date | date_to_xmlschema }}">{{ post.date | date: "%B %d, %Y" }}</time></span>{% if post.excerpt %} <span class="excerpt">{{ post.excerpt | remove: '\[ ... \]' | remove: '\( ... \)' | markdownify | strip_html | strip_newlines | escape_once }}</span>{% endif %}</a></article></li>
{% endfor %}
</ul>
