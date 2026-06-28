# XYZ Chat — UI Mockup

A zero-dependency, single-file HTML mockup of a Claude-style AI chat interface.  
Accessible (WCAG AA), mobile-friendly, dark-mode ready. Drop the file in a browser — it just works.

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
