---
layout: default
title: Home
---

# Colin Weinshenker

[GitHub](https://github.com/caweinshenker) · [npm](https://www.npmjs.com/~cshenks)

## Blog

{% for post in site.posts %}
- [{{ post.title }}]({{ post.url }}) - {{ post.date | date: "%B %d, %Y" }}
{% endfor %}
