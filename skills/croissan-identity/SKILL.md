---
name: croissan-identity
description: |
  Loads Croissan Studio brand context — voice, color tokens, type scale, pill/card
  vocabulary, anti-slop rules, КП deck structure. Activate whenever the user mentions
  Croissan Studio, Круассан Студио, the studio brand, or any Croissan-flavored output
  (marketing copy, KP/commercial-proposal decks, AI-product landing pages, brand-styled
  components). Also activates implicitly when the user is editing in a project with
  `--brand-primary: #2727CA`, the Croissan logo SVG, or the studio-identity repo
  somewhere in the workspace tree.
triggers:
  - "croissan"
  - "круассан"
  - "studio brand"
  - "studio-identity"
  - "croissanstudio"
  - "kp deck"
  - "кп"
  - "коммерческое предложение"
allowed-tools:
  - Read
  - Glob
  - Grep
---

# Croissan Studio identity

Loads the studio's brand and design system into context so any generated output —
copy, components, slides, decks, marketing pages — looks and reads like Croissan
Studio.

This skill is a **context loader**, not a task runner. It points you at the right
files; you do the work. Exception: КП-deck generation has a sibling task skill at
[`integrations/open-design/skills/croissan-kp/`](../../integrations/open-design/skills/croissan-kp/)
when running inside open-design.

## Resource map

When this skill activates, the studio-identity repo is mounted at the skill root. The
canonical layout:

```
.                                           ← studio-identity repo root
├── SUMMARY.md                              ← READ FIRST: the 20% that gives 80%
├── README.md                               ← repo overview + how to use this skill
├── brand/
│   ├── voice-and-tone.md                   ← examples + voice principles
│   ├── messaging.md                        ← reusable headline/CTA/proof patterns
│   ├── facts.md                            ← single source of truth for numbers / names / contacts
│   ├── sub-brands.md                       ← Studio vs Community
│   └── proposal-structure.md               ← КП narrative (11-slide compact + 18-slide canonical)
├── identity/
│   ├── colors.md                           ← full palette
│   ├── typography.md                       ← fonts + type scale (web + slides)
│   ├── iconography.md                      ← Lucide rules
│   └── logo/
│       └── usage.md                        ← lockup, sizing, surfaces
├── design-system/
│   ├── design-tokens.css                   ← drop-in CSS (Tailwind 4 / shadcn)
│   ├── components.md                       ← buttons, cards, badges, links, forms
│   ├── sections-and-layout.md              ← section skeleton, hero, page structure
│   ├── responsive.md                       ← breakpoints, mobile-first
│   ├── animations.md                       ← motion guidelines
│   ├── accessibility.md                    ← WCAG-AA floor + 9 a11y rules
│   └── decks.md                            ← FULL slide visual spec (1280×720, type, components)
├── tech/
│   ├── stack.md                            ← Next 16 / React 19 / Tailwind 4 defaults
│   ├── nextjs-patterns.md                  ← App Router patterns
│   ├── code-standards.md                   ← Ultracite, conventions
│   └── seo-geo.md                          ← SEO + GEO playbook
├── agents/
│   ├── creative-latitude.md                ← READ EARLY: locked / negotiable / free rings
│   ├── anti-ai-slop.md                     ← READ BEFORE GENERATING: 15 cardinal sins
│   ├── design-rules.md                     ← locked visual rules
│   ├── content-rules.md                    ← locked copy rules
│   └── checklists.md                       ← pre-commit checklists
└── assets/
    ├── logos/                              ← Croissan logo SVG (default + white)
    ├── client-logos/                       ← МТС, Яндекс, T1, Ростелеком, …
    ├── fonts/                              ← Right Grotesk + Golos Text + Inter + Geist Mono + Noto Sans
    ├── deck-template/                      ← single-file 11-slide HTML КП template
    └── open-design/                        ← (under integrations/) plug-in artifacts for nexu-io/open-design
```

## Activation workflow

When this skill activates, do this **in order**:

### Step 0 — Always read

1. **`SUMMARY.md`** — the single-file overview. Reading this alone gets you 80% of the
   way to brand-correct output for almost any task.
2. **`agents/creative-latitude.md`** — the three rings (locked / negotiable / free).
   Critical for understanding which decisions are yours vs. which need the user's OK.
3. **`agents/anti-ai-slop.md`** — the 15 cardinal sins. Read before generating, not
   after.

These three files together are ~1500 lines of context — small enough to fit anywhere.

### Step 1 — Read what's task-specific

Match the task to deeper docs:

| Task | Read these (in order) |
|------|-----------------------|
| Marketing copy / web copy | `brand/voice-and-tone.md`, `brand/messaging.md`, `brand/facts.md` |
| Marketing site / app component | `identity/colors.md`, `identity/typography.md`, `design-system/components.md`, `design-system/design-tokens.css` |
| Section / page layout | `design-system/sections-and-layout.md`, `design-system/responsive.md` |
| КП / pitch deck (visual) | `design-system/decks.md`, `identity/logo/usage.md` |
| КП / pitch deck (narrative) | `brand/proposal-structure.md`, `brand/voice-and-tone.md` |
| HTML deck (no Figma) | `assets/deck-template/index.html`, `assets/deck-template/README.md` |
| SEO / metadata | `tech/seo-geo.md`, `brand/facts.md` |
| Accessibility audit | `design-system/accessibility.md`, `agents/checklists.md` |

### Step 2 — Pull facts, never invent

Numbers, names, addresses, founder handles → from `brand/facts.md`. Do not inline these
in components — projects should mirror the pattern from `croissan-landing/lib/seo/facts.ts`
(import once, reference everywhere).

If a brief asks for a number that isn't in `facts.md`, ask the user — don't guess.
Inventing metrics is one of the cardinal sins in `anti-ai-slop.md`.

### Step 3 — Generate, then run anti-slop pre-commit

Before declaring done, walk through `agents/checklists.md`. The "Anti-slop pre-flight"
section is short and catches almost every regression. Specifically check:

- All accent colors are `--brand-primary` (`#2727CA`), no Tailwind indigo.
- No two-stop "trust" gradients on hero.
- No emoji as feature icons (Lucide SVG only; the typographic `🤍` on contact is the
  one exception).
- Russian copy uses «…» quotes, em-dashes (`—`), and `&nbsp;` before short prepositions.
- No invented metrics; everything traces to `facts.md` or a real engagement.
- No `lorem ipsum` / "Feature one/two/three" filler.

## Voice

The studio voice in one sentence: **caring, smart, slightly bold — partner not vendor,
concrete numbers over fuzzy adjectives, Russian-default**.

Headlines lean direct with a soft imperative («Зовите нас, …»). CTAs are dialogic
(«Написать нам», not «Оставить заявку»). Body uses em-dashes for flow. Avoid
corporate hedging («профессиональный», «комплексный», «инновационный»).

## Latitude

This is a **strong reference, not a strict template**. Three rings:

- **Locked** — brand colors, typefaces, logo, voice principles, factual metrics, a11y.
  Don't touch without founder approval.
- **Negotiable** — spacing, motion, novel pill variants. Adjust with one-line cause
  noted.
- **Free** — section layouts, copy, slide compositions, novel section types not in
  docs. Invent freely **inside the token system**.

Full treatment: `agents/creative-latitude.md`.

## Caveat — what this skill does NOT do

- Doesn't write code for you. Read the docs, then generate.
- Doesn't replace your judgment on creative latitude. The brand is a strong reference,
  not a script.
- Doesn't auto-load fonts or assets into a project. If a project needs the actual
  binaries (logo SVGs, font files), copy them from `assets/`.

## When to use a sibling skill instead

- Generating a КП inside open-design's UI → `integrations/open-design/skills/croissan-kp/`
  (a task skill that *runs* the КП generation, including the deck template seed).

This skill (`croissan-identity`) is the universal context loader. The open-design skill
is a specific task runner.
