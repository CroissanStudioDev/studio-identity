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

## P0 — universal cardinal sins

These are the patterns that mark a generation as "AI default" rather than "studio output."
Failing any of these is a regression.

### 1. Default Tailwind indigo as accent

Exactly any of: `#6366f1`, `#4f46e5`, `#4338ca`, `#3730a3`, `#8b5cf6`, `#7c3aed`,
`#a855f7`, plus the `bg-indigo-*` / `bg-violet-*` / `bg-purple-*` Tailwind utilities used
as a brand surface.

The studio's brand is `#2727CA` (Croissan blue — rich deep blue). It is **next to** indigo on the color wheel —
that makes it tempting to substitute. Don't. Use `--brand-primary` (`bg-brand`,
`text-brand`).

### 2. Two-stop "trust" gradients on the hero

Purple→blue, blue→cyan, indigo→pink, Croissan-blue→cyan. The "AI SaaS hero" gradient is the most
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
either (a) make the entire card `card.featured` (white inverse on brand-blue slides) or
(b) fold the label into the title line — no separate uppercase eyebrow row.

### 6. Invented metrics

`10× faster`, `99.9% uptime`, `3× more productive`, `300% engagement`, `~50ms latency` —
unless the number is from a **real engagement** or **[`brand/facts.md`](../brand/facts.md)**,
don't write it.

**Orphan statistics** — numbers without a baseline or source («3× faster than what?»,
«90% accuracy on what test set?») — are the same sin in disguise. Either name the
baseline (`«быстрее обычного RAG-пайплайна на той же GPU в 3 раза»`) or drop the
multiplier.

The Russian variant is just as common: «в&nbsp;10&nbsp;раз быстрее», «эффективность в&nbsp;3&nbsp;раза»,
«рост на&nbsp;200%». Same rule.

**"Join thousands of…" / "trusted by 10,000+"** — Croissan's truth is `15+ проектов`
with **named clients** (МТС, Ростелеком, Яндекс, T1, Positive Technologies). Don't pad
the number; name the engagement.

If the brief is missing a real metric and you need a placeholder, write
`{{TODO: real metric}}` and surface it in your hand-off. **Never invent.**

### 7. Filler copy

`lorem ipsum`, `Feature one / Feature two / Feature three`, `Lorem ipsum dolor`,
`placeholder text`, `sample content`, `Тут будет описание`, `Заполнить позже`.

An empty section is a **composition problem to solve**, not paper to fill with words.
If you don't know what goes there, leave the section out of the layout entirely or use
`{{labeled placeholder}}` and surface it.

---

## P0 — Croissan-specific cardinal sins

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

### 16. Gradient text on H1/H2

`background: linear-gradient(...); -webkit-background-clip: text; color: transparent;`
on a hero headline. Universal AI-SaaS giveaway, hard ban. Display H1 is **solid
`text-primary` on light surfaces** or **solid white on Croissan blue/black/graphite**. Same
rule applies to slide H1s.

If a designer wants emphasis on a single word inside an H1, use **opacity** (the
split-color H1 pattern from case-study slides — primary white + 60% white) — never
gradients.

### 17. Fake testimonials

`"Jane, Product Manager at TechCorp" + stock-headshot circle.` Hard ban. Quotes either
come from a real client we can name (or attribute as "клиент Х под NDA" with founder
sign-off) or they don't ship. Logos in the trust strip come from
[`assets/client-logos/`](../assets/client-logos/) only — real engagements, no
"as featured in" composites.

---

## P1 — soft tells, should-fix

The work ships if these slip through, but it stops feeling like ours.

- **Standard "Hero → Features → Pricing → FAQ → CTA" landing skeleton.** This is the
  AI-template SaaS shape. Our landing has Hero → **Cases** → Focus → Process → Pricing
  → CTA, with cases (named clients, real screenshots) early and not behind a fold.
- **Default 18-slide КП when 11 would do.** See [`brand/proposal-structure.md`](../brand/proposal-structure.md)
  for the criteria. Padding a КП makes it feel insecure; trust the compact structure
  when the brief is tech-led.
- **Brand blue used as wallpaper.** Cap repeated `var(--brand-primary)` accents at ~2 visible
  uses per web screen. On slides, use blue for covers, openers, and big ideas; case studies,
  product screenshots, and page-like compositions should usually start from graphite or white.
- **More than ~12 raw hex values outside `:root` / `@theme`.** If a file is shedding
  hex, tokens were not honored. Refactor.
- **Hyphenated bullet lists.** `- foo / - bar / - baz` with trivial labels. Either it's
  worth a real sentence each or it's a `pill-row`.
- **Section headers shouting** in `text-uppercase`. Marketing section H2s stay sentence case.
  On **slides**, don't stack a small uppercase line above the main heading — fold context into
  the H2, lead, pills, or card titles (see [`design-system/decks.md`](../design-system/decks.md)).
- **Emoji bullet points** (`✅ ❌ 🟢 🔴 ⚠️ ℹ️`). Inside this repo's docs, ✅/❌ are used
  to mark do/don't examples — that's fine and intentional. In *generated user-facing
  output*, no emoji bullets.
- **`<br>` in body paragraphs** on the marketing site. Use `<br>` only inside hero H1s
  (where line breaks are typographic decisions) and inside slide H1/H2 (same reason).
  Body paragraphs flow naturally.
- **Generic vision taglines.** «Meet the future of AI», «Empowering teams to ship
  faster», «The next generation of product studios». They say nothing. Replace with
  concrete: what we do, for whom, in what timeframe.
- **Vague "AI-powered" claims.** «AI-powered platform», «smart insights», «intelligent
  automation» without naming the model, the architecture, or the actual user outcome.
  Croissan voice uses concrete: `RAG`, `LLM-агент`, `GPT-4o`, `чат-бот для саппорта на
  300k пользователей`.
- **CTA inconsistency across a page.** Hero says "Get started", nav says "Sign up",
  footer says "Try free" — three CTAs, three voices, no shared library. CTAs must trace
  to [`../brand/messaging.md`](../brand/messaging.md). Pick one phrase and use it
  everywhere on the page.
- **Logo entrance animation on page load.** Scale-up, rotate-in, bounce, fade. Tanks
  LCP and reads as junky. The mark renders as-is; if a hero needs movement, use a
  short opacity fade on the *content below* the mark, not the mark itself.
- **Scroll-jacking / parallax-on-everything.** Smooth-scroll hijacks, locked sections,
  pinned-and-released hero on scroll, parallax on the brand mark. Kills keyboard nav,
  kills trackpad UX, kills accessibility. The browser's default scroll is already good.
- **Fade-up-on-scroll on every section.** Restraint clause: motion is allowed on
  *interactive* elements (button hover, modal entry, polaroid drag) and on the *first*
  viewport — never as page-wide entrance choreography. If every section animates in,
  no section stands out.
- **AI-image tells in illustrations.** Over-rendered glassy 3D blobs, asymmetric eyes
  or hands, "iridescent gradient mesh" backgrounds, "plasma" abstract textures. The
  3D croissant mascot is the only dimensional render in the system; everything else is
  flat SVG, real photography, or a screenshot.
- **Em-dash overuse and "It's not just X — it's Y" parallelism.** Cap at one em-dash
  per paragraph. The «не просто X — но Y» / «It's not just X — it's Y» rhetorical
  scaffold is banned outright; it's the most overused AI-prose construct of the era.
- **Lorem-ipsum-shaped real copy.** Three feature cards with identical sentence length
  and parallel rhythm («Быстрая разработка / Умная аналитика / Надёжная инфраструктура»).
  Vary the cadence — one short sentence, one with a sub-clause, one specific outcome.
- **Demo videos without poster frame, captions, or transcript.** Poster is a P1 a11y +
  LCP issue; captions are an a11y issue; transcript is a GEO issue (AI search engines
  index the transcript, not the video).

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
- **Icon-as-decoration soup.** Every bullet prefixed by a different Lucide icon picked
  more or less at random — `Zap` for one, `Sparkles` for the next, `Star` for the third.
  Icons earn their place by carrying meaning the text alone doesn't, or get cut. See
  the canonical icon-per-concept allowlist in [`../identity/iconography.md`](../identity/iconography.md).
- **Hidden desktop nav at `≥md:`.** Hamburger on a 1440-pixel screen is a SaaS template
  copy-paste. Show the nav inline; collapse only below `md:`.

---

## How to use this file

If you're an agent and you've just generated something:

1. Read your output once **looking for cardinal sins**. All P0 entries are non-negotiable.
2. If you find any, fix them before declaring done. Don't ask the user.
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

---

## Good tells — what to grade *toward*

The audit list above is what to grade *away from*. This section is what good output
looks like — concrete moves a reviewer can recognize as "this writer knows the brand."

- **Specific verbs over weasel verbs.** «Внедряем», «собираем», «оборачиваем» beat
  «помогаем», «обеспечиваем», «поддерживаем». «We embed RAG into your support flow»
  beats «We help you with AI».
- **Real numbers that trace to a real engagement** or to [`../brand/facts.md`](../brand/facts.md).
  `15+ проектов`, `300 000 пользователей`, `~300 мс на кадр`, `2–4 недели` — every one
  pulled from a real shipped project. The reviewer should be able to ask "where does
  this number come from?" and get a one-line answer.
- **Named clients, not "trusted by leading enterprises".** `МТС`, `Ростелеком`,
  `Яндекс`, `T1`, `Positive Technologies`. Listed in recognition order, not
  alphabetical.
- **Concrete deliverables, not "solutions".** `Telegram-бот для 300 000 пользователей`
  beats `решение для повышения вовлечённости`. The deliverable is what the user touches;
  the «solution» framing is what AI defaults to.
- **One technical term per claim, used correctly.** `RAG`, `ИИ-агент`, `LLM`,
  `FP8-квантизация`, `realtime-стилизация`. Signals expertise (Princeton: +32.7% AI
  citation rate). Don't stack three; pick the one that's load-bearing.
- **One em-dash per paragraph, used as a true parenthetical break.** «Бережно собираем
  идеи, оборачиваем их в технологии, тестируем, запускаем — и всё это в партнёрстве с
  вами.» — the dash earns the pause.
- **Russian quotes («…»), em-dashes (—), and `&nbsp;` before short prepositions** —
  these are typographic signals that someone wrote it, not generated it.
- **Partner-not-vendor framing.** «мы / вы», «в&nbsp;партнёрстве», «совместно». Avoid
  «заказчик / исполнитель», «оказываем услуги».
- **CTA that names the next action, not the meta-action.** «Написать нам» beats
  «Связаться с нами»; «Создать бриф» beats «Узнать больше»; «Забронировать звонок»
  beats «Оставить заявку».
- **Sections that vary in shape across the page.** Hero (left-aligned H1) → cases
  (card grid) → focus (chip cluster) → process (numbered list) → pricing (comparison
  table) → CTA (heavy-glass card). Each section reads as its own thing; the page has
  rhythm.
- **Photos that look like the team actually exists.** Real portraits in the polaroid
  treatment, real product screenshots in case-study slides, real client logos in the
  trust strip. If you can't trace a photo to a real person/product/client, don't ship
  it.
- **Comments in copy that earn their place.** A footnote on a number is good
  («¹ замер на потребительской GPU 4090, 1024×1024»); a footnote on a name is bad
  («¹ leading enterprise client»).

If a reviewer can identify three of these in a generated artifact, it's probably ours.
