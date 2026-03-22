## 17. 主题切换

### 17.1 主题检测

```typescript
// ui/src/ui/theme.ts
export type ThemeMode = "system" | "light" | "dark";
export type ResolvedTheme = "light" | "dark";

export function getSystemTheme(): ResolvedTheme {
  if (typeof window === "undefined" || typeof window.matchMedia !== "function") {
    return "dark";
  }
  return window.matchMedia("(prefers-color-scheme: dark)").matches
    ? "dark"
    : "light";
}

export function resolveTheme(mode: ThemeMode): ResolvedTheme {
  if (mode === "system") {
    return getSystemTheme();
  }
  return mode;
}
```

### 17.2 View Transition API

```css
/* 主题切换动画 */
@keyframes theme-circle-transition {
  0% {
    clip-path: circle(0% at var(--theme-switch-x, 50%) var(--theme-switch-y, 50%));
  }
  100% {
    clip-path: circle(150% at var(--theme-switch-x, 50%) var(--theme-switch-y, 50%));
  }
}

html.theme-transition {
  view-transition-name: theme;
}

html.theme-transition::view-transition-old(theme) {
  mix-blend-mode: normal;
  animation: none;
  z-index: 1;
}

html.theme-transition::view-transition-new(theme) {
  mix-blend-mode: normal;
  z-index: 2;
  animation: theme-circle-transition 0.4s var(--ease-out) forwards;
}

@media (prefers-reduced-motion: reduce) {
  html.theme-transition::view-transition-old(theme),
  html.theme-transition::view-transition-new(theme) {
    animation: none !important;
  }
}
```

### 17.3 切换实现

```typescript
async function switchTheme(newTheme: ThemeMode, event?: MouseEvent) {
  // 无 View Transition 支持时直接切换
  if (!document.startViewTransition) {
    setTheme(newTheme);
    return;
  }

  // 记录切换起点坐标（从点击位置扩散）
  if (event) {
    document.documentElement.style.setProperty(
      "--theme-switch-x",
      `${event.clientX}px`
    );
    document.documentElement.style.setProperty(
      "--theme-switch-y",
      `${event.clientY}px`
    );
  }

  document.documentElement.classList.add("theme-transition");

  await document.startViewTransition(() => {
    const resolved = resolveTheme(newTheme);
    document.documentElement.setAttribute("data-theme", resolved);
  }).finished;

  document.documentElement.classList.remove("theme-transition");
}
```

---
