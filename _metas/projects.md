---
layout: post
title: "Zadání"
category: "bar"
---

### Prostředí App lab

{% assign codeorg_projects = site.projects | where: "categories", "codeorg" | sort: "order" %}
{% for project in codeorg_projects %}

- [{{ project.title }}]({{ project.url }})
  {% endfor %}

### HTML, CSS, JS

{% assign html_projects = site.projects | where: "categories", "html" | sort: "order" %}
{% for project in html_projects %}

- [{{ project.title }}]({{ project.url }})
  {% endfor %}

### Node.js

{% assign node_projects = site.projects | where: "categories", "nodejs" | sort: "order" %}
{% for project in node_projects %}

- [{{ project.title }}]({{ project.url }})
  {% endfor %}
