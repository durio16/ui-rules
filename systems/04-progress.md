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
