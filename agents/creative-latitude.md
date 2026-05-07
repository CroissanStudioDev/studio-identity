# Creative latitude

This repo is a **strong reference, not a script**. The studio's voice and design system
are encoded here so future work feels coherent — but agents shouldn't *copy* this content,
they should *think within* it.

This doc tells you which decisions are yours to make freely, which are negotiable, and
which are locked.

---

## The three rings

```
  ┌─────────────────────── Locked ────────────────────────┐
  │                                                       │
  │   ┌──────────────── Negotiable ────────────────┐      │
  │   │                                            │      │
  │   │   ┌──────────── Free ────────────┐         │      │
  │   │   │  Layout, copy, slide        │         │      │
  │   │   │  composition, novel         │         │      │
  │   │   │  sections — invent inside   │         │      │
  │   │   │  the token system.          │         │      │
  │   │   └──────────────────────────────┘         │      │
  │   │   Spacing, type-scale tweaks, pill         │      │
  │   │   shape, motion — adjust with cause and    │      │
  │   │   document the deviation.                  │      │
  │   └────────────────────────────────────────────┘      │
  │   Brand colors, typefaces, logo, voice principles,    │
  │   factual metrics, accessibility floor — don't        │
  │   touch without founder approval.                     │
  └───────────────────────────────────────────────────────┘
```

---

## Free — invent freely, no one will object

You **don't** need to ask before:

- **Inventing a new section** the brief calls for that the docs don't cover (e.g.
  "interactive pricing slider", "side-by-side competitor comparison", "live model
  benchmark"). Use the existing tokens, type scale, and pill/card vocabulary inside
  whatever layout fits.
- **Writing fresh headlines and body copy** in the studio voice. The voice docs cover
  *examples*, not the full space. Don't paraphrase the examples — write new ones in the
  same shape.
- **Composing novel slide types** for КП subjects the canonical structure doesn't
  cover (compliance & security, rollout timeline, custom integration diagrams). The five
  slide kinds are the **trunk**, not the whole tree.
- **Creating monoline SVG icons** for technical concepts the brief introduces — stack
  diagrams, architecture sketches, protocol flows. 1.6–1.8 px stroke, `currentColor`,
  Lucide-style.
- **Adjusting copy length** to fit a layout. Better a tight 8-word headline that wraps
  cleanly than a 12-word one that breaks the slide.
- **Re-using a component out of context** — pulling the polaroid card pattern from the
  team-intro slide into a "press mentions" web section, or the metric-chip from
  case-study slides into the marketing site. The components are reusable.
- **Choosing whether 11 or 18 slides** fits the КП. Read [`brand/proposal-structure.md`](../brand/proposal-structure.md)
  for the criteria, then pick.

If your output is recognizably ours but doesn't appear in any single doc here, you
probably did the right thing.

---

## Negotiable — adjust with cause, document the deviation

You **may** deviate, but leave a one-line comment or PR note explaining why:

- **Tweaking spacing** (e.g., `py-20` instead of `py-16` on a section that needs it).
  Note: "this section has a tall hero asset, default `py-16` cropped it."
- **Adding a sixth pill variant** for a one-off use case. Note: "client logos pill —
  needed transparent border because logos already include their own backgrounds."
- **Substituting Inter for Golos Text** on a compliance/legal slide where rendering
  needs to survive untrusted environments (e.g., emailed without fonts). Note: "fallback
  for email-rendered preview."
- **Animating a section** with motion-library that goes beyond the 150–300 ms guideline
  (e.g., a slow ambient hero animation). Note: "ambient — no user input, runs once."
- **Skipping the team-intro slide** in a КП when the deal-owner already met the client.
  Note: "client met founders Q2 — skipping intro avoids redundancy."

If you can't articulate the cause in one line, the deviation isn't justified. Default
back.

---

## Locked — don't touch without founder approval

These are part of the brand. Changing them mid-project breaks recognition across
artifacts.

- **Brand colors.** Cobalt `#2727CA`, brand-dark `#150E47`, ink `#0E0E14`, paper white,
  graphite `#252527`, the chart oklch palette, error red. No new hues. No off-brand
  accents.
- **Typefaces.** Right Grotesk (web H1), Golos Text (everything else), Geist Mono (code),
  Noto Sans (server-rendered fallback). No fourth typeface.
- **Logo.** The mark, the wordmark, the three approved background tiles, the lockup
  conventions. Don't redraw, don't recolor, don't re-pair.
- **Voice principles.** Caring + smart + slightly bold. Partner-not-vendor framing.
  Concrete numbers over fuzzy adjectives. Russian-default. The principles are locked;
  the *examples* are illustrations only.
- **Factual metrics.** `15+`, `3+`, named clients (МТС, Ростелеком, Яндекс, T1, …),
  founder names, contact info. From [`brand/facts.md`](../brand/facts.md), nowhere else.
  If you need a number that's not there, **ask the user**, don't invent.
- **Accessibility floor.** WCAG AA, touch targets ≥ 44×44 px, `prefers-reduced-motion`
  respected, keyboard reachable, real labels on inputs.
- **The "Don't" list in [`design-rules.md`](design-rules.md).** Tailwind indigo, two-stop
  trust gradients, emoji as icons, stock photography, mid-grey backgrounds — these are
  marker-pen rules, not guidelines.

---

## When the docs disagree with each other

It happens. The docs were written across multiple sessions and code has shipped between
them. Reconcile in this order:

1. The **live code** in `~/Dev/croissan-landing` (web) and the **live deck masters** in
   the КПшки Figma file (slides) win over any spec document in this repo.
2. Among spec documents: the file closest to your task wins. Slide work? `decks.md`.
   Web component? `components.md`. Voice? `voice-and-tone.md`.
3. If still ambiguous: ask the user. Don't pick the rule that lets you ship — pick the
   one that's most likely to be right, and surface the conflict.

---

## When the docs are silent

The docs are silent on most of what you'll be asked to do — that's fine. Silence isn't
permission to invent broadly; it's permission to invent **inside the system**. The
test:

> If a teammate looked at your output without context, would they recognize it as ours?

If yes, you got the latitude right. If they'd ask "is this from a different studio?",
you went too far.

---

## Notes for specific agent types

**Code-generating agents (Cursor / Copilot / Claude Code in IDE)**: lean toward
matching live code. The codebase wins.

**Design-generating agents (open-design / Figma agent)**: lean toward matching the
DESIGN.md spec. It's the integration contract.

**Copy-generating agents**: lean toward matching the voice docs. Don't try to derive
voice from the visual system — they're separate contracts.

**Slide-generating agents**: read `decks.md` and `proposal-structure.md` together. They
cover the trunk. The branches are yours.
