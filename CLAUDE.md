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

## Redesign: INOVAR FLOOR MEDAN

The site is being rebuilt as **INOVAR FLOOR MEDAN** — an authorized franchise dealer of the Malaysian INOVAR FLOOR brand in Medan, Indonesia. See `docs/superpowers/specs/2026-04-18-inovar-floor-medan-redesign.md` for the full spec.

## Design Context

### Users
Local customers in Medan, Indonesia — residential (homeowners renovating) and commercial (hotel managers, property developers). They browse primarily on mobile during the day, comparing INOVAR FLOOR against cheaper Chinese alternatives. Job to be done: decide whether to trust this store and get in touch for a quote.

### Brand Personality
**Three words:** Prestigious · Trustworthy · Local

Authorized franchise of an international Malaysian flooring brand, 20+ years in Medan. Premium and authoritative but warm and locally rooted. Confident without being cold.

### Aesthetic Direction
Premium home interiors brand feel — editorial richness, dramatic imagery, sophisticated typography. Light base (warm sand/cream) with dark accent sections. First impression goal: "This is nothing like the cheap flooring shops."

**Must avoid:** Cheap/cluttered local shop feel, generic corporate blues/greys, dated flat design.

### Typography
- **Display/Headings: Gloock** (Google Fonts) — editorial serif, dramatic stroke contrast, luxury magazine feel
- **Body/UI: Figtree** (Google Fonts) — warm humanist sans, readable on mobile

### Design Principles
1. **Material warmth over digital sleekness** — Evoke wood grain, warmth, weight. Avoid cold tech aesthetics.
2. **Immediate quality signal** — Design must visually communicate superiority to cheap alternatives within first scroll.
3. **Editorial confidence** — Bold typography, generous white space, confident asymmetry. Don't center everything.
4. **Commercially purposeful** — Every section moves visitors toward a WhatsApp message or phone call.
5. **Locally grounded** — Indonesian language copy, Medan identity. International credential is a badge, not the whole story.
