# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Interactive biography and works overview of Johann Wolfgang von Goethe, implemented as two standalone HTML files with no build tools or dependencies.

## Architecture

- **`index.html`** — Scroll-based museum-style website (~88KB). Full biography, 12 works, poems (Erlkönig + Zauberlehrling full text), quotes, 3D animations. All CSS/JS embedded.
- **`slideshow.html`** — 26-slide presentation (~67KB) optimized for projector/beamer. Includes TTS (Web Speech API) with distinct character voices for Erlkönig, scrollable poem slides, sidebar navigation.

Both files are self-contained single-file HTML with embedded CSS and JS. No frameworks, no build step.

## Key Technical Details

- **Fonts**: Google Fonts (Playfair Display, Cormorant Garamond, EB Garamond) loaded via CDN
- **3D Effects**: CSS 3D Transforms (book animation in both files), CSS animations, parallax
- **Scroll Animations**: IntersectionObserver with `threshold: 0.02` (low threshold needed for tall poem sections)
- **Slideshow TTS**: Web Speech API with voice discovery for macOS German voices (Anna, Markus, etc.). Voice profiles per character role via pitch/rate modulation. Erlkönig uses 4 distinct voice profiles; Zauberlehrling has progressive panic effect (rate/pitch increase with stanza index).
- **Slideshow Navigation**: Keyboard (arrows, space, tab), click zones, swipe, mousewheel. Poem slides have special scroll behavior — mousewheel scrolls content, only navigates at scroll boundaries.
- **Sidebar**: Hidden left panel, triggered by mouse hover on left edge or Tab key. Built dynamically from `slideMeta` array.

## Content Language

All content is in German. Poems use historical orthography (e.g., "faßt", "ächzende").

## Conventions

- Color scheme: `--cream`, `--gold`, `--green-deep`, `--burgundy`, `--charcoal` (CSS custom properties)
- Slide indexing: `data-index` attributes must be sequential (0-based). Re-index with the python script pattern used previously if slides are added/removed.
- Poem slides use class `poem-slide` for special scroll/navigation handling
- Dark sections use class `dark-poem` for inverted color scheme