# Palette Refresh + Why INOVAR Section Redesign

**Date:** 2026-04-18
**Scope:** Whole-site color token swap · Why INOVAR section full redesign · Section reorder

---

## 1. Motivation

The current green/gold palette reads as a tropical eco brand rather than a luxury flooring label. The new direction is inspired by Aesop: warm, restrained, no greens, terracotta replacing metallic gold. Paired with a full redesign of the Why INOVAR section to showcase INOVAR's 9 proprietary technologies in a premium editorial layout.

---

## 2. Color Token Changes

All changes are made inside the `:root {}` block in `index.html`. Tokens are renamed and repurposed — nowhere in the HTML or CSS should `--green`, `--green-lt`, `--gold`, or `--gold-lt` remain after this change.

| Token | Old value | New value | Notes |
|---|---|---|---|
| `--dark` | `#1c2b1e` | `#1c1714` | Brown-black, not green-black |
| `--terra` | — | `#8c5e4a` | New primary accent (terracotta) |
| `--terra-lt` | — | `#b07a66` | Lighter terracotta for hover states |
| `--sand` | `#f5f0e8` | `#f2ede5` | Linen, slightly cleaner |
| `--warm-white` | `#faf8f4` | `#faf7f2` | Stays very close |
| `--text` | `#2c2c2c` | `#2c2420` | Warm brown-black |
| `--muted` | `#524840` | `#7a6b63` | Warm grey-brown |
| `--stone` | `#c8bfaf` | `#c4b8af` | Minimal change |
| `--green` | `#2d6a4f` | **removed** | Replace all uses with `--terra` |
| `--green-lt` | `#3d8a65` | **removed** | Replace all uses with `--terra-lt` |
| `--gold` | `#b8955a` | **removed** | Replace all uses with `--terra` |
| `--gold-lt` | `#d4aa70` | **removed** | Replace all uses with `--terra-lt` |
| `--info-bar-h` | `36px` | unchanged | |
| `--nav-h` | `70px` | unchanged | |

### Search-and-replace rules
After updating `:root`, do a full-file find-and-replace:
- `var(--green)` → `var(--terra)`
- `var(--green-lt)` → `var(--terra-lt)`
- `var(--gold)` → `var(--terra)`
- `var(--gold-lt)` → `var(--terra-lt)`
- `var(--gold-light)` → `var(--terra-lt)` (if present)

---

## 3. Section Reorder

Move the Why INOVAR section (`<!-- WHY INOVAR -->`) to sit **between the Stats strip and the Products section**. The new page order becomes:

1. Info bar
2. Navigation
3. Hero
4. Trust badges strip
5. Stats / social proof
6. **Why INOVAR** ← moved up from position 7
7. Products
8. Before/After slider
9. Gallery
10. Floor calculator
11. Testimonials
12. FAQ
13. Contact + Footer
14. Floating WhatsApp

---

## 4. Why INOVAR Section — Full Redesign

### 4.1 Layout

Replace the current 2-column (text left / cards right) layout entirely with a full-width editorial section:

- **Background:** `var(--dark)` — creates a visual anchor between the light sections
- **Padding:** `6rem 8%` desktop, `4rem 5%` mobile
- **Inner container:** max-width 1200px, centered

### 4.2 Section Header (centered)

```
[eyebrow] Teknologi Unggulan
[h2]      Dibangun untuk Iklim Tropis
[rule]    40px wide, 2px, var(--terra), centered, margin 1.2rem auto
[p]       CoreGuard Hardwood HDF — material inti eksklusif INOVAR yang menjadi
          fondasi dari setiap teknologi perlindungan di bawah ini.
```

- Eyebrow: `var(--terra-lt)`, 0.72rem, letter-spacing 0.15em, uppercase, Figtree 500
- H2: Gloock, ~2.6rem desktop / ~2rem mobile, `var(--warm-white)`
- Intro paragraph: Figtree 300, `var(--stone)`, max-width 560px, centered, 1.75 line-height

### 4.3 Feature Grid

9 cards in a CSS grid:
- **Desktop (>1024px):** `grid-template-columns: repeat(3, 1fr)`, gap 1.5rem
- **Tablet (768px–1024px):** `repeat(2, 1fr)`
- **Mobile (<768px):** `1fr`

**Card anatomy (top to bottom):**
1. Top border: 3px solid `var(--terra)` (`border-top: 3px solid var(--terra)` overrides the 1px default)
2. Padding: 1.8rem
3. SVG icon: 36×36px, `var(--terra-lt)` stroke/fill, margin-bottom 1rem
4. Feature name: Gloock, 1.1rem, `var(--warm-white)`, margin-bottom 0.4rem
5. Description: Figtree 300, 0.88rem, `var(--stone)`, line-height 1.75

**Card resting state:**
- Background: `rgba(255, 255, 255, 0.04)`
- Border: 1px solid `rgba(176, 122, 102, 0.15)` (terra at 15% opacity) — all four sides
- Top border overrides to 3px solid `var(--terra)` (see above)
- Border-radius: 4px

**Card hover state:**
- `transform: translateY(-5px)`
- Border-color: `rgba(176, 122, 102, 0.5)`
- Icon: `transform: scale(1.08)`
- Transition: 0.3s ease all

### 4.4 The 9 Features

| # | Name | Icon (SVG description) | Indonesian description |
|---|---|---|---|
| 1 | AquaBloc | Water droplet with waves beneath | CoreGuard Hardwood HDF menjadikan INOVAR lantai laminate paling tahan air di dunia. Sistem Interlocking Extra-Presisi mencegah rembesan air masuk melalui sambungan papan. |
| 2 | Termite Bloc | Shield with an X | Material CoreGuard tropical hardwood menjadikan INOVAR lantai laminate paling tahan rayap di pasaran — perlindungan sejati untuk iklim Indonesia yang lembab. |
| 3 | WaxGuard Plus | Layered circles (seal/wax stamp) | Teknologi vacumat terkini melapisi sambungan interlocking dengan paraffin, meredam bunyi berderit akibat tekanan dan meningkatkan ketahanan air secara keseluruhan. |
| 4 | Stain Resistant | Shield with droplet repelling off | Permukaan dilapisi coating khusus yang menolak noda dari tumpahan minuman, minyak, dan kotoran sehari-hari — tetap bersih dengan mudah. |
| 5 | Wear Resistant AC4 | Diamond / gem shape | Rating keausan AC4 memastikan lantai tahan terhadap lalu lintas tinggi — cocok untuk hunian aktif maupun area komersial. |
| 6 | UV Resistant | Sun with rays | Formulasi khusus melindungi warna dan tekstur lantai dari paparan sinar UV langsung — tidak pudar meski terkena cahaya matahari setiap hari. |
| 7 | CoreGuard HDF | Wood grain / stacked layers | Inti papan dari tropical hardwood HDF eksklusif yang lebih padat dan tahan lama dibanding HDF biasa — fondasi dari seluruh keunggulan INOVAR. |
| 8 | Anti Abrasive Overlay | Stacked horizontal lines (overlay) | Lapisan permukaan anti-abrasi yang melindungi lantai dari goresan furnitur, hak sepatu, dan penggunaan berat sehari-hari. |
| 9 | Nano Guard 7/24 | Shield with sparkle / atom | Teknologi nano aktif 24 jam yang menghambat pertumbuhan bakteri dan jamur — mencegah bau tidak sedap dan menjaga kebersihan lantai secara mikrobiologis. |

### 4.5 Scroll Animations

All existing `.reveal` / IntersectionObserver infrastructure stays — no new JS needed.

- Section header (`why-header`): `reveal` class (fade up)
- Each card: `reveal` class with stagger delays `reveal-d1` through `reveal-d9`
- Stagger increment: 0.1s per card (matching the existing d1–d5 pattern in the codebase)

Add delay classes d6–d9 (d1–d5 already exist):
```css
.reveal-d6 { transition-delay: 0.6s; }
.reveal-d7 { transition-delay: 0.7s; }
.reveal-d8 { transition-delay: 0.8s; }
.reveal-d9 { transition-delay: 0.9s; }
```

### 4.6 Bottom CTA

Below the grid, centered:
```
[p]   Ingin tahu produk mana yang paling cocok untuk ruangan Anda?
[a]   Konsultasi Gratis →   (btn-primary)
```
- Paragraph: `var(--stone)`, Figtree 300, margin-bottom 1.2rem
- Button links to `#kontak`

---

## 5. CSS Class Changes

The following old classes are **replaced entirely** — remove their CSS rules and HTML markup:

| Old class | Replacement |
|---|---|
| `.why-inner` | `.why-new-inner` |
| `.why-text` | removed (header is now centered, not columnar) |
| `.why-body` | removed |
| `.why-features` | `.why-grid` |
| `.why-feat-card` | `.why-card` |
| `.why-feat-icon` | `.why-card-icon` |
| `.why-feat-title` | `.why-card-name` |
| `.why-feat-desc` | `.why-card-desc` |

---

## 6. Products Section — Trim + "See More" CTA

### 6.1 Keep only first 4 products

Remove product cards 5–12 from the `.product-grid`. Keep only:
1. Eskimo
2. Balinese Teak Rio
3. Yangon Teak
4. Vendura

Delete all HTML for: Amber, Sumatran Teak, Safari Walnut, QLD Spotted Gum, Dinelli, Montreux Walnut, American Walnut, Monument Oak.

Also remove their corresponding CSS thumb classes (`pt-amber`, `pt-sumatran`, `pt-safari`, `pt-qld`, `pt-dinelli`, `pt-montreux`, `pt-american`, `pt-monument`) from the `<style>` block.

### 6.2 "See More" block

After the closing `</div>` of `.product-grid`, add a centred block:

```html
<div class="products-more reveal">
  <p class="products-more-text">
    Ini hanya sebagian kecil dari koleksi kami. Ada puluhan pilihan warna, tekstur, dan
    karakter kayu yang menunggu untuk Anda temukan — ceritakan proyek Anda kepada kami,
    dan kami akan merekomendasikan yang paling tepat untuk ruangan Anda.
  </p>
  <a href="https://wa.me/6261XXXXXXX?text=Halo%2C%20saya%20ingin%20melihat%20koleksi%20lengkap%20INOVAR%20FLOOR" class="btn-primary" target="_blank" rel="noopener">
    Lihat Koleksi Lengkap &rarr;
  </a>
</div>
```

**CSS for `.products-more`:**
```css
.products-more {
  text-align: center;
  margin-top: 3.5rem;
  padding: 2.5rem;
  border: 1px solid rgba(var(--stone), 0.4);
  border-radius: 4px;
  max-width: 620px;
  margin-left: auto;
  margin-right: auto;
}
.products-more-text {
  font-size: 1rem;
  line-height: 1.85;
  color: var(--muted);
  margin-bottom: 1.8rem;
  font-style: italic;
}
```

---

## 7. Out of Scope

- No changes to any other section's HTML structure — only color tokens change via search-and-replace
- No font changes
- No JS changes beyond adding delay classes
- Product section content unchanged
- Images folder unchanged
