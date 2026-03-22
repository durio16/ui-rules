## 3. 排版系统

### 3.1 字体堆栈

```css
/* 正文字体 - Space Grotesk（几何无衬线，有个性） */
--font-body: "Space Grotesk", -apple-system, BlinkMacSystemFont,
             "Segoe UI", Roboto, sans-serif;

/* 显示字体（标题） */
--font-display: "Space Grotesk", -apple-system, BlinkMacSystemFont,
                "Segoe UI", Roboto, sans-serif;

/* 代码字体 - JetBrains Mono（连字支持） */
--mono: "JetBrains Mono", ui-monospace, SFMono-Regular,
        "SF Mono", Menlo, Monaco, Consolas, monospace;
```

### 3.2 字体加载

```css
@import url("https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@400;500;600;700&family=JetBrains+Mono:wght@400;500&display=swap");
```

### 3.3 基础排版

```css
body {
  font: 400 14px/1.55 var(--font-body);
  letter-spacing: -0.02em;  /* 轻微负间距，更紧凑 */
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
```

### 3.4 字重规范

| 权重 | 用途 | 示例 |
|-----|-----|-----|
| `400` | 正文 | 段落文本、描述 |
| `500` | 半粗 | 按钮、标签、导航项 |
| `600` | 粗体 | 卡片标题、区块标题 |
| `700` | 特粗 | 页面标题、品牌名 |

### 3.5 标题样式

```css
.page-title {
  font-size: 26px;
  font-weight: 700;
  letter-spacing: -0.035em;  /* 大标题用更紧的间距 */
  line-height: 1.15;
  color: var(--text-strong);
}

.page-sub {
  color: var(--muted);
  font-size: 14px;
  font-weight: 400;
  margin-top: 6px;
  letter-spacing: -0.01em;
}

.card-title {
  font-size: 15px;
  font-weight: 600;
  letter-spacing: -0.02em;
  color: var(--text-strong);
}

.card-sub {
  color: var(--muted);
  font-size: 13px;
  margin-top: 6px;
  line-height: 1.5;
}
```

### 3.6 品牌排版

```css
.brand-title {
  font-size: 16px;
  font-weight: 700;
  letter-spacing: -0.03em;
  line-height: 1.1;
  color: var(--text-strong);
}

.brand-sub {
  font-size: 10px;
  font-weight: 500;
  color: var(--muted);
  letter-spacing: 0.05em;    /* 全大写用正间距 */
  text-transform: uppercase;
  line-height: 1;
}
```

---
