# CLAUDE.md — Круассан Студио identity context

You are working on a project for **Круассан Студио** (Croissan Studio), an AI product studio.
This file points you at the studio's identity and design context. Drop a copy of this file (or
a reference to it) at the root of any new studio project.

## What is this?

The full studio identity, design system, brand voice, and engineering defaults live at
`~/Dev/studio-identity/`. Treat that repo as the upstream default. The current project's own
`CLAUDE.md` overrides it when they conflict — but flag the drift so we can decide which one is
right.

## Read these files before starting non-trivial work

| When | Read |
|------|------|
| **Before any task** | [`agents/creative-latitude.md`](../agents/creative-latitude.md) — what's yours to invent vs. what's locked |
| **Before generating** | [`agents/anti-ai-slop.md`](../agents/anti-ai-slop.md) — LLM defaults we explicitly reject (indigo, gradients, emoji icons, invented metrics, Latin quotes in Russian, …) |
| Any UI work | [`agents/design-rules.md`](../agents/design-rules.md), [`identity/colors.md`](../identity/colors.md), [`design-system/components.md`](../design-system/components.md) |
| Any copy work | [`agents/content-rules.md`](../agents/content-rules.md), [`brand/voice-and-tone.md`](../brand/voice-and-tone.md) |
| Pitch deck / КП visual / slide layout | [`design-system/decks.md`](../design-system/decks.md), [`identity/logo/usage.md`](../identity/logo/usage.md) |
| КП narrative — what slides, in what order | [`brand/proposal-structure.md`](../brand/proposal-structure.md) |
| Building an HTML deck (no Figma) | [`assets/deck-template/`](../assets/deck-template/) — copy `index.html`, fill `{{placeholders}}`, print-to-PDF |
| Working inside open-design (or via the open-design skill registry) | [`integrations/open-design/`](../integrations/open-design/) — `croissan-kp` skill + Croissan DESIGN.md + deck template |
| Brand-mark / logo / wordmark work | [`identity/logo/usage.md`](../identity/logo/usage.md), [`brand/sub-brands.md`](../brand/sub-brands.md) |
| New project bootstrap | [`tech/stack.md`](../tech/stack.md), [`tech/nextjs-patterns.md`](../tech/nextjs-patterns.md) |
| SEO / metadata work | [`tech/seo-geo.md`](../tech/seo-geo.md), [`brand/facts.md`](../brand/facts.md) |
| Before reporting work as done | [`agents/checklists.md`](../agents/checklists.md) |

## Hard rules summary (full list in `agents/design-rules.md` + `agents/content-rules.md`)

- Tokens only — no raw hex, no `text-gray-*`.
- One `<h1>`, no skip-levels, Right Grotesk only on H1.
- Lucide icons only. No emoji as icons.
- `next/image` and `next/link` only.
- External links: `rel="noopener noreferrer" target="_blank"`.
- Forms: real `<label htmlFor>` for every input.
- Russian by default. Voice: caring, smart, slightly bold. Partner, not vendor.
- Numbers and names from `facts.ts` — never inlined.
- No emoji in copy. No corporate hedging.
- WCAG AA floor; touch targets ≥ 44×44 px.

## Stack defaults

Next.js 16 (App Router), React 19, TypeScript, Tailwind 4, shadcn/ui, Lucide, motion, react-hook-form,
Zod, Vitest, Playwright, Ultracite (Biome). Package manager: **pnpm**. Full details:
[`tech/stack.md`](../tech/stack.md).

## When live code disagrees with a doc

`~/Dev/croissan-landing` is the live reference codebase. If a snippet here looks outdated, **the
live code wins**. Update the doc as part of your task.

## Don't

- Don't run `pnpm install` in `~/Dev/studio-identity/` — it's docs and assets only, no package.json.
- Don't invent new design primitives if a similar one exists. Find and copy.
- Don't add aspirational rules to the identity repo — only document what we actually do.
- Don't push, force-push, or merge without explicit user permission.
