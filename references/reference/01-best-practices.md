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
