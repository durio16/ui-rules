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
