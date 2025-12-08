---
layout: default
title: 赵一格
---

<!-- 全局样式：左右分栏 + 折叠逻辑 -->
<style>
/* 左右分栏布局 */
.container {
  display: flex;
  gap: 20px;
  max-width: 1200px;
  margin: 0 auto;
  padding: 20px;
}

/* 左侧四级目录栏 */
.sidebar {
  width: 28%;
  min-width: 250px;
  background: #f8f9fa;
  padding: 15px;
  border-radius: 8px;
  border: 1px solid #eee;
  max-height: 80vh;
  overflow-y: auto;
}

/* 右侧个人简介区 */
.profile {
  width: 72%;
  background: #f0f8fb;
  padding: 30px;
  border-radius: 8px;
  border: 1px solid #eee;
}

/* 目录层级样式：四级缩进 + 折叠控制 */
/* 一级分类 */
.level-1 {
  margin: 10px 0;
  font-size: 1.1em;
  font-weight: bold;
  cursor: pointer;
  color: #2c3e50;
}
/* 二级分类 */
.level-2 {
  margin: 8px 0 8px 15px;
  font-size: 1em;
  cursor: pointer;
  color: #34495e;
}
/* 三级分类 */
.level-3 {
  margin: 6px 0 6px 30px;
  font-size: 0.95em;
  cursor: pointer;
  color: #7f8c8d;
}
/* 四级分类 */
.level-4 {
  margin: 4px 0 4px 45px;
  font-size: 0.9em;
  color: #95a5a6;
}
/* 文章列表 */
.post-list {
  margin: 4px 0 4px 60px;
  list-style: none;
  padding: 0;
  font-size: 0.85em;
}
.post-list li {
  margin: 3px 0;
  padding-left: 8px;
  border-left: 2px solid #ddd;
}
.post-list a {
  color: #3498db;
  text-decoration: none;
}
.post-list a:hover {
  color: #2980b9;
  text-decoration: underline;
}

/* 折叠/展开控制类：默认折叠（closed）/ 打开（open） */
.closed {
  display: none;
}
.open {
  display: block;
}

/* 响应式适配：手机端合并为上下布局 */
@media (max-width: 768px) {
  .container {
    flex-direction: column;
  }
  .sidebar, .profile {
    width: 100%;
    min-width: unset;
  }
}
</style>

<!-- 主体布局：左侧目录 + 右侧简介 -->
<div class="container">
  <!-- 左侧：四级可折叠目录 -->
  <div class="sidebar">
    <h3 style="margin-top: 0; color: #2c3e50;">📚 文章目录</h3>

    {% comment %} 第一步：按一级分类分组 {% endcomment %}
    {% assign first_level = site.posts | group_by: "categories[0]" %}
    {% for first_cat in first_level %}
      {% if first_cat.name != "" %}
        <!-- 一级分类（默认打开：加 open 类；默认折叠：改 closed） -->
        <div class="level-1" data-target="level-1-{{ forloop.index }}">
          ▶ {{ first_cat.name }} （{{ first_cat.items.size }}篇）
        </div>
        <div id="level-1-{{ forloop.index }}" class="open"> <!-- 这里控制一级默认状态：open/closed -->

          {% comment %} 第二步：按二级分类分组 {% endcomment %}
          {% assign second_level = first_cat.items | group_by: "categories[1]" %}
          {% for second_cat in second_level %}
            {% if second_cat.name != "" %}
              <!-- 二级分类（默认折叠：closed；默认打开：open） -->
              <div class="level-2" data-target="level-2-{{ forloop.parentloop.index }}-{{ forloop.index }}">
                ▶ {{ second_cat.name }} （{{ second_cat.items.size }}篇）
              </div>
              <div id="level-2-{{ forloop.parentloop.index }}-{{ forloop.index }}" class="closed"> <!-- 二级默认状态 -->

                {% comment %} 第三步：按三级分类分组 {% endcomment %}
                {% assign third_level = second_cat.items | group_by: "categories[2]" %}
                {% for third_cat in third_level %}
                  {% if third_cat.name != "" %}
                    <!-- 三级分类（默认折叠：closed；默认打开：open） -->
                    <div class="level-3" data-target="level-3-{{ forloop.parentloop.parentloop.index }}-{{ forloop.parentloop.index }}-{{ forloop.index }}">
                      ▶ {{ third_cat.name }} （{{ third_cat.items.size }}篇）
                    </div>
                    <div id="level-3-{{ forloop.parentloop.parentloop.index }}-{{ forloop.parentloop.index }}-{{ forloop.index }}" class="closed"> <!-- 三级默认状态 -->

                      {% comment %} 第四步：按四级分类分组 {% endcomment %}
                      {% assign fourth_level = third_cat.items | group_by: "categories[3]" %}
                      {% for fourth_cat in fourth_level %}
                        {% if fourth_cat.name != "" %}
                          <!-- 四级分类（无折叠，直接显示） -->
                          <div class="level-4">
                            📄 {{ fourth_cat.name }} （{{ fourth_cat.items.size }}篇）
                          </div>
                          <!-- 四级分类下的文章列表 -->
                          <ul class="post-list">
                            {% for post in fourth_cat.items %}
                              <li>
                                <a href="{{ post.url }}">{{ post.title }}</a>
                                <span style="color: #999; margin-left: 8px;">{{ post.date | date: "%Y-%m-%d" }}</span>
                              </li>
                            {% endfor %}
                          </ul>
                        {% else %}
                          <!-- 无四级分类：显示三级下的文章 -->
                          <ul class="post-list">
                            {% for post in third_cat.items %}
                              <li>
                                <a href="{{ post.url }}">{{ post.title }}</a>
                                <span style="color: #999; margin-left: 8px;">{{ post.date | date: "%Y-%m-%d" }}</span>
                              </li>
                            {% endfor %}
                          </ul>
                        {% endif %}
                      {% endfor %}
                    </div>
                  {% else %}
                    <!-- 无三级分类：显示二级下的文章 -->
                    <ul class="post-list">
                      {% for post in second_cat.items %}
                        <li>
                          <a href="{{ post.url }}">{{ post.title }}</a>
                          <span style="color: #999; margin-left: 8px;">{{ post.date | date: "%Y-%m-%d" }}</span>
                        </li>
                      {% endfor %}
                    </ul>
                  {% endif %}
                {% endfor %}
              </div>
            {% else %}
              <!-- 无二级分类：显示一级下的文章 -->
              <ul class="post-list">
                {% for post in first_cat.items %}
                  <li>
                    <a href="{{ post.url }}">{{ post.title }}</a>
                    <span style="color: #999; margin-left: 8px;">{{ post.date | date: "%Y-%m-%d" }}</span>
                  </li>
                {% endfor %}
              </ul>
            {% endif %}
          {% endfor %}
        </div>
      {% endif %}
    {% endfor %}
  </div>

  <!-- 右侧：大块个人简介（可自定义样式/内容） -->
  <div class="profile">
    <h2 style="color: #2c3e50; margin-top: 0;">👋 关于我</h2>
    <div style="line-height: 1.8; font-size: 1.1em; color: #34495e;">
      <p>你好！我是 [你的名字]，一名专注于 [你的领域，如：前端开发/后端架构/全栈开发] 的开发者。</p>
      
      <h3 style="color: #2980b9;">📌 核心技能</h3>
      <ul style="line-height: 1.8;">
        <li>编程语言：JavaScript/TypeScript、Python、Java、Go（按需修改）</li>
        <li>技术栈：React/Vue、Node.js、MySQL、Redis（按需修改）</li>
        <li>擅长领域：性能优化、工程化、中间件开发（按需修改）</li>
      </ul>

      <h3 style="color: #2980b9;">📝 博客定位</h3>
      <p>本博客主要分享 [你的博客方向，如：前端进阶技巧、后端实战经验、技术踩坑总结、学习笔记]，希望能和同领域的开发者交流成长。</p>

      <h3 style="color: #2980b9;">📞 联系方式</h3>
      <p>邮箱：<a href="mailto:your-email@xxx.com" style="color: #3498db;">your-email@xxx.com</a></p>
      <p>GitHub：<a href="https://github.com/viggo1" target="_blank" style="color: #3498db;">https://github.com/viggo1</a>（按需修改）</p>
      <p>其他：知乎/掘金/CSDN（按需补充）</p>

      <h3 style="color: #2980b9;">📊 博客数据</h3>
      <p>总文章数：<span style="font-weight: bold; color: #e74c3c;">{{ site.posts.size }}</span> 篇</p>
      <p>最后更新：<span style="color: #7f8c8d;">{{ site.posts.first.date | date: "%Y-%m-%d" }}</span></p>
    </div>
  </div>
</div>

<!-- 折叠/展开交互 JS -->
<script>
// 一级分类点击事件
document.querySelectorAll('.level-1').forEach(item => {
  item.addEventListener('click', () => {
    const targetId = item.getAttribute('data-target');
    const targetEl = document.getElementById(targetId);
    // 切换折叠/展开状态 + 切换箭头
    if (targetEl.classList.contains('closed')) {
      targetEl.classList.replace('closed', 'open');
      item.innerHTML = item.innerHTML.replace('▶', '▼');
    } else {
      targetEl.classList.replace('open', 'closed');
      item.innerHTML = item.innerHTML.replace('▼', '▶');
    }
  });
});

// 二级分类点击事件
document.querySelectorAll('.level-2').forEach(item => {
  item.addEventListener('click', () => {
    const targetId = item.getAttribute('data-target');
    const targetEl = document.getElementById(targetId);
    if (targetEl.classList.contains('closed')) {
      targetEl.classList.replace('closed', 'open');
      item.innerHTML = item.innerHTML.replace('▶', '▼');
    } else {
      targetEl.classList.replace('open', 'closed');
      item.innerHTML = item.innerHTML.replace('▼', '▶');
    }
  });
});

// 三级分类点击事件
document.querySelectorAll('.level-3').forEach(item => {
  item.addEventListener('click', () => {
    const targetId = item.getAttribute('data-target');
    const targetEl = document.getElementById(targetId);
    if (targetEl.classList.contains('closed')) {
      targetEl.classList.replace('closed', 'open');
      item.innerHTML = item.innerHTML.replace('▶', '▼');
    } else {
      targetEl.classList.replace('open', 'closed');
      item.innerHTML = item.innerHTML.replace('▼', '▶');
    }
  });
});

// 初始化：将默认折叠的分类箭头改为 ▶，默认打开的改为 ▼
document.querySelectorAll('.open').forEach(el => {
  const trigger = document.querySelector(`[data-target="${el.id}"]`);
  if (trigger) trigger.innerHTML = trigger.innerHTML.replace('▶', '▼');
});
</script>
