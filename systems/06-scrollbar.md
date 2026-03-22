## 20. 滚动条和焦点

### 20.1 滚动条样式

```css
/* Webkit 浏览器 */
::-webkit-scrollbar {
  width: 8px;
  height: 8px;
}

::-webkit-scrollbar-track {
  background: transparent;
}

::-webkit-scrollbar-thumb {
  background: var(--border);
  border-radius: var(--radius-full);
}

::-webkit-scrollbar-thumb:hover {
  background: var(--border-strong);
}

/* Firefox */
* {
  scrollbar-width: thin;
  scrollbar-color: var(--border) transparent;
}
```

### 20.2 隐藏滚动条

```css
.nav {
  scrollbar-width: none;  /* Firefox */
}

.nav::-webkit-scrollbar {
  display: none;  /* Chrome/Safari */
}
```

### 20.3 焦点样式

```css
/* 焦点环 */
--focus-ring: 0 0 0 2px var(--bg), 0 0 0 4px var(--ring);

/* 带发光的焦点（用于主要交互元素） */
--focus-glow: 0 0 0 2px var(--bg),
              0 0 0 4px var(--ring),
              0 0 20px var(--accent-glow);

:focus-visible {
  outline: none;
  box-shadow: var(--focus-ring);
}

/* 主要按钮焦点 */
.btn.primary:focus-visible {
  box-shadow: var(--focus-glow);
}
```

### 20.4 选中样式

```css
::selection {
  background: var(--accent-subtle);
  color: var(--text-strong);
}
```

---
