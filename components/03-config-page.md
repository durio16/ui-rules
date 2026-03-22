## 9. 配置页面

### 9.1 配置布局

```css
.config-layout {
  display: grid;
  grid-template-columns: 260px minmax(0, 1fr);
  gap: 0;
  height: calc(100vh - 160px);
  margin: -16px;
  border-radius: var(--radius-xl);
  overflow: hidden;
  border: 1px solid var(--border);
  background: var(--panel);
}
```

### 9.2 配置侧边栏

```css
.config-sidebar {
  display: flex;
  flex-direction: column;
  background: var(--bg-accent);
  border-right: 1px solid var(--border);
  min-height: 0;
  overflow: hidden;
}

:root[data-theme="light"] .config-sidebar {
  background: var(--bg-hover);
}

.config-sidebar__header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 18px 18px;
  border-bottom: 1px solid var(--border);
}

.config-sidebar__title {
  font-weight: 600;
  font-size: 14px;
  letter-spacing: -0.01em;
}
```

### 9.3 配置搜索

```css
.config-search {
  position: relative;
  padding: 14px;
  border-bottom: 1px solid var(--border);
}

.config-search__icon {
  position: absolute;
  left: 28px;
  top: 50%;
  transform: translateY(-50%);
  width: 16px;
  height: 16px;
  color: var(--muted);
  pointer-events: none;
}

.config-search__input {
  width: 100%;
  padding: 11px 36px 11px 42px;
  border: 1px solid var(--border);
  border-radius: var(--radius-md);
  background: var(--bg-elevated);
  font-size: 13px;
  outline: none;
  transition:
    border-color var(--duration-fast) ease,
    box-shadow var(--duration-fast) ease,
    background var(--duration-fast) ease;
}

.config-search__input::placeholder {
  color: var(--muted);
}

.config-search__input:focus {
  border-color: var(--accent);
  box-shadow: var(--focus-ring);
  background: var(--bg-hover);
}
```

### 9.4 配置导航项

```css
.config-nav__item {
  display: flex;
  align-items: center;
  gap: 12px;
  width: 100%;
  padding: 11px 14px;
  border: none;
  border-radius: var(--radius-md);
  background: transparent;
  color: var(--muted);
  font-size: 13px;
  font-weight: 500;
  text-align: left;
  cursor: pointer;
  transition:
    background var(--duration-fast) ease,
    color var(--duration-fast) ease;
}

.config-nav__item:hover {
  background: var(--bg-hover);
  color: var(--text);
}

.config-nav__item.active {
  background: var(--accent-subtle);
  color: var(--accent);
}

.config-nav__icon {
  width: 20px;
  height: 20px;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 15px;
  opacity: 0.7;
}

.config-nav__item:hover .config-nav__icon,
.config-nav__item.active .config-nav__icon {
  opacity: 1;
}
```

### 9.5 配置区块卡片

```css
.config-section-card {
  border: 1px solid var(--border);
  border-radius: var(--radius-lg);
  background: var(--bg-elevated);
  overflow: hidden;
  transition: border-color var(--duration-fast) ease;
}

.config-section-card:hover {
  border-color: var(--border-strong);
}

:root[data-theme="light"] .config-section-card {
  background: white;
}

.config-section-card__header {
  display: flex;
  align-items: flex-start;
  gap: 16px;
  padding: 20px 22px;
  background: var(--bg-accent);
  border-bottom: 1px solid var(--border);
}

.config-section-card__icon {
  width: 34px;
  height: 34px;
  color: var(--accent);
  flex-shrink: 0;
}

.config-section-card__title {
  margin: 0;
  font-size: 17px;
  font-weight: 600;
  letter-spacing: -0.01em;
}

.config-section-card__desc {
  margin: 5px 0 0;
  font-size: 13px;
  color: var(--muted);
  line-height: 1.45;
}

.config-section-card__content {
  padding: 22px;
}
```

---
