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
4. **Update page numbers** — `<span class="pn">NN / TT</span>`. Counted manually; if you add
   or remove slides, fix every slide's `pn`.
5. **Add images** to a sibling `images/` folder if you need demo screenshots, before/after
   pairs, etc. Reference as `<img src="images/foo.png">`.
6. **Print → Save as PDF** — that's the deliverable. The print CSS in this file locks
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
- 5 pill variants: `dark`, `light`, `outline`, `soft`, `deep`.
- 3 card variants: default (ink), `featured` (white), `outline`.
- 5 type sizes: `h-hero`, `h-xl`, `h-lg`, `h-md`, `h-sm`, plus `lead`, `body`, `meta`.
- Brand mark + wordmark top-left every slide; tracked uppercase page number bottom-right.

## When to use this vs Figma

| Use HTML template | Use Figma КПшки file |
|-------------------|----------------------|
| Fast turnaround (< 1 day to send) | Visual-heavy, custom illustrations |
| Engineer-led pitches | Designer-led pitches |
| Tech/quote-driven content | Photo-driven content (team intro, polaroids) |
| You want a live URL to send | You want a clean PDF only |
| You want clients to navigate themselves | One-shot send-and-forget |

Both are valid. Both inherit from [`../../design-system/decks.md`](../../design-system/decks.md).

## Editing rules

- **Don't introduce a second typeface.** Golos only. Weight + size + tracking do the work.
- **Don't add new color tokens** without updating `decks.md` and `identity/colors.md`.
- **Don't replace the croissant logo** with a re-drawn version. Use the inline SVG already
  in the file.
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
18-slide structure and start in Figma instead.
