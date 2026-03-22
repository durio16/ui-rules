## 16. 响应式设计

### 16.1 断点

| 断点 | 宽度 | 描述 |
|-----|------|-----|
| Desktop | > 1100px | 完整侧边栏 + 内容 |
| Tablet | 601-1100px | 水平导航 + 内容 |
| Mobile | 401-600px | 简化导航 + 内容 |
| Small Mobile | ≤ 400px | 最小化UI |

### 16.2 平板布局（1100px 及以下）

```css
@media (max-width: 1100px) {
  .shell {
    --shell-pad: 12px;
    --shell-gap: 12px;
    grid-template-columns: 1fr;
    grid-template-rows: auto auto 1fr;
    grid-template-areas:
      "topbar"
      "nav"
      "content";
  }

  .nav {
    position: static;
    max-height: none;
    display: flex;
    gap: 6px;
    overflow-x: auto;
    border-right: none;
    border-bottom: 1px solid var(--border);
    padding: 10px 14px;
    background: var(--bg);
    -webkit-overflow-scrolling: touch;
    scrollbar-width: none;
  }

  .nav::-webkit-scrollbar {
    display: none;
  }

  .nav-group {
    display: contents;
  }

  .nav-label {
    display: none;
  }

  .nav-item {
    padding: 8px 14px;
    font-size: 13px;
    border-radius: var(--radius-md);
    white-space: nowrap;
    flex-shrink: 0;
  }

  .grid-cols-2,
  .grid-cols-3 {
    grid-template-columns: 1fr;
  }
}
```

### 16.3 移动端布局（600px 及以下）

```css
@media (max-width: 600px) {
  .shell {
    --shell-pad: 8px;
    --shell-gap: 8px;
  }

  .topbar {
    padding: 10px 12px;
    gap: 8px;
  }

  .brand-title { font-size: 14px; }
  .brand-sub { display: none; }

  .nav {
    padding: 8px 10px;
    gap: 4px;
  }

  .nav-item {
    padding: 6px 10px;
    font-size: 12px;
  }

  .content-header { display: none; }

  .content {
    padding: 4px 4px 16px;
    gap: 12px;
  }

  .card {
    padding: 12px;
    border-radius: var(--radius-md);
  }

  .card-title { font-size: 13px; }

  .stat-grid {
    gap: 8px;
    grid-template-columns: repeat(2, 1fr);
  }

  .stat {
    padding: 10px;
    border-radius: var(--radius-md);
  }

  .stat-value { font-size: 18px; }

  .btn {
    padding: 8px 12px;
    font-size: 12px;
  }

  .chat-bubble {
    padding: 8px 12px;
    border-radius: var(--radius-md);
  }

  .chat-msg { max-width: 90%; }

  .theme-toggle {
    --theme-item: 24px;
    --theme-gap: 2px;
    --theme-pad: 3px;
  }

  .theme-icon {
    width: 12px;
    height: 12px;
  }
}
```

### 16.4 超小屏幕（400px 及以下）

```css
@media (max-width: 400px) {
  .shell { --shell-pad: 4px; }
  .topbar { padding: 8px 10px; }
  .brand-title { font-size: 13px; }
  .nav { padding: 6px 8px; }
  .nav-item { padding: 6px 8px; font-size: 11px; }
  .content { padding: 4px 4px 12px; gap: 10px; }
  .card { padding: 10px; }
  .stat { padding: 8px; }
  .stat-value { font-size: 16px; }
  .btn { padding: 6px 10px; font-size: 11px; }
  .chat-bubble { padding: 8px 10px; }

  .topbar-status .pill {
    padding: 3px 6px;
    font-size: 10px;
  }

  .theme-toggle {
    --theme-item: 22px;
    --theme-gap: 2px;
    --theme-pad: 2px;
  }

  .theme-icon {
    width: 11px;
    height: 11px;
  }
}
```

---
