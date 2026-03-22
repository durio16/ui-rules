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
