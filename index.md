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
  width: 100%;        /* 小屏幕占满 */
  max-width: 1200px;  /* 大屏幕限制宽度，避免左右块过度拉伸 */
  align-items: stretch; /* 保持左右/中块等高 */
  box-sizing: border-box; /* 防止padding撑大容器导致遮挡 */
     /*overflow: hidden; 防止子元素溢出遮挡 */
}

/* 左侧四级目录栏 */
.sidebar {
  position: relative;
  flex: 0 0 32%;
  width: 32%;
  max-width: 360px;
  min-width: 200px;
  background: #f8f9fa;
  padding: 15px;
  border-radius: 8px;
  border: 1px solid #eee;
  max-height: 180vh;
  overflow-y: auto;
  box-sizing: border-box;
  color: #2c3e50 !important;
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

/* Improved sidebar typography and collapsible categories */
.sidebar { font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, 'Helvetica Neue', Arial; font-size: 14px; }
.sidebar .section-title { display:inline-block; margin:0; font-size:1.05em; color:#22313F; }
.categories-header { display:flex; justify-content:space-between; align-items:center; gap:8px; }
.sidebar-toggle { background:transparent; border:1px solid #e1e4e8; color:#34495e; padding:4px 8px; border-radius:6px; cursor:pointer; font-size:0.85em; }
.sidebar .sidebar-toggle { position: absolute; right: -56px; top: 12px; box-shadow: 0 1px 4px rgba(0,0,0,0.06); background:#fff; }
.category-block { margin:6px 0; }
.category-header { display:flex; align-items:center; gap:8px; cursor:pointer; margin:6px 0; font-weight:600; color:#2c3e50; }
.category-header .caret { display:inline-block; transition: transform 0.18s ease; color:#3498db; }
.category-list { margin: 0 0 10px 16px; padding: 0; list-style: none; overflow: hidden; max-height: 1000px; transition: max-height 0.28s ease; }
.category-list.closed { max-height: 0 !important; }
.category-list li { margin: 4px 0; padding-left: 6px; border-left: 2px solid transparent; }
.category-list li a { color:#0066cc; text-decoration:none; font-weight:500; }
.category-list li a:hover { text-decoration:underline; }

.sidebar.collapsed { width:64px; min-width:64px; overflow:hidden; }
.sidebar.collapsed .section-title,
.sidebar.collapsed .cat-name,
.sidebar.collapsed .category-list { display:none !important; }
.sidebar.collapsed .category-header { justify-content:center; }
.sidebar.collapsed .category-header .caret { transform: rotate(90deg); }

/* ensure main content can shrink properly */
.profile { min-width: 0; }
</style>

<!-- 主体布局：左侧目录 + 右侧简介 -->
<div class="container">
  <!-- 左侧：目录 -->
  <div class="sidebar">
    <h3 style="margin-top: 0; color: #2c3e50;">📚 文章目录</h3>

  <div style="margin-top: 20px; border-top: 1px solid #ddd; padding-top: 10px;">
    <div class="categories-header">
      <h4 class="section-title">按分类</h4>
      <button id="sidebar-toggle" class="sidebar-toggle" aria-label="Toggle sidebar">收起</button>
    </div>
    {% assign all_cats = site.posts | map: 'categories' | flatten | uniq %}
    {% for cat in all_cats %}
      {% if cat != "" %}
        <div class="category-block">
          <h4 class="category-header" data-target="cat-{{ forloop.index }}"><span class="caret">▶</span><span class="cat-name">{{ cat }}</span></h4>
          <ul id="cat-{{ forloop.index }}" class="category-list open">
            {% for post in site.posts %}
              {% if post.categories contains cat %}
                <li>
                  <a href="{{ post.url }}">{{ post.title }}</a>
                </li>
              {% endif %}
            {% endfor %}
          </ul>
        </div>
      {% endif %}
    {% endfor %}
  </div>
</div>
   
<div class="profile">
    <h2 style="color: #2c3e50; margin-top: 0;">👋 每日三省吾身</h2>
    <div style="line-height: 1.8; font-size: 1.1em; color: #34495e;">
      <p>Stay hungry</p>
      <p>Stay foolish</p>
      <p>Do not multiply entity beyond necessity</p>

      <!-- 刮刮乐交互区 -->
      <div class="scratch-container" style="margin:12px 0;">
        <div class="scratch-card" style="width:260px; height:90px; border-radius:8px; overflow:hidden; box-shadow: 0 2px 6px rgba(0,0,0,0.08); position:relative;">
          <div class="scratch-back" style="width:100%; height:100%; display:flex; align-items:center; justify-content:center; background: linear-gradient(135deg,#fef9e7,#ecf8ff); font-weight:700; color:#2c3e50; font-size:1.05em;">
            MBTI: <span id="mbti-value" style="margin-left:8px; color:#e74c3c;">INTJ</span>
          </div>
          <canvas id="scratch-canvas" style="position:absolute; top:0; left:0; width:100%; height:100%; display:block;"></canvas>
        </div>
        <div style="font-size:0.85em; color:#7f8c8d; margin-top:6px;">刮开涂层查看我的MBTI（鼠标/手指拖动）</div>
      </div>

      <script>
      (function(){
        const canvas = document.getElementById('scratch-canvas');
        if(!canvas) return;
        const card = canvas.parentElement;
        const ctx = canvas.getContext('2d');
        const dpr = window.devicePixelRatio || 1;

        function setup(){
          const w = card.clientWidth;
          const h = card.clientHeight;
          canvas.width = Math.max(1, Math.floor(w * dpr));
          canvas.height = Math.max(1, Math.floor(h * dpr));
          canvas.style.width = w + 'px';
          canvas.style.height = h + 'px';
          ctx.setTransform(dpr,0,0,dpr,0,0);
          ctx.clearRect(0,0,w,h);
          ctx.fillStyle = '#bdbdbd';
          ctx.fillRect(0,0,w,h);
          ctx.fillStyle = '#8c8c8c';
          ctx.font = '14px sans-serif';
          ctx.textAlign = 'center';
          ctx.fillText('刮开这里', w/2, h/2 + 6);
        }

        let isDrawing = false;

        function getPointerPos(e){
          const rect = canvas.getBoundingClientRect();
          return { x: (e.clientX - rect.left), y: (e.clientY - rect.top) };
        }

        function scratchAt(x,y){
          ctx.globalCompositeOperation = 'destination-out';
          ctx.beginPath();
          ctx.arc(x, y, 18, 0, Math.PI*2);
          ctx.fill();
        }

        function pointerDown(e){
          isDrawing = true;
          canvas.setPointerCapture(e.pointerId);
          const p = getPointerPos(e);
          scratchAt(p.x, p.y);
        }
        function pointerMove(e){ if(!isDrawing) return; const p = getPointerPos(e); scratchAt(p.x, p.y); }
        function pointerUp(e){ isDrawing = false; try { canvas.releasePointerCapture(e.pointerId); } catch(_){} checkClear(); }

        function checkClear(){
          try{
            const img = ctx.getImageData(0,0,canvas.width,canvas.height);
            let trans = 0;
            for(let i = 3; i < img.data.length; i += 4){ if(img.data[i] === 0) trans++; }
            const total = img.data.length / 4;
            if(trans / total > 0.45){ ctx.clearRect(0,0,canvas.width,canvas.height); canvas.style.pointerEvents = 'none'; }
          }catch(e){/* security or read error: ignore */}
        }

        // events
        canvas.addEventListener('pointerdown', pointerDown);
        canvas.addEventListener('pointermove', pointerMove);
        window.addEventListener('pointerup', pointerUp);

        window.addEventListener('resize', setup);
        setup();
      })();
      </script>

      <h3 style="color: #2980b9;">📞 联系方式</h3>
      <p>邮箱：<a href="mailto:zhaoyige1@163.com" style="color: #3498db; text-decoration: none;">
      <span class="copyable-text" data-copy="zhaoyige1@163.com">zhaoyige1@163.com</span></a></p>
      <p>微信：<span class="copyable-text" data-copy="_iacgnaixihcub">_iacgnaixihcub</span></p>
      <p>GitHub：<a href="https://github.com/viggo1" target="_blank" style="color: #3498db;">https://github.com/viggo1</a></p>
      <h3 style="color: #2980b9;">📊 博客数据</h3>
      <p>总文章数：<span style="font-weight: bold; color: #e74c3c;">{{ site.posts.size }}</span> 篇</p>
      <p>最后更新：<span style="color: #7f8c8d;">{{ site.posts.first.date | date: "%Y-%m-%d" }}</span></p>
      
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

<!-- Sidebar collapse/expand behavior for categories -->
<script>
document.addEventListener('DOMContentLoaded', function(){
  const headers = document.querySelectorAll('.category-header');
  headers.forEach(h => {
    h.addEventListener('click', () => {
      const id = h.getAttribute('data-target');
      const list = document.getElementById(id);
      if(!list) return;
      const caret = h.querySelector('.caret');
      if(list.classList.contains('closed')){
        list.classList.remove('closed');
        caret.style.transform = 'rotate(0deg)';
      } else {
        list.classList.add('closed');
        caret.style.transform = 'rotate(90deg)';
      }
    });
  });

  const sidebarToggle = document.getElementById('sidebar-toggle');
  const sidebar = document.querySelector('.sidebar');
  if(sidebarToggle && sidebar){
    sidebarToggle.addEventListener('click', () => {
      if(sidebar.classList.contains('collapsed')){
        sidebar.classList.remove('collapsed');
        sidebarToggle.textContent = '收起';
      } else {
        sidebar.classList.add('collapsed');
        sidebarToggle.textContent = '展开';
      }
    });
  }
});
</script>
