# Palette Refresh + Why INOVAR Redesign Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Swap the whole-site colour palette to Aesop-inspired terracotta; rebuild Why INOVAR as a dark 3×3 feature grid moved above Products; trim Products to 4 cards with a "see more" CTA; replace the gallery static grid with a horizontal marquee.

**Architecture:** Single self-contained `index.html`. All changes are CSS/HTML/JS edits inside that one file. No build tools — open `index.html` in a browser to verify each task.

**Tech Stack:** HTML5, CSS3 (custom properties, grid, keyframes), Vanilla JS, Google Fonts (Gloock + Figtree)

**Spec:** `docs/superpowers/specs/2026-04-18-palette-why-section-redesign.md`

---

## File Map

| File | Action | What changes |
|---|---|---|
| `index.html` | Modify | `:root` tokens · Why INOVAR CSS+HTML · Products HTML+CSS · Gallery CSS+HTML+JS |

---

## Task 1: Palette Token Swap

**Files:** Modify `index.html` — `:root` block + all `var(--green*)` / `var(--gold*)` references

- [ ] **Step 1: Replace the `:root` block**

Find:
```css
:root {
  --dark:       #1c2b1e;
  --green:      #2d6a4f;
  --green-lt:   #3d8a65;
  --sand:       #f5f0e8;
  --warm-white: #faf8f4;
  --gold:       #b8955a;
  --gold-lt:    #d4aa70;
  --text:       #2c2c2c;
  --muted:      #524840;
  --stone:      #c8bfaf;
  --info-bar-h: 36px;
  --nav-h:      70px;
}
```

Replace with:
```css
:root {
  --dark:       #1c1714;
  --terra:      #8c5e4a;
  --terra-lt:   #b07a66;
  --sand:       #f2ede5;
  --warm-white: #faf7f2;
  --text:       #2c2420;
  --muted:      #7a6b63;
  --stone:      #c4b8af;
  --info-bar-h: 36px;
  --nav-h:      70px;
}
```

- [ ] **Step 2: Search-and-replace old token references (whole file, case-sensitive)**

Run each find-and-replace in order:
1. `var(--green-lt)` → `var(--terra-lt)`
2. `var(--green)` → `var(--terra)`
3. `var(--gold-lt)` → `var(--terra-lt)`
4. `var(--gold-light)` → `var(--terra-lt)`
5. `var(--gold)` → `var(--terra)`

- [ ] **Step 3: Verify no old tokens remain**

```bash
grep -n "var(--green\|var(--gold" index.html
```
Expected: no output (zero matches).

- [ ] **Step 4: Open `index.html` in browser and check**

- Nav WhatsApp button: warm terracotta, not green
- Info bar background: dark warm brown, no green tint
- Section eyebrows: rust/terracotta tone
- No green anywhere on the page

- [ ] **Step 5: Commit**

```bash
git add index.html
git commit -m "feat: swap site palette from green/gold to terracotta"
```

---

## Task 2: Add Reveal Stagger Delay Classes d6–d9

**Files:** Modify `index.html` — CSS `<style>` block

- [ ] **Step 1: Find `.reveal-d5` and append d6–d9 immediately after**

Find:
```css
.reveal-d5 { transition-delay: 0.5s; }
```

Replace with:
```css
.reveal-d5 { transition-delay: 0.5s; }
.reveal-d6 { transition-delay: 0.6s; }
.reveal-d7 { transition-delay: 0.7s; }
.reveal-d8 { transition-delay: 0.8s; }
.reveal-d9 { transition-delay: 0.9s; }
```

- [ ] **Step 2: Commit**

```bash
git add index.html
git commit -m "feat: add reveal stagger delay classes d6-d9"
```

---

## Task 3: Why INOVAR — CSS Replacement

**Files:** Modify `index.html` — delete old `.why-*` CSS, insert new rules

- [ ] **Step 1: Delete old Why INOVAR CSS rules**

Find and delete each of these rule blocks from `<style>`:
```
.why-section { ... }
.why-inner { ... }
.why-body { ... }
.why-features { ... }
.why-feat-card { ... }
.why-feat-card:hover { ... }
.why-feat-icon { ... }
.why-feat-title { ... }
.why-feat-desc { ... }
```

Also delete from inside `@media (max-width: 1024px)`:
```css
.why-inner { grid-template-columns: 1fr; gap: 3rem; }
```

And from inside `@media (max-width: 768px)`:
```css
.why-features { grid-template-columns: 1fr; }
```

- [ ] **Step 2: Insert new Why INOVAR CSS in place of deleted rules**

```css
/* ── WHY INOVAR ── */
.why-section {
  background: var(--dark);
  padding: 6rem 8%;
}
.why-inner {
  max-width: 1200px;
  margin: 0 auto;
}
.why-header {
  text-align: center;
  margin-bottom: 4rem;
}
.why-eyebrow {
  color: var(--terra-lt);
}
.why-title {
  color: var(--warm-white);
  margin-bottom: 0;
}
.why-rule {
  width: 40px;
  height: 2px;
  background: var(--terra);
  margin: 1.2rem auto;
}
.why-intro {
  font-size: 1rem;
  line-height: 1.75;
  color: var(--stone);
  max-width: 560px;
  margin: 0 auto;
  font-weight: 300;
}
.why-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 1.5rem;
  margin-bottom: 4rem;
}
.why-card {
  background: rgba(255, 255, 255, 0.04);
  border: 1px solid rgba(176, 122, 102, 0.15);
  border-top: 3px solid var(--terra);
  border-radius: 4px;
  padding: 1.8rem;
  transition: transform 0.3s ease, border-color 0.3s ease;
}
.why-card:hover {
  transform: translateY(-5px);
  border-color: rgba(176, 122, 102, 0.5);
  border-top-color: var(--terra);
}
.why-card-icon {
  color: var(--terra-lt);
  margin-bottom: 1rem;
  transition: transform 0.3s ease;
}
.why-card:hover .why-card-icon {
  transform: scale(1.08);
}
.why-card-name {
  font-family: 'Gloock', serif;
  font-size: 1.1rem;
  color: var(--warm-white);
  margin-bottom: 0.4rem;
}
.why-card-desc {
  font-size: 0.88rem;
  color: var(--stone);
  line-height: 1.75;
  font-weight: 300;
}
.why-cta {
  text-align: center;
}
.why-cta-text {
  color: var(--stone);
  font-size: 1rem;
  margin-bottom: 1.2rem;
  font-weight: 300;
}
```

- [ ] **Step 3: Add responsive overrides**

Inside `@media (max-width: 1024px)` block, add:
```css
.why-grid { grid-template-columns: repeat(2, 1fr); }
```

Inside `@media (max-width: 768px)` block, add:
```css
.why-grid { grid-template-columns: 1fr; }
.why-section { padding: 4rem 5%; }
```

- [ ] **Step 4: Commit**

```bash
git add index.html
git commit -m "feat: add Why INOVAR redesign CSS (dark section, 3x3 grid)"
```

---

## Task 4: Why INOVAR — HTML Rebuild + Section Move

**Files:** Modify `index.html` — delete old section HTML, insert rebuilt section before `<!-- PRODUCTS -->`

- [ ] **Step 1: Delete old Why INOVAR HTML block**

Find and delete everything from `<!-- WHY INOVAR -->` through the closing `</section>` tag of that section. The block begins with:
```html
  <!-- WHY INOVAR -->
  <section class="why-section" id="keunggulan">
```
Stop deleting at (and do NOT delete) `<!-- BEFORE/AFTER -->`.

- [ ] **Step 2: Insert new Why INOVAR HTML immediately before `<!-- PRODUCTS -->`**

```html
  <!-- WHY INOVAR -->
  <section class="why-section" id="keunggulan">
    <div class="why-inner">

      <div class="why-header reveal">
        <span class="section-eyebrow why-eyebrow">Teknologi Unggulan</span>
        <h2 class="section-title why-title">Dibangun untuk Iklim Tropis</h2>
        <div class="why-rule"></div>
        <p class="why-intro">CoreGuard Hardwood HDF — material inti eksklusif INOVAR yang menjadi fondasi dari setiap teknologi perlindungan di bawah ini.</p>
      </div>

      <div class="why-grid">

        <div class="why-card reveal reveal-d1">
          <div class="why-card-icon"><svg width="36" height="36" viewBox="0 0 36 36" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"><path d="M18 5c0 0-10 12-10 18a10 10 0 0020 0C28 17 18 5 18 5z"/><path d="M13 25a6 6 0 008 2" stroke-width="1.2" opacity="0.7"/></svg></div>
          <div class="why-card-name">AquaBloc</div>
          <div class="why-card-desc">CoreGuard Hardwood HDF menjadikan INOVAR lantai laminate paling tahan air di dunia. Sistem Interlocking Extra-Presisi mencegah rembesan air masuk melalui sambungan papan.</div>
        </div>

        <div class="why-card reveal reveal-d2">
          <div class="why-card-icon"><svg width="36" height="36" viewBox="0 0 36 36" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"><path d="M18 4L30 9v11c0 7-12 12-12 12S6 27 6 20V9z"/><line x1="13" y1="14" x2="23" y2="24"/><line x1="23" y1="14" x2="13" y2="24"/></svg></div>
          <div class="why-card-name">Termite Bloc</div>
          <div class="why-card-desc">Material CoreGuard tropical hardwood menjadikan INOVAR lantai laminate paling tahan rayap di pasaran — perlindungan sejati untuk iklim Indonesia yang lembab.</div>
        </div>

        <div class="why-card reveal reveal-d3">
          <div class="why-card-icon"><svg width="36" height="36" viewBox="0 0 36 36" fill="none" stroke="currentColor" stroke-width="1.5"><circle cx="18" cy="18" r="13"/><circle cx="18" cy="18" r="8"/><circle cx="18" cy="18" r="3"/></svg></div>
          <div class="why-card-name">WaxGuard Plus</div>
          <div class="why-card-desc">Teknologi vacumat terkini melapisi sambungan interlocking dengan paraffin, meredam bunyi berderit akibat tekanan dan meningkatkan ketahanan air secara keseluruhan.</div>
        </div>

        <div class="why-card reveal reveal-d4">
          <div class="why-card-icon"><svg width="36" height="36" viewBox="0 0 36 36" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"><path d="M18 4L30 9v11c0 7-12 12-12 12S6 27 6 20V9z"/><path d="M18 13c0 0-4 5-4 8a4 4 0 008 0c0-3-4-8-4-8z"/></svg></div>
          <div class="why-card-name">Stain Resistant</div>
          <div class="why-card-desc">Permukaan dilapisi coating khusus yang menolak noda dari tumpahan minuman, minyak, dan kotoran sehari-hari — tetap bersih dengan mudah.</div>
        </div>

        <div class="why-card reveal reveal-d5">
          <div class="why-card-icon"><svg width="36" height="36" viewBox="0 0 36 36" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"><polygon points="18,4 31,13 26,29 10,29 5,13"/><line x1="5" y1="13" x2="31" y2="13"/><line x1="12" y1="4" x2="10" y2="29"/><line x1="24" y1="4" x2="26" y2="29"/></svg></div>
          <div class="why-card-name">Wear Resistant AC4</div>
          <div class="why-card-desc">Rating keausan AC4 memastikan lantai tahan terhadap lalu lintas tinggi — cocok untuk hunian aktif maupun area komersial.</div>
        </div>

        <div class="why-card reveal reveal-d6">
          <div class="why-card-icon"><svg width="36" height="36" viewBox="0 0 36 36" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round"><circle cx="18" cy="18" r="6"/><line x1="18" y1="3" x2="18" y2="8"/><line x1="18" y1="28" x2="18" y2="33"/><line x1="3" y1="18" x2="8" y2="18"/><line x1="28" y1="18" x2="33" y2="18"/><line x1="8.1" y1="8.1" x2="11.6" y2="11.6"/><line x1="24.4" y1="24.4" x2="27.9" y2="27.9"/><line x1="27.9" y1="8.1" x2="24.4" y2="11.6"/><line x1="11.6" y1="24.4" x2="8.1" y2="27.9"/></svg></div>
          <div class="why-card-name">UV Resistant</div>
          <div class="why-card-desc">Formulasi khusus melindungi warna dan tekstur lantai dari paparan sinar UV langsung — tidak pudar meski terkena cahaya matahari setiap hari.</div>
        </div>

        <div class="why-card reveal reveal-d7">
          <div class="why-card-icon"><svg width="36" height="36" viewBox="0 0 36 36" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round"><rect x="4" y="7" width="28" height="6" rx="1"/><rect x="4" y="15" width="28" height="6" rx="1"/><rect x="4" y="23" width="28" height="6" rx="1"/></svg></div>
          <div class="why-card-name">CoreGuard HDF</div>
          <div class="why-card-desc">Inti papan dari tropical hardwood HDF eksklusif yang lebih padat dan tahan lama dibanding HDF biasa — fondasi dari seluruh keunggulan INOVAR.</div>
        </div>

        <div class="why-card reveal reveal-d8">
          <div class="why-card-icon"><svg width="36" height="36" viewBox="0 0 36 36" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"><path d="M5 28l13-7 13 7"/><path d="M5 22l13-7 13 7"/><path d="M5 16l13-7 13 7"/><path d="M5 10l13-7 13 7" stroke-width="2.2"/></svg></div>
          <div class="why-card-name">Anti Abrasive Overlay</div>
          <div class="why-card-desc">Lapisan permukaan anti-abrasi yang melindungi lantai dari goresan furnitur, hak sepatu, dan penggunaan berat sehari-hari.</div>
        </div>

        <div class="why-card reveal reveal-d9">
          <div class="why-card-icon"><svg width="36" height="36" viewBox="0 0 36 36" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"><path d="M18 4L30 9v11c0 7-12 12-12 12S6 27 6 20V9z"/><circle cx="18" cy="18" r="3"/><line x1="18" y1="11" x2="18" y2="15"/><line x1="18" y1="21" x2="18" y2="25"/><line x1="11" y1="18" x2="15" y2="18"/><line x1="21" y1="18" x2="25" y2="18"/></svg></div>
          <div class="why-card-name">Nano Guard 7/24</div>
          <div class="why-card-desc">Teknologi nano aktif 24 jam yang menghambat pertumbuhan bakteri dan jamur — mencegah bau tidak sedap dan menjaga kebersihan lantai secara mikrobiologis.</div>
        </div>

      </div>

      <div class="why-cta reveal">
        <p class="why-cta-text">Ingin tahu produk mana yang paling cocok untuk ruangan Anda?</p>
        <a href="#kontak" class="btn-primary">Konsultasi Gratis &rarr;</a>
      </div>

    </div>
  </section>

```

- [ ] **Step 3: Verify page order and section appearance in browser**

Scroll from top and confirm order:
1. Hero → 2. Trust badges → 3. Stats → 4. **Why INOVAR (dark)** → 5. Products → 6. Before/After → ...

Check within Why INOVAR:
- Dark background, 9 cards in 3×3 grid
- Each card has terracotta top border
- SVG icons render in rust/terracotta colour
- Header text is visible on dark background
- Cards lift on hover

- [ ] **Step 4: Commit**

```bash
git add index.html
git commit -m "feat: rebuild Why INOVAR HTML, move above products"
```

---

## Task 5: Products — Trim to 4 Cards + Remove Unused CSS

**Files:** Modify `index.html` — delete 8 product card divs + their `.pt-*` CSS thumb classes

- [ ] **Step 1: Delete product cards 5–12**

Inside `<div class="product-grid">`, keep only the first 4 `.product-card` divs. The result should be exactly:

```html
    <div class="product-grid">

      <div class="product-card reveal">
        <div class="product-thumb pt-eskimo"><span class="product-thumb-label">Lihat Detail</span></div>
        <div class="product-name">Eskimo</div>
        <div class="product-tag">Premium Collection</div>
        <a href="https://wa.me/6261XXXXXXX?text=Halo%2C%20saya%20tertarik%20dengan%20produk%20Eskimo.%20Boleh%20minta%20penawaran%20harga%3F" class="btn-primary product-btn" target="_blank" rel="noopener">Minta Penawaran</a>
      </div>

      <div class="product-card reveal reveal-d1">
        <div class="product-thumb pt-balinese"><span class="product-thumb-label">Lihat Detail</span></div>
        <div class="product-name">Balinese Teak Rio</div>
        <div class="product-tag">Premium Collection</div>
        <a href="https://wa.me/6261XXXXXXX?text=Halo%2C%20saya%20tertarik%20dengan%20produk%20Balinese%20Teak%20Rio.%20Boleh%20minta%20penawaran%20harga%3F" class="btn-primary product-btn" target="_blank" rel="noopener">Minta Penawaran</a>
      </div>

      <div class="product-card reveal reveal-d2">
        <div class="product-thumb pt-yangon"><span class="product-thumb-label">Lihat Detail</span></div>
        <div class="product-name">Yangon Teak</div>
        <div class="product-tag">Premium Collection</div>
        <a href="https://wa.me/6261XXXXXXX?text=Halo%2C%20saya%20tertarik%20dengan%20produk%20Yangon%20Teak.%20Boleh%20minta%20penawaran%20harga%3F" class="btn-primary product-btn" target="_blank" rel="noopener">Minta Penawaran</a>
      </div>

      <div class="product-card reveal reveal-d3">
        <div class="product-thumb pt-vendura"><span class="product-thumb-label">Lihat Detail</span></div>
        <div class="product-name">Vendura</div>
        <div class="product-tag">Premium Collection</div>
        <a href="https://wa.me/6261XXXXXXX?text=Halo%2C%20saya%20tertarik%20dengan%20produk%20Vendura.%20Boleh%20minta%20penawaran%20harga%3F" class="btn-primary product-btn" target="_blank" rel="noopener">Minta Penawaran</a>
      </div>

    </div>
```

- [ ] **Step 2: Remove unused CSS thumb classes from `<style>`**

Search and delete each of these rule blocks:
- `.pt-amber { ... }`
- `.pt-sumatran { ... }`
- `.pt-safari { ... }`
- `.pt-qld { ... }`
- `.pt-dinelli { ... }`
- `.pt-montreux { ... }`
- `.pt-american { ... }`
- `.pt-monument { ... }`

Keep: `.pt-eskimo`, `.pt-balinese`, `.pt-yangon`, `.pt-vendura`

- [ ] **Step 3: Verify in browser**

Products section shows exactly 4 cards. No broken layout or missing styles.

- [ ] **Step 4: Commit**

```bash
git add index.html
git commit -m "feat: trim products to 4 cards, remove unused CSS"
```

---

## Task 6: Products — "See More" CTA

**Files:** Modify `index.html` — add HTML after `.product-grid` + add CSS

- [ ] **Step 1: Add "see more" block after `.product-grid`**

Find the closing `</div>` of `.product-grid` (immediately after the Vendura card). Insert after it:

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

- [ ] **Step 2: Add CSS after `.product-grid` rules in `<style>`**

```css
.products-more {
  text-align: center;
  margin: 3.5rem auto 0;
  padding: 2.5rem;
  border: 1px solid rgba(196, 184, 175, 0.5);
  border-radius: 4px;
  max-width: 620px;
}
.products-more-text {
  font-size: 1rem;
  line-height: 1.85;
  color: var(--muted);
  margin-bottom: 1.8rem;
  font-style: italic;
}
```

- [ ] **Step 3: Verify in browser**

After the 4 product cards, a bordered box with italic text and a terracotta "Lihat Koleksi Lengkap →" button appears.

- [ ] **Step 4: Commit**

```bash
git add index.html
git commit -m "feat: add products see-more CTA block"
```

---

## Task 7: Gallery — Horizontal Marquee

**Files:** Modify `index.html` — replace gallery CSS, replace gallery HTML, update lightbox JS

- [ ] **Step 1: Delete old gallery CSS**

Find and delete the CSS rules for: `.gallery-grid`, `.gallery-item`, `.gallery-overlay` (and any hover variants or responsive overrides for these classes).

- [ ] **Step 2: Insert marquee CSS in their place**

```css
/* ── GALLERY MARQUEE ── */
.gallery-track-wrap {
  overflow: hidden;
  width: 100%;
  cursor: pointer;
  margin-top: 2rem;
}
.gallery-track {
  display: flex;
  gap: 1rem;
  width: max-content;
  animation: gallery-scroll 30s linear infinite;
}
.gallery-track:hover {
  animation-play-state: paused;
}
.gallery-slide {
  flex: 0 0 340px;
  height: 260px;
  border-radius: 4px;
  overflow: hidden;
}
.gallery-slide img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.5s ease;
}
.gallery-slide:hover img {
  transform: scale(1.05);
}
@keyframes gallery-scroll {
  0%   { transform: translateX(0); }
  100% { transform: translateX(-50%); }
}
@media (max-width: 768px) {
  .gallery-slide { flex: 0 0 260px; height: 200px; }
  .gallery-track { animation-duration: 22s; }
}
```

- [ ] **Step 3: Replace gallery HTML**

Find `<div class="gallery-grid">` and everything inside it (all `.gallery-item` divs through the closing `</div>`). Replace the entire block with:

```html
    <div class="gallery-track-wrap">
      <div class="gallery-track">
        <div class="gallery-slide" onclick="openLightbox(0)"><img src="images/gallery-1.jpg" alt="Galeri 1" loading="lazy"></div>
        <div class="gallery-slide" onclick="openLightbox(1)"><img src="images/gallery-2.jpg" alt="Galeri 2" loading="lazy"></div>
        <div class="gallery-slide" onclick="openLightbox(2)"><img src="images/gallery-3.jpg" alt="Galeri 3" loading="lazy"></div>
        <div class="gallery-slide" onclick="openLightbox(3)"><img src="images/gallery-4.jpg" alt="Galeri 4" loading="lazy"></div>
        <div class="gallery-slide" onclick="openLightbox(4)"><img src="images/gallery-5.jpg" alt="Galeri 5" loading="lazy"></div>
        <div class="gallery-slide" onclick="openLightbox(5)"><img src="images/gallery-6.jpg" alt="Galeri 6" loading="lazy"></div>
        <div class="gallery-slide" onclick="openLightbox(6)"><img src="images/gallery-7.jpg" alt="Galeri 7" loading="lazy"></div>
        <div class="gallery-slide" onclick="openLightbox(7)"><img src="images/gallery-8.jpg" alt="Galeri 8" loading="lazy"></div>
        <div class="gallery-slide" onclick="openLightbox(8)"><img src="images/gallery-9.jpg" alt="Galeri 9" loading="lazy"></div>
        <div class="gallery-slide" onclick="openLightbox(0)"><img src="images/gallery-1.jpg" alt="Galeri 1" loading="lazy"></div>
        <div class="gallery-slide" onclick="openLightbox(1)"><img src="images/gallery-2.jpg" alt="Galeri 2" loading="lazy"></div>
        <div class="gallery-slide" onclick="openLightbox(2)"><img src="images/gallery-3.jpg" alt="Galeri 3" loading="lazy"></div>
        <div class="gallery-slide" onclick="openLightbox(3)"><img src="images/gallery-4.jpg" alt="Galeri 4" loading="lazy"></div>
        <div class="gallery-slide" onclick="openLightbox(4)"><img src="images/gallery-5.jpg" alt="Galeri 5" loading="lazy"></div>
        <div class="gallery-slide" onclick="openLightbox(5)"><img src="images/gallery-6.jpg" alt="Galeri 6" loading="lazy"></div>
        <div class="gallery-slide" onclick="openLightbox(6)"><img src="images/gallery-7.jpg" alt="Galeri 7" loading="lazy"></div>
        <div class="gallery-slide" onclick="openLightbox(7)"><img src="images/gallery-8.jpg" alt="Galeri 8" loading="lazy"></div>
        <div class="gallery-slide" onclick="openLightbox(8)"><img src="images/gallery-9.jpg" alt="Galeri 9" loading="lazy"></div>
      </div>
    </div>
```

- [ ] **Step 4: Update lightbox JS**

Find in `<script>`:
```js
var lbImages = Array.from(document.querySelectorAll('.gallery-item img'));
```

Replace with:
```js
var lbImages = Array.from(document.querySelectorAll('.gallery-slide img')).slice(0, 9);
```

- [ ] **Step 5: Verify in browser**

- Images scroll continuously left, pausing on hover
- Clicking any image opens lightbox
- Lightbox prev/next cycles through 9 unique images only (no duplicates)

- [ ] **Step 6: Commit**

```bash
git add index.html
git commit -m "feat: replace gallery grid with horizontal marquee"
```
