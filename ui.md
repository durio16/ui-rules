# OpenClaw UI Skill Guide - 完整版

> 这是一个极其详尽的UI设计规范技能指南，涵盖OpenClaw项目前端UI的**所有**细节，可用于在你的项目中保持完全一致的风格。

---

## 目录

1. [设计语言概述](#1-设计语言概述)
2. [颜色系统](#2-颜色系统)
3. [排版系统](#3-排版系统)
4. [间距和圆角](#4-间距和圆角)
5. [动画系统](#5-动画系统)
6. [布局系统](#6-布局系统)
7. [组件详解](#7-组件详解)
8. [聊天界面](#8-聊天界面)
9. [配置页面](#9-配置页面)
10. [表单控件](#10-表单控件)
11. [Web Components (Lit)](#11-web-components-lit)
12. [CLI 样式](#12-cli-样式)
13. [TUI 终端界面](#13-tui-终端界面)
14. [表格渲染](#14-表格渲染)
15. [图标系统](#15-图标系统)
16. [响应式设计](#16-响应式设计)
17. [主题切换](#17-主题切换)
18. [进度条系统](#18-进度条系统)
19. [Banner和品牌](#19-banner和品牌)
20. [滚动条和焦点](#20-滚动条和焦点)
21. [最佳实践](#21-最佳实践)
22. [文件结构参考](#22-文件结构参考)
23. [依赖清单](#23-依赖清单)
24. [快速参考卡片](#24-快速参考卡片)

---

## 1. 设计语言概述

OpenClaw 采用**多层UI系统**，覆盖三个界面层级：

| 层级 | 技术栈 | 用途 | 主要文件 |
|-----|-------|-----|---------|
| **Web UI** | Lit (Web Components) + CSS | 浏览器界面 | `ui/src/` |
| **TUI** | pi-tui + chalk | 终端富文本界面 | `src/tui/` |
| **CLI** | @clack/prompts + chalk | 命令行交互 | `src/cli/` |

### 设计理念

- **温暖的浅色主题（Warm Light）**为默认，避免纯白背景
- **红色作为品牌标识色（Signature Red）** - `#dc2626` (浅色默认) / `#ff5c5c` (深色)
- **简洁、功能优先** - 最小化视觉干扰
- **动画流畅但不花哨** - 使用 `ease-out` 缓动，时长 120-350ms
- **一致的圆角和阴影** - 统一的视觉语言
- **无障碍优先** - 尊重 `prefers-reduced-motion`

---

## 2. 颜色系统

### 2.1 Lobster 调色板 (CLI/TUI 标准)

这是所有终端输出的统一调色板，称为 "Lobster Seam"：

```typescript
// src/terminal/palette.ts
export const LOBSTER_PALETTE = {
  accent: "#FF5A2D",        // 主品牌色 - 红橙色（🦞龙虾色）
  accentBright: "#FF7A3D",  // 亮版本 - 悬停/焦点状态
  accentDim: "#D14A22",     // 暗版本 - 按下状态
  info: "#FF8A5B",          // 信息 - 浅橙色
  success: "#2FBF71",       // 成功 - 绿色
  warn: "#FFB020",          // 警告 - 黄色
  error: "#E23D2D",         // 错误 - 红色
  muted: "#8B7F77",         // 柔和 - 灰褐色（用于次要信息）
} as const;
```

### 2.2 Web UI 浅色主题 (默认)

```css
::root {
  /* ========== 背景层级 - 温暖的浅色 ========== */
  --bg: #fafafa;              /* L1: 主背景 */
  --bg-accent: #f5f5f5;       /* L2: 强调背景 */
  --bg-elevated: #ffffff;     /* L3: 浮起层 */
  --bg-hover: #f0f0f0;        /* 悬停状态 */
  --bg-muted: #f0f0f0;        /* 柔和背景 */
  --bg-content: #f5f5f5;

  /* ========== 卡片/表面 ========== */
  --card: #ffffff;
  --card-foreground: #18181b;
  --card-highlight: rgba(0, 0, 0, 0.03);
  --popover: #ffffff;
  --popover-foreground: #18181b;

  /* ========== 面板 ========== */
  --panel: #fafafa;
  --panel-strong: #f5f5f5;
  --panel-hover: #ebebeb;
  --chrome: rgba(250, 250, 250, 0.95);
  --chrome-strong: rgba(250, 250, 250, 0.98);

  /* ========== 文本 ========== */
  --text: #3f3f46;
  --text-strong: #18181b;
  --chat-text: #3f3f46;
  --muted: #71717a;
  --muted-strong: #52525b;
  --muted-foreground: #71717a;

  /* ========== 边框 ========== */
  --border: #e4e4e7;
  --border-strong: #d4d4d8;
  --border-hover: #a1a1aa;
  --input: #e4e4e7;
  --ring: #dc2626;

  /* ========== 主品牌色 - 标志性红色 ========== */
  --accent: #dc2626;
  --accent-hover: #ef4444;
  --accent-muted: #dc2626;
  --accent-subtle: rgba(220, 38, 38, 0.12);
  --accent-foreground: #ffffff;
  --accent-glow: rgba(220, 38, 38, 0.15);
  --primary: #dc2626;
  --primary-foreground: #ffffff;

  /* ========== 第二强调色 - 青色 ========== */
  --secondary: #f4f4f5;
  --secondary-foreground: #3f3f46;
  --accent-2: #0d9488;
  --accent-2-muted: rgba(13, 148, 136, 0.75);
  --accent-2-subtle: rgba(13, 148, 136, 0.12);

  /* ========== 语义颜色 ========== */
  --ok: #16a34a;
  --ok-muted: rgba(22, 163, 74, 0.75);
  --ok-subtle: rgba(22, 163, 74, 0.1);

  --destructive: #dc2626;
  --destructive-foreground: #fafafa;

  --warn: #d97706;
  --warn-muted: rgba(217, 119, 6, 0.75);
  --warn-subtle: rgba(217, 119, 6, 0.1);

  --danger: #dc2626;
  --danger-muted: rgba(220, 38, 38, 0.75);
  --danger-subtle: rgba(220, 38, 38, 0.1);

  --info: #2563eb;

  /* ========== 焦点样式 ========== */
  --focus: rgba(220, 38, 38, 0.2);
  --focus-ring: 0 0 0 2px var(--bg), 0 0 0 4px var(--ring);
  --focus-glow: 0 0 0 2px var(--bg), 0 0 0 4px var(--ring), 0 0 16px var(--accent-glow);

  /* ========== 网格线 ========== */
  --grid-line: rgba(0, 0, 0, 0.05);

  /* ========== 阴影 ========== */
  --shadow-sm: 0 1px 2px rgba(0, 0, 0, 0.06);
  --shadow-md: 0 4px 12px rgba(0, 0, 0, 0.08), 0 0 0 1px rgba(0, 0, 0, 0.04);
  --shadow-lg: 0 12px 28px rgba(0, 0, 0, 0.12), 0 0 0 1px rgba(0, 0, 0, 0.04);
  --shadow-xl: 0 24px 48px rgba(0, 0, 0, 0.15), 0 0 0 1px rgba(0, 0, 0, 0.04);
  --shadow-glow: 0 0 24px var(--accent-glow);

  /* ========== 主题切换动画坐标 ========== */
  --theme-switch-x: 50%;
  --theme-switch-y: 50%;

  color-scheme: light;
}
```

### 2.3 Web UI 深色主题

```css
::root[data-theme="dark"] {
  /* ========== 背景层级 - 温暖的深色 ========== */
  --bg: #12141a;              /* L1: 主背景 */
  --bg-accent: #14161d;       /* L2: 强调背景 */
  --bg-elevated: #1a1d25;     /* L3: 浮起层 */
  --bg-hover: #262a35;        /* 悬停状态 */
  --bg-muted: #262a35;        /* 柔和背景 */

  /* ========== 卡片/表面 ========== */
  --card: #181b22;
  --card-foreground: #f4f4f5;
  --card-highlight: rgba(255, 255, 255, 0.05);
  --popover: #181b22;
  --popover-foreground: #f4f4f5;

  /* ========== 面板 ========== */
  --panel: #12141a;
  --panel-strong: #1a1d25;
  --panel-hover: #262a35;
  --chrome: rgba(18, 20, 26, 0.95);
  --chrome-strong: rgba(18, 20, 26, 0.98);

  /* ========== 文本 ========== */
  --text: #e4e4e7;
  --text-strong: #fafafa;
  --chat-text: #e4e4e7;
  --muted: #71717a;
  --muted-strong: #52525b;
  --muted-foreground: #71717a;

  /* ========== 边框 ========== */
  --border: #27272a;
  --border-strong: #3f3f46;
  --border-hover: #52525b;
  --input: #27272a;
  --ring: #ff5c5c;

  /* ========== 主品牌色 ========== */
  --accent: #ff5c5c;
  --accent-hover: #ff7070;
  --accent-muted: #ff5c5c;
  --accent-subtle: rgba(255, 92, 92, 0.15);
  --accent-foreground: #fafafa;
  --accent-glow: rgba(255, 92, 92, 0.25);
  --primary: #ff5c5c;
  --primary-foreground: #ffffff;

  /* ========== 第二强调色 ========== */
  --secondary: #1e2028;
  --secondary-foreground: #f4f4f5;
  --accent-2: #14b8a6;
  --accent-2-muted: rgba(20, 184, 166, 0.7);
  --accent-2-subtle: rgba(20, 184, 166, 0.15);

  /* ========== 语义颜色 ========== */
  --ok: #22c55e;
  --ok-muted: rgba(34, 197, 94, 0.75);
  --ok-subtle: rgba(34, 197, 94, 0.12);

  --destructive: #ef4444;
  --destructive-foreground: #fafafa;

  --warn: #f59e0b;
  --warn-muted: rgba(245, 158, 11, 0.75);
  --warn-subtle: rgba(245, 158, 11, 0.12);

  --danger: #ef4444;
  --danger-muted: rgba(239, 68, 68, 0.75);
  --danger-subtle: rgba(239, 68, 68, 0.12);

  --info: #3b82f6;

  /* ========== 焦点样式 ========== */
  --focus: rgba(255, 92, 92, 0.25);
  --focus-ring: 0 0 0 2px var(--bg), 0 0 0 4px var(--ring);
  --focus-glow: 0 0 0 2px var(--bg), 0 0 0 4px var(--ring), 0 0 20px var(--accent-glow);

  /* ========== 网格线 ========== */
  --grid-line: rgba(255, 255, 255, 0.04);

  /* ========== 阴影 ========== */
  --shadow-sm: 0 1px 2px rgba(0, 0, 0, 0.2);
  --shadow-md: 0 4px 12px rgba(0, 0, 0, 0.25), 0 0 0 1px rgba(255, 255, 255, 0.03);
  --shadow-lg: 0 12px 28px rgba(0, 0, 0, 0.35), 0 0 0 1px rgba(255, 255, 255, 0.03);
  --shadow-xl: 0 24px 48px rgba(0, 0, 0, 0.4), 0 0 0 1px rgba(255, 255, 255, 0.03);
  --shadow-glow: 0 0 30px var(--accent-glow);

  color-scheme: dark;
}
```

### 2.4 TUI 颜色 (终端富文本)

TUI 使用独立的颜色系统，更适合终端环境：

```typescript
// src/tui/theme/theme.ts
const palette = {
  // 基础文本
  text: "#E8E3D5",          // 米色文本（非纯白）
  dim: "#7B7F87",           // 暗灰（次要信息）

  // 强调色
  accent: "#F6C453",        // 金黄重点（非红色，在终端更醒目）
  accentSoft: "#F2A65A",    // 柔和重点

  // 边框和背景
  border: "#3C414B",        // 边框
  userBg: "#2B2F36",        // 用户消息背景
  userText: "#F3EEE0",      // 用户消息文本

  // 系统消息
  systemText: "#9BA3B2",    // 系统文本

  // 工具执行状态背景
  toolPendingBg: "#1F2A2F", // 工具待处理（青灰）
  toolSuccessBg: "#1E2D23", // 工具成功（暗绿）
  toolErrorBg: "#2F1F1F",   // 工具错误（暗红）
  toolTitle: "#F6C453",     // 工具标题
  toolOutput: "#E1DACB",    // 工具输出文本

  // Markdown 元素
  quote: "#8CC8FF",         // 引用文本
  quoteBorder: "#3B4D6B",   // 引用边框
  code: "#F0C987",          // 代码
  codeBlock: "#1E232A",     // 代码块背景
  codeBorder: "#343A45",    // 代码块边框
  link: "#7DD3A5",          // 链接（绿色）

  // 状态
  error: "#F97066",
  success: "#7DD3A5",
};
```

---

## 3. 排版系统

### 3.1 字体堆栈

```css
/* 正文字体 - Space Grotesk（几何无衬线，有个性） */
--font-body: "Space Grotesk", -apple-system, BlinkMacSystemFont,
             "Segoe UI", Roboto, sans-serif;

/* 显示字体（标题） */
--font-display: "Space Grotesk", -apple-system, BlinkMacSystemFont,
                "Segoe UI", Roboto, sans-serif;

/* 代码字体 - JetBrains Mono（连字支持） */
--mono: "JetBrains Mono", ui-monospace, SFMono-Regular,
        "SF Mono", Menlo, Monaco, Consolas, monospace;
```

### 3.2 字体加载

```css
@import url("https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@400;500;600;700&family=JetBrains+Mono:wght@400;500&display=swap");
```

### 3.3 基础排版

```css
body {
  font: 400 14px/1.55 var(--font-body);
  letter-spacing: -0.02em;  /* 轻微负间距，更紧凑 */
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
```

### 3.4 字重规范

| 权重 | 用途 | 示例 |
|-----|-----|-----|
| `400` | 正文 | 段落文本、描述 |
| `500` | 半粗 | 按钮、标签、导航项 |
| `600` | 粗体 | 卡片标题、区块标题 |
| `700` | 特粗 | 页面标题、品牌名 |

### 3.5 标题样式

```css
.page-title {
  font-size: 26px;
  font-weight: 700;
  letter-spacing: -0.035em;  /* 大标题用更紧的间距 */
  line-height: 1.15;
  color: var(--text-strong);
}

.page-sub {
  color: var(--muted);
  font-size: 14px;
  font-weight: 400;
  margin-top: 6px;
  letter-spacing: -0.01em;
}

.card-title {
  font-size: 15px;
  font-weight: 600;
  letter-spacing: -0.02em;
  color: var(--text-strong);
}

.card-sub {
  color: var(--muted);
  font-size: 13px;
  margin-top: 6px;
  line-height: 1.5;
}
```

### 3.6 品牌排版

```css
.brand-title {
  font-size: 16px;
  font-weight: 700;
  letter-spacing: -0.03em;
  line-height: 1.1;
  color: var(--text-strong);
}

.brand-sub {
  font-size: 10px;
  font-weight: 500;
  color: var(--muted);
  letter-spacing: 0.05em;    /* 全大写用正间距 */
  text-transform: uppercase;
  line-height: 1;
}
```

---

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

## 11. Web Components (Lit)

### 11.1 组件结构

```typescript
import { LitElement, html, css } from "lit";
import { customElement, property, state } from "lit/decorators.js";

@customElement("my-component")
export class MyComponent extends LitElement {
  @property({ type: String }) title = "";
  @state() private isOpen = false;

  static styles = css`
    :host {
      display: block;
    }
    /* 使用 CSS 变量保持主题一致 */
    .container {
      background: var(--card);
      border-radius: var(--radius-lg);
      border: 1px solid var(--border);
      padding: 20px;
    }
    .container:hover {
      border-color: var(--border-strong);
    }
  `;

  render() {
    return html`
      <div class="container">
        <h2>${this.title}</h2>
        <slot></slot>
      </div>
    `;
  }
}
```

### 11.2 常用指令

```typescript
import { repeat } from "lit/directives/repeat.js";
import { ref, createRef } from "lit/directives/ref.js";
import { classMap } from "lit/directives/class-map.js";
import { styleMap } from "lit/directives/style-map.js";

// repeat - 高效列表渲染
${repeat(items, item => item.id, item => html`<li>${item.name}</li>`)}

// ref - DOM 引用
private inputRef = createRef<HTMLInputElement>();
<input ${ref(this.inputRef)}>

// classMap - 条件类名
<div class=${classMap({
  active: this.isActive,
  disabled: this.isDisabled,
  'has-error': this.hasError
})}>

// styleMap - 条件样式
<div style=${styleMap({
  '--theme-index': String(this.themeIndex)
})}>
```

### 11.3 主组件示例

```typescript
// ui/src/ui/app.ts
@customElement("openclaw-app")
export class OpenClawApp extends LitElement {
  @state() private view: ViewName = "chat";
  @state() private theme: ThemeMode = "system";

  static styles = css`
    :host {
      display: block;
      position: relative;
      z-index: 1;
      min-height: 100vh;
    }
  `;

  render() {
    return html`
      <div class="shell ${classMap({
        'shell--chat': this.view === 'chat',
        'shell--chat-focus': this.isChatFocused
      })}">
        ${this.renderTopbar()}
        ${this.renderNav()}
        ${this.renderContent()}
      </div>
    `;
  }
}
```

---

## 12. CLI 样式

### 12.1 Chalk 主题

```typescript
// src/terminal/theme.ts
import chalk, { Chalk } from "chalk";
import { LOBSTER_PALETTE } from "./palette.js";

const hasForceColor =
  typeof process.env.FORCE_COLOR === "string" &&
  process.env.FORCE_COLOR.trim().length > 0 &&
  process.env.FORCE_COLOR.trim() !== "0";

const baseChalk = process.env.NO_COLOR && !hasForceColor
  ? new Chalk({ level: 0 })
  : chalk;

const hex = (value: string) => baseChalk.hex(value);

export const theme = {
  accent: hex(LOBSTER_PALETTE.accent),
  accentBright: hex(LOBSTER_PALETTE.accentBright),
  accentDim: hex(LOBSTER_PALETTE.accentDim),
  info: hex(LOBSTER_PALETTE.info),
  success: hex(LOBSTER_PALETTE.success),
  warn: hex(LOBSTER_PALETTE.warn),
  error: hex(LOBSTER_PALETTE.error),
  muted: hex(LOBSTER_PALETTE.muted),
  heading: baseChalk.bold.hex(LOBSTER_PALETTE.accent),
  command: hex(LOBSTER_PALETTE.accentBright),
  option: hex(LOBSTER_PALETTE.warn),
} as const;

export const isRich = () => Boolean(baseChalk.level > 0);

export const colorize = (rich: boolean, color: (value: string) => string, value: string) =>
  rich ? color(value) : value;
```

### 12.2 使用示例

```typescript
import { theme } from "./terminal/theme.js";

// 标题
console.log(theme.heading("🦞 OpenClaw Configuration"));

// 成功/错误/警告
console.log(theme.success("✓ Configuration saved"));
console.log(theme.error("✗ Failed to connect"));
console.log(theme.warn("⚠ Using default values"));

// 命令和选项
console.log(`Run ${theme.command("openclaw config")} to view settings`);
console.log(`Use ${theme.option("--verbose")} for detailed output`);

// 柔和文本
console.log(theme.muted("Press Ctrl+C to exit"));
```

### 12.3 提示样式

```typescript
// src/terminal/prompt-style.ts
import { isRich, theme } from "./theme.js";

export const stylePromptMessage = (message: string): string =>
  isRich() ? theme.accent(message) : message;

export const stylePromptTitle = (title?: string): string | undefined =>
  title && isRich() ? theme.heading(title) : title;

export const stylePromptHint = (hint?: string): string | undefined =>
  hint && isRich() ? theme.muted(hint) : hint;
```

---

## 13. TUI 终端界面

### 13.1 TUI 主题

```typescript
// src/tui/theme/theme.ts
import type { MarkdownTheme, SelectListTheme } from "@mariozechner/pi-tui";
import chalk from "chalk";
import { highlight, supportsLanguage } from "cli-highlight";

const palette = {
  text: "#E8E3D5",
  dim: "#7B7F87",
  accent: "#F6C453",
  accentSoft: "#F2A65A",
  border: "#3C414B",
  // ... 完整调色板见第2节
};

const fg = (hex: string) => (text: string) => chalk.hex(hex)(text);
const bg = (hex: string) => (text: string) => chalk.bgHex(hex)(text);

export const theme = {
  fg: fg(palette.text),
  dim: fg(palette.dim),
  accent: fg(palette.accent),
  accentSoft: fg(palette.accentSoft),
  success: fg(palette.success),
  error: fg(palette.error),
  header: (text: string) => chalk.bold(fg(palette.accent)(text)),
  system: fg(palette.systemText),
  userBg: bg(palette.userBg),
  userText: fg(palette.userText),
  toolTitle: fg(palette.toolTitle),
  toolOutput: fg(palette.toolOutput),
  toolPendingBg: bg(palette.toolPendingBg),
  toolSuccessBg: bg(palette.toolSuccessBg),
  toolErrorBg: bg(palette.toolErrorBg),
  border: fg(palette.border),
  bold: (text: string) => chalk.bold(text),
  italic: (text: string) => chalk.italic(text),
};
```

### 13.2 Markdown 主题

```typescript
export const markdownTheme: MarkdownTheme = {
  heading: (text) => chalk.bold(fg(palette.accent)(text)),
  link: (text) => fg(palette.link)(text),
  linkUrl: (text) => chalk.dim(text),
  code: (text) => fg(palette.code)(text),
  codeBlock: (text) => fg(palette.code)(text),
  codeBlockBorder: (text) => fg(palette.codeBorder)(text),
  quote: (text) => fg(palette.quote)(text),
  quoteBorder: (text) => fg(palette.quoteBorder)(text),
  hr: (text) => fg(palette.border)(text),
  listBullet: (text) => fg(palette.accentSoft)(text),
  bold: (text) => chalk.bold(text),
  italic: (text) => chalk.italic(text),
  strikethrough: (text) => chalk.strikethrough(text),
  underline: (text) => chalk.underline(text),
  highlightCode,  // 代码高亮函数
};
```

### 13.3 选择列表主题

```typescript
export const selectListTheme: SelectListTheme = {
  selectedPrefix: (text) => fg(palette.accent)(text),
  selectedText: (text) => chalk.bold(fg(palette.accent)(text)),
  description: (text) => fg(palette.dim)(text),
  scrollInfo: (text) => fg(palette.dim)(text),
  noMatch: (text) => fg(palette.dim)(text),
};

export const searchableSelectListTheme = {
  ...selectListTheme,
  searchPrompt: (text) => fg(palette.accentSoft)(text),
  searchInput: (text) => fg(palette.text)(text),
  matchHighlight: (text) => chalk.bold(fg(palette.accent)(text)),
};
```

---

## 14. 表格渲染

### 14.1 表格API

```typescript
// src/terminal/table.ts
export type TableColumn = {
  key: string;           // 数据键
  header: string;        // 列标题
  align?: "left" | "right" | "center";
  minWidth?: number;
  maxWidth?: number;
  flex?: boolean;        // 弹性列，优先收缩/扩展
};

export type RenderTableOptions = {
  columns: TableColumn[];
  rows: Array<Record<string, string>>;
  width?: number;        // 终端宽度
  padding?: number;      // 单元格内边距（默认1）
  border?: "unicode" | "ascii" | "none";
};

export function renderTable(opts: RenderTableOptions): string;
```

### 14.2 使用示例

```typescript
import { renderTable } from "./terminal/table.js";

const columns = [
  { key: "name", header: "Name", flex: true },
  { key: "status", header: "Status", minWidth: 10 },
  { key: "count", header: "Count", align: "right" as const },
];

const rows = [
  { name: "Project Alpha", status: "Running", count: "42" },
  { name: "Project Beta", status: "Stopped", count: "0" },
];

console.log(renderTable({
  columns,
  rows,
  width: 80,
  border: "unicode",
}));
```

输出：
```
┌─────────────────┬──────────┬───────┐
│ Name            │ Status   │ Count │
├─────────────────┼──────────┼───────┤
│ Project Alpha   │ Running  │    42 │
│ Project Beta    │ Stopped  │     0 │
└─────────────────┴──────────┴───────┘
```

### 14.3 边框字符

```typescript
// Unicode 边框（默认）
const unicodeBox = {
  tl: "┌", tr: "┐", bl: "└", br: "┘",
  h: "─", v: "│",
  t: "┬", ml: "├", m: "┼", mr: "┤", b: "┴",
};

// ASCII 边框（兼容模式）
const asciiBox = {
  tl: "+", tr: "+", bl: "+", br: "+",
  h: "-", v: "|",
  t: "+", ml: "+", m: "+", mr: "+", b: "+",
};
```

### 14.4 ANSI 感知

表格渲染器正确处理：
- SGR 颜色码
- OSC-8 超链接
- Unicode 字符宽度
- 单元格内换行

---

## 15. 图标系统

### 15.1 图标定义（Lucide 风格）

```typescript
// ui/src/ui/icons.ts
import { html, type TemplateResult } from "lit";

export const icons = {
  // 导航图标
  messageSquare: html`
    <svg viewBox="0 0 24 24">
      <path d="M21 15a2 2 0 0 1-2 2H7l-4 4V5a2 2 0 0 1 2-2h14a2 2 0 0 1 2 2z" />
    </svg>
  `,
  barChart: html`
    <svg viewBox="0 0 24 24">
      <line x1="12" x2="12" y1="20" y2="10" />
      <line x1="18" x2="18" y1="20" y2="4" />
      <line x1="6" x2="6" y1="20" y2="16" />
    </svg>
  `,
  settings: html`
    <svg viewBox="0 0 24 24">
      <path d="M12.22 2h-.44a2 2 0 0 0-2 2v.18a2 2 0 0 1-1 1.73l-.43.25..." />
      <circle cx="12" cy="12" r="3" />
    </svg>
  `,

  // UI 图标
  menu: html`
    <svg viewBox="0 0 24 24">
      <line x1="4" x2="20" y1="12" y2="12" />
      <line x1="4" x2="20" y1="6" y2="6" />
      <line x1="4" x2="20" y1="18" y2="18" />
    </svg>
  `,
  x: html`
    <svg viewBox="0 0 24 24">
      <path d="M18 6 6 18" />
      <path d="m6 6 12 12" />
    </svg>
  `,
  check: html`
    <svg viewBox="0 0 24 24"><path d="M20 6 9 17l-5-5" /></svg>
  `,
  search: html`
    <svg viewBox="0 0 24 24">
      <circle cx="11" cy="11" r="8" />
      <path d="m21 21-4.3-4.3" />
    </svg>
  `,
  loader: html`
    <svg viewBox="0 0 24 24">
      <path d="M12 2v4" />
      <path d="m16.2 7.8 2.9-2.9" />
      <path d="M18 12h4" />
      <path d="m16.2 16.2 2.9 2.9" />
      <path d="M12 18v4" />
      <path d="m4.9 19.1 2.9-2.9" />
      <path d="M2 12h4" />
      <path d="m4.9 4.9 2.9 2.9" />
    </svg>
  `,

  // 工具图标
  wrench: html`
    <svg viewBox="0 0 24 24">
      <path d="M14.7 6.3a1 1 0 0 0 0 1.4l1.6 1.6a1 1 0 0 0 1.4 0l3.77-3.77..." />
    </svg>
  `,
  fileCode: html`
    <svg viewBox="0 0 24 24">
      <path d="M14.5 2H6a2 2 0 0 0-2 2v16a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V7.5L14.5 2z" />
      <polyline points="14 2 14 8 20 8" />
      <path d="m10 13-2 2 2 2" />
      <path d="m14 17 2-2-2-2" />
    </svg>
  `,

  // 更多图标...
} as const;

export type IconName = keyof typeof icons;

export function icon(name: IconName): TemplateResult {
  return icons[name];
}

export function renderIcon(name: IconName, className = "nav-item__icon"): TemplateResult {
  return html`<span class=${className} aria-hidden="true">${icons[name]}</span>`;
}
```

### 15.2 图标样式规范

```css
/* 所有图标的通用样式 */
svg {
  stroke: currentColor;
  fill: none;
  stroke-width: 1.5px;
  stroke-linecap: round;
  stroke-linejoin: round;
}

/* 尺寸变体 */
.icon-sm svg { width: 14px; height: 14px; }
.icon-md svg { width: 16px; height: 16px; }
.icon-lg svg { width: 20px; height: 20px; }
.icon-xl svg { width: 24px; height: 24px; }
```

---

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

## 17. 主题切换

### 17.1 主题检测

```typescript
// ui/src/ui/theme.ts
export type ThemeMode = "system" | "light" | "dark";
export type ResolvedTheme = "light" | "dark";

export function getSystemTheme(): ResolvedTheme {
  if (typeof window === "undefined" || typeof window.matchMedia !== "function") {
    return "dark";
  }
  return window.matchMedia("(prefers-color-scheme: dark)").matches
    ? "dark"
    : "light";
}

export function resolveTheme(mode: ThemeMode): ResolvedTheme {
  if (mode === "system") {
    return getSystemTheme();
  }
  return mode;
}
```

### 17.2 View Transition API

```css
/* 主题切换动画 */
@keyframes theme-circle-transition {
  0% {
    clip-path: circle(0% at var(--theme-switch-x, 50%) var(--theme-switch-y, 50%));
  }
  100% {
    clip-path: circle(150% at var(--theme-switch-x, 50%) var(--theme-switch-y, 50%));
  }
}

html.theme-transition {
  view-transition-name: theme;
}

html.theme-transition::view-transition-old(theme) {
  mix-blend-mode: normal;
  animation: none;
  z-index: 1;
}

html.theme-transition::view-transition-new(theme) {
  mix-blend-mode: normal;
  z-index: 2;
  animation: theme-circle-transition 0.4s var(--ease-out) forwards;
}

@media (prefers-reduced-motion: reduce) {
  html.theme-transition::view-transition-old(theme),
  html.theme-transition::view-transition-new(theme) {
    animation: none !important;
  }
}
```

### 17.3 切换实现

```typescript
async function switchTheme(newTheme: ThemeMode, event?: MouseEvent) {
  // 无 View Transition 支持时直接切换
  if (!document.startViewTransition) {
    setTheme(newTheme);
    return;
  }

  // 记录切换起点坐标（从点击位置扩散）
  if (event) {
    document.documentElement.style.setProperty(
      "--theme-switch-x",
      `${event.clientX}px`
    );
    document.documentElement.style.setProperty(
      "--theme-switch-y",
      `${event.clientY}px`
    );
  }

  document.documentElement.classList.add("theme-transition");

  await document.startViewTransition(() => {
    const resolved = resolveTheme(newTheme);
    document.documentElement.setAttribute("data-theme", resolved);
  }).finished;

  document.documentElement.classList.remove("theme-transition");
}
```

---

## 18. 进度条系统

### 18.1 进度条 API

```typescript
// src/cli/progress.ts
type ProgressOptions = {
  label: string;
  indeterminate?: boolean;
  total?: number;
  enabled?: boolean;
  delayMs?: number;
  stream?: NodeJS.WriteStream;
  fallback?: "spinner" | "line" | "log" | "none";
};

export type ProgressReporter = {
  setLabel: (label: string) => void;
  setPercent: (percent: number) => void;
  tick: (delta?: number) => void;
  done: () => void;
};

export function createCliProgress(options: ProgressOptions): ProgressReporter;

// 便捷包装
export async function withProgress<T>(
  options: ProgressOptions,
  work: (progress: ProgressReporter) => Promise<T>,
): Promise<T>;
```

### 18.2 使用示例

```typescript
import { createCliProgress, withProgress } from "./cli/progress.js";

// 手动控制
const progress = createCliProgress({
  label: "Downloading...",
  total: 100,
});
progress.tick(10);
progress.setLabel("Processing...");
progress.tick(40);
progress.done();

// 自动管理
await withProgress({ label: "Installing..." }, async (progress) => {
  await install();
  progress.setPercent(50);
  await configure();
  progress.setPercent(100);
});
```

### 18.3 进度条特性

- **OSC 进度协议** - 现代终端原生支持
- **Fallback 支持**：
  - `spinner` - @clack/prompts 旋转动画
  - `line` - 简单文本行
  - `log` - 非 TTY 输出
  - `none` - 静默
- **防重叠** - 同时只允许一个活跃进度
- **延迟启动** - 可配置延迟，避免闪烁

---

## 19. Banner和品牌

### 19.1 ASCII 艺术

```typescript
// src/cli/banner.ts
const LOBSTER_ASCII = [
  "▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄",
  "██░▄▄▄░██░▄▄░██░▄▄▄██░▀██░██░▄▄▀██░████░▄▄▀██░███░██",
  "██░███░██░▀▀░██░▄▄▄██░█░█░██░█████░████░▀▀░██░█░█░██",
  "██░▀▀▀░██░█████░▀▀▀██░██▄░██░▀▀▄██░▀▀░█░██░██▄▀▄▀▄██",
  "▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀",
  "                  🦞 OPENCLAW 🦞                    ",
  " ",
];
```

### 19.2 彩色 Banner

```typescript
export function formatCliBannerArt(options: BannerOptions = {}): string {
  const rich = options.richTty ?? isRich();
  if (!rich) {
    return LOBSTER_ASCII.join("\n");
  }

  const colorChar = (ch: string) => {
    if (ch === "█") return theme.accentBright(ch);  // 实心 - 亮色
    if (ch === "░") return theme.accentDim(ch);     // 点状 - 暗色
    if (ch === "▀") return theme.accent(ch);        // 上半 - 主色
    return theme.muted(ch);                          // 其他 - 柔和
  };

  const colored = LOBSTER_ASCII.map((line) => {
    if (line.includes("OPENCLAW")) {
      return (
        theme.muted("              ") +
        theme.accent("🦞") +
        theme.info(" OPENCLAW ") +
        theme.accent("🦞")
      );
    }
    return splitGraphemes(line).map(colorChar).join("");
  });

  return colored.join("\n");
}
```

### 19.3 单行 Banner

```typescript
export function formatCliBannerLine(version: string, options: BannerOptions = {}): string {
  const commit = options.commit ?? resolveCommitHash({ env: options.env });
  const tagline = pickTagline(options);
  const rich = options.richTty ?? isRich();
  const title = "🦞 OpenClaw";

  if (rich) {
    return `${theme.heading(title)} ${theme.info(version)} ${theme.muted(
      `(${commit})`,
    )} ${theme.muted("—")} ${theme.accentDim(tagline)}`;
  }

  return `${title} ${version} (${commit}) — ${tagline}`;
}
```

---

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

## 21. 最佳实践

### 21.1 颜色使用

- **始终使用 CSS 变量**，不要硬编码颜色值
- **语义颜色**：`--ok`, `--warn`, `--danger`, `--info`
- **背景层级**：`--bg` < `--bg-elevated` < `--card`
- **文本层级**：`--muted` < `--text` < `--text-strong`
- **主题兼容**：检查 `[data-theme="light"]` 覆盖

### 21.2 动画使用

- **微交互**：`--duration-fast` (120ms)
- **页面过渡**：`--duration-normal` (200ms)
- **复杂动画**：`--duration-slow` (350ms)
- **优先使用** `transform` 和 `opacity`（GPU加速）
- **尊重** `prefers-reduced-motion`
- **避免**持续动画（脉冲除外）

### 21.3 组件设计

- 使用 `:host` 设置 Web Component 基础样式
- 保持单向数据流
- 使用 `@state` 管理内部状态
- 使用 `@property` 暴露公共接口
- 避免在样式中使用 `!important`

### 21.4 CLI 输出

- 使用 **Lobster 调色板**保持一致性
- 尊重 `NO_COLOR` 环境变量
- 表格使用 **Unicode 边框**（支持降级到 ASCII）
- 进度条使用 **OSC 协议**（支持降级）
- 使用 `isRich()` 检测颜色支持

### 21.5 响应式设计

- **移动优先**或**桌面优先**，保持一致
- 使用 **CSS 变量**管理间距（`--shell-pad`）
- 使用 **容器查询**（`container-type: inline-size`）
- 导航在小屏幕变为**水平滚动**

### 21.6 性能优化

- 使用 `repeat()` 指令渲染列表
- 避免不必要的重渲染
- 使用 `will-change` 提示动画元素
- 延迟加载非关键内容

---

## 22. 文件结构参考

```
your-project/
├── src/
│   ├── terminal/
│   │   ├── palette.ts           # Lobster 调色板定义
│   │   ├── theme.ts             # Chalk 主题对象
│   │   ├── table.ts             # 表格渲染器
│   │   ├── ansi.ts              # ANSI 转义码处理
│   │   ├── progress-line.ts     # 进度行管理
│   │   ├── links.ts             # OSC-8 超链接
│   │   └── prompt-style.ts      # 提示样式装饰器
│   ├── cli/
│   │   ├── progress.ts          # CLI 进度条
│   │   ├── banner.ts            # CLI Banner
│   │   └── tagline.ts           # 随机标语
│   └── tui/
│       ├── theme/
│       │   ├── theme.ts         # TUI 主题
│       │   └── syntax-theme.ts  # 代码高亮主题
│       └── components/
│           ├── chat-log.ts
│           ├── assistant-message.ts
│           └── user-message.ts
├── ui/
│   └── src/
│       ├── main.ts              # Web UI 入口
│       ├── styles/
│       │   ├── base.css         # CSS 变量 + 基础样式
│       │   ├── layout.css       # Shell 布局
│       │   ├── layout.mobile.css # 响应式
│       │   ├── components.css   # 组件样式
│       │   ├── config.css       # 配置页面
│       │   └── chat/
│       │       ├── layout.css
│       │       ├── text.css
│       │       ├── grouped.css
│       │       ├── tool-cards.css
│       │       └── sidebar.css
│       └── ui/
│           ├── app.ts           # 主应用组件
│           ├── theme.ts         # 主题切换逻辑
│           ├── icons.ts         # SVG 图标库
│           ├── controllers/     # 业务逻辑控制器
│           └── views/           # UI 视图模板
└── package.json
```

---

## 23. 依赖清单

```json
{
  "dependencies": {
    "lit": "^3.3.2",                    // Web Components
    "chalk": "^5.6.2",                  // CLI 颜色
    "@clack/prompts": "^1.0.0",         // CLI 交互提示
    "osc-progress": "^0.3.0",           // OSC 进度条协议
    "@mariozechner/pi-tui": "^0.51.6",  // 终端 UI 框架
    "cli-highlight": "^2.1.11",         // 代码高亮
    "marked": "^17.0.1"                 // Markdown 解析
  },
  "devDependencies": {
    "vite": "^6.x"                      // Web UI 构建
  }
}
```

---

## 24. 快速参考卡片

### 颜色速查

| 类别 | 深色值 | 浅色值 |
|-----|-------|-------|
| 主背景 | `#12141a` | `#fafafa` |
| 浮起层 | `#1a1d25` | `#ffffff` |
| 卡片 | `#181b22` | `#ffffff` |
| 文本 | `#e4e4e7` | `#3f3f46` |
| 强调文本 | `#fafafa` | `#18181b` |
| 柔和文本 | `#71717a` | `#71717a` |
| 主色 | `#ff5c5c` | `#dc2626` |
| 成功 | `#22c55e` | `#16a34a` |
| 警告 | `#f59e0b` | `#d97706` |
| 危险 | `#ef4444` | `#dc2626` |
| 信息 | `#3b82f6` | `#2563eb` |
| 边框 | `#27272a` | `#e4e4e7` |

### 动画速查

| 类型 | 持续时间 | 缓动 |
|-----|---------|-----|
| 微交互 | `120ms` | `ease-out` |
| 标准过渡 | `200ms` | `ease-out` |
| 复杂动画 | `350ms` | `ease-out` |
| 弹性效果 | `200ms` | `ease-spring` |

### 圆角速查

| 变量 | 值 | 用途 |
|-----|---|-----|
| `--radius-sm` | 6px | 标签、inline-code |
| `--radius-md` | 8px | 按钮、输入框 |
| `--radius-lg` | 12px | 卡片、气泡 |
| `--radius-xl` | 16px | 对话框、大容器 |
| `--radius-full` | 9999px | 圆形、pill |

### 间距速查

| 用途 | 值 |
|-----|---|
| 卡片内边距 | `20px` |
| 统计卡片 | `14px 16px` |
| 按钮 | `9px 16px` |
| 小按钮 | `6px 10px` |
| 输入框 | `8px 12px` |
| 导航项 | `8px 10px` |

### 字体速查

| 用途 | 大小 | 权重 |
|-----|-----|-----|
| 正文 | 14px | 400 |
| 按钮/标签 | 13px | 500 |
| 卡片标题 | 15px | 600 |
| 页面标题 | 26px | 700 |
| 品牌名 | 16px | 700 |
| 统计值 | 24px | 700 |
| 小标签 | 11-12px | 500 |

---

*此技能指南基于 OpenClaw 项目 UI 系统完整整理。最后更新: 2026年2月*
