# INOVAR FLOOR MEDAN — Website Redesign Spec
**Date:** 2026-04-18
**Approach:** Sales-First Landing Page

---

## Overview

Complete redesign of `index.html` for **INOVAR FLOOR MEDAN** — an authorized franchise dealer of the Malaysian INOVAR FLOOR brand, located in Medan, Indonesia. The business has been operating for 20+ years and has completed 1,000+ installation projects including hotels, commercial buildings, apartment complexes, and the Berastagi complex.

**Primary goal:** Drive sales enquiries via WhatsApp and phone calls from new and returning customers in Medan.

**Language:** Mostly Bahasa Indonesia for body copy; product names and brand taglines remain in English.

---

## Design System

### Color Palette
| Token | Hex | Usage |
|---|---|---|
| `--dark` | `#1c2b1e` | Nav, footer, dark sections, text |
| `--green` | `#2d6a4f` | Primary brand accent, buttons, CTAs |
| `--green-lt` | `#3d8a65` | Hover states |
| `--sand` | `#f5f0e8` | Page background |
| `--warm-white` | `#faf8f4` | Card backgrounds |
| `--gold` | `#b8955a` | Secondary accent, dividers, highlights |
| `--text` | `#2c2c2c` | Body text |
| `--muted` | `#7a7068` | Subtext, captions |
| `--stone` | `#c8bfaf` | Borders, dividers |

### Typography
- **Headings:** Cormorant Garamond (serif) — 300/400/500 weights
- **Body/UI:** Jost (sans-serif) — 300/400/500 weights
- Both loaded via Google Fonts (already in project)

### Animations
All implemented in vanilla CSS + minimal vanilla JS (no external animation libraries):
- **Scroll reveal:** `IntersectionObserver` — elements fade + slide up 30px when entering viewport (`transition: opacity 0.6s ease, transform 0.6s ease`)
- **Staggered children:** Cards/grid items stagger entry with `transition-delay` increments of 100ms
- **Parallax hero:** CSS `transform: translateY()` on scroll via JS, subtle 0.3x rate
- **Counter animation:** JS counts up from 0 to target number over 1.5s when stat strip enters viewport
- **Hover effects:** CSS transitions only — no JS for hover states
- **Smooth scroll:** `scroll-behavior: smooth` on `html`

---

## Page Structure

### 0. SEO Meta Tags (in `<head>`)
```html
<title>INOVAR FLOOR MEDAN — Lantai Laminate Premium Terbaik di Medan</title>
<meta name="description" content="Distributor resmi INOVAR FLOOR di Medan. Lantai laminate premium tahan rayap, tahan air, tahan gores. 20+ tahun pengalaman, 1000+ proyek. Hubungi kami untuk penawaran terbaik.">
<meta name="keywords" content="lantai laminate Medan, toko lantai Medan, INOVAR FLOOR Medan, lantai kayu Medan Timur, distributor lantai laminate Sumatera Utara">
<meta property="og:title" content="INOVAR FLOOR MEDAN">
<meta property="og:description" content="Lantai laminate premium — tahan rayap, tahan air, tahan gores. Distributor resmi Medan.">
```

---

### 1. Top Info Bar
Slim strip at very top of page. Dark background (`--dark`). Small cream text.

**Layout (3 columns):**
- Left: `📍 Jl. M.H Thamrin No.1-i, Medan Timur`
- Center: `📞 (061) 4559900` &nbsp;·&nbsp; `📱 [mobile TBD]`
- Right: `Sen–Sab: 09.00–16.00 WIB &nbsp;·&nbsp; Minggu: Tutup`

**Mobile:** Collapses to single centered line — phone number + hours only. Address hidden.

---

### 2. Navigation
Sticky (`position: fixed`). Dark background (`--dark`). Below top bar (offset matches bar height).

**Left:** Logo — `INOVAR FLOOR` in Cormorant Garamond serif, `MEDAN` in smaller green text below.

**Center links:** Produk · Keunggulan · Kalkulator · Kontak

**Right:** Green button — `💬 Chat WhatsApp` — links to `https://wa.me/6261XXXXXXX` (mobile number TBD).

**Mobile:** Hamburger menu. Links stack vertically. WhatsApp button always visible.

**Scroll behaviour:** Nav gains a subtle shadow on scroll.

---

### 3. Hero Section
Full viewport height (`100vh`). Two-column grid.

**Left — Text column (padding 6rem 5% 6rem 8%):**
- Eyebrow: `Authorized Dealer · Medan, Indonesia` (small caps, gold)
- Headline: `"Lantai Impian Anda,`
  `Kualitas Internasional"` — Cormorant Garamond, large (`clamp(3rem, 5vw, 5.5rem)`), dark
- Subheading (Indonesian): *"Distributor resmi INOVAR FLOOR di Medan. Lantai laminate premium — tahan rayap, tahan air, dan tahan gores — untuk rumah, apartemen, dan gedung komersial Anda."*
- Phone number: `(061) 4559900` displayed large and bold, gold color
- CTA row:
  - Primary: green button `Hubungi via WhatsApp →`
  - Secondary: text link `Lihat Koleksi ↓`

**Right — Wood texture panel:**
- Full height, rich dark wood gradient (`#c8a882` → `#7a5535` → `#4a2e18`)
- CSS wood-grain overlay (repeating-linear-gradient, same technique as current)
- Floating glass badge bottom-left: `"Franchise Resmi INOVAR FLOOR Malaysia"`

**Animation:** Hero text fades in on load (staggered — eyebrow first, then h1, then sub, then CTAs). Parallax on right panel on scroll.

---

### 4. Quality Trust Badges Strip
Full-width dark section (`--dark`). 4 columns. Immediately after hero — first thing visitors see after scrolling.

| Icon | Title (EN) | Description (ID) |
|---|---|---|
| 🛡️ | Termite Bloc | *Perlindungan total dari serangan rayap* |
| 💧 | Aqua Bloc | *Tahan air, ideal untuk iklim tropis Indonesia* |
| ✨ | Stain Resistant | *Permukaan tahan noda, mudah dibersihkan* |
| 💪 | Wear Resistant | *Lapisan AC4 tahan gores dan tekanan berat* |

**Mobile:** 2×2 grid.
**Animation:** Slide up on scroll, staggered entry.

---

### 5. Stats / Social Proof Strip
Warm sand background. 4 stats in a row. Animated counters trigger when section enters viewport.

| Stat | Label |
|---|---|
| 20+ | Tahun Pengalaman |
| 1,000+ | Proyek Selesai |
| 12 | Koleksi Premium |
| Seumur Hidup | Garansi Produk |

Below stats, a single line in smaller text: *"Dipercaya oleh hotel, gedung perkantoran, apartemen, dan kompleks Berastagi."*

**Note:** First 3 stats use animated number counters. The 4th ("Seumur Hidup") is static text — no counter animation.

---

### 6. Produk Kami (Collections)
Section id: `#produk`

**Header:**
- Eyebrow: `Koleksi Kami`
- H2: `Produk INOVAR FLOOR Premium`
- Subtext: *"Semua koleksi tersedia di toko kami. Diskon khusus tersedia — hubungi kami untuk penawaran terbaik."*
- Gold banner strip: `✦ Diskon Tersedia · Hubungi Kami Sekarang`

**Grid:** 4 columns (3-col at 1024px, 2-col at 768px, 1-col at 480px).

**12 Products:**
1. Eskimo — warm light birch tones
2. Balinese Teak Rio — rich warm teak
3. Yangon Teak — deep golden teak
4. Vendura — light grey-beige contemporary
5. Amber — warm amber honey tones
6. Sumatran Teak — dark rich sumatran tones
7. Safari Walnut — mid-brown walnut
8. QLD Spotted Gum — pale eucalyptus with grain
9. Dinelli — cool dark walnut
10. Montreux Walnut — elegant mid-grey walnut
11. American Walnut — classic dark American walnut
12. Monument Oak — light stone/grey oak

Each card:
- Wood-tone gradient swatch (unique `repeating-linear-gradient` per product, aspect-ratio 3/4)
- Product name in English (Cormorant Garamond)
- Tag: `Premium Collection`
- Green button: `Minta Penawaran` — links to WhatsApp with pre-filled message: *"Halo, saya tertarik dengan produk [Product Name]. Boleh minta penawaran harga?"*

**Card hover:** Swatch zooms 1.03x, dark overlay fades in, button slides up from bottom.
**Animation:** Cards stagger into view on scroll.

---

### 7. Mengapa INOVAR FLOOR?
Section id: `#keunggulan`

Two-column layout. Left: text. Right: 2×2 feature grid.

**Left:**
- Eyebrow: `Keunggulan Kami`
- H2: `Bukan Sekadar Lantai Biasa`
- Body (Indonesian): *"Banyak produk lantai murah di pasaran yang terlihat bagus namun cepat rusak — retak, mengembang, dan berjamur. INOVAR FLOOR dirancang khusus untuk iklim tropis seperti Indonesia: tahan lembab, tahan rayap, dan mampu bertahan selama puluhan tahun meski digunakan setiap hari."*
- Secondary paragraph: *"Sebagai franchise resmi dari Malaysia, setiap produk INOVAR FLOOR telah melalui uji standar internasional. Bukan hanya indah — tapi investasi jangka panjang untuk properti Anda."*

**Right:** 4 feature cards (2×2 grid) — expanded version of trust badges with fuller descriptions.

**Animation:** Text slides in from left, feature grid slides in from right, on scroll.

---

### 8. Before/After Slider
Full-width section. Dark background. Drag-to-reveal comparison.

- Heading: *"Transformasi Nyata"*
- Subtext: *"Geser untuk melihat perbedaannya"*
- Drag handle divides "Sebelum" (Before) / "Sesudah" (After) photos
- Implementation: pure CSS + vanilla JS drag handler (no library)
- **Image placeholders:** `images/before.jpg` and `images/after.jpg` — user to provide

---

### 9. Galeri Pemasangan
Section id: `#galeri`

- Eyebrow: `Hasil Nyata`
- H2: `Galeri Pemasangan`
- Subtext: *"Hasil pemasangan INOVAR FLOOR di rumah dan gedung pelanggan kami"*
- Uniform grid: 3 columns, 3 rows = 9 photos (2-col on mobile)
- Clicking any photo opens a lightbox (fullscreen overlay with prev/next navigation)
- Lightbox: pure vanilla JS, no library
- **Image placeholders:** `images/gallery-1.jpg` through `images/gallery-9.jpg` — user to provide Instagram photos
- Caption on hover: optional short label (e.g. "Apartemen Medan, 2024")

---

### 10. Kalkulator Kebutuhan Lantai
Section id: `#kalkulator`

Warm sand background. Centered, max-width 600px.

- Eyebrow: `Rencanakan Proyek Anda`
- H2: `Kalkulator Kebutuhan Lantai`
- Subtext: *"Masukkan ukuran ruangan untuk menghitung kebutuhan lantai Anda"*

**Form:**
- Input: `Panjang Ruangan (meter)` — number input
- Input: `Lebar Ruangan (meter)` — number input
- Optional input: `Jumlah Ruangan` — number input, default 1
- Button: `Hitung Sekarang` (green)

**Result (animates in on calculate):**
- `Luas total: X m²`
- `Estimasi kebutuhan: X m² (termasuk 10% cadangan)`
- Collection recommendation:
  - < 15 m²: *"Cocok untuk: Eskimo, Vendura, Monument Oak — desain compact yang elegan"*
  - 15–30 m²: *"Cocok untuk: Sumatran Teak, Balinese Teak Rio, Safari Walnut — karakter kuat untuk ruang menengah"*
  - > 30 m²: *"Cocok untuk: American Walnut, Montreux Walnut, Yangon Teak — kesan luas dan mewah"*
- Green CTA button: `Dapatkan Penawaran via WhatsApp →`
  - Pre-fills WhatsApp message: *"Halo, saya perlu lantai untuk ruangan X m². Bisa minta penawaran terbaik?"*

**Animation:** Result section slides down with smooth reveal.

---

### 11. Testimoni Pelanggan
Warm off-white background. 3 testimonial cards.

Each card:
- Large opening quote mark (gold, decorative)
- Quote text (Indonesian)
- Customer name + location (e.g. *"Pelanggan dari Medan Sunggal"*)
- 5-star rating (gold stars)

**Placeholder content (replace with real testimonials):**
1. *"Kualitas lantainya luar biasa, sudah 5 tahun dipasang masih seperti baru. Tim INOVAR FLOOR Medan sangat profesional dan ramah."* — Budi S., Medan Selayang
2. *"Saya pasang di seluruh unit apartemen saya, hasilnya memuaskan. Tahan lama dan mudah dirawat."* — Hendra L., Medan Baru
3. *"Produknya premium, harganya bersaing. Puas banget, rekomendasikan ke siapa saja yang mau renovasi lantai."* — Sari W., Medan Sunggal

**Animation:** Cards stagger fade+slide-up on scroll (same pattern as product cards).

---

### 12. FAQ Section
Clean white background. Accordion style — click to expand/collapse answers.

**6 Questions:**
1. *Berapa lama proses pemasangan lantai laminate?* — Tergantung luas area, rata-rata 50–80 m² per hari.
2. *Apakah lantai laminate bisa dipasang di kamar mandi?* — Produk INOVAR dengan teknologi Aqua Bloc tahan percikan air, namun tidak disarankan untuk area yang terendam air sepenuhnya.
3. *Bagaimana cara merawat lantai laminate INOVAR?* — Cukup disapu dan dipel dengan kain lembab. Hindari air berlebihan dan bahan kimia keras.
4. *Apakah INOVAR FLOOR menyediakan jasa pemasangan?* — Ya, kami menyediakan jasa pemasangan profesional untuk setiap pembelian produk.
5. *Berapa garansi produk INOVAR FLOOR?* — Garansi seumur hidup untuk penggunaan residensial.
6. *Apakah ada minimum order?* — Tidak ada minimum order. Kami melayani dari satu ruangan hingga proyek gedung berskala besar.

**Animation:** Smooth accordion expand/collapse with CSS transitions.

---

### 13. Kontak & Lokasi
Section id: `#kontak`

Full-width. Dark background (`--dark`). Two columns.

**Left — Contact Details:**
- H2: `Kunjungi Toko Kami` (white, large)
- Large phone: `(061) 4559900` (gold, very prominent)
- Mobile: `[TBD]` (gold)
- WhatsApp button: green, large — `Chat WhatsApp Sekarang`
- Address with map link: `Jl. M.H Thamrin No.1-i, Sidodadi, Kec. Medan Tim., Kota Medan, Sumatera Utara 20233`
- Opening hours table:
  ```
  Senin – Sabtu   09.00 – 16.00 WIB
  Minggu          Tutup
  ```
- Tagline: *"Kami siap membantu Anda menemukan lantai yang tepat — datang langsung atau hubungi kami."*

**Right — Google Maps:**
- Embedded `<iframe>` Google Maps for the Medan Timur address
- Border-radius 8px, full height

---

### 14. Floating WhatsApp Button
Fixed position, bottom-right corner, always visible on all pages/scroll positions.

- Green circle button with WhatsApp icon (SVG)
- Hover tooltip: *"Ada pertanyaan? Chat kami!"*
- Subtle pulse animation to draw attention
- Links to `https://wa.me/6261XXXXXXX?text=Halo%2C%20saya%20ingin%20bertanya%20tentang%20produk%20INOVAR%20FLOOR` (mobile number TBD)
- On mobile: slightly larger tap target (56px)

---

### 15. Footer
Dark (`--dark`). Full-width.

**Top row:**
- Logo: `INOVAR FLOOR MEDAN` (Cormorant Garamond, white + green accent)
- Tagline: *"Distributor Resmi INOVAR FLOOR · Medan, Indonesia"*

**Bottom row:**
- Left: `© 2026 INOVAR FLOOR MEDAN. All rights reserved.`
- Right: Quick links — Produk · Keunggulan · Kalkulator · Kontak

---

## Assets Required (User to Provide)

| File | Description |
|---|---|
| `images/before.jpg` | Before photo for Before/After slider |
| `images/after.jpg` | After photo for Before/After slider |
| `images/gallery-1.jpg` → `gallery-9.jpg` | Instagram installation photos (9 total) |
| Mobile WhatsApp number | For WhatsApp links throughout |
| Real customer testimonials | To replace placeholder quotes |

---

## Technical Notes

- **Single file:** All HTML, CSS, JS in `index.html`. No build tools, no dependencies, no external JS libraries.
- **Fonts:** Google Fonts (Cormorant Garamond + Jost) — already loaded.
- **No jQuery, no Bootstrap, no AOS** — all animations in vanilla JS/CSS.
- **Images folder:** Create `images/` directory in project root for gallery, before/after photos.
- **WhatsApp links:** Use `https://wa.me/62XXXXXXXXXX` format (Indonesian number without leading 0).
- **Google Maps embed:** Standard `<iframe>` embed code from Google Maps — no API key required.
- **Brochure assets:** When user provides scanned brochure, image assets can be added to the quality section.
- **`.gitignore`:** Add `images/` placeholder note; add `.superpowers/` to gitignore.

---

## Responsive Breakpoints
| Breakpoint | Change |
|---|---|
| 1024px | Product grid 4→3 col; hero stack |
| 768px | Most grids go 2-col; nav collapses to hamburger |
| 480px | Product grid 2→1 col; single column everything |