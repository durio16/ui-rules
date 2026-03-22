# OpenClaw UI Skill Guide

> 完整的 UI 设计规范技能指南，涵盖前端 UI 的所有细节。

## 目录结构

### 核心规范 (core/)
- [01-overview.md](core/01-overview.md) - 设计语言概述
- [02-colors.md](core/02-colors.md) - 颜色系统
- [03-typography.md](core/03-typography.md) - 排版系统
- [04-spacing.md](core/04-spacing.md) - 间距和圆角
- [05-animation.md](core/05-animation.md) - 动画系统
- [06-layout.md](core/06-layout.md) - 布局系统

### 组件规范 (components/)
- [01-components.md](components/01-components.md) - 组件详解
- [02-chat-ui.md](components/02-chat-ui.md) - 聊天界面
- [03-config-page.md](components/03-config-page.md) - 配置页面
- [04-forms.md](components/04-forms.md) - 表单控件

### 技术实现 (implementation/)
- [01-web-components.md](implementation/01-web-components.md) - Web Components (Lit)
- [02-cli.md](implementation/02-cli.md) - CLI 样式
- [03-tui.md](implementation/03-tui.md) - TUI 终端界面
- [04-tables.md](implementation/04-tables.md) - 表格渲染

### 辅助系统 (systems/)
- [01-icons.md](systems/01-icons.md) - 图标系统
- [02-responsive.md](systems/02-responsive.md) - 响应式设计
- [03-themes.md](systems/03-themes.md) - 主题切换
- [04-progress.md](systems/04-progress.md) - 进度条系统
- [05-banner.md](systems/05-banner.md) - Banner和品牌
- [06-scrollbar.md](systems/06-scrollbar.md) - 滚动条和焦点

### 参考指南 (reference/)
- [01-best-practices.md](reference/01-best-practices.md) - 最佳实践
- [02-structure.md](reference/02-structure.md) - 文件结构参考
- [03-dependencies.md](reference/03-dependencies.md) - 依赖清单
- [04-quick-reference.md](reference/04-quick-reference.md) - 快速参考卡片

## 设计理念

- **温暖的浅色主题（Warm Light）**为默认
- **红色作为品牌标识色** - `#dc2626` (浅色) / `#ff5c5c` (深色)
- **简洁、功能优先** - 最小化视觉干扰
- **无障碍优先** - 尊重 `prefers-reduced-motion`

## 快速开始

1. 新项目？从 [core/01-overview.md](core/01-overview.md) 开始
2. 找组件？查看 [components/](components/)
3. 主题切换？参考 [systems/03-themes.md](systems/03-themes.md)
4. 快速查阅？使用 [reference/04-quick-reference.md](reference/04-quick-reference.md)
