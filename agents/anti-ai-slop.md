# Anti-AI-slop rules

The patterns LLMs default to that we explicitly reject. This isn't "what the brand
requires" — that's [`design-rules.md`](design-rules.md). This is "what your training
data wants you to ship that we will catch and send back."

> Pattern adapted from
> [`nexu-io/open-design/craft/anti-ai-slop.md`](https://github.com/nexu-io/open-design/blob/main/craft/anti-ai-slop.md)
> (Apache-2.0), tightened to Croissan-specific tells.

Severity:
- **P0 — must-fix.** A reviewer will reject the work. Treat as a hard rule, even though
  this file isn't framed as one.
- **P1 — should-fix.** Soft tells; the work ships, but it doesn't feel like ours.
- **P2 — nice-to-fix.** Polish.

---

## P0 — the seven cardinal sins

These are the patterns that mark a generation as "AI default" rather than "studio output."
Failing any of these is a regression.

### 1. Default Tailwind indigo as accent

Exactly any of: `#6366f1`, `#4f46e5`, `#4338ca`, `#3730a3`, `#8b5cf6`, `#7c3aed`,
`#a855f7`, plus the `bg-indigo-*` / `bg-violet-*` / `bg-purple-*` Tailwind utilities used
as a brand surface.

The studio's brand is `#2727CA` (cobalt). It is **next to** indigo on the color wheel —
that makes it tempting to substitute. Don't. Use `--brand-primary` (`bg-brand`,
`text-brand`).

### 2. Two-stop "trust" gradients on the hero

Purple→blue, blue→cyan, indigo→pink, cobalt→cyan. The "AI SaaS hero" gradient is the most
recognizable LLM-default pattern in 2024–2026 web design.

Croissan's web hero is a **flat near-white surface** (`--background`). Croissan's slide
hero is a **flat brand-blue surface** (`--brand-primary`). The only gradient in the entire
system is the `number-box` chip surface, and it is hidden inside a 32-px-radius box.
**No hero gradients.**

### 3. Emoji as feature icons

`✨ 🚀 🎯 ⚡ 🔥 💡 ⭐ 🤖` inside `<h*>`, `<button>`, `<li>`, or anything tagged
`class*="icon"` / `class*="feature"`.

Use Lucide SVG (`lucide-react`), 1.6–1.8 px stroke, `currentColor`. The single allowed
exception is the typographic `🤍` on the КП contact slide — it is decoration, not an icon.

### 4. Tailwind / system-ui sans on display type

Display type — H1 on the marketing site, H1 on slides — uses **Right Grotesk Bold** (web)
or **Golos UI Bold 90 px** (slides). If you find yourself typing `font-family: Inter` or
`font-family: -apple-system, system-ui, sans-serif` on an H1, you are in slop territory.

Body and H2/H3 use Golos Text — that's correct. The tell is using the body family for the
hero headline.

### 5. Rounded card with a colored left-border accent

The canonical "AI dashboard tile" — `rounded-xl border-l-4 border-l-blue-500`. We don't
ship this shape. Cards in our system have:

- A 1 px **all-around** hairline (`border-black/5` on white, `border-white/18` on dark).
- **No** left-border accent. **No** colored stripes.

If a section feels like it needs a left-border accent for visual emphasis, the answer is
either (a) make the entire card `card.featured` (white inverse on cobalt slides) or
(b) add a tracked uppercase eyebrow (`.lbl` / `.meta` class) at the top.

### 6. Invented metrics

`10× faster`, `99.9% uptime`, `3× more productive`, `300% engagement`, `~50ms latency` —
unless the number is from a **real engagement** or **[`brand/facts.md`](../brand/facts.md)**,
don't write it.

The Russian variant is just as common: «в&nbsp;10&nbsp;раз быстрее», «эффективность в&nbsp;3&nbsp;раза»,
«рост на&nbsp;200%». Same rule.

If the brief is missing a real metric and you need a placeholder, write
`{{TODO: real metric}}` and surface it in your hand-off. **Never invent.**

### 7. Filler copy

`lorem ipsum`, `Feature one / Feature two / Feature three`, `Lorem ipsum dolor`,
`placeholder text`, `sample content`, `Тут будет описание`, `Заполнить позже`.

An empty section is a **composition problem to solve**, not paper to fill with words.
If you don't know what goes there, leave the section out of the layout entirely or use
`{{labeled placeholder}}` and surface it.

---

## P0 — Croissan-specific cardinal sins (eight more)

These are P0 too but they're brand-specific, not the universal LLM tells above.

### 8. Russian copy with Latin straight quotes

`"привет"` is the AI tell. We use «привет». Always. Even in code comments if the comment
is in Russian.

The same applies to apostrophes — `'это'` is wrong; we don't use single Russian quotes,
we use the regular text without quotes or fall back to «…».

### 9. Hyphens where em-dashes belong

`Мы студия - заботливая` — wrong (regular hyphen with spaces).
`Мы студия — заботливая` — right (em-dash, U+2014, with spaces).

The minus-with-spaces version is a near-universal tell that the copy was generated
without locale-aware typography. There's no in-between: it's `—` or restructure the
sentence.

### 10. Russian copy without non-breaking spaces

`за 2-4 недели`, `с ИИ`, `на рынке`, `15+ проектов` — every short preposition and short
standalone word in Russian copy gets a `&nbsp;` before it. Not "if it fits" — every time.

The compiled tells:
- `за&nbsp;2-4&nbsp;недели`
- `с&nbsp;ИИ`
- `на&nbsp;рынке`
- `15+&nbsp;проектов`

In HTML, literal `&nbsp;`. In React/JSX, `{" "}` or `&nbsp;` if HTML-passthrough.
In Markdown destined for Figma, the actual U+00A0 character.

### 11. КП vendor-template framing

The phrase «Заказчик» / «Исполнитель» / «Клиент имеет право» / «В соответствии с
требованиями» — these are corporate-template tells. We are a **partner**, not a vendor.

Use:
- ✅ «мы / вы», «совместно», «в&nbsp;партнёрстве»
- ❌ «заказчик / исполнитель»
- ✅ «помогаем разобраться», «оборачиваем идею в&nbsp;технологию»
- ❌ «оказываем услуги», «проводим работы»

### 12. Generic AI-marketing phrases

«Передовые AI-решения», «инновационные технологии искусственного интеллекта»,
«комплексная цифровая трансформация», «революционный подход» — all of these are LLM
defaults when asked to describe an AI studio. They say nothing.

Replace with concrete: what we actually do (`ИИ-агенты`, `RAG-системы`, `чат-боты`),
in what timeframe (`за 2–4 недели`), for whom (`МТС`, `Яндекс`, `T1`).

### 13. Stock photography

`unsplash.com`, `placehold.co`, `picsum.photos`, `placekitten.com`, `pexels.com`, plus
the visual cliché: business handshakes, "diverse team in glass office", "futuristic
hologram cityscape", "robot hand touching human hand."

We use real photos:
- Real team portraits → [`assets/client-logos/`](../assets/client-logos/) for client logos.
- Real product screenshots in case-study slides.
- For prototype demos that don't exist yet: `{{labeled placeholder box}}`, not stock.

If a placeholder image is genuinely needed mid-development, use the project's own
`.ph-img` class (transparent box with a 1 px hairline), not an external CDN.

### 14. Mid-grey backgrounds

Surfaces are: brand `#2727CA`, paper white, ink black `#0E0E14`, graphite `#252527`. That's it.

If a slide or page section uses `bg-zinc-700`, `bg-slate-800`, `bg-neutral-600`, or any
hex between `#404040` and `#909090`, that's the AI-design-system midtone — not ours.

### 15. Drop-shadows on every card

`box-shadow: 0 10px 30px rgba(0,0,0,0.15)` on a marketing card, `shadow-lg` on a list
item, `shadow-xl` on a hero CTA — this is the AI-dashboard aesthetic and the system
intentionally rejects it.

The **only** drop-shadow in the whole system is on polaroid photo cards
(`drop-shadow(0px 4px 10px rgba(0,0,0,0.25))`). Glass surfaces use `backdrop-blur`,
not shadow. Cards use a hairline border.

---

## P1 — soft tells, should-fix

The work ships if these slip through, but it stops feeling like ours.

- **Standard "Hero → Features → Pricing → FAQ → CTA" landing skeleton.** This is the
  AI-template SaaS shape. Our landing has Hero → **Cases** → Focus → Process → Pricing
  → CTA, with cases (named clients, real screenshots) early and not behind a fold.
- **Default 18-slide КП when 11 would do.** See [`brand/proposal-structure.md`](../brand/proposal-structure.md)
  for the criteria. Padding a КП makes it feel insecure; trust the compact structure
  when the brief is tech-led.
- **`var(--brand-primary)` used 6+ times in the rendered body.** Cap at ~2 visible uses
  per screen — primary CTA + one accent. Beyond that, the brand color stops being the
  brand color and becomes wallpaper.
- **More than ~12 raw hex values outside `:root` / `@theme`.** If a file is shedding
  hex, tokens were not honored. Refactor.
- **Hyphenated bullet lists.** `- foo / - bar / - baz` with trivial labels. Either it's
  worth a real sentence each or it's a `pill-row`.
- **Section headers shouting** in `text-uppercase`. We don't shout headers; eyebrow
  labels shout (`.meta`, `.lbl`), section H2s don't.
- **Emoji bullet points** (`✅ ❌ 🟢 🔴 ⚠️ ℹ️`). Inside this repo's docs, ✅/❌ are used
  to mark do/don't examples — that's fine and intentional. In *generated user-facing
  output*, no emoji bullets.
- **`<br>` in body paragraphs** on the marketing site. Use `<br>` only inside hero H1s
  (where line breaks are typographic decisions) and inside slide H1/H2 (same reason).
  Body paragraphs flow naturally.

---

## P2 — polish, nice-to-fix

- **Comments inside generated code** that say "Add your X here", "Replace this with your
  brand color", "Customize as needed." Either the slot has a `{{placeholder}}` label or
  it doesn't need one — explanatory comments in committed deck/section code are slop.
- **Section IDs missing on slides / web sections.** Without `id="hero"` or `data-od-id`
  on a section, comment-mode tools and anchor links can't target them.
- **Generic SVG file names.** `image1.svg`, `icon-2.svg`, `Frame123.svg`. Use semantic
  names: `mts-logo.svg`, `process-step-3.svg`, `polaroid-frame.svg`.
- **Russian copy that introduces an English word with a definite-article-like
  construction.** «Тот самый AI-агент» / «наш собственный RAG» — usually fine. But
  «продвинутый AI» as a flagship adjective is borrowed-machine-translation phrasing.
  Better to drop the adjective.
- **Consecutive slides with the same `slide.<surface>` class.** More than 3 in a row
  flattens the deck. Vary brand → divider → content → case → divider.

---

## How to use this file

If you're an agent and you've just generated something:

1. Read your output once **looking for cardinal sins**. The seven generic + eight
   Croissan-specific are P0.
2. If you find any, fix them before declaring done. Don't ask the user; these are
   non-negotiable.
3. Soft tells (P1) — fix if you have time, surface in hand-off if you don't.
4. Polish (P2) — note for follow-up.

If you're a reviewer:

- Send back P0 violations without comment. The agent should know to look.
- Annotate P1 violations as "soft" — the work ships if everything else is right.
- P2 violations are advisory.

## Cross-references

- Locked rules: [`design-rules.md`](design-rules.md), [`content-rules.md`](content-rules.md)
- What's safe to invent: [`creative-latitude.md`](creative-latitude.md)
- Pre-commit checks: [`checklists.md`](checklists.md)
- The DESIGN.md anti-slop section in the open-design integration:
  [`../integrations/open-design/design-systems/croissan/DESIGN.md`](../integrations/open-design/design-systems/croissan/DESIGN.md)
  (section 7 — Do's and Don'ts)
