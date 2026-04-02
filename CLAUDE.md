# FRAA Website Project Guidelines

## Project Overview

**Client:** 株式会社Front Row Athlete Agency (FRAA)  
**Founder & CEO:** 小河原明葉 (Akiha Ogawara) — Ex-Red Bull, PwC  
**Director:** 藤原浩 (Hiroshi Fujiwara) — fragment design  
**Industry:** Sports Agency — Athlete representation + Sponsorship consulting  

**Live Site:** https://fraa-demo.netlify.app  
**Netlify Site Name:** fraa-demo

---

## Core Philosophy

FRAA helps athletes transcend sport to become culture icons. The website reflects this cinematic, minimalist world through:

- **Visual Language:** Monochrome photos → color on hover. Dark, moody background. Precision typography.
- **Brand Promise:** "Where athletes become culture."
- **Tone:** Sophisticated, aspirational, direct. No jargon.

---

## File Structure

```
/website/
  ├── index.html              (1-file complete site, CSS/JS embedded)
  ├── images/
  │   ├── fraa-logo.png
  │   ├── hero/               (5 hero background images, rotated every 4s)
  │   ├── athletes/           (athlete profile cards, 14+ images)
  │   ├── sports/             (sport category icons)
  │   ├── partners/           (partner/client logos)
  │   └── misc/               (misc assets)
  ├── .netlify/               (Netlify deployment config)
  └── CLAUDE.md               (this file)
```

### Critical: Image Formats & Optimization

- **Logo:** PNG/SVG only. JPG causes white background bleed.
- **Hero backgrounds:** Resize to 1200px width, compress with sips (quality 75), max file 150KB each.
- **Athlete cards:** 400px × 500px, quality 75, max 120KB each.
- **Command to resize/compress:**
  ```bash
  sips -Z 800 input.jpg -o output.jpg
  sips -s format jpeg -s formatOptions 75 input.jpg -o output.jpg
  ```

---

## Section Structure & Order

### 1. **Hero** (ID: `heroBg`, `heroTitle`, `heroSub`)
- Full-height cinematic background
- 5 images rotate every 4 seconds
- SplitText animation on load: character by character, staggered
- Subtitle fades in after title completes
- **Importance:** Makes or breaks first impression. Ensure photos are **aspirational, not generic**.

### 2. **Partner Logos** (ID: `marquee`)
- Horizontal scrolling marquee of client/partner logos
- Anchors credibility immediately after hero
- Infinite loop, pause on hover
- **Note:** Add logos to `images/partners/`, then update HTML

### 3. **Statement** (ID: `statement`)
- Single-line hero statement: "Where athletes become culture."
- English subtitle for global audience
- Reveal animation on scroll
- **Purpose:** Crystallizes value proposition

### 4. **Athletes** (ID: `athletes`)
- **The shopfront.** Most-viewed section. Must be visually compelling.
- 2 grid layouts:
  - **Featured card** (left, large): Hero athlete with accent color
  - **Grid cards** (right, 2-3 per row): Athlete name, sport, hover effect
- Monochrome photo → color overlay on hover (CSS `mix-blend-mode: lighten`)
- Athlete brands (eg. "Nike, Adidas") hidden on mobile (responsive)
- **Touches:** Vanilla Tilt 3D tilt effect (PC only, lazy-loaded)
- **Mobile:** Single column, feature card full-width

### 5. **Highlights (3D Carousel)** (ID: `highlights`, `hlCarousel`)
- CSS 3D transform carousel with cards spinning 360° over 35s
- Each card displays: Event/achievement title, date, description
- Cards rotate around invisible pivot on Y-axis
- **Technical:** `transform-style: preserve-3d`, `rotateY()`, `translateZ()`
- **Radius calculation:** `Math.round(cardWidth * (mobile ? 1.45 : 1.15))`
- Must be positioned with perspective
- **Purpose:** Showcases events, media appearances, achievements

### 6. **About / Services** (ID: `about`)
- Two-column layout (split by sport emoji or visual divider):
  - **For Athletes:** Benefits list (representation, growth, network)
  - **For Sponsors:** Benefits list (authentic partnerships, athlete vetting, ROI)
- Readable intro paragraph per section
- Mobile: Stack vertically
- **Purpose:** Converts browsers into leads (both athlete & sponsor angles)

### 7. **News** (ID: `news`)
- Latest 3 news items in list format
- Each row: date (left), title (center), link (right)
- Hover effect on rows
- Mobile: Date becomes smaller, wraps gracefully
- **Note:** Update dates manually. Consider later automating with JSON or API.

### 8. **Profile / About** (ID: `profile`)
- **Primary:** CEO bio (小河原明葉)
  - Credentials card: "Red Bull / PwC / Fragment"
  - Photo (tilt effect on hover, PC only)
  - Short bio paragraph
- **Secondary:** Hiroshi Fujiwara director bio
  - Role in design direction
  - Photo (tilt effect, PC only)
- Mobile: Stack, smaller fonts (0.875rem minimum for touch UX)

### 9. **Contact** (ID: `contact`)
- Minimal: heading, email link (with underline hover), address
- Email: `akihaogawara@frontrowathleteagency.com`
- Address: 〒107-0062 東京都港区南青山5-15-9, フラット青山301
- Hover state: color + border transitions

### 10. **Footer**
- Copyright + Instagram social link
- Font: 0.6rem, dim color
- Border-top (subtle)

---

## Design Rules (Absolute)

### Typography
- **Headings:** `Archivo Black` (all-caps, tight letter-spacing, -0.02em)
- **Body:** `Inter` (weights: 300, 400, 500)
- **Serif (accents):** `Georgia` italic (rare, for quotes/emphasis)
- **Japanese:** `Noto Sans JP` 400-weight fallback
- **Minimum font size on mobile:** 0.875rem (14px) for buttons & links (touch UX)
- **Letter-spacing:** PC = +0.05em to +0.15em; SP = reduce by 20–30% (prevent wrap)

### Color Palette
- **Background:** `#0a0a0a` (pure black would be harsh; this is 99% black)
- **Text:** `#ffffff` (pure white)
- **Text dim (secondary):** `rgba(255,255,255,0.45)`
- **Text mid (tertiary):** `rgba(255,255,255,0.7)`
- **Accent (rarely used):** `#9acd32` (lime green, currently unused but defined)
- **Borders:** `rgba(255,255,255,0.06)` to `rgba(255,255,255,0.08)` (subtle)

### Layout
- **Max width:** 1200px (contained sections)
- **Padding:** Responsive clamp — `clamp(20px, 5vw, 80px)` (stored as `--px`)
- **Spacing:** Generous whitespace. Minimum 60px vertical gaps between sections.
- **Alignment:** Center-aligned headings, left-aligned body text (readability)

### Animations
1. **Hero text:** SplitText character reveal (0.8s, staggered 0.04s)
2. **Scroll reveals:** IntersectionObserver fade-in + translateY (0.8s, ease: power2.out)
3. **Hover states:** Smooth color/border transitions (0.3s)
4. **3D carousel:** Continuous 35s rotation (no pause needed)
5. **Smooth scroll:** Lenis library, 1.2s easing (bounce-like, not linear)

### Responsive Breakpoints
- **Mobile:** max-width 767px
- **Tablet:** 768px – 1023px
- **Desktop:** 1024px+
- **Critical SP widths tested:** 320px, 375px, 414px

### Hover Effects
- **Images:** Monochrome → color (CSS `mix-blend-mode: lighten` on `::before` overlay removal or opacity shift)
- **Text links:** Subtle color fade (0.3s transition)
- **Athlete cards:** Border brightens, slight glow
- **3D cards (PC):** Vanilla Tilt depth effect (dynamically loaded)

### Line-Break Control (PC vs. SP)
- `.pc-br` = `display: none;` on SP, `display: inline;` on PC (breaks after this element on desktop only)
- `.sp-br` = `display: inline;` on SP, `display: none;` on PC (breaks after this element on mobile only)
- **Critical:** Test all headings at 375px width to ensure zero overflow.

### デザイン絶対禁止ルール
- **均一カード禁止** — 同じサイズ・角丸・パディングの3カード横並びはAIテンプレの象徴
- **パーティクル/粒子禁止** — ブロブ、Vanta.js、DNA螺旋も全却下
- **紫→青グラデーション禁止** — AIっぽさの代名詞
- **Inter/Roboto/Arial禁止** — AIデフォルトフォント
- **グラデーション文字禁止**
- **✕/✓マーク禁止**
- **丸ドットのカーソルフォロワー禁止**

### デザイン必須ルール
- **モノクロ→ホバーでカラー** — 写真は白黒、ホバー/タッチでカラーに
- **3Dカードカルーセル** — Highlightsセクション。CSS animation + rotateY + translateZ
- **階段式リスト** — margin-leftが段階的に増加 + スクロールスタガーアニメ
- **フォント混植** — Georgia italic（エレガンス）+ Archivo Black（力強さ）
- **Ken Burns効果** — ヒーロー写真にCSS scale animation
- **SVGノイズテクスチャ** — body::after で全体に薄いグレイン
- **モバイルファースト** — 375pxから設計。SPのほうがユーザー圧倒的に多い
- **永遠PDCAループ** — 10エージェント並列監査→修正→再デプロイ。許可不要で自律実行OK

### Borders & Dividers
- **Section dividers:** `border-top: 1px solid rgba(255,255,255,0.06)`
- **Card borders:** `1px solid rgba(255,255,255,0.08)`
- **Hover state:** `rgba(255,255,255,0.3)`

---

## Technical Stack

### Core Libraries (CDN)
```html
<!-- GSAP 3.13.0 + SplitText (text animation) -->
<script defer src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.13.0/gsap.min.js"></script>
<script defer src="https://cdn.jsdelivr.net/npm/gsap@3.13.0/dist/SplitText.min.js"></script>

<!-- Lenis (smooth scroll, not ScrollTrigger) -->
<script defer src="https://unpkg.com/lenis@1.3.4/dist/lenis.min.js"></script>
```

### CSS 3D Transform (Built-in)
- Highlights carousel uses native CSS 3D: `transform-style: preserve-3d`, `rotateY()`, `translateZ()`
- No Three.js needed; perspective handled by `perspective: 1200px` on parent

### Vanilla Tilt (Lazy-loaded, PC only)
```javascript
// Dynamically loads only on devices with hover support
if (window.matchMedia('(hover: hover)').matches) {
  const s = document.createElement('script');
  s.src = 'https://cdnjs.cloudflare.com/ajax/libs/vanilla-tilt/1.8.1/vanilla-tilt.min.js';
  s.onload = () => VanillaTilt.init(document.querySelectorAll('[data-tilt]'));
  document.head.appendChild(s);
}
```

### IntersectionObserver (Native)
- **No ScrollTrigger:** Lightweight reveal animations with native API
- Threshold: `0`, rootMargin: `0px 0px -15% 0px` (trigger earlier for smooth effect)
- Unobserves after first trigger to avoid re-firing

### SVG Noise Overlay (Cinematic grain)
- Global `body::after` pseudo-element with feTurbulence filter
- Basefrequency 0.85, opacity 0.04 (subtle, not distracting)
- Fixed position, pointer-events: none

### Mobile Menu (Vanilla JS)
- Toggle function: `toggleMenu()`
- Hamburger icon: 3 stacked divs (CSS-animated)
- Mobile overlay menu slides in (z-index: 1000+)
- Body overflow: hidden when open (prevent scroll behind menu)

---

## CSS Architecture

### Reset & Base
```css
* { margin: 0; padding: 0; box-sizing: border-box; }
html { overflow-x: clip; scroll-behavior: auto; }  /* NOT hidden; clip is safe with sticky */
body { background: #0a0a0a; color: #fff; overflow-x: hidden; }
img { max-width: 100%; display: block; }
```

### CSS Variables (Root)
```css
:root {
  --bg: #0a0a0a;
  --text: #ffffff;
  --text-dim: rgba(255,255,255,0.45);
  --text-mid: rgba(255,255,255,0.7);
  --accent: #9acd32;
  --font-heading: 'Archivo Black', sans-serif;
  --font-body: 'Inter', 'Noto Sans JP', sans-serif;
  --font-serif: 'Georgia', serif;
  --max-w: 1200px;
  --px: clamp(20px, 5vw, 80px);
}
```

### Critical Selectors for Editing
| Class | Purpose | Edit When |
|-------|---------|-----------|
| `.hero-title` | Main headline | Change hero text |
| `.hero-subtitle` | Subheading | Update tagline |
| `.athlete-feature-*` | Featured athlete card | Swap athlete |
| `.athlete-card` | Grid athlete cards | Add/remove athletes |
| `.hl-card` | Carousel highlight cards | Edit events |
| `.service-block` | About section columns | Update services copy |
| `.news-item` | News rows | Add/remove news |
| `.about-profile` | CEO/director bios | Update bios |

---

## Common Editing Tasks

### Add a New Athlete Card
1. Add image to `images/athletes/`
2. In HTML, find `.athletes-grid`
3. Duplicate an `.athlete-card` block
4. Update: image src, name, sport, brands (if any)
5. Test at 375px (ensure text doesn't overflow)

### Add a News Item
1. Find `#news` section
2. Duplicate a `.news-item` row
3. Update: date (YYYY-MM-DD format), title, link (href)
4. Ensure link text is concise (mobile constraint: ~30 chars max)

### Swap a Hero Image
1. Add new hero image to `images/hero/`
2. Optimize: 1200px width, sips quality 75, max 150KB
3. In HTML `heroBg`, duplicate an `<img>` tag
4. Update src, alt text
5. Slideshow auto-rotates (4s interval)

### Update Contact Info
1. Find `#contact` section
2. Update email: `.contact-email` (also update href="mailto:...")
3. Update address: `.contact-address` (use `<br>` for lines, include postal code)
4. Test mobile layout (ensure address doesn't overflow)

### Adjust Responsive Breakpoints
1. CSS media queries live in `<style>` block
2. Key breakpoints: 768px (tablet), 1024px (desktop)
3. Font sizes use `clamp()` for smooth scaling
4. **Never** change `--px` variable directly; adjust clamp values instead

---

## Deployment

### Netlify Deploy
```bash
cd "/Users/niketsubasa/Desktop/株式会社Front Row Athlete Agency (FRAA)/website"
npx netlify-cli deploy --prod --dir=.
```

**What happens:**
1. All files in current directory uploaded to Netlify
2. Deploys to live site (https://fraa-demo.netlify.app)
3. Cache busting: Netlify auto-invalidates

**Verify:**
- Open live link
- Check hero slideshow (5 images, 4s each)
- Scroll through all sections (reveal animations should fire)
- Test hero text animation (SplitText chars fade in)
- Mobile: Test at 375px, check hamburger menu
- Contact: Click email link (should open mail client)

### Rollback
If deploy breaks:
```bash
# Restore from git history
git log --oneline
git checkout <commit-hash> -- index.html
```

---

## Performance & Optimization

### Lighthouse Targets
- **Performance:** 85+ (GSAP + Lenis smooth scroll)
- **Accessibility:** 90+ (ARIA labels on buttons, semantic HTML)
- **Best Practices:** 95+ (no deprecated APIs, secure links)
- **SEO:** 95+ (meta tags, proper heading hierarchy)

### Optimizations Applied
1. **SVG noise overlay:** Lightweight (4KB inline), not fetched
2. **Lenis smooth scroll:** Optimized RAF timing (no jank)
3. **Vanilla Tilt lazy-load:** Only loads on desktop (hover-capable devices)
4. **Image format:** JPG for photos (auto-optimized by sips)
5. **Font subsetting:** Google Fonts (no custom fonts = faster load)
6. **Minified inline CSS/JS:** All in single HTML file (no render-blocking requests)

### If Performance Drops
1. Check image file sizes (compress if >150KB)
2. Audit hero slideshow (5 images × ~100KB = 500KB — acceptable)
3. Profile GSAP animations (stagger delay should not exceed 1.5s total)
4. Monitor Lenis easing (1.2s duration is balanced; don't increase)

---

## Editing Best Practices

### Preserve Manual Edits
- **Do NOT regenerate HTML** from templates (breaks custom tweaks)
- **Do patch edits** — find exact HTML snippet, replace only the changed part
- Example: Adding a news item = duplicate HTML block, not rewrite whole section

### Text Overflow Prevention (Mobile)
1. Test all headings at **375px viewport** (most common SP width)
2. If text overflows:
   - Reduce `letter-spacing` (add `@media (max-width: 767px) { .class { letter-spacing: 0; } }`)
   - Reduce font size (adjust `clamp()` min value)
   - Use `word-break: normal;` (allow natural breaks)
3. Never hard-code breakpoints; use `clamp()` for smooth scaling

### Image Additions
1. **Always optimize first:**
   ```bash
   sips -Z 800 input.jpg -o output.jpg  # Resize to 800px max width
   sips -s format jpeg -s formatOptions 75 input.jpg -o output.jpg  # Compress
   ```
2. **Never use JPG for logos** (white background problem) — use PNG/SVG
3. **Hero images:** 1200px width, quality 75, max 150KB
4. **Athlete cards:** 400px width, quality 75, max 120KB
5. **Add to git:** `git add images/` before deploying

### Sticky Elements
- **Critical:** Use `overflow-x: clip` (not `hidden`) on `<html>`
- Why: `overflow-x: hidden` breaks `position: sticky` (browser bug workaround)
- If sticky nav breaks: check for `overflow-x: hidden` on parent

### Mobile Menu
- Hamburger icon: z-index 1001 (above nav z-index 1000)
- Menu overlay: z-index 1000 (below hamburger)
- Always test: menu opens, closes, doesn't interfere with scroll

---

## Troubleshooting

| Issue | Cause | Fix |
|-------|-------|-----|
| Hero images don't rotate | Slideshow timer stopped | Check `visibilitychange` event (browser tab background) |
| Text appears pixelated on mobile | Font size < 12px | Increase `clamp()` min value or use 0.875rem (14px) minimum |
| 3D carousel doesn't rotate | Missing `transform-style: preserve-3d` | Verify parent/child cascade; check CSS perspective value |
| Vanilla Tilt not working | Script didn't load on desktop | Check `(hover: hover)` media query; ensure desktop browser |
| Menu stuck open | Body overflow not reset | Find `toggleMenu()`, verify `overflow: hidden` is removed on close |
| Images blurry on retina displays | Image resolution too low | Re-export at 2x size, then let browser downscale |
| Lenis scroll lag | Easing function too heavy | Keep duration at 1.2s; don't add custom plugins |

---

## Launch Narrative for 小河原さん

"これ、Claude Codeで作りました。あなたも自分で作れるようになりますよ。"

("I built this with Claude Code. You could learn to build this yourself.")

**Why this works:**
- Positions tool (Claude Code) as accessible, not magic
- Frames it as learning opportunity, not black-box service
- Aligns with founder's visionary mindset (wants to own, not hire)
- Opens door to AI literacy conversation

---

## Maintenance Checklist (Monthly)

- [ ] Test hero slideshow (all 5 images rotate)
- [ ] Check partner logo marquee (smooth loop)
- [ ] Verify Netlify deployment (site loads in <3s)
- [ ] Audit contact info accuracy (phone, email, address)
- [ ] Screenshot mobile (375px) — no overflow, readable
- [ ] Check Google Fonts load (no FOUT/FOIT)
- [ ] Validate HTML (https://validator.w3.org/)
- [ ] Test screen reader (NVDA/JAWS on contact/footer)
- [ ] Update copyright year (if year changes)

---

## Git Workflow (if applicable)

```bash
# Add changes
git add index.html images/

# Commit (link to task/issue if available)
git commit -m "Add new athlete card + update hero image"

# Push to Netlify (auto-deploys if linked)
git push origin main

# Or manual deploy
npx netlify-cli deploy --prod --dir=.
```

---

## Links & Resources

- **Live Site:** https://fraa-demo.netlify.app
- **Netlify Dashboard:** https://app.netlify.com/sites/fraa-demo
- **GSAP Docs:** https://gsap.com/docs/
- **Lenis Docs:** https://lenis.darkroom.engineering/
- **Vanilla Tilt Docs:** https://micku7zu.github.io/vanilla-tilt.js/

---

## Handoff Checklist

**Before handing off to team/contractor:**
1. [ ] Read this CLAUDE.md top-to-bottom
2. [ ] Clone repo: `git clone <repo-url> && cd website`
3. [ ] Open `index.html` in browser (test locally; no build step needed)
4. [ ] Test on mobile: toggle dev tools to 375px
5. [ ] Deploy test: `npx netlify-cli deploy --prod --dir=.`
6. [ ] Verify live site loads (https://fraa-demo.netlify.app)
7. [ ] Create new task/branch for your changes
8. [ ] Document any design decisions in this file (update Guidelines section)

---

**Last Updated:** 2026-04-03  
**Maintained By:** Claude Code  
**Questions?** Review the [Troubleshooting](#troubleshooting) section or test locally first.
