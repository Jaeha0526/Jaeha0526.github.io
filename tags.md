---
layout: page
title: Tags
menu: true
order: 4
description: >
  Every tag across the site, with the posts that carry it.
---

{% assign tag_names = "" | split: "," %}
{% for tag in site.tags %}
  {% assign tag_names = tag_names | push: tag[0] %}
{% endfor %}
{% assign tag_names = tag_names | sort_natural %}

<div style="margin:0 0 2.5rem 0; line-height:2.4;">
{% for name in tag_names %}
  {% assign posts_for_tag = site.tags[name] %}
  <a href="#tag-{{ name | slugify }}"
     style="display:inline-block; margin:0 .45rem .2rem 0; padding:.28rem .7rem; border-radius:999px;
            border:1px solid rgba(128,128,128,.35); font-size:.88rem; text-decoration:none; white-space:nowrap;">{{ name }}<span class="faded" style="opacity:.65;"> {{ posts_for_tag.size }}</span></a>
{% endfor %}
</div>

{% for name in tag_names %}
  {% assign posts_for_tag = site.tags[name] %}

<h2 id="tag-{{ name | slugify }}" class="hr-bottom">{{ name }} <span class="faded" style="font-size:.75em; font-weight:normal;">· {{ posts_for_tag.size }} post{% if posts_for_tag.size != 1 %}s{% endif %}</span></h2>

<ul class="related-posts" style="margin-bottom:2.5rem;">
{% for post in posts_for_tag %}
  <li style="list-style:none; margin:0 0 .7rem 0;">
    <a href="{{ post.url | relative_url }}" class="heading flip-title" style="font-size:1.02rem;">{{ post.title }}</a>
    <time class="faded fine" datetime="{{ post.date | date_to_xmlschema }}" style="display:block; font-size:.78rem;">{{ post.date | date: site.data.strings.date_formats.post | default: "%d %b %Y" }}</time>
  </li>
{% endfor %}
</ul>
{% endfor %}
