---
layout: home  # 指定使用上面新建的 home.html 布局
title: 首页  # 主页标题
---

# 欢迎来到我的网站！

这是一个完全静态的网站，包含「最新文章」和「文章搜索」功能，无需服务器和数据库。

## 📚 最新文章
<!-- 自动读取 _posts 文件夹里的文章，显示最近3篇 -->
{% for post in site.posts limit:3 %}
- 📅 {{ post.date | date: "%Y-%m-%d" }} → [{{ post.title }}]({{ post.url }})
{% endfor %}

{% if site.posts.size > 3 %}
- [查看全部文章 →]({{ site.baseurl }}/all-posts.html)
{% endif %}

## 🔍 搜索文章
想找特定内容？点击下方进入搜索页面：
> [前往搜索页面]({{ site.baseurl }}/search.html)