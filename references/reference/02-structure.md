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
