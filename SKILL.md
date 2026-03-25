---
name: rtl
description: Display Hebrew, Arabic, and Persian/Farsi responses inside an HTML Artifact with proper RTL layout. Use this skill whenever the user writes in Hebrew, Arabic, or Persian/Farsi. Always render the answer in a right-to-left HTML widget — never respond in plain chat.
---

# RTL Language Responses

When the user writes in Hebrew, Arabic, or Persian/Farsi, render the entire answer inside an HTML Artifact using `direction: rtl` and `text-align: right`.

## When to trigger

- User message contains Hebrew characters (U+0590–U+05FF)
- User message contains Arabic/Perso-Arabic characters (U+0600–U+06FF, U+FB50–U+FDFF, U+FE70–U+FEFF)
- User asks to respond in Hebrew, Arabic, or Persian/Farsi
- User explicitly invokes `/rtl`

## How to render

Always use the Artifact system with the following base structure:

```html
<div style="direction: rtl; text-align: right; font-family: var(--font-sans); padding: 1rem 0;">
  <!-- content here -->
</div>
```

## Layout rules

Use the minimal layout that fits the content:

**Short answer / single fact:**
```html
<div style="direction: rtl; text-align: right; font-family: var(--font-sans); padding: 1rem 0;">
  <p style="font-size: 15px; color: var(--color-text-primary); line-height: 1.7; margin: 0;">
    התשובה כאן.
  </p>
</div>
```

**Prose / explanation (multiple paragraphs):**
```html
<div style="direction: rtl; text-align: right; font-family: var(--font-sans); padding: 1rem 0;">
  <p style="font-size: 15px; color: var(--color-text-primary); line-height: 1.7; margin: 0 0 1rem;">פסקה ראשונה...</p>
  <p style="font-size: 15px; color: var(--color-text-primary); line-height: 1.7; margin: 0;">פסקה שנייה...</p>
</div>
```

**List / bullet points:**
```html
<div style="direction: rtl; text-align: right; font-family: var(--font-sans); padding: 1rem 0;">
  <ul style="padding-right: 1.25rem; padding-left: 0; margin: 0; font-size: 15px; color: var(--color-text-primary); line-height: 1.7;">
    <li>פריט א׳</li>
    <li>פריט ב׳</li>
    <li>פריט ג׳</li>
  </ul>
</div>
```

**Section headings:**
```html
<h2 style="font-size: 18px; font-weight: 500; color: var(--color-text-primary); margin: 0 0 0.75rem; border-bottom: 0.5px solid var(--color-border-tertiary); padding-bottom: 8px;">כותרת</h2>
```

**Mixed Hebrew + LTR content** (e.g. code, numbers, proper nouns in Latin script):
```html
<div style="direction: rtl; text-align: right; font-family: var(--font-sans); padding: 1rem 0;">
  <p style="font-size: 15px; color: var(--color-text-primary); line-height: 1.7; margin: 0;">
    הפונקציה <span style="direction: ltr; display: inline-block; font-family: monospace;">getUserName()</span> מחזירה מחרוזת.
  </p>
</div>
```

## Design rules

- Always wrap everything in a `direction: rtl; text-align: right` container
- Use `padding-right` instead of `padding-left` for indentation
- For inline LTR segments (code, URLs, numbers), wrap in `<span style="direction: ltr; display: inline-block;">`
- Never hardcode colors — always use CSS variables (`var(--color-text-primary)`, etc.)
- Use `font-weight: 500` for headings, `400` for body
- No gradients, shadows, or decorative effects
- Keep background transparent on the outer container
- Line height: at least `1.7` for Hebrew, at least `1.9` for Arabic and Persian/Farsi
