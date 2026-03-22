## 4. 间距和圆角

### 4.1 圆角系统

```css
--radius-sm: 6px;     /* 小元素：标签、小按钮、inline-code */
--radius-md: 8px;     /* 默认：按钮、输入框、导航项 */
--radius-lg: 12px;    /* 卡片、面板、聊天气泡 */
--radius-xl: 16px;    /* 大容器、对话框、配置页面 */
--radius-full: 9999px; /* 圆形：头像、徽章、pill */
--radius: 8px;        /* 快捷变量 = md */
```

### 4.2 阴影系统

```css
/* ========== 深色主题阴影 ========== */
/* 特点：更重的阴影 + 微妙的内边框高亮 */
--shadow-sm: 0 1px 2px rgba(0, 0, 0, 0.2);
--shadow-md: 0 4px 12px rgba(0, 0, 0, 0.25),
             0 0 0 1px rgba(255, 255, 255, 0.03);  /* 边缘高亮 */
--shadow-lg: 0 12px 28px rgba(0, 0, 0, 0.35),
             0 0 0 1px rgba(255, 255, 255, 0.03);
--shadow-xl: 0 24px 48px rgba(0, 0, 0, 0.4),
             0 0 0 1px rgba(255, 255, 255, 0.03);
--shadow-glow: 0 0 30px var(--accent-glow);  /* 强调发光 */

/* ========== 浅色主题阴影 ========== */
/* 特点：更轻的阴影 */
--shadow-sm: 0 1px 2px rgba(0, 0, 0, 0.06);
--shadow-md: 0 4px 12px rgba(0, 0, 0, 0.08),
             0 0 0 1px rgba(0, 0, 0, 0.04);
--shadow-lg: 0 12px 28px rgba(0, 0, 0, 0.12),
             0 0 0 1px rgba(0, 0, 0, 0.04);
--shadow-xl: 0 24px 48px rgba(0, 0, 0, 0.15),
             0 0 0 1px rgba(0, 0, 0, 0.04);
--shadow-glow: 0 0 24px var(--accent-glow);
```

### 4.3 内部高亮（Card Highlight）

深色UI的重要技巧 - 顶部内发光创造深度感：

```css
.card {
  box-shadow: var(--shadow-sm),
              inset 0 1px 0 var(--card-highlight);  /* 顶部内发光 */
}

.card:hover {
  box-shadow: var(--shadow-md),
              inset 0 1px 0 var(--card-highlight);
}
```

---
