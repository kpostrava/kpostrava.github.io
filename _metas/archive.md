---
layout: post
title: "Archiv"
category: "bar"
---

{% for archived_class in site.archive %}

- [{{ archived_class.title }}]({{ archived_class.url }})
  {% endfor %}
