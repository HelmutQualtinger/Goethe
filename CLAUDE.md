# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Interactive biography and works overview of Johann Wolfgang von Goethe (1749–1832), implemented as two standalone HTML files, a Markdown handout, and a PDF. No build tools or dependencies.

## Files

- **`index.html`** (~95KB) — Scroll-based museum-style website. Full biography (6 chapters + family section), 12 works, 6 poems (Erlkönig + Zauberlehrling as full text with speaker labels), quotes, 3D book animation, Goethe portrait. Dark/light theme toggle.
- **`slideshow.html`** (~81KB) — 29-slide presentation optimized for projector. TTS with distinct character voices, scrollable poem and biography slides, sidebar navigation. Dark/light theme toggle.
- **`handout.md`** — Markdown version of the full biography with poems, convertible to PDF.
- **`handout.pdf`** — PDF handout generated via pandoc.
- **`img/goethe-stieler.jpg`** — Stieler portrait (1828), public domain from Wikimedia. Referenced by all three content files.

## Architecture

Both HTML files are self-contained single-file HTML with all CSS and JS embedded inline. No frameworks, no build step.

### index.html
- CSS custom properties for theming: `--cream`, `--gold`, `--green-deep`, `--burgundy`, `--charcoal`
- `[data-theme="dark"]` overrides for dark mode; default is light
- IntersectionObserver with `threshold: 0.02` (low threshold needed for tall poem sections)
- 3D book: CSS 3D Transforms with mouse interaction via `requestAnimationFrame`
- Theme state persisted in `localStorage` key `goethe-theme`

### slideshow.html
- 29 slides with `data-index` attributes (0-based, must be sequential)
- `[data-theme="light"]` overrides for light mode; default is dark
- `slideMeta` array (in JS) must match slide count and order — used for sidebar navigation
- Poem slides use class `poem-slide` for special scroll/navigation handling
- Biography slides use `.left-col` with `overflow-y: auto` for scrolling
- `getScrollableArea()` function handles both poem and biography scroll detection
- TTS: Web Speech API with voice discovery for macOS German voices. Voice profiles per character via pitch/rate. Zauberlehrling has progressive panic effect.
- Navigation: keyboard (arrows, space, tab, F, Home/End), click zones, swipe, mousewheel with scroll boundary detection

## Common Commands

```bash
# View in browser
open index.html
open slideshow.html

# Generate PDF from markdown
pandoc handout.md -o handout.pdf --pdf-engine=xelatex \
  -V geometry:"portrait,margin=2cm" -V fontsize=11pt \
  -V documentclass=article -V mainfont="Helvetica" -V lang=de

# Re-index slides after adding/removing (python3)
python3 -c "
import re
with open('slideshow.html','r') as f: content = f.read()
counter = [0]
def repl(m):
    idx = counter[0]; counter[0] += 1
    return re.sub(r'data-index=\"\d+\"', f'data-index=\"{idx}\"', m.group(0))
content = re.sub(r'<div class=\"slide [^\"]*?\"[^>]*data-index=\"\d+\"', repl, content)
with open('slideshow.html','w') as f: f.write(content)
print(f'Re-indexed {counter[0]} slides')
"
```

## Conventions

- All content is in German. Poems use historical orthography (e.g., "faßt", "ächzende").
- Google Fonts: Playfair Display, Cormorant Garamond, EB Garamond (loaded via CDN)
- When adding slides: update both `data-index` attributes (use re-index script) AND the `slideMeta` array in JS
- Dark sections in index.html use class `dark-poem` for inverted color scheme
- Theme toggle button: `z-index: 99999`, fixed top-right corner
- Slide backgrounds: use clean solid colors or simple linear-gradients (no radial-gradient ellipses — they cause visual artifacts on projection)
