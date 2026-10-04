# Personal homepage

The source of my personal homepage: who I am, what I am working on, and the notes I write down.

**Live:** https://homepage-9cw.pages.dev

## What it is

- A single static page, hand-written in HTML and CSS — no framework, no build step
- No external requests: no CDN, no web fonts, no icon library (the icons are inline SVG)
- Responsive down to phone widths, with a light/dark toggle that follows the system preference
- Typography-first layout with a sticky sidebar, so the page stays readable as more sections get added

## Files

| File | What it is |
| --- | --- |
| `index.html` | The page itself: intro, projects, notes, about, and the inline SVG icon set |
| `style.css` | All styling; colours are defined once at the top in `:root` |
| `favicon.svg` | Site icon |
| `_headers` | Response headers |

## Editing

- Text, links and sections live in `index.html`
- Colours (`--bg`, `--ink`, `--accent`, ...), spacing and breakpoints live in `style.css`
