# Zalloween Landing Page — Plan

Single-file landing page built with modern HTML, CSS, and minimal vanilla JavaScript.

## Files to create

| File | Purpose |
|---|---|
| `/workspace/index.html` | The single-file page (HTML + CSS + JS) |
| `/workspace/fonts/butcherman.ttf` | Butcherman 400, downloaded from Google Fonts (self-hosted) |
| `/workspace/fonts/amaranth-regular.ttf` | Amaranth 400 |
| `/workspace/fonts/amaranth-bold.ttf` | Amaranth 700 |

Fonts are **downloaded**, not referenced from Google Fonts at runtime. Both are registered with local `@font-face` rules.

## Source data

- 43 JPEG images in `/workspace/images/`, named by numeric tweet ID (e.g. `1984215235478376686.jpeg`).
- Two files share one ID: `1984154997085639009-1.jpeg` and `1984154997085639009-2.jpeg`. Strip the `-1`/`-2` suffix — both link to the same tweet.

## Page structure

```
<header>            sticky, "Zalloween" in Butcherman, #F3B724
<main>
  <div band>        "2026 Edition" — #F3B724 bg, #271219 text
  <section box>     lorem ipsum, #F3B724 bg, #271219 text
  <div band>        "2025 Edition"
  <div masonry>     all 43 images, reversed file-name order
</main>
<footer>            narrow, a couple of lorem ipsum lines
<modal>             hidden overlay: full-width real-color image (tweet link)
```

## Layout & styling

- **Background:** `#271219` (page).
- **Titles / headings:** `#F3B724`. **Body text:** white. **Box text:** `#271219` (decided for contrast on the gold box).
- **Header:** `position: sticky; top: 0`, with z-index above the modal-free content; title "Zalloween" in Butcherman.
- **Edition bands:** narrow full-width bands, `#F3B724` background, `#271219` text ("2026 Edition", "2025 Edition").
- **Box:** `#F3B724` background with lorem ipsum placeholder text.
- **Masonry grid:** CSS multi-column (`columns` + `break-inside: avoid`) — pure CSS, no JS.
- **Footer:** narrow, lorem ipsum placeholder lines.

## Image behaviour

1. **Grid order:** reversed file-name order (descending lexicographic sort).
2. **Dark overlay:** each thumbnail wrapped in a `figure` with an `::after` layer of `#271219` at ~90% opacity — image faintly visible; opacity fades to 0 on hover (pure CSS).
3. **Click → modal:** overlay opens with the image at full width in real colors (no dark overlay).
4. **Tweet link:** in the modal, the image itself is an `<a>` to `https://x.com/jenkin27/status/<id>` (id = file name without `.jpeg`, minus any `-1`/`-2` suffix).
5. **Close modal:** × button, backdrop click, or `Esc`.

## JavaScript (minimal)

- One small inline `<script>` (~20 lines), modal-only:
  - open on thumbnail click (sets modal image `src` and tweet `href`),
  - close on ×, backdrop, `Esc`.
- The image list is **hardcoded in the HTML** (generated at build time in reversed order) — no runtime fetch, no manifest, no build step.

## Implementation notes

- Modern syntax: custom properties for the palette, no frameworks, semantic elements.
- All assets local: fonts in `fonts/`, images in `images/`. Page must work fully offline.
- Verify: header sticks on scroll, hover reveals color, modal opens full-width with real colors and correct tweet URLs, `-1`/`-2` files resolve to the shared status ID.
