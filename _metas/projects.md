---
layout: post
title: "Zadání"
category: "bar"
---

### Prostředí code.org

{% assign codeorg_projects = site.projects | where: "categories", "codeorg" | sort: "order" %}
{% for project in codeorg_projects %}

- [{{ project.title }}]({{ project.url }})
  {% endfor %}

### HTML, CSS, JS

{% assign codeorg_projects = site.projects | where: "categories", "html" | sort: "order" %}
{% for project in codeorg_projects %}

- [{{ project.title }}]({{ project.url }})
  {% endfor %}
