# Design rules — hard

These are the **locked** rules — the ones that, if violated, ship a defect. They protect
the brand and the user (a11y), so they don't bend.

For everything *not* on this list — layout choices, novel slide types, copy patterns,
fresh section ideas — see [`creative-latitude.md`](creative-latitude.md). The studio
**wants** agents to invent freely inside the token system; this file is the perimeter,
not the script.

## Colors

- Use **tokens only**: `bg-brand`, `text-brand-dark`, `text-primary-60`, `text-error`.
  Never `bg-[#2727CA]`, `text-gray-500`, `text-zinc-700`, etc.
- Body text is **never lighter than `text-primary-60`** on the light background. `text-primary-50`
  is for placeholders only.

## Typography

- Exactly **one `<h1>`** per page.
- Heading hierarchy: H1 → H2 → H3 → H4. **No skip-levels.**
- Right Grotesk **only on H1** (and rare brand-mark wordmarks).
- Use `next/font` for everything. No inline `<link>` to Google Fonts.
- Russian text uses non-breaking spaces (`&nbsp;`) before short words.

## Components

- **Find an existing component first.** Don't invent a new card / button / form variant if one
  exists. Live reference: `croissan-landing/components/`.
- Buttons: `h-[44px]` minimum (built into our `<Button>`). Hero buttons use `rounded-[16px] py-7`.
- Cards: `rounded-3xl border border-black/5 bg-white` for the standard card.
- Forms: every input has a `<label htmlFor="id">`. Placeholder-only labels are forbidden.

## Iconography

- **Lucide only.** No emoji, no Heroicons, no Material, no FontAwesome.
- Icon-only buttons need `aria-label`. Decorative icons next to text need `aria-hidden="true"`.
- Sizes: `size-4` (16px) inline, `size-5` (20px) in buttons, `size-6` (24px) standalone.

## Images

- **`next/image` only.** Never `<img>`.
- Always set `alt`. Decorative duplicates use `alt=""` + `aria-hidden="true"`.
- Photo content is **WebP**. JPEG/PNG only when a tool requires it.

## Links

- Internal: `<Link>` from `next/link`. Never `<a href="/...">`.
- External: `rel="noopener noreferrer" target="_blank"`. No exceptions.

## Motion

- Animate **only `transform` and `opacity`**.
- Duration **150–300 ms** for micro-interactions.
- `prefers-reduced-motion` is global. Don't override.

## Accessibility floor

- WCAG **AA**. Minimum contrast 4.5:1 for body, 3:1 for large.
- Touch targets ≥ 44×44 px.
- Every interactive element reachable by keyboard with a visible focus state.

## What this means for AI agents

If you're about to write something that violates one of these rules, **stop and ask the user**.
Don't ship a workaround. The cost of asking is one round-trip; the cost of brand drift is much higher.

## What this *doesn't* mean

This file does not say "match every example in the repo verbatim." Most of design is
the gray area in between these locked rules — section composition, novel layouts, fresh
copy. That's [`creative-latitude.md`](creative-latitude.md)'s territory. Read it.
