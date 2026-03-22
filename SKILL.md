---
name: ui-design-guide
description: UI 设计规范技能指南，用于生成前端界面时保持一致的视觉风格。当需要创建 HTML 报告、数据分析页面、年度总结页面，或需要遵循统一的颜色、排版、布局规范时使用此技能。包含颜色系统、排版系统、组件规范、动画效果等完整设计语言。
---

# UI Design Guide

本技能提供完整的前端 UI 设计规范，确保生成的界面具有一致的视觉风格和用户体验。

## 适用场景

- 生成 HTML 报告页面（年度总结、数据分析报告等）
- 创建前端界面时需要统一的视觉风格
- 需要遵循颜色、排版、布局规范
- 主题切换（浅色/深色模式）
- 组件设计和样式定义

## 使用方法

### 快速参考

1. **新项目入门** → 阅读 `references/core/01-overview.md`
2. **颜色规范** → 查看 `references/core/02-colors.md`
3. **组件设计** → 参考 `references/components/` 目录
4. **主题切换** → 使用 `references/systems/03-themes.md`
5. **快速查阅** → 使用 `references/reference/04-quick-reference.md`

### 规范结构

```
references/
├── core/           # 核心设计规范
│   ├── 01-overview.md      - 设计语言概述
│   ├── 02-colors.md        - 颜色系统（浅色/深色主题）
│   ├── 03-typography.md    - 排版系统
│   ├── 04-spacing.md       - 间距和圆角
│   ├── 05-animation.md     - 动画系统
│   └── 06-layout.md        - 布局系统
├── components/     # 组件规范
│   ├── 01-components.md    - 组件详解
│   ├── 02-chat-ui.md       - 聊天界面
│   ├── 03-config-page.md   - 配置页面
│   └── 04-forms.md         - 表单控件
├── implementation/ # 技术实现
│   ├── 01-web-components.md - Web Components
│   ├── 02-cli.md           - CLI 样式
│   ├── 03-tui.md           - TUI 终端界面
│   └── 04-tables.md        - 表格渲染
├── systems/        # 辅助系统
│   ├── 01-icons.md         - 图标系统
│   ├── 02-responsive.md    - 响应式设计
│   ├── 03-themes.md        - 主题切换
│   ├── 04-progress.md      - 进度条系统
│   ├── 05-banner.md        - Banner 和品牌
│   └── 06-scrollbar.md     - 滚动条和焦点
└── reference/      # 参考指南
    ├── 01-best-practices.md - 最佳实践
    ├── 02-structure.md     - 文件结构参考
    ├── 03-dependencies.md  - 依赖清单
    └── 04-quick-reference.md - 快速参考卡片
```

## 设计理念

- **温暖的浅色主题为默认**，避免纯白背景
- **红色作为品牌标识色** - `#dc2626` (浅色) / `#ff5c5c` (深色)
- **简洁、功能优先** - 最小化视觉干扰
- **无障碍优先** - 尊重 `prefers-reduced-motion`

## 核心 CSS 变量

```css
/* 浅色主题（默认） */
::root {
  --bg: #fafafa;
  --text: #3f3f46;
  --accent: #dc2626;
  --border: #e4e4e7;
  --card: #ffffff;
}

/* 深色主题 */
[data-theme="dark"] {
  --bg: #12141a;
  --text: #e4e4e7;
  --accent: #ff5c5c;
  --border: #27272a;
  --card: #181b22;
}
```

## 注意事项

1. 生成 HTML 页面时，优先使用 CSS 变量而非硬编码颜色值
2. 动画时长控制在 120-350ms，使用 `ease-out` 缓动
3. 确保颜色对比度满足 WCAG 无障碍标准
4. 支持主题切换时，使用 `data-theme` 属性
