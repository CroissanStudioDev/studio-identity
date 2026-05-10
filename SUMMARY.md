# Croissan Studio — brand context (single-file)

**One-paragraph summary.** Croissan Studio is a Russian-default AI product studio.
Voice is caring, smart, slightly bold — partner not vendor, concrete numbers over fuzzy
adjectives. Visual identity runs on a single Croissan blue (`#2727CA`) over near-white,
with black and graphite (`#252527`) as premium and case-study surfaces. Two typefaces
do all the work: **Right Grotesk Bold** for web H1, **Golos Text** for everything else.

This file is **the 20% of the brand that gives 80% value** — designed to be pasted into
any chat (Cursor, Claude.ai, ChatGPT, Windsurf, Continue, …) when the dev wants
brand-correct output without installing anything.

> **For the full system:** [`README.md`](README.md). For agents that read skills:
> [`skills/croissan-identity/SKILL.md`](skills/croissan-identity/SKILL.md). For
> open-design users: [`integrations/open-design/`](integrations/open-design/).

---

## Color tokens (locked)

```css
--brand-primary:        #2727CA;   /* Croissan blue — every CTA, every accent */
--brand-primary-hover:  #2424B4;   /* hover state on primary */
--brand-dark:           #150E47;   /* near-black, same hue family */
--brand-black:          #0E0E14;   /* premium / cover surface */
--brand-graphite:       #252527;   /* CASE-STUDY slides only */
--background:           oklch(0.98 0.01 260);  /* near-white canvas */
--color-error:          #E53935;
```

**Surface vocabulary on slides:**

```css
--croissan-blue-soft: #3D3DE0;   /* secondary pill on brand slide bg */
--croissan-blue-deep: #1F1FA8;   /* alternative secondary pill */
--croissan-blue-card: #2D2DFC;   /* number-box surface */
--croissan-blue-lav:  #BCBCFF;   /* text inside number-box (lavender) */
--paper-dim:     rgba(255,255,255,.72);   /* secondary text on dark */
--paper-mute:    rgba(255,255,255,.55);   /* tertiary text on dark */
--line:          rgba(255,255,255,.18);   /* dividers on dark */
```

**Tailwind class equivalents:** `bg-brand`, `text-brand`, `text-brand-dark`,
`text-error`. **Body text opacity scale on light:** `text-primary` (100%), `text-primary-90`,
`-80`, `-70`, `-60`. **Anything below `-60` is placeholder-only — never reading text.**

---

## Typefaces

| Role | Family | Source |
|------|--------|--------|
| Web H1 (display) | **Right Grotesk** Bold | studio-licensed, file at `assets/fonts/right-grotesk/accent-typeface.woff2` |
| Web body, sub-headings, slide content | **Golos Text** | OFL — Google Fonts (`Golos Text`) or bundled at `assets/fonts/golos-text/` |
| Mono | **Geist Mono** | OFL — Google Fonts |
| Slide metric chips (case-study) | **Inter** Medium | OFL — Google Fonts |
| Server-side rendering (OG / PDF) | **Noto Sans** | OFL — bundled at `assets/fonts/noto-sans/` |

Locked. Don't introduce a third sans-serif. If a project shows up needing one, that's a
brand-decision conversation with founders.

## Type scale

**Web:**

```
H1   font-bold text-5xl text-primary leading-[1] -tracking-[1.2px] md:text-7xl
     style: var(--font-right-grotesk)         ← only place Right Grotesk appears
H2   font-semibold text-3xl tracking-tight md:text-5xl
H3   font-medium text-2xl tracking-tight md:text-3xl lg:text-4xl
Lead text-lg text-primary-60 leading-[150%] md:text-xl
Body text-primary-60   (opacity-scaled brand-dark on light)
```

**Slides (1280×720 master, fixed pixel):**

```
H1 standard   Golos UI Bold (or Golos Text Bold) 90px / line-height 1 / -1.8px tracking
H1 case-study Same as above but Medium weight; often split-color for the accented word
Lead          Golos Text Regular 48px / 1.2 / -0.96px / opacity 0.8
Caption       Golos Text Regular 32px / 1.2 / -0.64px / opacity 0.8
Card body     Golos Text SemiBold 32px / 1.2 / color #BCBCFF on Croissan blue
Tag/sticker   Golos UI Medium (or Golos Text Medium) 18px / line-height 1
```

Russian-default: em-dashes (`—`), Russian quotes («…»), non-breaking spaces (`&nbsp;`)
before short prepositions (`с&nbsp;ИИ`, `за&nbsp;2-4&nbsp;недели`).

---

## Components — pill / card vocabulary

The brand is heavy on **pills and cards**. There are exactly **3 pill variants** (filled
only — no outline, no white «light» pill on brand slides) and **2 card variants** — don't
add a fourth pill type or a third card chrome without a brand decision.

**Pills** (border-radius 999px, padding ~`.85em 1.25em`, weight 500 ~1vw):

```
.pill.dark    bg #0E0E14, white text          — accent tags, contact chips on brand bg
.pill.soft    bg #3D3DE0, white text          — service / tag clusters
.pill.deep    bg #1F1FA8, white text          — alternative when soft would clash
```

**Cards** on Croissan-blue slide backgrounds (border-radius 18px, padding `2.6vh 1.6vw`):

```
.card           bg #0E0E14 (or `#1A1A22` ink-soft for contrast), white text — default / alt tier
.card.featured  bg white, brand-blue text       — recommended option / highlighted tier
```

---

## Voice — caring, smart, slightly bold

**Headlines** — direct, conversational, often soft imperatives:

```
✅ "Зовите нас, когда нужен продукт с ИИ"
✅ "Внедряем ИИ в существующие продукты и создаём новые с нуля"
❌ "Профессиональная разработка AI-решений"
❌ "Комплексные услуги по внедрению ИИ"
```

**CTAs** — friendly, dialogic:

```
✅ "Написать нам", "Создать бриф", "Забронировать звонок"
❌ "Оставить заявку", "Заказать консультацию"
```

**Body** — warm, conversational, em-dashes for flow:

```
✅ "Мы ваша заботливая студия полного цикла. Бережно собираем идеи, оборачиваем
    их в технологии, тестируем, запускаем — и всё это в партнёрстве с вами."
❌ "Наша компания предоставляет полный спектр услуг..."
```

**КП copy** — partner not vendor: «мы / вы», «в&nbsp;партнёрстве». Forbidden:
«заказчик / исполнитель», «оказываем услуги», «комплексные решения».

**Concrete numbers always.** `15+`, `2–4 недели`, `3+ года`. Never «много», «быстро»,
«эффективно». And **don't invent metrics** — if it's not from a real engagement, write
`{{TODO: real metric}}` and surface it.

---

## Anti-slop — patterns we explicitly reject

These are the LLM defaults that mark a generation as "AI default" rather than ours.
Treat as P0:

1. **Tailwind indigo** (`#6366f1`, `#4f46e5`, `#4338ca`, `#8b5cf6`, `#7c3aed`) used as
   accent. Use `--brand-primary` `#2727CA`. Indigo is *next to* Croissan blue — that's why
   models reach for it. Don't.
2. **Two-stop "trust" gradients** on hero (purple→blue, blue→cyan, indigo→pink,
   Croissan-blue→cyan). Flat surfaces only. The only gradient anywhere in the system is the
   number-box chip surface, hidden inside a 32px-radius box.
3. **Emoji as feature icons** (`✨ 🚀 🎯 ⚡ 🔥 💡`). Use Lucide SVG, 1.6–1.8px stroke,
   `currentColor`. The single allowed exception is the typographic `🤍` on the КП
   contact slide.
4. **Sans-serif system-ui on display H1.** Web H1 = Right Grotesk. Slide H1 = Golos
   UI/Text Bold 90 px. `Inter` / `system-ui` on display is a near-universal AI tell.
5. **Rounded card with colored left-border accent** (`rounded-xl border-l-4
   border-l-blue-500`). The "AI dashboard tile." Drop either the radius or the border.
6. **Invented metrics** — `10× faster`, `99.9% uptime`, `3× more productive`, also the
   Russian variant: «в 10 раз быстрее», «эффективность в 3 раза». If not from a real
   source, write `{{TODO}}`.
7. **Filler copy** — `lorem ipsum`, `Feature one / two / three`, "Тут будет описание".
8. **Russian Latin straight quotes** — `"привет"` is wrong; «привет» is right.
9. **Hyphens where em-dashes belong** — `Мы студия - заботливая` is wrong; `—` is right.
10. **Russian without `&nbsp;`** before short prepositions. `с&nbsp;ИИ`, `за&nbsp;2-4&nbsp;недели`.
11. **«Заказчик / Исполнитель» framing** in КП copy. Partner, not vendor. Use «мы / вы».
12. **Generic AI-marketing phrases** — «передовые AI-решения», «инновационные
    технологии искусственного интеллекта», «комплексная цифровая трансформация».
13. **Stock photography** — Unsplash, picsum, "diverse team in glass office," handshake
    composites. Real team, real screenshots.
14. **Mid-grey backgrounds.** Surfaces are: Croissan blue, white, black, graphite. Anything in
    between (zinc-700, slate-800) is the AI midtone — not ours.
15. **Drop-shadows on cards.** Polaroids are the only exception in the system.

---

## Five canonical slide kinds

Vary across consecutive slides — never run >3 of the same kind in a row:

1. **Cover** — H1 + 3D mark inline + caption + logo strip. Brand background.
2. **Section divider** — same H1 layout as cover, no body. Lead is one line.
3. **Content with chips** — H1 + lead + 2×2 grid of number-boxes.
4. **Team intro** — H1 + polaroid photo cards + sticker tags.
5. **Case study** — graphite `#252527`, H1 Medium with split-color, lead, metric chips,
   screenshot composition.

---

## Where to find more

Everything in this file maps to one or more deeper docs at
[`https://github.com/CroissanStudioDev/studio-identity`](https://github.com/CroissanStudioDev/studio-identity).
**Single sources of truth**: voice → `brand/voice-and-tone.md`; slide visual primitives →
`design-system/decks.md`; token hex values → `design-system/design-tokens.css`. Other
docs (including this one) surface extracts; if they drift, the SoT wins.

| Topic | Deeper doc |
|-------|-----------|
| Voice + copy patterns | [`brand/voice-and-tone.md`](brand/voice-and-tone.md), [`brand/messaging.md`](brand/messaging.md) |
| Numbers, names, contacts | [`brand/facts.md`](brand/facts.md) |
| КП narrative (what slides, in what order) | [`brand/proposal-structure.md`](brand/proposal-structure.md) |
| Web components | [`design-system/components.md`](design-system/components.md), [`design-system/sections-and-layout.md`](design-system/sections-and-layout.md) |
| Slide visual spec (full) | [`design-system/decks.md`](design-system/decks.md) |
| Anti-slop full list (15 + softs + polish) | [`agents/anti-ai-slop.md`](agents/anti-ai-slop.md) |
| Creative latitude (what's free vs locked) | [`agents/creative-latitude.md`](agents/creative-latitude.md) |
| Logo + wordmark | [`identity/logo/usage.md`](identity/logo/usage.md), `assets/logos/` |
| Fonts (with READMEs per family) | [`assets/fonts/`](assets/fonts/) |
| Drop-in CSS tokens | [`design-system/design-tokens.css`](design-system/design-tokens.css) |
| HTML deck template (single-file) | [`assets/deck-template/index.html`](assets/deck-template/index.html) |
| Open-design integration | [`integrations/open-design/`](integrations/open-design/) |

---

## Use this in a project (3 ways, ordered cheapest first)

1. **Just paste this file's URL into the chat.**
   `https://raw.githubusercontent.com/CroissanStudioDev/studio-identity/main/SUMMARY.md`.
   Cursor, Claude.ai, ChatGPT, Windsurf — all let you reference URLs as context. No install.

2. **One-line install for Claude Code.**
   ```
   curl -sL https://raw.githubusercontent.com/CroissanStudioDev/studio-identity/main/bin/install | bash
   ```
   Clones the repo to `~/.croissan/identity` and symlinks the skill to `~/.claude/skills/croissan-identity`. Available globally — every project on the machine.

3. **Clone the full repo.**
   For editing the brand itself, or for projects that need the actual binary assets
   (logos, fonts, deck template HTML).
