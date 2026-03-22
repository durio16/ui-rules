## 10. 表单控件

### 10.1 基础输入框

```css
.cfg-input {
  flex: 1;
  padding: 11px 14px;
  border: 1px solid var(--border-strong);
  border-radius: var(--radius-md);
  background: var(--bg-accent);
  font-size: 14px;
  outline: none;
  transition:
    border-color var(--duration-fast) ease,
    box-shadow var(--duration-fast) ease,
    background var(--duration-fast) ease;
}

.cfg-input::placeholder {
  color: var(--muted);
  opacity: 0.7;
}

.cfg-input:focus {
  border-color: var(--accent);
  box-shadow: var(--focus-ring);
  background: var(--bg-hover);
}

:root[data-theme="light"] .cfg-input {
  background: white;
}
```

### 10.2 文本域

```css
.cfg-textarea {
  width: 100%;
  padding: 12px 14px;
  border: 1px solid var(--border-strong);
  border-radius: var(--radius-md);
  background: var(--bg-accent);
  font-family: var(--mono);
  font-size: 13px;
  line-height: 1.55;
  resize: vertical;
  outline: none;
  transition:
    border-color var(--duration-fast) ease,
    box-shadow var(--duration-fast) ease;
}

.cfg-textarea:focus {
  border-color: var(--accent);
  box-shadow: var(--focus-ring);
}
```

### 10.3 下拉选择

```css
.cfg-select {
  padding: 11px 40px 11px 14px;
  border: 1px solid var(--border-strong);
  border-radius: var(--radius-md);
  background-color: var(--bg-accent);
  background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='16' height='16' viewBox='0 0 24 24' fill='none' stroke='%23888' stroke-width='2'%3E%3Cpolyline points='6 9 12 15 18 9'%3E%3C/polyline%3E%3C/svg%3E");
  background-repeat: no-repeat;
  background-position: right 12px center;
  font-size: 14px;
  cursor: pointer;
  outline: none;
  appearance: none;
  transition:
    border-color var(--duration-fast) ease,
    box-shadow var(--duration-fast) ease;
}

.cfg-select:focus {
  border-color: var(--accent);
  box-shadow: var(--focus-ring);
}
```

### 10.4 数字输入

```css
.cfg-number {
  display: inline-flex;
  border: 1px solid var(--border-strong);
  border-radius: var(--radius-md);
  overflow: hidden;
  background: var(--bg-accent);
}

.cfg-number__btn {
  width: 44px;
  border: none;
  background: var(--bg-elevated);
  color: var(--text);
  font-size: 18px;
  font-weight: 300;
  cursor: pointer;
  transition: background var(--duration-fast) ease;
}

.cfg-number__btn:hover:not(:disabled) {
  background: var(--bg-hover);
}

.cfg-number__btn:disabled {
  opacity: 0.4;
  cursor: not-allowed;
}

.cfg-number__input {
  width: 85px;
  padding: 11px;
  border: none;
  border-left: 1px solid var(--border);
  border-right: 1px solid var(--border);
  background: transparent;
  font-size: 14px;
  text-align: center;
  outline: none;
  -moz-appearance: textfield;
}

.cfg-number__input::-webkit-outer-spin-button,
.cfg-number__input::-webkit-inner-spin-button {
  -webkit-appearance: none;
  margin: 0;
}
```

### 10.5 分段控件

```css
.cfg-segmented {
  display: inline-flex;
  padding: 4px;
  border: 1px solid var(--border);
  border-radius: var(--radius-md);
  background: var(--bg-accent);
}

.cfg-segmented__btn {
  padding: 9px 18px;
  border: none;
  border-radius: var(--radius-sm);
  background: transparent;
  color: var(--muted);
  font-size: 13px;
  font-weight: 500;
  cursor: pointer;
  transition:
    background var(--duration-fast) ease,
    color var(--duration-fast) ease,
    box-shadow var(--duration-fast) ease;
}

.cfg-segmented__btn:hover:not(:disabled):not(.active) {
  color: var(--text);
}

.cfg-segmented__btn.active {
  background: var(--accent);
  color: white;
  box-shadow: var(--shadow-sm);
}
```

### 10.6 开关切换

```css
.cfg-toggle-row {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 18px;
  padding: 16px 18px;
  border: 1px solid var(--border);
  border-radius: var(--radius-lg);
  background: var(--bg-accent);
  cursor: pointer;
  transition:
    background var(--duration-fast) ease,
    border-color var(--duration-fast) ease;
}

.cfg-toggle-row:hover:not(.disabled) {
  background: var(--bg-hover);
  border-color: var(--border-strong);
}

.cfg-toggle {
  position: relative;
  flex-shrink: 0;
}

.cfg-toggle input {
  position: absolute;
  opacity: 0;
  width: 0;
  height: 0;
}

.cfg-toggle__track {
  display: block;
  width: 50px;
  height: 28px;
  background: var(--bg-elevated);
  border: 1px solid var(--border-strong);
  border-radius: var(--radius-full);
  position: relative;
  transition:
    background var(--duration-normal) ease,
    border-color var(--duration-normal) ease;
}

.cfg-toggle__track::after {
  content: "";
  position: absolute;
  top: 3px;
  left: 3px;
  width: 20px;
  height: 20px;
  background: var(--text);
  border-radius: var(--radius-full);
  box-shadow: var(--shadow-sm);
  transition:
    transform var(--duration-normal) var(--ease-out),
    background var(--duration-normal) ease;
}

.cfg-toggle input:checked + .cfg-toggle__track {
  background: var(--ok-subtle);
  border-color: rgba(34, 197, 94, 0.4);
}

.cfg-toggle input:checked + .cfg-toggle__track::after {
  transform: translateX(22px);
  background: var(--ok);
}

.cfg-toggle input:focus + .cfg-toggle__track {
  box-shadow: var(--focus-ring);
}
```

---
