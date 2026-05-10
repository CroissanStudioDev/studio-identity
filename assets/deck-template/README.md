# HTML deck template

Single-file vanilla HTML/CSS/JS template for **commercial proposals (КП)** and short
pitches. No build step, no dependencies beyond Google Fonts (Golos Text).

Fastest path from idea → sendable PDF in ~30 minutes for an 11-slide proposal.

## Files

```
index.html    — the entire deck. Copy, fill in {{placeholders}}, ship.
README.md     — this file
```

That's it. No `package.json`, no `node_modules`, no bundler.

## How to use

1. **Copy** `index.html` into a new project folder (e.g. `deck-<client>-<date>/`).
2. **Open** in a browser to preview live (no server needed — `file://` works).
3. **Replace `{{placeholders}}`** with your content. Search for `{{` to find them all.
4. **Add images** to a sibling `images/` folder if you need demo screenshots, before/after
   pairs, etc. Reference as `<img src="images/foo.png">`.
5. **Print → Save as PDF** — that's the deliverable. The print CSS in this file locks
   each slide to a 1920×1080 page and disables nav UI automatically.

## Controls (live preview)

| Action | Key / gesture |
|--------|---------------|
| Next / prev slide | ← → ↑ ↓ Space PgUp PgDn |
| First / last | Home / End |
| Overview grid | **Esc** |
| Mouse / trackpad | Wheel (vertical or horizontal) |
| Touch | Swipe |
| Jump via URL | `?slide=4` |

Position is saved to localStorage between reloads.

## Visual spec

This template is a **direct implementation** of the visual system in
[`../../design-system/decks.md`](../../design-system/decks.md). If you change
something fundamental here (type scale, color tokens, card variants), update that doc too.

Stack:
- **Golos Text** (Google Fonts) — only typeface; weight + size do all the work.
- CSS tokens: `--croissan-blue` (+ `-deep`, `-soft`) for the brand slide background and pill fills.
- Surface modes: loud Croissan blue for covers/openers/big ideas; graphite for cases,
  product screenshots, and calmer page-like slides; white for dense reading and logo fields.
- Density helpers: default padding for long КП content, `.slide.tight` for editorial
  visual moments, `.slide.card-protected` when tight outer margins need cards to carry
  the reading space.
- **3 pill variants** (filled only): `dark`, `soft`, `deep` — no outline, no white pill on brand slides.
- **2 card variants**: default (ink or ink-soft fill), `featured` (white) — no outline cards.
- Type scale: `h-hero`, `h-xl`, `h-lg`, `h-md`, `h-sm`, plus `lead`, `body`.
- Brand ownership modes: use a large cropped croissant on loud covers, a quiet top-left
  lockup for standalone business slides, or surface/type ownership inside a coherent deck.
  **No slide page numbers** in the layout.

## When to use this vs the designer-led path

| Use HTML template | Use a designer-built master |
|-------------------|-----------------------------|
| Fast turnaround (< 1 day to send) | Visual-heavy, custom illustrations |
| Engineer-led pitches | Designer-led pitches |
| Tech/quote-driven content | Photo-driven content (team intro, polaroids) |
| You want a live URL to send | You want a clean PDF only |
| You want clients to navigate themselves | One-shot send-and-forget |

Both are valid. Both inherit from [`../../design-system/decks.md`](../../design-system/decks.md).
The designer-led masters live in the studio's private design archive — ask a founder.

## Editing rules

- **Don't introduce a second typeface.** Golos only. Weight + size + tracking do the work.
- **Don't add new color tokens** without updating `decks.md` and `identity/colors.md`.
- **Don't replace the croissant logo** with a re-drawn version. Use the inline SVG already
  in the file.
- **Don't use brand blue as wallpaper.** For case studies, product screenshots, and
  page-like slides, start from graphite or white.
- **Don't add JS frameworks.** Vanilla. If you need state, you're in the wrong file —
  use the React/Next setup instead.
- **Don't ship the deck with `{{placeholders}}` still in it.** Search for `{{` before sending.

## Compact 11-slide structure

This template embodies the **compact КП narrative** documented in
[`../../brand/proposal-structure.md`](../../brand/proposal-structure.md).
Use this when:
- The proposal is engineer-led / scope-tight.
- The client has already met us; we're skipping the deep team intro.
- The total contract is small enough that an 18-slide deck would feel heavy.

For longer proposals (deep case studies, multi-team, multi-phase), use the canonical
18-slide structure with a designer-built master from the private archive instead.
