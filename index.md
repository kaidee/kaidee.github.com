---
layout: page
title: Hang
header: Hang
---

这是 Hang 的个人网站的最新版本，使用  [Jekyll](https://github.com/mojombo/jekyll)  搭建。

事实证明每次快过年的时候就闹心！~~
嗯，，这个不该是介绍页面么。。 妈的！



---
###最近发布的文章
{% for post in site.posts %} 
<li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ post.url }}">{{ post.title }}</a></li> 
{% endfor %}