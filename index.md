---
layout: default
title: Viggo
---

<!-- 全局样式：左右分栏 + 折叠逻辑 -->
<style>
/* 左右分栏布局 */
.container {
  display: flex;
  gap: 20px;
  margin: 0 auto;
  padding: 20px;
  width: 100%;        /* 小屏幕占满，大屏幕最多1200px */
  box-sizing: border-box; /* 防止padding撑大容器导致遮挡 */
     /*overflow: hidden; 防止子元素溢出遮挡 */
}

/* 左侧四级目录栏 */
.sidebar {
  width: 28%;
  min-width: 250px;
  background: #f8f9fa;
  padding: 15px;
  border-radius: 8px;
  border: 1px solid #eee;
  max-height: 180vh;
  overflow-y: auto;
  box-sizing: border-box; /* 关键：padding不撑大宽度 */
}

/* 右侧个人简介区 */
.profile {
  flex: 1;
  background: #f0f8fb;
  padding: 30px;
  min-width: 300px; /* 小屏幕最小宽度，不挤 */
  border-radius: 8px;
  border: 1px solid #eee;
  box-sizing: border-box; /* 核心：避免padding导致宽度超了遮挡 */
  overflow: hidden; /* 防止内容溢出出现白色 */
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
        <!-- 一级分类 -->
        <div class="level-1" data-target="level-1-{{ forloop.index }}">
          ▶ {{ first_cat.name }} （{{ first_cat.items.size }}篇）
        </div>
        <div id="level-1-{{ forloop.index }}" class="open"> <!-- 控制一级默认状态：open/closed -->

          {% comment %} 第二步：按二级分类分组 {% endcomment %}
          {% assign second_level = first_cat.items | group_by: "categories[1]" %}
          {% for second_cat in second_level %}
            {% if second_cat.name != "" %}
              <!-- 二级分类 -->
              <div class="level-2" data-target="level-2-{{ forloop.parentloop.index }}-{{ forloop.index }}">
                ▶ {{ second_cat.name }} （{{ second_cat.items.size }}篇）
              </div>
              <div id="level-2-{{ forloop.parentloop.index }}-{{ forloop.index }}" class="closed"> <!-- 二级默认状态 -->

                {% comment %} 第三步：按三级分类分组 {% endcomment %}
                {% assign third_level = second_cat.items | group_by: "categories[2]" %}
                {% for third_cat in third_level %}
                  {% if third_cat.name != "" %}
                    <!-- 三级分类 -->
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

<div class="profile">
    <h2 style="color: #2c3e50; margin-top: 0;">👋 关于我</h2>
    <div style="line-height: 1.8; font-size: 1.1em; color: #34495e;">
      <p>你好，我是赵一格，一只野生医学计算机混血研究生</p>
      <p>标签：#ENTJ </p>
      <p>      #学习=吃饭 </p> 
      <p>      #效率=生命 </p>
      
      <h3 style="color: #2980b9;">🎓 教育背景</h3>
      <ul style="line-height: 1.8;">
        <li>研究生：2024.09-2027.07 西安交通大学 电子信息系 生物医学工程（研二）</li>
        <li>本科：2020.09-2024.06 暨南大学 计算机系 软件工程（绩点前10%，曾获奖学金）</li>
      </ul>

      <h3 style="color: #2980b9;">💻 核心技能</h3>
      <ul style="line-height: 1.8;">
        <li>技术能力：熟悉PyTorch框架、多模态数据建模、语言模型微调</li>
        <li>工具掌握：Office、Axure、Figma、Dify、Linux、Docker；常用Markdown、偏爱Claude</li>
        <li>软技能：跨域协作、项目落地、MECE问题拆解、用户需求分析、英文技术文档读写（CET-6 530+）</li>
      </ul>

      <h3 style="color: #2980b9;">📞 联系方式</h3>
      <p>邮箱：<a href="mailto:zhaoyige1@163.com" style="color: #3498db; text-decoration: none;">
      <span class="copyable-text" data-copy="zhaoyige1@163.com">zhaoyige1@163.com</span></a></p>
      <p>微信：<span class="copyable-text" data-copy="_iacgnaixihcub">_iacgnaixihcub</span></p>
      <p>GitHub：<a href="https://github.com/viggo1" target="_blank" style="color: #3498db;">https://github.com/viggo1</a></p>
      <h3 style="color: #2980b9;">📊 博客数据</h3>
      <p>总文章数：<span style="font-weight: bold; color: #e74c3c;">{{ site.posts.size }}</span> 篇</p>
      <p>最后更新：<span style="color: #7f8c8d;">{{ site.posts.first.date | date: "%Y-%m-%d" }}</span></p>
      <p>个人信条：Stay hungry, Stay foolish —— 永远对未知保持好奇，用技术创造价值</p>
    </div>
  </div>
</div>

<!-- 折叠/展开交互 JS（未修改，确保功能正常） -->
<script>
document.querySelectorAll('.level-1').forEach(item => {
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

document.querySelectorAll('.open').forEach(el => {
  const trigger = document.querySelector(`[data-target="${el.id}"]`);
  if (trigger) trigger.innerHTML = trigger.innerHTML.replace('▶', '▼');
});
</script>

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

<!-- 悬停复制 CSS：悬浮样式 + 提示文案 -->
<style>
/* 可复制文字的基础样式（行内元素，不打乱排版） */
.copyable-text {
  display: inline; /* 保持行内，和普通文字排版一致 */
  padding: 2px 4px; /* 轻微内边距，突出可点击区域 */
  background: #f0f8fb; /* 浅背景色，提示可交互 */
  border-radius: 3px; /* 圆角更美观 */
  color: #3498db; /* 蓝色文字，区分普通文字 */
  cursor: pointer; /* 鼠标悬浮变“手型”，提示可点击 */
  position: relative; /* 用于定位悬浮提示 */
}

/* 悬浮时加深背景，增强反馈 */
.copyable-text:hover {
  background: #e6f7ff;
}

/* 悬浮提示：默认隐藏，hover时显示“点击复制” */
.copyable-text::after {
  content: "点击复制";
  position: absolute;
  top: -28px; /* 提示框在文字上方 */
  left: 50%;
  transform: translateX(-50%); /* 水平居中 */
  background: #333; /* 深色提示框，醒目 */
  color: #fff;
  font-size: 12px;
  padding: 4px 8px;
  border-radius: 4px;
  white-space: nowrap; /* 防止提示文字换行 */
  opacity: 0; /* 默认透明 */
  visibility: hidden; /* 默认隐藏（不占空间） */
  transition: all 0.2s ease; /* 悬浮时平滑显示 */
  z-index: 9999; /* 提至最高层级，不会被任何元素遮挡 */
  pointer-events: none; /* 提示框不影响点击下方内容 */
}

/* 鼠标悬浮时显示提示 */
.copyable-text:hover::after {
  opacity: 1;
  visibility: visible;
}

/* 复制成功后：提示文案改为“已复制！”（通过JS加类实现） */
.copyable-text.copied::after {
  content: "已复制！";
  background: #52c41a; /* 绿色提示，区分成功状态 */
}
</style>

<!-- JavaScript：点击复制功能 + 成功反馈 -->
<script>
// 选中所有可复制的文字元素
const copyElements = document.querySelectorAll('.copyable-text');

copyElements.forEach(el => {
  el.addEventListener('click', () => {
    // 1. 获取要复制的内容（从data-copy属性取，避免和显示文本不一致）
    const copyContent = el.getAttribute('data-copy');
    
    // 2. 执行复制（兼容现代浏览器的Clipboard API）
    navigator.clipboard.writeText(copyContent).then(() => {
      // 3. 复制成功：添加“copied”类，显示“已复制”提示
      el.classList.add('copied');
      
      // 4. 2秒后移除“copied”类，恢复原提示
      setTimeout(() => {
        el.classList.remove('copied');
      }, 2000);
    }).catch(err => {
      // 兼容旧浏览器/权限问题：降级用文本框复制
      const textArea = document.createElement('textarea');
      textArea.value = copyContent;
      document.body.appendChild(textArea);
      textArea.select();
      document.execCommand('copy');
      document.body.removeChild(textArea);
      
      // 同样显示成功反馈
      el.classList.add('copied');
      setTimeout(() => el.classList.remove('copied'), 2000);
    });
  });
});
</script>
