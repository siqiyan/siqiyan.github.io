---
layout: default
title: Home
---

## 🤖Project and Demostration

Here are some projects I've been working on.

---

{% for post in site.posts limit:10 %}

### [{{ post.title }}]({{ post.url }})

{{ post.date | date: "%B %d, %Y" }}

{{ post.excerpt }}

{% endfor %}
