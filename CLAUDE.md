# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

A static, no-build website published via **GitHub Pages** and served at `links.clearpass.me` (see `CNAME`). It hosts simple, mobile-first "link in bio" / payment landing pages for ClearPass clients. There is no build step, package manager, test suite, or framework — editing an `.html` file and pushing to `main` deploys it.

## Structure & conventions

- The root `index.html` is the ClearPass hub linking out to per-client pages.
- Each client gets its own top-level directory (`asa_tennis/`, `isaac_climbing/`) containing its page(s) and a local `assets/` folder holding that client's `logo.png`.
- Shared favicons and the ClearPass logo live in the root `/assets/` and are referenced with absolute paths (`/assets/...`) so they resolve from any client subdirectory.
- Pages are **fully self-contained**: HTML + a single inline `<style>` block, no shared CSS/JS files. New pages are created by copying an existing one and adapting it.

### Page anatomy (consistent across all pages)

- `<html lang="he">` — content is Hebrew / RTL.
- A centered `.page` card (`max-width: 360px`) containing a `.logo` image, an `<h1>`, and a vertical stack of `a.button` link elements.
- Buttons are full-width colored blocks (`display: block`, `border-radius: 8px`, white bold text) with a darker `:hover`. Color-variant classes (e.g. `pink-button`, `light-blue-button`, `orange-button` in `isaac_climbing/links.html`) follow this same pattern.
- Open Graph + Twitter Card meta tags drive link previews; `og:image`/`og:url` use absolute `https://links.clearpass.me/...` URLs.

### Notable per-page details

- `isaac_climbing/links.html` loads the **Heebo** Google Font (`fonts.googleapis.com`) and renders emoji via the **Twemoji** CDN script (`twemoji.parse` on `DOMContentLoaded`). It is the most styled page and the best template for new font/emoji-rich pages.
- Button links point to external services: ClearPass form flows (`forms.clearpass.me/...`) and payment providers (`meshulam.co.il/quick_payment?b=...`, `hugim.org.il`). These hardcoded URLs/tokens are the primary thing edited when updating a client page.

## Working in this repo

- Preview locally by opening the `.html` file directly in a browser, or serve the root with any static server (e.g. `python3 -m http.server`) so absolute `/assets/` paths resolve.
- Keep new pages RTL (`lang="he"`, Hebrew copy) and reuse the existing `.page` / `.button` structure rather than introducing new layout systems.
