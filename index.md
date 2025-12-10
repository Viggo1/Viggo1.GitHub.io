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
  width: 40%;
  background: #f8f9fa;
  padding: 15px;
  border-radius: 8px;
  border: 1px solid #eee;
  max-height: 180vh;
  overflow-y: auto;
  box-sizing: border-box; /* 关键：padding不撑大宽度 */
  visibility: visible !important; /* 强制可见 */
  opacity: 1 !important; /* 强制不透明 */
  color: #2c3e50 !important; /* 强制文字颜色（避免和背景一致） */
}


/* 右侧个人简介区 */
.profile {
  flex: 1;
  background: #f0f8fb;
  padding: 30px;
  width: 60%;
  border-radius: 8px;
  border: 1px solid #eee;
  box-sizing: border-box; /* 核心：避免padding导致宽度超了遮挡 */
  overflow: hidden; /* 防止内容溢出出现白色 */
}

/* 一级分类 */
#custom-sidebar.level-1 {
  margin: 8px 0;
  font-size: 1.1em;
  font-weight: bold;
  cursor: pointer;
  color: #2c3e50 !important; /* 强制黑色，避免和背景融合 */
}

/* 文章列表：彻底简化缩进，确保在容器内 */
#custom-sidebar.post-list {
  margin: 2px 0 2px 35px !important; /* 缩进从60px→35px，强制生效 */
  list-style: disc !important; /* 强制显示列表符号，确认存在 */
  padding: 0 !important;
  font-size: 0.85em;
  color: #3498db !important; /* 强制蓝色，醒目 */
}
#custom-sidebar.post-list li {
  margin: 3px 0 !important;
  padding-left: 5px !important;
  border-left: 2px solid #ddd;
}
#custom-sidebar.post-list a {
  color: #3498db !important; /* 强制蓝色链接 */
  text-decoration: underline !important; /* 强制下划线，确认是链接 */
}

/* 折叠/展开控制类：默认折叠（closed）/ 打开（open） */
#custom-sidebar.closed {
  display: none;
}
#custom-sidebar.open {
  display: block;
}

/* 响应式适配：手机端合并为上下布局 */
@media (max-width: 768px) {
  .container {
    flex-direction: column;
  }
  .custom-sidebar, .profile {
    width: 100%;
    min-width: unset;
  }
}
</style>

<!-- 主体布局：左侧目录 + 右侧简介 -->
<div class="container">
  <!-- 左侧：目录 -->
  <div class="sidebar">
    <h3 style="margin-top: 0; color: #2c3e50;">📚 文章目录</h3>

  <div style="margin-top: 20px; border-top: 1px solid #ddd; padding-top: 10px;">
    <h4 style="color: #000 !important;">按分类</h4>
    {% assign all_cats = site.posts | map: 'categories' | flatten | uniq %}
    {% for cat in all_cats %}
      {% if cat != "" %}
        <h4 style="color: #000 !important; margin: 5px 0 !important;">{{ cat }}</h4>
        <ul style="margin: 0 0 10px 20px !important; padding: 0 !important; color: #000 !important;">
          {% for post in site.posts %}
            {% if post.categories contains cat %}
              <li style="margin: 3px 0 !important;">
                <a href="{{ post.url }}" style="color: #007bff !important;">{{ post.title }}</a>
              </li>
            {% endif %}
          {% endfor %}
        </ul>
      {% endif %}
    {% endfor %}
  </div>
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



<!-- 通用切换函数（复用逻辑） -->
<script>
function toggleCategory(item) {
  const targetId = item.getAttribute('data-target');
  const targetEl = document.getElementById(targetId);
  if (!targetEl) return; // 防止找不到元素报错
  if (targetEl.classList.contains('closed')) {
    targetEl.classList.replace('closed', 'open');
    item.innerHTML = item.innerHTML.replace('▶', '▼');
  } else {
    targetEl.classList.replace('open', 'closed');
    item.innerHTML = item.innerHTML.replace('▼', '▶');
  }
}


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
