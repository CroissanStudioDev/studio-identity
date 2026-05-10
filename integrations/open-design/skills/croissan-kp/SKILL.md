---
name: croissan-kp
description: |
  Single-file horizontal-swipe HTML commercial proposal (КП) for Croissan
  Studio. Built by copying the seed `assets/croissan-deck.html` (which
  carries the proven deck-framework nav script) and filling in the
  11-slide narrative from `references/proposal-structure.md`. Use when
  the brief is a Croissan Studio client proposal (КП), pitch deck for an
  AI product engagement, or scope-tight commercial offer in Russian.
triggers:
  - "кп"
  - "коммерческое предложение"
  - "croissan"
  - "круассан"
  - "deck for croissan"
  - "pitch deck"
  - "ai studio proposal"
od:
  mode: deck
  scenario: product
  preview:
    type: html
    entry: index.html
  design_system:
    requires: true
    sections: [color, typography, layout, components]
    prefer: croissan
---

# Croissan КП Skill

Produce a single-file horizontal-swipe HTML commercial proposal for a Croissan Studio
client engagement. Tech-led, scope-tight, 11 slides by default.

## Resource map

```
croissan-kp/
├── SKILL.md                            ← you're reading this
├── assets/
│   └── croissan-deck.html              ← seed: tokens + slide primitives + deck-framework runtime (READ FIRST)
└── references/
    ├── DESIGN.md                       ← full Croissan design system (the 9-section spec)
    ├── proposal-structure.md           ← 11-slide narrative + canonical 18-slide alternative
    ├── voice-and-tone.md               ← examples + voice principles
    ├── facts.md                        ← single source of truth for numbers / names / contacts
    ├── creative-latitude.md            ← what to invent, what not to invent
    └── anti-ai-slop.md                 ← LLM defaults we explicitly reject (read BEFORE generating)
```

> **Note on packaging.** This SKILL.md sits in the studio's **open-design
> integration mirror**. To install: `cp -r integrations/open-design/skills/croissan-kp/
> <open-design-root>/skills/`, plus `cp integrations/open-design/templates/croissan-deck.html
> <open-design-root>/templates/`, plus `cp -r integrations/open-design/design-systems/croissan/
> <open-design-root>/design-systems/`. See [`../../README.md`](../../README.md).

## Workflow

### Step 0 — Pre-flight

1. **Read `assets/croissan-deck.html` end-to-end** — both the framework `<style>` block
   and the runtime `<script>` block. The script solves five iframe-nav bugs (real scroller
   detection, dual capture-phase listeners, auto-focus, `--deck-scale` math, position
   persistence) — do not rewrite it.
2. **Read `references/DESIGN.md`** — especially section 4 (component stylings),
   section 7 (do's and don'ts), and section 9 (agent prompt guide).
3. **Read `references/proposal-structure.md`** — pick **11-slide compact** unless the
   brief explicitly asks for the full 18-slide canonical structure.
4. **Read `references/facts.md`** — pull every studio-level number/name from here.
   Never invent metrics about Croissan itself.
5. **Read `references/creative-latitude.md`** — know which decisions are yours to make
   freely vs which require asking.
6. **Read `references/anti-ai-slop.md`** — the LLM patterns we will reject on review.
   All P0 cardinal sins are non-negotiable; treat them as hard rules even though that
   file isn't framed as one. The "good tells" section at the bottom is what to grade
   toward.

### Step 1 — Copy the seed

Copy `assets/croissan-deck.html` to the project root as `index.html`. The seed already
embeds the Croissan token block (`--croissan-blue`, `--graphite`, `--paper-dim`, etc.) and the
three-pill / two-card vocabulary; do not redefine these.

### Step 2 — Decide the narrative shape BEFORE writing any slide

The seed ships an **11-slide compact** structure. Override only with cause:

| Brief signal | Use |
|--------------|-----|
| Client we already know · scope-tight · tech-led · single deal-owner | **11 slides (compact)** — the seed default |
| First КП · big contract · multi-case · big-B2B/госструктура | **18 slides (canonical)** — see proposal-structure.md and add: deep team intro, 3 case slides, process detail, brief-mirror, scope, packages |

If you switch to 18 slides, **don't** delete the existing 11 — duplicate the file and edit
the second copy.

### Step 3 — Fill the slides in pass-by-pass order

**Pass 1: cover + offer (slides 1, 4)**. Get the studio identity and the proposal title
locked in first — those are what gets quoted in the email body.

**Pass 2: cases (slide 2)**. Pick **two** shipped projects from the studio's portfolio
that are *similar in shape* to the client's brief. Not the most recent, not the most
prestigious — the most analogous. Pull metrics from real engagement data; if you
don't have it, place a clearly-labelled `{{TODO: real metric}}` and surface it in your
hand-off.

**Pass 3: scope (slides 3, 5, 6, 7, 8)**. This is where the offer takes shape:
- Slide 3 (one-stop shop): use the six-pill list verbatim from the seed unless the brief
  is for an unusual service mix.
- Slide 5 (what it does): the brief's product, **mirrored back** in our voice — see
  `references/proposal-structure.md` "Зеркало клиента."
- Slide 6 (demo): four real screenshots if a prototype exists; else four wireframes; else
  four placeholder boxes labelled with what they *will* show.
- Slide 7 (tech): research candidates as `pill.dark` chips (real model/library names),
  our optimization layer in a `card` (concrete techniques + numbers).
- Slide 8 (infra): featured card = recommended config; second column = filled `card` on `ink-soft` for minimum tier.

**Pass 4: numbers (slides 9, 10)**. Stage prices first, total second. Pricing must come
from a real engagement template — never invent. If the brief doesn't include a budget
hint, put **clearly-labelled placeholders** (`{{XXX 000 ₽}}`) and stop; ask the user.

**Pass 5: contact (slide 11)**. Single deal-owner — usually CTO or CPO depending on the
project type. Pull from `facts.md` FOUNDERS list.

### Step 4 — Self-review

Run the checklist below before declaring done. Failing any P0 item = ship is not ready.

#### P0 — must-fix
- [ ] **All P0 cardinal sins from `references/anti-ai-slop.md` cleared.** Walk the
  whole P0 section before declaring done — Tailwind indigo, hero gradients, gradient
  text on H1, emoji icons, fake testimonials, invented metrics, filler copy, Latin
  quotes in Russian, missing `&nbsp;`, «заказчик / исполнитель», generic AI-marketing
  phrases, stock photography, mid-grey backgrounds, decorative drop-shadows.
- [ ] No `{{placeholders}}` left anywhere. Search `{{`.
- [ ] No `pill.outline`, `pill.light`, or `card.outline` unless the brief explicitly overrides (default is filled-only).
- [ ] Brand mark + wordmark present on **every slide** (including covers, dividers, totals).
- [ ] All studio-level metrics traceable to `references/facts.md`.
- [ ] Pricing slide totals match the sum of stage prices.

#### P1 — should-fix
- [ ] No more than 3 consecutive slides of the same `slide.<surface>` class. Vary the rhythm.
- [ ] Cases slide (2) shows two projects, not three. The compact deck doesn't have room for three.
- [ ] H1 on case-study slides uses Medium, not Bold. (Slide 5+ if applied.)
- [ ] At least one slide uses `card.featured` to indicate the recommended option.
- [ ] Final price block on totals slide is right-aligned, large (>9.5vw equivalent), tabular.

#### P2 — nice-to-fix
- [ ] Slide 3's six-pill list reflects the actual focus areas relevant to this client.
- [ ] Tech-stack chips on slide 7 are real, public, named libraries — not "Custom AI."
- [ ] Demo grid (slide 6) captions are specific, not generic.

### Step 5 — Hand-off

Print to PDF (Chrome → Print → Save as PDF) for client send. Designer-led КП masters
live in the studio's private design archive and are updated by humans; this HTML deck
is the agent-friendly path.

## Creative latitude

This skill is a **strong reference, not a strict template**. The 11 slide skeletons cover
the trunk of the КП narrative — branches are yours to invent within the design system:

- **New slide types** the brief calls for (e.g., "compliance & security", "analytics
  dashboard preview", "rollout timeline beyond 3 weeks") — invent the layout using the
  pill/card/grid vocabulary already in the seed.
- **Slide ordering** within constraints: Cover always slide 1, CTA always last, pricing
  before contact. Everything in between is yours.
- **Headlines** that fit the voice — caring, smart, slightly bold. Don't paraphrase
  examples; invent fresh ones in the same shape.

What you don't invent: brand colors, typefaces, the logo, the wordmark conventions, or
studio-level metrics. See `references/creative-latitude.md` for the full out-of-scope list.

## Notes on packaging

This skill expects to be installed alongside two siblings:

1. `<open-design-root>/templates/croissan-deck.html` — the seed it copies.
2. `<open-design-root>/design-systems/croissan/DESIGN.md` — referenced as the active
   `od.design_system.prefer`.

Both ship from the same `integrations/open-design/` mirror in the studio-identity repo.
If either is missing, the skill falls back to the open-design `default` design system
and the bare `templates/deck-framework.html` — the deck still renders, but loses the
brand vocabulary.
