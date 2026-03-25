# Claude RTL Skill — Session Notes

## Project summary

A skill for Claude (desktop and web) that renders Hebrew, Arabic, and Persian/Farsi responses as inline HTML artifacts with proper RTL layout, instead of plain LTR chat text.

## Key files

- `SKILL.md` — the installable skill file (uploaded via Customize → Upload Skill)
- `README.md` — install and usage instructions
- `assets/` — before/after screenshots

## Install flow

Users download `SKILL.md`, open Claude (desktop or web), go to **Customize → Upload Skill**, and select the file. The skill triggers automatically on Hebrew (U+0590–U+05FF) and Arabic/Farsi (U+0600–U+06FF, U+FB50–U+FDFF, U+FE70–U+FEFF) input.

## Skill design decisions

- Skill must be a `.md` file — NOT a ZIP. Claude's upload skill UI accepts `.md` directly.
- The skill must say **do NOT use file tools** — otherwise Claude creates an artifact as a separate file instead of rendering inline.
- Keep the skill minimal — it runs on nearly every prompt so token count matters.
- Supported languages narrowed to Hebrew, Arabic, Farsi only (removed Urdu, Yiddish, Syriac, etc.).
- No examples in the skill file — kept to template + rules only.

## Rendering rules (in SKILL.md)

- `direction: rtl; text-align: right` on outer container
- `line-height: 1.7` for Hebrew, `1.9` for Arabic/Farsi
- `padding-right` for list indentation
- Inline LTR content wrapped in `<span style="direction: ltr; display: inline-block;">`
- Colors via CSS variables only (`var(--color-text-primary)`, etc.)
