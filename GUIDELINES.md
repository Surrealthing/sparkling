# Sparkling Mindz — Design & Code Guidelines

Single-file static HTML/CSS/JS. No build tools, no frameworks. All pages follow this spec exactly.

---

## Fonts

```html
<link href="https://fonts.googleapis.com/css2?family=Bricolage+Grotesque:opsz,wght@12..96,300;12..96,400;12..96,500;12..96,600;12..96,700;12..96,800&family=Inter:wght@400;500;600;700;800&family=Lato:wght@400;700&display=swap" rel="stylesheet">
```

| Role | Font | Notes |
|------|------|-------|
| Headings h1/h2/h3 | Bricolage Grotesque | letter-spacing: -0.5px |
| Body / UI | Inter | Default body font |
| Badge / award labels | Lato | Used only in floating badge widgets |

---

## Design Tokens (CSS custom properties)

```css
:root {
  --blue:   #00aeef;
  --pink:   #ff2d78;
  --purple: #9b3dff;
  --amber:  #f5a623;
  --green:  #a5d91a;
  --teal:   #00c9b1;
  --dark:   #1a1a1a;
  --char:   #2c2c2c;
  --d60:    #444444;  /* dark at 60% prominence */
  --d40:    #888888;  /* dark at 40% prominence */
}
```

---

## Layout

- **Content width**: 1200px, centered
- **Section padding pattern**: `padding: 96px max(24px, calc((100% - 1200px) / 2))`
- **Body**: `min-width: 1200px` (no mobile breakpoints — desktop only)
- **Body top padding**: `padding-top: 68px` (accounts for fixed nav height)

---

## Typography Scale

```css
h1 { font-size: clamp(2.4rem, 4.5vw, 3.8rem); font-weight: 800; }
h2 { font-size: 40px; font-weight: 700; line-height: 44px; }
.eyebrow { font-family: Inter; font-size: 14px; font-weight: 600; letter-spacing: 1.38px; text-transform: uppercase; color: var(--d60); }
```

---

## Buttons

All buttons: `border-radius: 100px`, `font-size: 16px`, `font-weight: 600`, `padding: 16px 40px`

| Class | Background | Hover |
|-------|-----------|-------|
| `.btn-blue` | `var(--blue)` | `#0090ca` |
| `.btn-pink` | `var(--pink)` | no change (opacity:1) |
| `.btn-purple` | `var(--purple)` | no change |
| `.btn-teal` | `var(--teal)` | no change |
| `.btn-outline` | transparent + border | slight bg tint |
| `.btn-sm` | — | `padding: 10px 20px; font-size: 14px` |

**Rule**: On hover, never `filter:brightness()` on colored buttons — it dims the text. Use explicit color or `opacity:1` (no-op).

---

## Text Links

```css
.text-link {
  display: inline-flex; align-items: center; gap: 6px;
  font-family: Inter; font-weight: 500; font-size: 16px;
  color: var(--d60); letter-spacing: .2px; transition: color .15s;
}
.text-link:hover { color: var(--blue); }
.link-arrow { display: inline-flex; align-items: center; transition: transform .2s ease; }
.text-link:hover .link-arrow { transform: translateX(4px); }
```

Arrow SVG (reuse this exact markup):
```html
<span class="link-arrow">
  <svg xmlns="http://www.w3.org/2000/svg" width="18" height="12" viewBox="0 0 18 12" fill="none">
    <path d="M0.75 5.75671H15.75" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"/>
    <path d="M12.3125 0.75L17.0938 5.75672L12.3125 10.7634" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"/>
  </svg>
</span>
```

For smaller contexts (e.g. blog cards at 13px), use `.blog-read` which mirrors `.text-link` at 13px:
```css
.blog-read { /* same as .text-link but font-size: 13px */ }
```

---

## Section Backgrounds (gradient pattern)

Each section uses a soft tinted gradient rising from bottom to white:

| Section | Gradient |
|---------|----------|
| About / Discovery | `linear-gradient(to top, #f4eaff 0%, #fff 95%)` — purple tint |
| Steps / Blog | `linear-gradient(to top, #f7ffe2 0%, #fff 80%)` — green tint |
| Spaces / School / Testimonials | `linear-gradient(to top, #e3fffb 0%, #fff 80%)` — teal tint |
| Preschool | `linear-gradient(to top, #ffe8f0 0%, #fff 80%)` — pink tint |
| Instagram | `linear-gradient(to top, #fff3df 0%, #fff 80%)` — amber tint |
| CTA Banner | `linear-gradient(to top, #bfeeff 0%, #fff 80%)` — blue tint |

---

## Section Header Pattern (centered)

```html
<div class="section-header" style="text-align:center; margin-bottom:56px">
  <p class="eyebrow">Label</p>
  <h2>Title with <em style="font-style:normal; color:var(--ACCENT)">accent word</em></h2>
</div>
```

Each section has its own accent colour matching its gradient tint (purple → purple, teal → teal, pink → pink, etc.).

---

## Two-Column Section Layout

Used in: Preschool, School, Discovery, About

```css
.section-inner {
  display: grid;
  grid-template-columns: [left-width]px 1fr;
  gap: [gap]px;
  align-items: center; /* or start for timeline */
}
```

| Section | Left col | Gap |
|---------|----------|-----|
| Preschool | 503px | 80px |
| School | 512px | 80px |
| Discovery | 497px | 165px |
| About | 1fr 1fr | 80px |

---

## Floating Badges / Award Widgets

Small floating cards anchored absolutely to photo columns:

```css
.badge-widget {
  position: absolute;
  background: #fff;
  border: 1px solid #ebebeb;
  border-radius: 8px;
  box-shadow: 0 8px 24px rgba(0,0,0,.07);
  display: flex; align-items: center; gap: 11px;
  padding: 0 18px; height: 65px;
}
.badge-icon {
  border-radius: 9px; width: 36px; height: 36px;
  display: flex; align-items: center; justify-content: center;
}
.badge-label { font-family: Lato; font-weight: 700; font-size: 15px; color: #1d1d1d; }
```

---

## Tags / Pills

```css
.tag { font-family: Inter; font-size: 12px; font-weight: 500; border-radius: 100px; padding: 5px 12px; }
.tag-purple { background: rgba(155,61,255,.1); color: var(--purple); }
.tag-teal   { background: rgba(0,201,177,.1);  color: var(--teal); }
.tag-pink   { background: rgba(255,45,120,.1); color: var(--pink); }
```

**Blog category tag** (light blue):
```css
.blog-cat { background: rgba(0,174,239,.12); color: var(--blue); font-weight: 500; border-radius: 100px; padding: 3px 10px; font-size: 11px; }
```

---

## Cards

### Blog Card
```css
.blog-card { background: #fff; border-radius: 16px; overflow: hidden; }
.blog-card:hover { box-shadow: 0 8px 32px rgba(0,0,0,.08); transform: translateY(-4px); }
.blog-thumb { height: 160px; position: relative; overflow: hidden; }
/* thumb uses a bt-grad div (gradient overlay) + img absolutely positioned */
.blog-body { padding: 20px; }
.blog-title { font-family: Bricolage Grotesque; font-weight: 700; font-size: 15px; line-height: 1.4; }
.blog-excerpt { font-size: 13px; line-height: 1.55; color: #424242; }
```

### White Info Card (timeline / value)
```css
.s-card { background: #fff; border-radius: 16px; box-shadow: 0 8px 24px rgba(0,0,0,.07); padding: 24px 28px; }
```

---

## Timeline (School section)

- Vertical dashed line connecting icon dots: `border-left: 2px dashed rgba(0,0,0,.18)`
- Dots are 64×64 Figma asset images (colored circle SVGs)
- Line position is computed by JS at `DOMContentLoaded` and `resize` by measuring `.s-dot` bounding rects
- Line runs from center of first dot to center of last dot

```javascript
(function(){
  function positionTimelineLine(){
    var dots = document.querySelectorAll('.s-dot');
    var line = document.querySelector('.s-timeline-line');
    if(!dots.length || !line) return;
    var tlRect = line.parentElement.getBoundingClientRect();
    var firstRect = dots[0].getBoundingClientRect();
    var lastRect = dots[dots.length - 1].getBoundingClientRect();
    line.style.top = (firstRect.top - tlRect.top + firstRect.height / 2) + 'px';
    line.style.bottom = (tlRect.bottom - lastRect.bottom + lastRect.height / 2) + 'px';
  }
  document.addEventListener('DOMContentLoaded', positionTimelineLine);
  window.addEventListener('resize', positionTimelineLine);
})();
```

---

## Navigation

- Fixed, transparent by default; on scroll adds `scrolled` class via JS
- Scrolled state: `background: rgba(255,255,255,0.92)`, `backdrop-filter: blur(8px)`, subtle border
- Full logo panel collapses on scroll; compact logo + brand name slides in
- Dropdown menus on hover (CSS only, `display:none` → `display:block`)

---

## Footer

- Background: `#1a1a1a` (near-black)
- Content padding: same `max(24px, calc((100% - 1200px) / 2))` pattern
- Social icon buttons: 36×36, `background:#2c2c2c`, `border-radius:8px`
- Contact icons: 32×32, `background:#2c2c2c`, `border-radius:8px`
- Body text: `#888` | Section titles: `#fff` | Hover links: `#ccc`
- Decorative sparkles: `opacity:.4`

---

## Sparkle Decorations

Absolute-positioned decorative sparkle images appear in most sections. They are always:
- `pointer-events: none`
- Sized 25–86px
- Source: Figma asset URLs

---

## Asset URLs

All images come from Figma MCP: `https://www.figma.com/api/mcp/asset/{uuid}`

**Note**: These URLs expire after ~7 days. When re-exporting, fetch fresh URLs from Figma node using `get_design_context` or `get_screenshot` with `forceCode:true`.

---

## Figma File Reference

- **File key**: `qgvl6AY5eALD1aR5BS92gd`
- **Homepage frame**: `Desktop - 10` (node-id `478-…`)
- **Body width for Figma capture parity**: 1440px frame → 1200px content area

---

## Common Patterns Checklist (for new pages)

- [ ] Include all 3 Google Fonts
- [ ] Copy `:root` token block exactly
- [ ] `body { padding-top: 68px }` for fixed nav
- [ ] `html { min-width: 1200px }`
- [ ] Copy nav HTML + scroll JS from index.html
- [ ] Use section padding formula for every section
- [ ] Match section gradient to accent colour
- [ ] `.eyebrow` above every `h2` in section headers
- [ ] Use `.text-link` + arrow SVG for all "view more" CTAs
- [ ] Blog category tags use light blue pill (`.blog-cat`)
- [ ] No `filter:brightness()` on hover states for colored buttons
- [ ] Copy footer HTML + sparkle decorations from index.html

---

## Mobile Responsive Rules (added after preschool pass)

### Breakpoints
- **Tablet**: `@media (max-width: 1024px)` — 2-col layouts collapse to `1fr 1fr` or adjusted grids
- **Mobile**: `@media (max-width: 768px)` — single column, carousels, pill/sparkle repositioning
- On mobile, `body { min-width: 1200px }` is lifted via a parent override allowing fluid width

### Horizontal Card Carousels (Spaces, Instagram, Blog)
Uniform 70/30 formula — first card shows full, next 30% peeks:
```css
.grid {
  display:flex; overflow-x:auto;
  justify-content:flex-start;                 /* MUST override desktop justify-content:center */
  scroll-snap-type:x mandatory;
  scroll-padding-left:20px;                   /* makes snap respect the 20px gutter */
  padding-left:20px!important; padding-right:20px;
  gap:14px;                                   /* insta uses 12px */
  scrollbar-width:none;
}
.grid::-webkit-scrollbar{display:none}
.card {
  flex:0 0 calc(70vw - 34px);                 /* 20px + card + 14px gap + 30vw peek = 100vw */
  width:calc(70vw - 34px);
  scroll-snap-align:start; flex-shrink:0;
}
```
**Gotchas we hit and fixed:**
- Desktop `justify-content:center` must be explicitly reset to `flex-start` on mobile, otherwise overflow centers and cuts off card 1.
- `scroll-snap-align:start` without `scroll-padding-left` snaps cards flush to container edge and eats the 20px gutter. Always set `scroll-padding-left:20px` on the scroll container.
- Use `padding-left:20px!important` because sections often carry their own padding via the `max(24px, calc(...))` formula; for mobile carousels, zero the section padding and put it back on the grid.

### Preschool Orbit (Rings + Photo) Mobile Pattern
The Figma layout is a 521×452 container with absolutely positioned rings, photo, pills, and sparkles. On mobile, keep the Figma layout intact and scale the whole thing with CSS `zoom`:
```css
.preschool-right{
  width:521px; height:452px; margin:0 auto; overflow:visible;
  zoom:0.68;                                  /* scales size AND layout box */
}
.orbit-img  { left:calc(50% - 226px); top:0;   width:452px; height:452px }   /* rings SVG */
.orbit-photo{ left:calc(50% - 132px); top:94px;width:264px; height:264px }   /* concentric photo */
```
- `zoom` is preferred over `transform:scale()` because it shrinks the box dimensions (page flows correctly). Supported in all modern browsers incl. Firefox 126+.
- Center both the 452 SVG and the 264 photo via `calc(50% - halfwidth)` to keep all three circles (two outlines + filled photo) concentric on the container's horizontal center.
- For vertical concentricity: ring center Y = `top + 226`, photo center Y = `top + 132`. Setting ring `top:0` and photo `top:94` puts both centers at Y=226 → concentric.
- Pills and sparkles stay at their Figma absolute positions; they scale along via `zoom`.

### Sparkle Positioning on Mobile
On mobile, desktop sparkles are typically too large and positioned using desktop-relative coords that overflow the viewport. Rules:
- **Shrink** to ~20–32px (from 49–81px desktop).
- **Reposition** with viewport-relative units (`right:20px`, `left:8px`) or `calc(50% - …)` to hug the nearest image edge instead of floating far from it.
- **Never `display:none`** sparkles on mobile — the brand relies on them. Shrink and nudge instead.

---

## Asset Strategy

### Local assets (MANDATORY)
All images must be served from the repo. Figma MCP CDN URLs (`https://www.figma.com/api/mcp/asset/{uuid}`) **expire in ~7 days**. Pipeline:
1. Grep `index.html` for any `figma.com/api/mcp/asset/` references.
2. `curl` each UUID into `assets/images/figma/{uuid}.<ext>`.
3. Detect the real extension via `file --mime-type` (many Figma assets are SVG served without a `.svg` extension — always check the first bytes for `<svg`).
4. Rewrite the `src=` in HTML to `assets/images/figma/<uuid>.<ext>`.

### Asset folder layout
```
assets/
  icons/               # stable icons that won't change (social, generic)
  images/
    figma/             # raw Figma exports keyed by UUID (no human naming needed)
    preschool/         # hand-named section assets (rings, sparkles, icons)
    values/            # value-card icons (joyful-learning.svg, etc.)
```

### Filename tip
When the user drops an asset via `/Users/.../Desktop/Name.svg`, watch for **non-breaking space** (`c2 a0`) in the filename (shows up in hex as `Name\xc2\xa0.svg`). Use a glob (`Name*.svg`) to cp — quoted filenames with regular spaces will fail.

---

## Micro-animation System

Two layers added globally via the last `<style>` block + last `<script>` block:

### 1. Scroll-reveal (scale + fade + lift)
```css
@media (prefers-reduced-motion: no-preference){
  .reveal{opacity:0; transform:scale(.86) translateY(16px);
          transition:opacity .8s ease-out, transform .8s cubic-bezier(.22,.75,.2,1)}
  .reveal.in-view{opacity:1; transform:none}
}
```
JS auto-tags a curated list of selectors (hero imgs, cards, preschool photo, testimonials, events, steps, d-stats, etc.) with `.reveal` + a staggered `transition-delay` of `(i%6)*60ms`, then an `IntersectionObserver` (threshold 0.12) flips `.in-view` on entry.

### 2. Sparkle twinkle (continuous, staggered)
```css
@keyframes twinkle{0%,100%{opacity:.85;transform:scale(1) rotate(0)}
                   50%  {opacity:1;  transform:scale(1.18) rotate(6deg)}}
.hero-sparkle img, .about-sparkle img, .preschool-sp img,
.disc-sparkle img, .cta-sparkle img, .sp-deco img{
  animation: twinkle 3.2s ease-in-out infinite;
  transform-origin:center; will-change:transform,opacity;
}
/* stagger delays per-element so they don't pulse in unison */
```
Apply twinkle on the inner `<img>`, not the container — the container may carry parallax `transform`.

### 3. Parallax (subtle, scroll-driven)
Non-reveal elements get `data-parallax` set by JS and receive:
```css
[data-parallax]{transform:translate3d(0,var(--py,0),0); transition:transform .08s linear; will-change:transform}
```
JS loops through groups with speed values (15–45px range), computes `(elemCenter − viewportCenter)/vh` progress on scroll (rAF-throttled, passive listener), and writes `--py` per element. Targets: all sparkle containers, `.orbit-img`, `.cambridge-badge`, `.hero-award`. **Never parallax a `.reveal` element** — transforms will fight.

All motion respects `prefers-reduced-motion: reduce`.

---

## Working Method & Feedback Style (Ajith)

When building or extending pages for this project, match this collaboration rhythm:

### How feedback arrives
- **Screenshots with tiny directives** — "a bit up", "smaller, closer to images", "add left margin", "central align". Crops are narrow; the fix is almost always a single CSS property tweak, not a redesign. Resist the urge to refactor.
- **One thing at a time.** Ajith iterates: ship small, look, nudge again. Don't batch speculative fixes into one edit.
- **Pixel-level fidelity to Figma is the baseline.** If something looks off, check the Figma node first (`get_design_context` / `get_metadata`), don't guess.

### What to do
- Make the smallest edit that resolves the observation. A padding change is not an excuse to restructure a section.
- When matching Figma, **keep the Figma absolute positions intact** and scale on mobile with `zoom` — don't reinvent the layout per breakpoint.
- When the user says "centered", verify with math: for concentric circles, `top + radius == containerCenterY` for every layer.
- After edits that touch many files (asset downloads, URL rewrites), commit + push so the live Vercel URL reflects the change.

### What to avoid
- **No warm / golden tints.** Amber, copper, muted gold are out. When color is needed, lean on the cool brand tokens (`--blue`, `--purple`, `--teal`, `--pink`).
- **No pastel dilution.** Use the saturated brand colors at full strength; tint backgrounds are already soft (see gradient table).
- **No generic marketing copy.** Don't invent taglines or stats. Pull from the content doc, or leave copy unchanged.
- **No template layouts.** If a section doesn't exist in Figma, don't improvise one — ask.
- **No `display:none` as a mobile shortcut.** Shrink and reposition instead; the brand's charm is in the sparkles and decorations.
- **Don't narrate.** Keep responses short; state the fix, stop.

### Iteration contract
When Ajith sends a screenshot + one-line directive:
1. Identify the single property (or two) that moves the rendered state toward the directive.
2. Edit it.
3. One-sentence confirmation of what changed and where.
4. Wait for the next screenshot.

---

## Deployment

- **GitHub**: https://github.com/Surrealthing/sparkling (branch `main`)
- **Vercel**: project `sparkling` under `surrealthings-projects`. Deploy via `vercel --prod --yes`. New projects have **Deployment Protection** enabled by default — disable in Settings → Deployment Protection to make the URL public.
