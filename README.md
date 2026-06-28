# Kiara Standard Chat UI

A zero-dependency, single-file HTML mockup of a Claude-style AI chat interface.  
Accessible (WCAG AA), mobile-friendly, dark-mode ready. Drop the file in a browser — it just works.

---

## Why a standard UI?

### Ship faster, argue less

Every new project that starts from scratch spends the first few days on the same decisions: layout, colors, font sizes, button states, mobile breakpoints. With a standard UI, those decisions are made once and reused everywhere. New features go straight to building logic — not rebuilding chrome.

### Consistency across products

When every Kiara-built interface shares the same structure, users only learn it once. Switching between tools feels familiar, not foreign. That trust compounds — users explore more, make fewer errors, and need less support.

### Accessibility for free

WCAG AA compliance (focus rings, ARIA labels, touch targets, contrast ratios) is hard to retrofit. It's much cheaper to inherit it from a baseline that already passes. Every new project built on this UI starts compliant instead of starting broken.

### Easier handoffs

Designers, developers, and external collaborators share a common reference point. "Use the standard chip component" is a one-sentence brief. Without a standard, the same conversation takes a meeting.

### One fix, everywhere

When a bug or improvement is found — a focus state that's too faint, a touch target that's too small — fixing it in the standard propagates to every product built on it. Without a standard, the same bug lives independently in ten places.

| Without standard UI | With standard UI |
|---|---|
| 2–4 days on setup per project | Start on day one |
| Inconsistent look across tools | Instantly recognisable |
| Accessibility retrofitted later | Compliant from the start |
| Each team reinvents the same patterns | Shared vocabulary, faster reviews |
| Bugs fixed project-by-project | Fix once, benefit everywhere |

---

## Quick start

```bash
# Open directly in your browser
open xyz-chat.html

# Or serve locally
npx serve .
python3 -m http.server 8080
```

No build step. No npm install. No backend.

---

## What's included

| Feature | Detail |
|---|---|
| Responsive sidebar | Collapses to slide-in drawer on mobile (≤560px) |
| Dark mode | Automatic via `prefers-color-scheme` |
| Accessible | WCAG AA compliant — see checklist below |
| Quick-action chips | Write / Strategize / Analyze / Code |
| Send button state | Activates only when input is non-empty |
| Keyboard support | `Enter` to send, `Shift+Enter` for newline, `Escape` to close sidebar |
| Icons | Tabler Icons (CDN, ~5800 outline icons) |

---

## Accessibility checklist

| Criterion | Implementation |
|---|---|
| Skip link | `Skip to chat input` — visible on focus, links to `#main-input` |
| Touch targets | All interactive elements ≥ 36px (user row ≥ 44px) |
| Focus rings | `outline: 2px solid var(--fill-accent)` on every focusable element |
| Screen readers | `aria-label` on all icon-only buttons; `aria-current="page"` on active chat |
| Sidebar state | `aria-expanded` on hamburger toggle; `aria-controls` points to sidebar |
| Form labelling | `<label for="main-input">` (visually hidden); `aria-describedby` for hint text |
| Send button | `aria-disabled` toggled (not `disabled` attribute) — remains focusable |
| Overlay | `aria-hidden="true"` when closed; focus traps return to trigger on close |
| Live regions | `aria-live="polite"` on greeting |
| Decorative icons | `aria-hidden="true"` on all `<i class="ti ...">` |
| Semantic HTML | `<nav>`, `<main>`, `<ul role="list">`, `<role="group">` for chips |
| Color contrast | All text/bg combos ≥ 4.5:1 (checked in both light and dark) |

---

## Customisation

### Rebrand

Edit the logo block in the HTML:

```html
<!-- Change display name -->
XYZ Chat

<!-- Change the diamond logo mark to any inline SVG -->
<div class="logo-mark"> ... </div>
```

### Colors

Override CSS variables in `:root` (light) and the `@media (prefers-color-scheme: dark)` block:

```css
:root {
  --fill-accent: #your-brand-color;
  --text-accent: #your-brand-dark;
  --bg-accent:   #your-brand-tint;
}
```

### Add chat messages

Replace `.main-scroll` content with a message thread. Example structure:

```html
<div class="message-thread" role="log" aria-label="Conversation" aria-live="polite">
  <article class="msg msg-user">
    <p>Hello!</p>
  </article>
  <article class="msg msg-ai" aria-label="XYZ Chat reply">
    <p>Hi Dave, how can I help?</p>
  </article>
</div>
```

### Wire up an API

```js
async function sendToAPI(userMessage) {
  const res = await fetch('https://your-api/chat', {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify({ message: userMessage })
  });
  const data = await res.json();
  return data.reply;
}
```

---

## File structure

```
xyz-chat.html   ← entire app (HTML + CSS + JS, no external files except icon CDN)
README.md       ← this file
```

---

## Browser support

| Browser | Version |
|---|---|
| Chrome / Edge | 90+ |
| Firefox | 88+ |
| Safari | 14+ |
| Mobile Safari (iOS) | 14+ |
| Android Chrome | 90+ |

Uses `100dvh` for correct mobile viewport height on iOS Safari.

---

## License

MIT — free to use, modify, and redistribute.

---

## 概要（日本語）

**Kiara Standard Chat UI** は、AIチャット画面の標準テンプレートです。  
HTMLファイル1つで完結し、インストール不要。ブラウザで開くだけで動作します。

**主なメリット：**

| メリット | 内容 |
|---|---|
| 開発時間の短縮 | 毎回ゼロから作らなくていい。デザイン判断は一度だけ |
| 統一されたUX | すべてのKiaraツールが同じ見た目・操作感 |
| アクセシビリティ対応済み | WCAG AA準拠をそのまま継承。後から直す必要なし |
| ダークモード自動対応 | OSの設定に合わせて自動で切り替わる |
| モバイル対応 | スマートフォンでも崩れない（560px以下でドロワー表示） |

> 標準UIを使うことで、新しいプロジェクトは「UIを作る」のではなく「機能を作る」ことに集中できます。
