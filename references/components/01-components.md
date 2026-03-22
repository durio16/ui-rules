## 7. 组件详解

### 7.1 卡片

```css
.card {
  border: 1px solid var(--border);
  background: var(--card);
  border-radius: var(--radius-lg);
  padding: 20px;
  animation: rise 0.35s var(--ease-out) backwards;
  transition:
    border-color var(--duration-normal) var(--ease-out),
    box-shadow var(--duration-normal) var(--ease-out),
    transform var(--duration-normal) var(--ease-out);
  box-shadow:
    var(--shadow-sm),
    inset 0 1px 0 var(--card-highlight);  /* 关键：顶部内发光 */
}

.card:hover {
  border-color: var(--border-strong);
  box-shadow:
    var(--shadow-md),
    inset 0 1px 0 var(--card-highlight);
}
```

### 7.2 统计卡片

```css
.stat {
  background: var(--card);
  border-radius: var(--radius-md);
  padding: 14px 16px;
  border: 1px solid var(--border);
  transition:
    border-color var(--duration-normal) var(--ease-out),
    box-shadow var(--duration-normal) var(--ease-out);
  box-shadow: inset 0 1px 0 var(--card-highlight);
}

.stat:hover {
  border-color: var(--border-strong);
  box-shadow:
    var(--shadow-sm),
    inset 0 1px 0 var(--card-highlight);
}

.stat-label {
  color: var(--muted);
  font-size: 11px;
  font-weight: 500;
  text-transform: uppercase;
  letter-spacing: 0.04em;
}

.stat-value {
  font-size: 24px;
  font-weight: 700;
  margin-top: 6px;
  letter-spacing: -0.03em;
  line-height: 1.1;
}

.stat-value.ok { color: var(--ok); }
.stat-value.warn { color: var(--warn); }
```

### 7.3 按钮

```css
.btn {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  gap: 8px;
  border: 1px solid var(--border);
  background: var(--bg-elevated);
  padding: 9px 16px;
  border-radius: var(--radius-md);
  font-size: 13px;
  font-weight: 500;
  letter-spacing: -0.01em;
  cursor: pointer;
  transition:
    border-color var(--duration-fast) var(--ease-out),
    background var(--duration-fast) var(--ease-out),
    box-shadow var(--duration-fast) var(--ease-out),
    transform var(--duration-fast) var(--ease-out);
}

.btn:hover {
  background: var(--bg-hover);
  border-color: var(--border-strong);
  transform: translateY(-1px);  /* 微妙上浮 */
  box-shadow: var(--shadow-sm);
}

.btn:active {
  background: var(--secondary);
  transform: translateY(0);
  box-shadow: none;
}

.btn svg {
  width: 16px;
  height: 16px;
  stroke: currentColor;
  fill: none;
  stroke-width: 1.5px;
  stroke-linecap: round;
  stroke-linejoin: round;
  flex-shrink: 0;
}

/* 主要按钮 */
.btn.primary {
  border-color: var(--accent);
  background: var(--accent);
  color: var(--primary-foreground);
  box-shadow: 0 1px 2px rgba(0, 0, 0, 0.2);
}

.btn.primary:hover {
  background: var(--accent-hover);
  border-color: var(--accent-hover);
  box-shadow:
    var(--shadow-md),
    0 0 20px var(--accent-glow);  /* 发光效果 */
}

/* 活动状态 */
.btn.active {
  border-color: var(--accent);
  background: var(--accent-subtle);
  color: var(--accent);
}

/* 危险按钮 */
.btn.danger {
  border-color: transparent;
  background: var(--danger-subtle);
  color: var(--danger);
}

.btn.danger:hover {
  background: rgba(239, 68, 68, 0.15);
}

/* 小按钮 */
.btn--sm {
  padding: 6px 10px;
  font-size: 12px;
}

/* 禁用状态 */
.btn:disabled {
  opacity: 0.5;
  cursor: not-allowed;
}
```

### 7.4 键盘快捷键徽章

```css
.btn-kbd {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  margin-left: 6px;
  padding: 2px 5px;
  font-family: var(--mono);
  font-size: 11px;
  font-weight: 500;
  line-height: 1;
  border-radius: 4px;
  background: rgba(255, 255, 255, 0.15);
  color: inherit;
  opacity: 0.8;
}

.btn.primary .btn-kbd {
  background: rgba(255, 255, 255, 0.2);
}

:root[data-theme="light"] .btn-kbd {
  background: rgba(0, 0, 0, 0.08);
}
```

### 7.5 Pills 和 Chips

```css
.pill {
  display: inline-flex;
  align-items: center;
  gap: 6px;
  border: 1px solid var(--border);
  padding: 6px 12px;
  border-radius: var(--radius-full);
  background: var(--secondary);
  font-size: 13px;
  font-weight: 500;
  transition: border-color var(--duration-fast) ease;
}

.pill:hover {
  border-color: var(--border-strong);
}

.pill.danger {
  border-color: var(--danger-subtle);
  background: var(--danger-subtle);
  color: var(--danger);
}

/* Chips - 更紧凑 */
.chip {
  font-size: 12px;
  font-weight: 500;
  border: 1px solid var(--border);
  border-radius: var(--radius-full);
  padding: 5px 12px;
  color: var(--muted);
  background: var(--secondary);
  transition:
    border-color var(--duration-fast) var(--ease-out),
    background var(--duration-fast) var(--ease-out),
    transform var(--duration-fast) var(--ease-out);
}

.chip:hover {
  border-color: var(--border-strong);
  transform: translateY(-1px);
}

.chip-ok {
  color: var(--ok);
  border-color: rgba(34, 197, 94, 0.3);
  background: var(--ok-subtle);
}

.chip-warn {
  color: var(--warn);
  border-color: rgba(245, 158, 11, 0.3);
  background: var(--warn-subtle);
}
```

### 7.6 状态指示器

```css
.statusDot {
  width: 8px;
  height: 8px;
  border-radius: var(--radius-full);
  background: var(--danger);
  box-shadow: 0 0 8px rgba(239, 68, 68, 0.5);  /* 发光效果 */
  animation: pulse-subtle 2s ease-in-out infinite;
}

.statusDot.ok {
  background: var(--ok);
  box-shadow: 0 0 8px rgba(34, 197, 94, 0.5);
  animation: none;  /* 成功状态不需要脉冲 */
}
```

### 7.7 主题切换器

```css
.theme-toggle {
  --theme-item: 28px;
  --theme-gap: 2px;
  --theme-pad: 4px;
  position: relative;
}

.theme-toggle__track {
  position: relative;
  display: grid;
  grid-template-columns: repeat(3, var(--theme-item));
  gap: var(--theme-gap);
  padding: var(--theme-pad);
  border-radius: var(--radius-full);
  border: 1px solid var(--border);
  background: var(--secondary);
}

/* 滑动指示器 */
.theme-toggle__indicator {
  position: absolute;
  top: 50%;
  left: var(--theme-pad);
  width: var(--theme-item);
  height: var(--theme-item);
  border-radius: var(--radius-full);
  transform: translateY(-50%)
    translateX(calc(var(--theme-index, 0) * (var(--theme-item) + var(--theme-gap))));
  background: var(--accent);
  transition: transform var(--duration-normal) var(--ease-out);
  z-index: 0;
}

.theme-toggle__button {
  height: var(--theme-item);
  width: var(--theme-item);
  display: grid;
  place-items: center;
  border: 0;
  border-radius: var(--radius-full);
  background: transparent;
  color: var(--muted);
  cursor: pointer;
  position: relative;
  z-index: 1;
  transition: color var(--duration-fast) ease;
}

.theme-toggle__button:hover {
  color: var(--text);
}

.theme-toggle__button.active {
  color: var(--accent-foreground);
}

.theme-icon {
  width: 14px;
  height: 14px;
  stroke: currentColor;
  fill: none;
  stroke-width: 1.5px;
  stroke-linecap: round;
  stroke-linejoin: round;
}
```

### 7.8 Callouts（提示框）

```css
.callout {
  padding: 14px 16px;
  border-radius: var(--radius-md);
  background: var(--secondary);
  border: 1px solid var(--border);
  font-size: 13px;
  line-height: 1.5;
  position: relative;
}

.callout.danger {
  border-color: rgba(239, 68, 68, 0.25);
  background: linear-gradient(135deg, rgba(239, 68, 68, 0.08) 0%, rgba(239, 68, 68, 0.04) 100%);
  color: var(--danger);
}

.callout.info {
  border-color: rgba(59, 130, 246, 0.25);
  background: linear-gradient(135deg, rgba(59, 130, 246, 0.08) 0%, rgba(59, 130, 246, 0.04) 100%);
  color: var(--info);
}

.callout.success {
  border-color: rgba(34, 197, 94, 0.25);
  background: linear-gradient(135deg, rgba(34, 197, 94, 0.08) 0%, rgba(34, 197, 94, 0.04) 100%);
  color: var(--ok);
}
```

---
