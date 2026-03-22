## 8. 聊天界面

### 8.1 聊天布局

```css
.chat {
  position: relative;
  display: flex;
  flex-direction: column;
  flex: 1 1 0;
  height: 100%;
  min-height: 0;
  overflow: hidden;
  background: transparent !important;
  border: none !important;
}

.chat-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 12px;
  flex-wrap: nowrap;
  flex-shrink: 0;
  padding-bottom: 12px;
  margin-bottom: 12px;
  background: transparent;
}

.chat-thread {
  flex: 1 1 0;
  overflow-y: auto;
  overflow-x: hidden;
  padding: 12px 4px;
  margin: 0 -4px;
  min-height: 0;
  border-radius: 12px;
  background: transparent;
}

/* 粘性输入框 */
.chat-compose {
  position: sticky;
  bottom: 0;
  flex-shrink: 0;
  display: flex;
  flex-direction: column;
  gap: 12px;
  margin-top: auto;
  padding: 12px 4px 4px;
  background: linear-gradient(to bottom, transparent, var(--bg) 20%);
  z-index: 10;
}
```

### 8.2 分组消息布局（Slack风格）

```css
.chat-group {
  display: flex;
  gap: 12px;
  align-items: flex-start;
  margin-bottom: 16px;
  margin-left: 4px;
  margin-right: 16px;
}

/* 用户消息靠右 */
.chat-group.user {
  flex-direction: row-reverse;
  justify-content: flex-start;
}

.chat-group-messages {
  display: flex;
  flex-direction: column;
  gap: 2px;
  max-width: min(900px, calc(100% - 60px));
}

.chat-group.user .chat-group-messages {
  align-items: flex-end;
}

/* 页脚（发送者 + 时间） */
.chat-group-footer {
  display: flex;
  gap: 8px;
  align-items: baseline;
  margin-top: 6px;
}

.chat-sender-name {
  font-weight: 500;
  font-size: 12px;
  color: var(--muted);
}

.chat-group-timestamp {
  font-size: 11px;
  color: var(--muted);
  opacity: 0.7;
}
```

### 8.3 头像

```css
.chat-avatar {
  width: 40px;
  height: 40px;
  border-radius: 8px;
  background: var(--panel-strong);
  display: grid;
  place-items: center;
  font-weight: 600;
  font-size: 14px;
  flex-shrink: 0;
  align-self: flex-end;  /* 与最后一条消息对齐 */
  margin-bottom: 4px;
}

.chat-avatar.user {
  background: var(--accent-subtle);
  color: var(--accent);
}

.chat-avatar.assistant {
  background: var(--secondary);
  color: var(--muted);
}
```

### 8.4 聊天气泡

```css
.chat-bubble {
  position: relative;
  display: inline-block;
  border: 1px solid transparent;
  background: var(--card);
  border-radius: var(--radius-lg);
  padding: 10px 14px;
  box-shadow: none;
  transition:
    background 150ms ease-out,
    border-color 150ms ease-out;
  max-width: 100%;
  word-wrap: break-word;
}

.chat-bubble:hover {
  background: var(--bg-hover);
}

/* 浅色主题恢复边框 */
:root[data-theme="light"] .chat-bubble {
  border-color: var(--border);
  box-shadow: inset 0 1px 0 var(--card-highlight);
}

/* 用户气泡 */
.chat-group.user .chat-bubble {
  background: var(--accent-subtle);
  border-color: transparent;
}

:root[data-theme="light"] .chat-group.user .chat-bubble {
  border-color: rgba(234, 88, 12, 0.2);
  background: rgba(251, 146, 60, 0.12);
}

/* 流式动画 */
.chat-bubble.streaming {
  animation: pulsing-border 1.5s ease-out infinite;
}

@keyframes pulsing-border {
  0%, 100% { border-color: var(--border); }
  50% { border-color: var(--accent); }
}
```

### 8.5 阅读指示器（三个点）

```css
.chat-reading-indicator {
  background: transparent;
  border: 1px solid var(--border);
  padding: 12px;
  display: inline-flex;
}

.chat-reading-indicator__dots {
  display: flex;
  gap: 6px;
  align-items: center;
}

.chat-reading-indicator__dots span {
  width: 6px;
  height: 6px;
  border-radius: 50%;
  background: var(--muted);
  animation: reading-pulse 1.4s ease-in-out infinite;
}

.chat-reading-indicator__dots span:nth-child(1) { animation-delay: 0s; }
.chat-reading-indicator__dots span:nth-child(2) { animation-delay: 0.2s; }
.chat-reading-indicator__dots span:nth-child(3) { animation-delay: 0.4s; }
```

### 8.6 工具卡片

```css
.chat-tool-card {
  border: 1px solid var(--border);
  border-radius: 8px;
  padding: 12px;
  margin-top: 8px;
  background: var(--card);
  box-shadow: inset 0 1px 0 var(--card-highlight);
  transition:
    border-color 150ms ease-out,
    background 150ms ease-out;
  max-height: 120px;
  overflow: hidden;
}

.chat-tool-card:hover {
  border-color: var(--border-strong);
  background: var(--bg-hover);
}

.chat-tool-card__header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 8px;
}

.chat-tool-card__title {
  display: inline-flex;
  align-items: center;
  gap: 6px;
  font-weight: 600;
  font-size: 13px;
  line-height: 1.2;
}

.chat-tool-card__icon {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  width: 16px;
  height: 16px;
  flex-shrink: 0;
}

.chat-tool-card__icon svg {
  width: 14px;
  height: 14px;
  stroke: currentColor;
  fill: none;
  stroke-width: 1.5px;
}

.chat-tool-card__preview {
  font-size: 11px;
  color: var(--muted);
  margin-top: 8px;
  padding: 8px 10px;
  background: var(--secondary);
  border-radius: var(--radius-md);
  white-space: pre-wrap;
  overflow: hidden;
  max-height: 44px;
  line-height: 1.4;
  border: 1px solid var(--border);
}
```

### 8.7 复制按钮

```css
.chat-copy-btn {
  position: absolute;
  top: 6px;
  right: 8px;
  border: 1px solid var(--border);
  background: var(--bg);
  color: var(--muted);
  border-radius: var(--radius-md);
  padding: 4px 6px;
  font-size: 14px;
  line-height: 1;
  cursor: pointer;
  opacity: 0;
  pointer-events: none;
  transition:
    opacity 120ms ease-out,
    background 120ms ease-out;
}

.chat-bubble:hover .chat-copy-btn {
  opacity: 1;
  pointer-events: auto;
}

.chat-copy-btn:hover {
  background: var(--bg-hover);
}

/* 复制成功状态 */
.chat-copy-btn[data-copied="1"] {
  opacity: 1;
  pointer-events: auto;
  border-color: var(--ok-subtle);
  background: var(--ok-subtle);
  color: var(--ok);
}

/* 触摸设备始终显示 */
@media (hover: none) {
  .chat-copy-btn {
    opacity: 1;
    pointer-events: auto;
  }
}
```

---
