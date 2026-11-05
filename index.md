---
layout: page
title: Articles
---

# OT Security Field Notes

By **Pavithran Ganesan**

Exploring operational technology cybersecurity: network architecture, segmentation, risk assessment, and IEC 62443.

## Latest articles

{% if site.posts.size > 0 %}
{% for post in site.posts %}
### [{{ post.title }}]({{ post.url | relative_url }})

{{ post.date | date: "%d %B %Y" }}{% if post.description %} — {{ post.description }}{% endif %}

{% endfor %}
{% else %}
Articles are on the way. This space will bring together longer-form OT cybersecurity writing and practical engineering perspectives.
{% endif %}
