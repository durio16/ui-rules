## 11. Web Components (Lit)

### 11.1 组件结构

```typescript
import { LitElement, html, css } from "lit";
import { customElement, property, state } from "lit/decorators.js";

@customElement("my-component")
export class MyComponent extends LitElement {
  @property({ type: String }) title = "";
  @state() private isOpen = false;

  static styles = css`
    :host {
      display: block;
    }
    /* 使用 CSS 变量保持主题一致 */
    .container {
      background: var(--card);
      border-radius: var(--radius-lg);
      border: 1px solid var(--border);
      padding: 20px;
    }
    .container:hover {
      border-color: var(--border-strong);
    }
  `;

  render() {
    return html`
      <div class="container">
        <h2>${this.title}</h2>
        <slot></slot>
      </div>
    `;
  }
}
```

### 11.2 常用指令

```typescript
import { repeat } from "lit/directives/repeat.js";
import { ref, createRef } from "lit/directives/ref.js";
import { classMap } from "lit/directives/class-map.js";
import { styleMap } from "lit/directives/style-map.js";

// repeat - 高效列表渲染
${repeat(items, item => item.id, item => html`<li>${item.name}</li>`)}

// ref - DOM 引用
private inputRef = createRef<HTMLInputElement>();
<input ${ref(this.inputRef)}>

// classMap - 条件类名
<div class=${classMap({
  active: this.isActive,
  disabled: this.isDisabled,
  'has-error': this.hasError
})}>

// styleMap - 条件样式
<div style=${styleMap({
  '--theme-index': String(this.themeIndex)
})}>
```

### 11.3 主组件示例

```typescript
// ui/src/ui/app.ts
@customElement("openclaw-app")
export class UIApp extends LitElement {
  @state() private view: ViewName = "chat";
  @state() private theme: ThemeMode = "system";

  static styles = css`
    :host {
      display: block;
      position: relative;
      z-index: 1;
      min-height: 100vh;
    }
  `;

  render() {
    return html`
      <div class="shell ${classMap({
        'shell--chat': this.view === 'chat',
        'shell--chat-focus': this.isChatFocused
      })}">
        ${this.renderTopbar()}
        ${this.renderNav()}
        ${this.renderContent()}
      </div>
    `;
  }
}
```

---
