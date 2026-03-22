## 6. 布局系统

### 6.1 Shell 布局（主框架）

```css
.shell {
  --shell-pad: 16px;
  --shell-gap: 16px;
  --shell-nav-width: 220px;
  --shell-topbar-height: 56px;
  --shell-focus-duration: 200ms;
  --shell-focus-ease: var(--ease-out);

  height: 100vh;
  display: grid;
  grid-template-columns: var(--shell-nav-width) minmax(0, 1fr);
  grid-template-rows: var(--shell-topbar-height) 1fr;
  grid-template-areas:
    "topbar topbar"
    "nav content";
  gap: 0;
  animation: dashboard-enter 0.4s var(--ease-out);
  transition: grid-template-columns var(--shell-focus-duration) var(--shell-focus-ease);
  overflow: hidden;
}

/* 动态视口高度支持 */
@supports (height: 100dvh) {
  .shell {
    height: 100dvh;
  }
}
```

### 6.2 聊天焦点模式

```css
/* 隐藏导航，全屏聊天 */
.shell--chat-focus {
  grid-template-columns: 0px minmax(0, 1fr);
}

.shell--chat-focus .nav {
  width: 0;
  padding: 0;
  border-width: 0;
  overflow: hidden;
  pointer-events: none;
  opacity: 0;
}

.shell--chat-focus .content-header {
  opacity: 0;
  transform: translateY(-8px);
  max-height: 0px;
  padding: 0;
  pointer-events: none;
}
```

### 6.3 顶栏

```css
.topbar {
  grid-area: topbar;
  position: sticky;
  top: 0;
  z-index: 40;
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 16px;
  padding: 0 20px;
  height: var(--shell-topbar-height);
  border-bottom: 1px solid var(--border);
  background: var(--bg);
}

.topbar-left {
  display: flex;
  align-items: center;
  gap: 12px;
}

.topbar-status {
  display: flex;
  align-items: center;
  gap: 8px;
}
```

### 6.4 侧边导航

```css
.nav {
  grid-area: nav;
  overflow-y: auto;
  overflow-x: hidden;
  padding: 16px 12px;
  background: var(--bg);
  scrollbar-width: none;  /* Firefox */
  transition:
    width var(--shell-focus-duration) var(--shell-focus-ease),
    padding var(--shell-focus-duration) var(--shell-focus-ease),
    opacity var(--shell-focus-duration) var(--shell-focus-ease);
  min-height: 0;
}

.nav::-webkit-scrollbar {
  display: none;  /* Chrome/Safari */
}

/* 导航组 */
.nav-group {
  margin-bottom: 20px;
  display: grid;
  gap: 2px;
}

.nav-group__items {
  display: grid;
  gap: 1px;
}

/* 导航标签 */
.nav-label {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 8px;
  width: 100%;
  padding: 6px 10px;
  font-size: 11px;
  font-weight: 500;
  color: var(--muted);
  margin-bottom: 4px;
  background: transparent;
  border: none;
  cursor: pointer;
  text-align: left;
  border-radius: var(--radius-sm);
  transition:
    color var(--duration-fast) ease,
    background var(--duration-fast) ease;
}

.nav-label:hover {
  color: var(--text);
  background: var(--bg-hover);
}
```

### 6.5 导航项

```css
.nav-item {
  position: relative;
  display: flex;
  align-items: center;
  justify-content: flex-start;
  gap: 10px;
  padding: 8px 10px;
  border-radius: var(--radius-md);
  border: 1px solid transparent;
  background: transparent;
  color: var(--muted);
  cursor: pointer;
  text-decoration: none;
  transition:
    border-color var(--duration-fast) ease,
    background var(--duration-fast) ease,
    color var(--duration-fast) ease;
}

.nav-item__icon {
  width: 16px;
  height: 16px;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-shrink: 0;
  opacity: 0.7;
  transition: opacity var(--duration-fast) ease;
}

.nav-item__icon svg {
  width: 16px;
  height: 16px;
  stroke: currentColor;
  fill: none;
  stroke-width: 1.5px;
  stroke-linecap: round;
  stroke-linejoin: round;
}

.nav-item__text {
  font-size: 13px;
  font-weight: 500;
  white-space: nowrap;
}

.nav-item:hover {
  color: var(--text);
  background: var(--bg-hover);
}

.nav-item:hover .nav-item__icon {
  opacity: 1;
}

.nav-item.active {
  color: var(--text-strong);
  background: var(--accent-subtle);
}

.nav-item.active .nav-item__icon {
  opacity: 1;
  color: var(--accent);
}
```

### 6.6 内容区域

```css
.content {
  grid-area: content;
  padding: 12px 16px 32px;
  display: block;
  min-height: 0;
  overflow-y: auto;
  overflow-x: hidden;
}

.content > * + * {
  margin-top: 24px;
}

:root[data-theme="light"] .content {
  background: var(--bg-content);  /* 浅色主题内容区有背景色 */
}

/* 聊天模式 */
.content--chat {
  display: flex;
  flex-direction: column;
  gap: 24px;
  overflow: hidden;
  padding-bottom: 0;
}
```

### 6.7 网格工具类

```css
.grid {
  display: grid;
  gap: 20px;
}

.grid-cols-2 {
  grid-template-columns: repeat(2, minmax(0, 1fr));
}

.grid-cols-3 {
  grid-template-columns: repeat(3, minmax(0, 1fr));
}

.stat-grid {
  display: grid;
  gap: 14px;
  grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
}

.note-grid {
  display: grid;
  gap: 16px;
  grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
}

.row {
  display: flex;
  gap: 12px;
  align-items: center;
}

.stack {
  display: grid;
  gap: 12px;
  grid-template-columns: minmax(0, 1fr);
}

.filters {
  display: flex;
  flex-wrap: wrap;
  gap: 8px;
  align-items: center;
}
```

---
