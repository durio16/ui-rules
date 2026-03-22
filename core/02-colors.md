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
