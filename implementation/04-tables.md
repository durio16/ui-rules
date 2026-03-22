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
