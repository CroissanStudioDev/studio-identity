# Design System Inspired by Croissan Studio

> Category: Agency & Studio
> Caring AI studio. Cobalt-blue brand on near-white, with a black premium tier and graphite case-study surface. Russian-default typography on Right Grotesk + Golos Text. Pill-and-card vocabulary, polaroid photography, no emoji.

## 1. Visual Theme & Atmosphere

Croissan Studio's identity feels like a confident product team that happens to look you in the eye — Russian-default copy, real numbers, real client logos, and a single cobalt-blue (`#2727CA`) doing 90% of the brand work. The system places enormous faith in **typography over chrome**: the heaviest UI element is usually a pill, the deepest shadow appears only on a polaroid photo card. There are no gradients on hero surfaces, no glassmorphism on web, no decorative illustration outside the croissant mark itself.

The voice is "caring, smart, slightly bold" — and the visuals match. Slides and product pages alike commit hard to **brand primary as a full background**: an entire 1280×720 cover slide is `#2727CA`, white text, two buttons. The web equivalent is a near-white canvas with a single `bg-brand` CTA. White or black are admitted only when the use case earns it: white for content-heavy reading and the marketing site, black `#000` for premium covers and contrast moments, and **graphite `#252527`** as a fourth surface — exclusively for case-study slides where product screenshots need a softer-than-black backdrop.

The signature mark is a stylized croissant — three crescent strokes around an offset rotated ellipse, intentionally asymmetric. It exists in two modes: a **flat 2D SVG** (the working logo, used everywhere from navbar to slide chrome) and a **3D rendered version** (used as a mascot on deck covers and hero accents — never as a UI control). Wordmark lockups put the croissant inline at the right of the word "Studio."

A second sibling identity — **Croissan Community** — uses the same lockup system for non-commercial work (meetups, OSS, talks). The two never appear in one composition.

**Key Characteristics:**
- Cobalt-blue `#2727CA` as the only brand accent. White on brand, brand on white, white on black — the full surface vocabulary.
- A **fourth surface** for case studies: graphite `#252527`. Distinct from `#000`; softer for screenshots.
- Type scale runs on **two typefaces only**: Right Grotesk Bold for H1 (web) and Golos Text for everything else (web, slides, body, decks).
- Pill-and-card vocabulary. Five pill variants (`dark`, `light`, `outline`, `soft`, `deep`) and three card variants (default `ink`, `featured` white, `outline`) carry most data presentation.
- **Polaroid photo card** for team portraits — bg white, asymmetric padding (top 30, bottom 40, sides 20), `rounded-[1px]`, drop-shadow, rotated ±2–4°. Fully recognizable.
- **Slides Tag sticker** — `backdrop-blur-20` on `rgba(0,0,0,0.25)`, pill, white text-shadow. Floats over photos at small angles.
- Numbers are concrete and tabular: `15+`, `2–4 недели`, `300 000`. Never approximate ("много", "быстро") and never invented.
- Russian-default typography: em-dashes (`—`), Russian quotes («…»), non-breaking spaces before short prepositions.
- **No emoji as icons.** Lucide SVG only on web; flat exported SVG on slides.

## 2. Color Palette & Roles

### Primary
- **Cobalt** (`#2727CA`): The single brand color. CSS variable `--brand-primary`. Used for primary CTA backgrounds, accent text, deck/slide backgrounds (most slides), and the signature mark itself. The single highest-visibility color across the system.
- **Cobalt Hover** (`#2424B4`): A darker variant. CSS variable `--brand-primary-hover`. Used only as the hover/active state on primary CTAs.

### Secondary surfaces on cobalt
- **Cobalt Soft** (`#3D3DE0`): Used as the secondary pill background (`pill.soft`) when stacking many tags — services list, wardrobe options, etc.
- **Cobalt Deep** (`#1F1FA8`): Alternative secondary pill (`pill.deep`) when `cobalt-soft` would clash. Used sparingly.
- **Cobalt Lavender** (`#BCBCFF`): The text color used inside `number-box` chips on a brand-primary slide background — soft enough to read against the brand-blue gradient surface.

### Backgrounds & surfaces
- **Canvas** (`oklch(0.98 0.01 260)`, ≈ `#FAFAFB`): The default page background on the marketing site. Cooler than pure white, holds a hint of brand hue.
- **Paper** (`#FFFFFF`): True white. Used inside cards, white-mode slides, and `pill.light`.
- **Ink Black** (`#0E0E14` / `#000000`): The premium surface — deck covers, video title cards, high-contrast social. Two values used interchangeably; `#0E0E14` reads better on backlit displays, `#000` for print/PDF.
- **Graphite** (`#252527`): Exclusive surface for **case-study slides** in КП decks. Not a fallback for black — pick deliberately when a slide is product-screenshot-led.

### Neutrals & text
- **Brand Dark** (`#150E47`): The system's "near-black" for body text on the marketing site. Same hue family as the primary — that's what makes greys look coherent without going monochrome. CSS variable `--brand-dark`. Used as `text-primary` (100%), with opacity scale: `text-primary-90` (90%), `-80`, `-70`, `-60`, `-50` — anything below 60% is decorative-only (placeholders), not reading text.
- **Hairline** (`black at 5%`): The standard 1px border (`border-black/5`) on white cards. Subtle enough that the card still feels "open."
- **Paper Dim** (`white at 72%`): Secondary text on dark surfaces (slides, footers, case studies).
- **Paper Mute** (`white at 55%`): Tertiary text on dark — page numbers, captions, eyebrow labels.
- **Line** (`white at 18%`): The 1px divider on dark surfaces (between stage rows in a pricing breakdown, around outline cards).

### Semantic
- **Error Red** (`#E53935`): Form validation errors, destructive warnings. CSS variable `--color-error`.

### Chart palette (oklch, hue 260)
```
--chart-1: oklch(0.55 0.25 260);   /* primary — always the lead series */
--chart-2: oklch(0.65 0.20 200);   /* cyan */
--chart-3: oklch(0.60 0.25 320);   /* magenta */
--chart-4: oklch(0.70 0.20 150);   /* green */
--chart-5: oklch(0.65 0.25 30);    /* orange */
```

`chart-1` is **always** the primary series. Reordering breaks brand recognition.

### Gradients (used sparingly, slides only)
The only gradient that appears in the system is the **number-box surface** on cobalt slides:

```
linear-gradient(180deg, rgba(14,14,181,0) 0%, rgba(14,14,181,0.3) 100%)
on top of solid #2D2DFC
```

Never a hero gradient. Never a "trust" two-stop sweep. If you find yourself reaching for a gradient, the answer is "use a solid surface and let typography carry it."

## 3. Typography Rules

### Font Family
- **Right Grotesk** (display, H1 only on web): Local font file. CSS variable `--font-right-grotesk`. Used **only for the H1 of marketing pages** — bold, slightly cheeky, modern. Lowering it into H2/H3 makes the system noisy.
- **Golos Text** (body and slides): Google Fonts. CSS variable `--font-geist-sans`. Carries every line of body, every H2/H3 on web, and **every line on slides** (including H1 on slides — Right Grotesk is web-only).
- **Golos UI Bold** (slides H1): A weight of Golos used for slide titles at 90 px. On the web, this is `font-bold` Golos Text.
- **Geist Mono** (mono): Google Fonts via `next/font`. CSS variable `--font-geist-mono`. Code blocks, technical readouts.
- **Noto Sans** (server-side rendering): Bundled TTFs (Regular + Bold) for OG-image generation and PDF rendering where Google Fonts isn't reachable.

### Hierarchy (web)

| Role | Size | Weight | Line Height | Letter Spacing | Notes |
|------|------|--------|-------------|----------------|-------|
| H1 (page hero) | `text-5xl` (48 px) → `md:text-7xl` (72 px) | 700 | `leading-[1]` | `-tracking-[1.2px]` (-1.7%) | Exactly **one** per page. Right Grotesk only. |
| H2 (section) | `text-3xl` (30 px) → `md:text-5xl` (48 px) | 600 | `tracking-tight` | — | Golos Text. |
| H3 (sub-section) | `text-2xl` (24 px) → `md:text-3xl` (30 px) → `lg:text-4xl` (36 px) | 500 | `tracking-tight` | — | — |
| Lead paragraph | `text-lg` → `md:text-xl` (18→20 px) | 400 | `leading-[150%]` | — | `text-primary-60` |
| Body | base | 400 | default | — | `text-primary-60` |
| Small / caption | `text-sm` (14 px) | 400 | default | — | `text-primary-70` |
| Inline emphasis | inherit | 500 | default | — | `text-primary-90` |

### Hierarchy (decks / slides — fixed pixel)

| Role | Size | Weight | Line Height | Letter Spacing | Notes |
|------|------|--------|-------------|----------------|-------|
| H1 standard | 90 px | 700 (Bold) | 1.0 | −1.8 px (≈ −2%) | Cover, agenda, content slides. White on cobalt. |
| H1 case-study | 90 px | 500 (Medium) | 1.0 | −1.8 px | On graphite. Often **split-color**: white + `rgba(255,255,255,0.6)` for the accented word (client name, NDA, stack). |
| Lead / subtitle | 48 px | 400 | 1.2 | −0.96 px | white at 80% opacity. `max-width: 800 px`. |
| Caption / pre-strip | 32 px | 400 | 1.2 | −0.64 px | white at 80%. Above logo strips. |
| Card body (chip large) | 32 px | 600 | 1.2 | −0.96 px | `#BCBCFF` on brand. |
| Tag / sticker / metric chip | 18 px | 500 | 1.0 / 1.2 | −0.36 px | white. With `text-shadow: 0 0 8px rgba(0,0,0,0.2)` when over photos. |

### Hierarchy (HTML deck framework — viewport-relative)

The HTML deck template ([`../../templates/croissan-deck.html`](../../templates/croissan-deck.html)) uses a viewport-relative scale so a single deck reads at any projector resolution:

```
.h-hero { font-weight:700; font-size:6.4vw; line-height:1.02; letter-spacing:-.025em }
.h-xl   { font-weight:700; font-size:4.6vw; line-height:1.05; letter-spacing:-.022em }
.h-lg   { font-weight:700; font-size:3.2vw; line-height:1.10; letter-spacing:-.018em }
.h-md   { font-weight:700; font-size:2.2vw; line-height:1.15; letter-spacing:-.012em }
.h-sm   { font-weight:600; font-size:1.5vw; line-height:1.20; letter-spacing:-.005em }
.lead   { font-weight:500; font-size:max(17px,1.55vw); line-height:1.4 }
.body   { font-weight:400; font-size:max(15px,1.15vw); line-height:1.5 }
.meta   { font-weight:500; font-size:max(11px,.85vw); letter-spacing:.14em; text-transform:uppercase }
.num    { font-weight:800; font-variant-numeric:tabular-nums; letter-spacing:-.04em }
```

### Russian niceties (mandatory)

- **Em-dashes** (`—`), not hyphens, for parenthetical breaks.
- **Russian quotes** «…», not straight ones, in body copy.
- **Non-breaking spaces** (`&nbsp;`) before short prepositions and standalone short words: `с&nbsp;ИИ`, `за&nbsp;2-4&nbsp;недели`, `на&nbsp;рынке`.
- Number groupings: `110&nbsp;000 пользователей` (non-breaking space between digits and unit).

### Hierarchy rules

- Exactly **one `<h1>`** per page or per deck.
- No skip-levels: H1 → H2 → H3.
- Don't fake a heading with a styled `<p>`.
- On slides, **don't shrink the 90 px H1** to fit. Rewrite shorter, or break across two lines.

## 4. Component Stylings

### Buttons (web)

Built on shadcn `<Button>` with `cva`. Built-ins: `h-[44px]` minimum touch target, `cursor-pointer`, `focus-visible:ring-[3px]`, `transition-all`.

- **Primary CTA**: `bg-brand hover:bg-[var(--brand-primary-hover)] text-white` — the only place `--brand-primary` becomes a full surface.
- **Hero variant**: `rounded-[16px] px-8 py-7 text-[16px]` — taller, larger radius. Use for the hero CTA only.
- **Secondary outline**: `variant="outline"` with the same hero proportions.
- Standard radius: `rounded-[12px]`. Hero radius: `rounded-[16px]`.

### Pills / chips (slides, the signature device)

Five variants. Same shape (`rounded-[999px]`, `padding ≈ .85em 1.25em`, Golos Medium ≈ 1vw, `letter-spacing: -.005em`), differ only in fill:

| Variant | Surface | Text | When |
|---------|---------|------|------|
| `pill.dark`    | `#0E0E14` (ink) | white | Case headlines, accent tags |
| `pill.light`   | white | `#2727CA` | CTA chip, contact info |
| `pill.outline` | transparent + 45% white border | white | Meta info — "3 weeks", "Под ключ" |
| `pill.soft`    | `#3D3DE0` (cobalt-soft) | white | Service / tag clusters |
| `pill.deep`    | `#1F1FA8` (cobalt-deep) | white | Alternative when `soft` would clash |

If you want a sixth pill variant, **don't** — use one of the existing five with adjusted padding or weight instead.

### Cards (web)

```
Standard:  rounded-3xl border border-black/5 bg-white
Case card: same, with overflow-hidden, image gets m-2 mb-0 + rounded-2xl inset
Glass:     rounded-[20px] bg-background/80 backdrop-blur-md
Heavy glass (CTA): rounded-3xl bg-gradient-to-br from-white/10 to-white/5 shadow-sm backdrop-blur-[100px]
```

### Cards (slides)

Three variants on cobalt-blue slides. Same shape (`border-radius:18px`, `padding:2.6vh 1.6vw`, `display:flex; flex-direction:column; gap:1vh; height:100%`):

| Variant | Surface | Text | When |
|---------|---------|------|------|
| `card` (default) | `#0E0E14` | white | Standard mode card, stage card |
| `card.featured` | white | `#2727CA` | Recommended option, "starred" mode, featured tier |
| `card.outline` | transparent + 1px white-18% border | white | Minimum / alternative tier |

Inside each card:
- `.lbl` — `letter-spacing:.14em; text-transform:uppercase; color:paper-mute; ~12px` — tracked uppercase eyebrow.
- `.ttl` — Bold `~1.7vw`, `letter-spacing:-.012em` — the title.
- `.desc` — Regular `~1vw`, `color:paper-dim` — the body.
- `.price` — Bold `~2vw`, `tabular-nums`, `margin-top:auto; padding-top:1.4vh` — pinned to card bottom.

### Polaroid photo card

For team portraits in slide 2 ("Опытные основатели"). Highly recognizable.

```
bg: white
shadow: drop-shadow(0px 4px 10px rgba(0,0,0,0.25))
padding: pt-30 pb-40 px-20         ← asymmetric, polaroid-style
rounded-[1px]                       ← almost-rectangular
inner photo:
  rounded-[4px]
  inset shadow: inset 0px 2px 12px rgba(0,0,0,0.1)
rotation: ±2°…±4° (each polaroid different)
```

### Slides Tag (sticker over photos)

```
backdrop-blur-[20px]
bg: rgba(0,0,0,0.25)
rounded-[100px]
padding: px-24 py-12
text: Golos UI Medium 18px, white, line-height 1.2
text-shadow: 0 0 8px rgba(0,0,0,0.2)
rotation: ±1°…±7°
```

### Number-box / chip (cobalt slides only)

```
rounded-[32px]
padding: pt-32 pb-28 px-32          ← bottom slightly tighter
background: linear-gradient(180deg, rgba(14,14,181,0) 0%, rgba(14,14,181,0.3) 100%)
            on top of solid #2D2DFC
text: Golos Text SemiBold 32px, color #BCBCFF
height: 87px (fixed)
```

### Stage row (slide pricing breakdown)

```
display: grid; grid-template-columns: auto 1fr auto;
padding: 1.8vh 0;
border-top: 1px solid var(--line);     /* white at 18% */
last-of-type also gets border-bottom

.num-lbl  /* "Этап 01" — uppercase tracked, paper-mute */
.nm       /* SemiBold ~1.25vw — name */
.pr       /* Bold ~1.4vw, tabular-nums — price */
```

### Final price block

Used **once** per deck, on the totals slide:

```
font-weight: 800
font-size: 9.5–11vw          ← only place this size is allowed
font-variant-numeric: tabular-nums
letter-spacing: -.04em
align: right
```

### Demo grid (4-frame proof)

```
display: grid; grid-template-columns: repeat(4, 1fr); gap: 1vw;
each figure:
  .img — aspect-ratio:1/1; rounded-[14px]; overflow:hidden
  .cap — flex justify-between; ~12px
        .k (key, bold white) on left, metainfo (paper-dim) on right
```

### Floating black badge

The "В&nbsp;них мы особо хороши" sticker over a pill grid:

```
.badge-floating { position:relative }
.badge-floating .lab {
  position:absolute; top:-.85em; left:1.2vw;
  background:#0E0E14; color:white;
  font-size:~12px; padding:.5em .85em; border-radius:999px;
}
```

### Forms (web)

- Every input has a real `<label htmlFor>` matching its `id`. Placeholder-only labels are forbidden.
- Validate with **Zod**, wire with **react-hook-form**.
- Error messages are specific («Укажите телефон или Telegram»), not generic («Ошибка»).
- `role="alert"` on the element that displays the error.
- Inline error: `text-error text-sm` under the field.
- Global error: `bg-red-50 border-red-200 text-error rounded-xl p-4`.

### Icons

**Lucide only** (`lucide-react`), locked in `components.json`. Sizes: `size-4` (16 px) inline with text, `size-5` (20 px) in buttons, `size-6` (24 px) standalone. Decorative icons get `aria-hidden="true"`; icon-only buttons get `aria-label`. **Never emoji as icons.**

## 5. Layout Principles

### Web — section skeleton

Every page section follows one shape:

```html
<section className="py-16 md:py-32">
  <div className="mx-auto max-w-7xl px-6">
    <div className="mx-auto mb-6 max-w-2xl px-2 md:mb-24 md:text-center">
      <h2 className="font-semibold text-3xl tracking-tight md:text-5xl">…</h2>
    </div>
    {/* content */}
  </div>
</section>
```

| What | Mobile | Desktop |
|------|--------|---------|
| Vertical padding | `py-16` | `md:py-32` |
| Horizontal padding | `px-6` (`px-8` on hero) | — |
| Container | `max-w-7xl mx-auto` (1280 px) | — |
| Text column | `max-w-2xl` (sections) · `max-w-[680px]` (hero) | — |

### Web — hero

```html
<section className="flex min-h-screen flex-col justify-center py-16">
  <div className="mx-auto flex max-w-7xl flex-1 flex-col justify-center px-8 py-16 md:p-16">
    <div className="mx-auto max-w-[680px] space-y-8 md:text-center">
      {/* H1, lead, CTAs */}
    </div>
  </div>
</section>
```

`min-h-screen` — hero owns the first viewport. `space-y-8` between blocks.

### Web — landing section order

1. Hero — H1, lead, primary + secondary CTA, brand strip.
2. Cases — 3–5 recent shipped projects.
3. Focus — what we do (AI agents, RAG, chatbots).
4. Process — 4 steps.
5. Pricing / engagement — typical packages.
6. CTA — repeat the hero CTA in a heavy-glass card.
7. Footer — contacts, founders, legal.

### Slides — universal chrome

Every slide carries:
- **Brand mark + wordmark** top-left (`28 px` SVG + "Круассан Студио" Golos Bold ≈14–16 px, gap `.55em`).
- **Page number** bottom-right (`01 / 11` format, Golos Medium ≈12 px, `letter-spacing:.16em` uppercase tracked, `tabular-nums`, `paper-mute`).
- Outer padding: `7vh` top/bottom, `6vw` left/right (≈ `75.6 px / 115.2 px` on a 1920×1080 page).

The brand mark is **never removed** — not on cover, not on the section divider, not on the totals slide. Page numbers are updated by hand when slide count changes.

### Slides — five canonical kinds

Vary across consecutive slides — never run more than 3 of the same kind in a row, the deck flattens.

1. **Cover** — H1 + 3D mark inline + caption + logo strip. Brand background.
2. **Section divider** — same H1 layout as cover, no body. Lead is one line. Lots of empty space — that's the pace.
3. **Content with chips** — H1 + lead + 2×2 grid of number-boxes. For "what we do," "process," "team roles."
4. **Team intro** — H1 + polaroid photo cards + sticker tags. The most "human" slide.
5. **Case study** — graphite `#252527`, H1 Medium with split-color, lead, metric chips, screenshot composition (slightly tilted card, optional hand-drawn arrow annotation).

## 6. Depth & Elevation

The system commits to **flatness as a design choice**. Most surfaces have no shadow. Depth is communicated through **opacity, border, and surface change** — not blur or shadow.

| Element | Treatment |
|---------|-----------|
| Web cards (default) | `border border-black/5 bg-white` — 1 px hairline only. No shadow. |
| Glass card (navbar, forms) | `bg-background/80 backdrop-blur-md` — translucent, blurred backdrop. |
| Heavy glass (CTA hero card) | `bg-gradient-to-br from-white/10 to-white/5 shadow-sm backdrop-blur-[100px]` — the **only** shadowed surface on web, and it's `shadow-sm`. |
| Slide cards | No shadow. Solid fill or 1 px line on transparent. |
| **Polaroid photo card** | `drop-shadow(0px 4px 10px rgba(0,0,0,0.25))` — the **only** drop-shadowed component in the system. Pairs with `inset 0px 2px 12px rgba(0,0,0,0.1)` on the inner photo. |
| Slides Tag (sticker) | `backdrop-blur-[20px]` over photo, plus `text-shadow: 0 0 8px rgba(0,0,0,0.2)` for legibility — the only place text-shadow appears. |
| Buttons / chips | `transition-all duration-300`. No press-state shadow change. |

If you reach for `box-shadow: 0 10px 30px rgba(0,0,0,0.15)` on a marketing card, you're off-brand. Pick a hairline border or a translucent surface instead.

## 7. Do's and Don'ts

### Do

- ✅ **Tokens only**. `bg-brand`, `text-brand-dark`, `text-primary-60`, `text-error`. Never `bg-[#2727CA]`, `text-gray-500`, `text-zinc-700`.
- ✅ **Concrete numbers**. `15+ проектов`, `за 2–4 недели`, `300 000 пользователей`. From [`brand/facts.md`](../../../../brand/facts.md), never inlined.
- ✅ **Russian by default**. Em-dashes, Russian quotes, non-breaking spaces.
- ✅ **One H1 per page**, hierarchy intact (H1 → H2 → H3, no skips).
- ✅ **Lucide SVG icons**. Decorative gets `aria-hidden`; icon-only buttons get `aria-label`.
- ✅ **`next/image` and `next/link`**, never `<img>` or `<a href="/...">` for internal nav.
- ✅ **External links**: `rel="noopener noreferrer" target="_blank"`.
- ✅ **Real photography**. Real team, real client logos, real product screenshots.
- ✅ **Print/PDF CSS** on HTML decks. Lock the slide to 1920×1080 for export.
- ✅ **Brand mark + page number on every slide** — the deck chrome is non-negotiable.
- ✅ **Touch targets ≥ 44×44 px**, WCAG AA contrast.

### Don't

- ❌ **Default Tailwind indigo** (`#6366f1`, `#4f46e5`, `#4338ca`, `#3730a3`, `#8b5cf6`, `#7c3aed`, `#a855f7`). Use `--brand-primary` (`#2727CA`).
- ❌ **Two-stop "trust" gradients** (purple→blue, blue→cyan, indigo→pink) on heroes. Solid surfaces only.
- ❌ **Emoji as icons** (`✨`, `🚀`, `⚡`, `🎯`). Lucide SVG. The `🤍` on the contact slide is the **only** allowed emoji and it's typographic, not iconic.
- ❌ **Stock photography** (Unsplash, placehold.co, picsum). Real assets only — see [`assets/client-logos/`](../../../../assets/client-logos/).
- ❌ **Mid-grey backgrounds**. Brand, white, black, or graphite `#252527` — nothing in between.
- ❌ **More than 5 pill variants** or **more than 3 card variants**. The system is intentionally short.
- ❌ **Drop shadows on cards**. Polaroids are the exception.
- ❌ **Auto-layout "smartness"** on slide masters. Slides are absolute-positioned; duplicate the master frame and edit.
- ❌ **Studio + Community wordmarks in one composition**. They are siblings, not partners.
- ❌ **Invented metrics**. If you can't trace it to [`brand/facts.md`](../../../../brand/facts.md) or a real client engagement, don't ship it.
- ❌ **Filler copy** (`lorem ipsum`, "Feature one / two / three"). An empty section is a composition problem to solve, not paper to fill.
- ❌ **`text-primary-50` and below** for reading text. Placeholders only.
- ❌ **CSS-in-JS**. Tailwind-only on web; vanilla CSS on HTML decks.
- ❌ **Barrel files** (`index.ts` re-exports). Import from concrete paths.

## 8. Responsive Behavior

**Mobile-first.** Write the mobile layout without prefixes; add `md:` etc. for desktop.

| Prefix | Min-width | What it means |
|--------|-----------|---------------|
| (none) | 0 | Mobile |
| `sm:` | 640 px | Tablet portrait |
| `md:` | **768 px** | **Primary breakpoint — desktop starts here** |
| `lg:` | 1024 px | Large desktop |
| `xl:` | 1280 px | Wide desktop |

`md:` is the workhorse. `sm:` mostly arranges buttons side-by-side. `lg:`/`xl:` are for fine-tuning.

### Common patterns

```
className="hidden md:block"
className="md:hidden"
className="flex flex-col md:flex-row"
className="text-3xl md:text-5xl"
className="py-16 md:py-32"
className="gap-4 md:gap-8"
className="w-full md:w-auto"
```

### Slides — fixed canvas

Slide masters are **1280×720 absolute-positioned** in Figma. The HTML deck framework uses a 1920×1080 logical canvas with `transform: scale(--deck-scale)`; the runtime calculates `--deck-scale` to fit the viewport. Don't try to make slides responsive — they don't reflow.

The HTML template ([`../../templates/croissan-deck.html`](../../templates/croissan-deck.html)) does collapse some grids at `max-width: 900 px` for mobile preview, but the canonical experience is fullscreen on desktop or PDF.

### Touch & motion

- Touch targets: **minimum 44×44 px**. `<Button>` enforces this; for custom controls, use padding.
- `touch-action: manipulation` on `a, button, [role="button"]` — kills the 300 ms iOS tap delay.
- `prefers-reduced-motion` is wired globally — animations collapse to ~0 ms automatically. Don't override.
- Animate **only `transform` and `opacity`**, durations 150–300 ms. Never `width`/`height`/`top`/`left`.

## 9. Agent Prompt Guide

This section tells an agent how to **use this design system without copying it verbatim**. Treat the rules above as a strong reference, not a script. The system has gaps — fill them with judgment, not invention.

### Use as a reference, not a template

- **Pull tokens before patterns.** Always reach for `--brand-primary`, the type scale, and the pill/card vocabulary first. They're stable.
- **Match the *feel*, not the layout.** If a brief calls for an unusual section ("animated logo wall", "side-by-side comparison with a competitor", "interactive pricing slider"), invent the layout — but use *our* tokens, *our* type scale, *our* pill vocabulary inside it.
- **Borrow, don't transplant.** Pulling the team-intro slide structure from the КП deck into a marketing site case study is fine — but adapt the proportions, swap polaroid for case-card, and don't ship a slide layout pretending to be a web section.
- **When two rules conflict, pick the one closer to the running surface** (web rules win in `app/`, deck rules win in `assets/deck-template/`).

### What's in scope for invention

- **New section types** the brief mentions but the docs don't cover. Invent the layout; honor the tokens.
- **New copy patterns** that fit the voice (caring + smart + slightly bold). The voice docs cover *examples*, not the full space.
- **New slide compositions** for proposals about specifically tech-led products. The five canonical slide kinds are the **trunk**, not the whole tree.
- **Iconography for technical concepts** the brief introduces (e.g., a stack diagram). Lucide-style monoline SVG, 1.6–1.8 px stroke, `currentColor`.

### What's out of scope for invention

- New **brand colors**. The palette is locked. Cobalt + black + white + graphite, plus chart oklch, plus error red. Anything else needs founder approval.
- New **typefaces**. Right Grotesk + Golos Text + Geist Mono. Period.
- New **logo lockups**. Use the SVG mark + the wordmark conventions in [`identity/logo/usage.md`](../../../../identity/logo/usage.md).
- **Stand-in numbers** that conflict with [`brand/facts.md`](../../../../brand/facts.md). If the brief contradicts facts.md, surface the conflict before shipping.
- **Voice in another language** unless the brief is explicitly English-audience.

### Workflow when invoked

1. Read this DESIGN.md and at least one of: [`design-system/decks.md`](../../../../design-system/decks.md) (for slides), [`design-system/components.md`](../../../../design-system/components.md) (for web).
2. Pull facts from [`brand/facts.md`](../../../../brand/facts.md). Don't inline numbers.
3. Match the brief to one of the five slide kinds (or the web section pattern). If none fit, **invent within the token system**, not outside it.
4. Run the pre-ship checklist: [`agents/checklists.md`](../../../../agents/checklists.md).
5. If you broke a "Don't" rule deliberately, leave a one-line comment explaining why.

### Tone hooks for generation

- Headlines: direct, with personality. Use «мы» / «вы» to create connection. Soft imperatives are fine.
  - ✅ «Зовите нас, когда нужен продукт с&nbsp;ИИ»
  - ❌ «Профессиональная разработка AI-решений»
- CTAs: action-oriented, friendly. «Написать нам», «Создать бриф», «Начать проект».
  - ❌ «Оставить заявку», «Заказать консультацию»
- Errors: concrete. «Укажите телефон или Telegram», not «Ошибка».
- Concrete > fuzzy: `15+`, not «много»; `2–4 недели`, not «быстро».

### Source files inside this repo

| Need | File |
|------|------|
| Voice + tone examples | [`brand/voice-and-tone.md`](../../../../brand/voice-and-tone.md) |
| Numbers, names, addresses | [`brand/facts.md`](../../../../brand/facts.md) |
| Web section + component spec | [`design-system/components.md`](../../../../design-system/components.md) |
| Slide visual spec | [`design-system/decks.md`](../../../../design-system/decks.md) |
| Deck narrative (КП structure) | [`brand/proposal-structure.md`](../../../../brand/proposal-structure.md) |
| HTML deck template | [`assets/deck-template/index.html`](../../../../assets/deck-template/index.html) |
| Hard rules (visual + copy) | [`agents/design-rules.md`](../../../../agents/design-rules.md), [`agents/content-rules.md`](../../../../agents/content-rules.md) |
| Latitude — what to invent freely | [`agents/creative-latitude.md`](../../../../agents/creative-latitude.md) |
| Anti-slop — LLM defaults we reject | [`agents/anti-ai-slop.md`](../../../../agents/anti-ai-slop.md) |
