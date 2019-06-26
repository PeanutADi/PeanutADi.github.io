---
layout: page
title: About
description: Coding life
keywords: Zhang Maliang, SYSU
comments: true
menu: 关于
permalink: /about/
---

Coding life

Learning to code, learning to live

## 联系

{% for website in site.data.social %}
* {{ website.sitename }}：[@{{ website.name }}]({{ website.url }})
{% endfor %}

## Skill Keywords

{% for category in site.data.skills %}
### {{ category.name }}
<div class="btn-inline">
{% for keyword in category.keywords %}
<button class="btn btn-outline" type="button">{{ keyword }}</button>
{% endfor %}
</div>
{% endfor %}
