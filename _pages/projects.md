---
layout: page
title: projects
permalink: /projects/
description: My projects.
nav: true
nav_order: 3
display_categories: [work]
horizontal: false
---

<div class="projects">
  {% if site.enable_project_categories and page.display_categories %}
    {% assign categories = page.display_categories %}
  {% else %}
    {% assign categories = nil %}
  {% endif %}

{% if categories %}
{% assign projects_grouped = page.display_categories %}
{% else %}
{% assign projects_grouped = "all" | split: "," %}
{% endif %}

{% for category in projects_grouped %}
{% if category != "all" %}
<a id="{{ category }}" href="#{{ category }}">

<h2 class="category">{{ category }}</h2>
</a>
{% assign projects_to_show = site.projects | where: "category", category | sort: "importance" %}
{% else %}
{% assign projects_to_show = site.projects | sort: "importance" %}
{% endif %}

    {% if page.horizontal %}
      <div class="container">
        <div class="row row-cols-2">
          {% for project in projects_to_show %}
            {% include projects_horizontal.liquid %}
          {% endfor %}
        </div>
      </div>
    {% else %}
      <div class="grid">
        {% for project in projects_to_show %}
          {% include projects.liquid %}
        {% endfor %}
      </div>
    {% endif %}

{% endfor %}

</div>
