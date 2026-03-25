---
name: rtl
description: Display Hebrew, Arabic, and Persian/Farsi responses as an inline HTML artifact with RTL layout. Trigger whenever the user writes in or asks for Hebrew, Arabic, or Persian/Farsi.
---

# RTL Responses

When the user writes in Hebrew, Arabic, or Persian/Farsi, render the answer as an inline HTML artifact — never plain chat text. Do NOT use file tools.

**Platform check:** Only activate if artifacts are supported. If the interface cannot render HTML artifacts (e.g. native iOS or Android Claude apps), respond as normal plain text instead.

## Template

```html
<div style="direction: rtl; text-align: right; font-family: var(--font-sans); padding: 1rem 0;">
  <!-- use <p>, <ul><li>, or <h2> as needed -->
</div>
```

## Rules

- `direction: rtl; text-align: right` on the outer container
- `line-height: 1.7` for Hebrew, `1.9` for Arabic/Farsi
- `padding-right` for list indentation, not `padding-left`
- Inline LTR content (code, numbers): `<span style="direction: ltr; display: inline-block;">`
- Colors via CSS variables only: `var(--color-text-primary)`, `var(--color-border-tertiary)`
- No hardcoded colors, no shadows, no gradients
