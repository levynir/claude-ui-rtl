# Claude RTL Skill

A Claude Code skill that renders responses in right-to-left (RTL) languages inside a properly formatted HTML widget, instead of plain left-to-right chat text.

## Supported languages

Any RTL language is automatically detected and rendered correctly, including:

| Language | Script |
|---|---|
| Hebrew | Hebrew |
| Arabic | Arabic |
| Persian / Farsi | Perso-Arabic |
| Urdu | Perso-Arabic (Nastaliq) |
| Yiddish | Hebrew |
| Pashto | Perso-Arabic |
| Kurdish (Sorani) | Perso-Arabic |
| Sindhi | Perso-Arabic |
| Uyghur | Perso-Arabic |
| Syriac | Syriac |
| Dhivehi | Thaana |

## Installation

1. Download [`rtl.skill`](https://raw.githubusercontent.com/levynir/claude-ui-rtl/main/rtl.skill)
2. Open Claude (desktop or web)
3. Go to **Customize → Upload Skill**
4. Select the file

## Usage

The skill triggers **automatically** whenever your message contains RTL-script characters. You can also invoke it explicitly:

```
/rtl
```

### Examples

Simply write in any RTL language and Claude will render the response in an RTL widget:

```
מה זה בינה מלאכותית?
```
```
ما هو الذكاء الاصطناعي؟
```
```
هوش مصنوعی چیست؟
```

## How it works

When triggered, Claude renders the response inside an HTML Artifact with:

- `direction: rtl; text-align: right` on the container
- `padding-right` (not `padding-left`) for list indentation
- `direction: ltr; display: inline-block` wrappers for any inline LTR content (code, URLs, numbers)
- Claude UI CSS variables for colors — works correctly in both light and dark mode
- Appropriate line heights (≥ 1.9 for Arabic/Persian scripts which need more vertical space)

No colors are hardcoded — the widget respects the active Claude UI theme automatically.

## Layout variants

The skill automatically selects the appropriate layout based on content:

- **Short answer** — single paragraph
- **Prose** — multiple paragraphs with spacing
- **List** — `<ul>` with RTL-aware indentation
- **Sections** — headings with a subtle divider
- **Cards** — bordered containers for structured or comparison data
- **Mixed content** — RTL prose with inline LTR segments (code snippets, proper nouns)

## File

| File | Description |
|---|---|
| `rtl.skill` | The installable skill (ZIP archive containing `SKILL.md`) |
