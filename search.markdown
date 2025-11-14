---
layout: page
title: 文章搜索
---
<div class="search-container">
  <input type="text" id="search-input" placeholder="输入关键词搜索文章...">
  <ul id="search-results"></ul>
</div>

<!-- 引入搜索依赖 -->
<script src="https://cdn.jsdelivr.net/npm/lunr@2.3.9/lunr.min.js"></script>
<script>
// 1. 加载文章数据（Jekyll 自动生成 JSON）
fetch('{{ site.baseurl }}/search.json')
  .then(res => res.json())
  .then(posts => {
    // 2. 初始化搜索索引
    const idx = lunr(function () {
      this.field('title'); // 搜索标题
      this.field('content'); // 搜索正文
      this.ref('url'); // 文章链接
      posts.forEach(post => this.add(post));
    });

    // 3. 绑定搜索输入事件
    const input = document.getElementById('search-input');
    const results = document.getElementById('search-results');
    input.addEventListener('input', e => {
      results.innerHTML = '';
      const query = e.target.value.trim();
      if (!query) return;
      // 执行搜索
      const matches = idx.search(query);
      // 显示结果
      matches.forEach(match => {
        const post = posts.find(p => p.url === match.ref);
        const li = document.createElement('li');
        li.innerHTML = `<a href="${post.url}">${post.title}</a><p>${post.date}</p>`;
        results.appendChild(li);
      });
    });
  });