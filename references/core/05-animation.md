## 5. 动画系统

### 5.1 缓动函数

```css
/* 默认出场 - 快速开始，平滑结束 */
--ease-out: cubic-bezier(0.16, 1, 0.3, 1);

/* 双向缓动 */
--ease-in-out: cubic-bezier(0.4, 0, 0.2, 1);

/* 弹性效果 - 轻微过冲 */
--ease-spring: cubic-bezier(0.34, 1.56, 0.64, 1);
```

### 5.2 持续时间

```css
--duration-fast: 120ms;    /* 微交互：hover、focus */
--duration-normal: 200ms;  /* 标准过渡：展开、收起 */
--duration-slow: 350ms;    /* 复杂动画：页面转场 */
```

### 5.3 关键帧动画

```css
/* 上升进入 - 用于卡片、列表项 */
@keyframes rise {
  from {
    opacity: 0;
    transform: translateY(8px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

/* 淡入 - 通用 */
@keyframes fade-in {
  from { opacity: 0; }
  to { opacity: 1; }
}

/* 缩放进入 - 用于模态框 */
@keyframes scale-in {
  from {
    opacity: 0;
    transform: scale(0.95);
  }
  to {
    opacity: 1;
    transform: scale(1);
  }
}

/* 仪表盘进入 - 更大的位移 */
@keyframes dashboard-enter {
  from {
    opacity: 0;
    transform: translateY(12px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

/* 骨架屏闪烁 - 加载占位符 */
@keyframes shimmer {
  0% { background-position: -200% 0; }
  100% { background-position: 200% 0; }
}

/* 微妙脉冲 - 状态指示器 */
@keyframes pulse-subtle {
  0%, 100% { opacity: 1; }
  50% { opacity: 0.7; }
}

/* 发光脉冲 - 强调元素 */
@keyframes glow-pulse {
  0%, 100% { box-shadow: 0 0 0 rgba(255, 92, 92, 0); }
  50% { box-shadow: 0 0 20px var(--accent-glow); }
}

/* 旋转 - 加载动画 */
@keyframes spin {
  to { transform: rotate(360deg); }
}

/* 聊天流式脉冲 - 边框颜色变化 */
@keyframes chatStreamPulse {
  0%, 100% { border-color: var(--border); }
  50% { border-color: var(--accent); }
}

/* 阅读指示器点动画 */
@keyframes reading-pulse {
  0%, 60%, 100% {
    opacity: 0.3;
    transform: scale(0.8);
  }
  30% {
    opacity: 1;
    transform: scale(1);
  }
}
```

### 5.4 交错动画

```css
.stagger-1 { animation-delay: 0ms; }
.stagger-2 { animation-delay: 50ms; }
.stagger-3 { animation-delay: 100ms; }
.stagger-4 { animation-delay: 150ms; }
.stagger-5 { animation-delay: 200ms; }
.stagger-6 { animation-delay: 250ms; }
```

### 5.5 减少动画偏好

```css
@media (prefers-reduced-motion: reduce) {
  .chat-bubble.streaming {
    animation: none;
    border-color: var(--accent);  /* 静态高亮代替动画 */
  }

  .chat-reading-indicator__dots > span {
    animation: none;
    opacity: 0.6;
  }
}
```

---
