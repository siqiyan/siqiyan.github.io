---
layout: default
title: Home
---

## 🤖Project and Demostration

Here are some projects I've been working on.

---

{% for post in site.posts limit:5 %}

### [{{ post.title }}]({{ Post.url }})

{{ post.date | date: "%B %d, %Y" }}

{{ post.excerpt }}

{% end for %}
