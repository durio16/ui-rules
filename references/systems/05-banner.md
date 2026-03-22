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
  const title = "🦞 UI App";

  if (rich) {
    return `${theme.heading(title)} ${theme.info(version)} ${theme.muted(
      `(${commit})`,
    )} ${theme.muted("—")} ${theme.accentDim(tagline)}`;
  }

  return `${title} ${version} (${commit}) — ${tagline}`;
}
```

---
