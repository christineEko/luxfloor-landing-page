# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

**LuxFloor** — a single-page static HTML/CSS landing page for a premium laminate flooring brand. No build tools, no frameworks, no dependencies. The entire site lives in `index.html`.

## Development

Open `index.html` directly in a browser — no build step or local server required.

## Architecture

All HTML, CSS, and any future JavaScript are self-contained in `index.html`. The page is organized into these sections (in order):

1. **Nav** — Fixed header with glassmorphism backdrop blur
2. **Hero** — Full-viewport two-column grid with headline and hero image
3. **Section Divider** — Decorative element
4. **Collections** — 5-column product card grid (responsive: 3-col at 1024px, 2-col at 768px)
5. **Features Strip** — Dark-background 4-column icon grid (responsive: 2-col at 768px)
6. **Footer** — Logo and copyright

## Design System

All design tokens are defined as CSS custom properties at the top of the `<style>` block:

- **Colors**: `--cream`, `--warm-white`, `--stone`, `--walnut`, `--espresso`, `--gold`, `--gold-light`, `--text`, `--muted`
- **Typography**: Cormorant Garamond (serif, headings) + Jost (sans-serif, body) via Google Fonts
- **Responsive breakpoints**: 1024px and 768px

Product cards use `repeating-linear-gradient` for wood-grain texture backgrounds. New collections should follow the same gradient pattern with colors drawn from the palette.

## Content Status

Product cards are currently placeholders ("Product Name", "Collection Placeholder", "From $X.XX / sq ft"). These will need real product data when building out the catalogue.
