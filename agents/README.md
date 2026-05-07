# Guidelines for AI agents

This directory tells AI agents (Claude Code, Cursor, Copilot, custom subagents, ultraplan agents,
GSD agents) how to use the studio-identity repo.

## Read first, in this order

1. [`creative-latitude.md`](creative-latitude.md) — **read this first**. Tells you what's
   yours to invent freely vs. what's locked. The rest of this repo makes more sense with
   this in mind.
2. [`anti-ai-slop.md`](anti-ai-slop.md) — concrete LLM defaults we explicitly reject.
   Read **before generating**, not after. If you skip this and ship something with a
   Tailwind-indigo accent, you'll have to redo it.
3. [`design-rules.md`](design-rules.md) — locked visual rules. Violating these is a defect.
4. [`content-rules.md`](content-rules.md) — locked copy rules. Violating these breaks the brand voice.
5. [`checklists.md`](checklists.md) — pre-commit checklists, copy them into your TodoWrite.
6. [`../brand/facts.md`](../brand/facts.md) — every number and name we ship.
7. The relevant deeper doc when you start a specific task (typography, components, SEO, etc.).

## How to apply this repo to a project

When you join a studio project (any repo under `~/Dev/`):

1. **Look at the project's CLAUDE.md.** That's authoritative for project-specific rules.
2. **Treat this repo as the upstream default.** When the project's CLAUDE.md is silent, fall back here.
3. **When this repo and the project disagree, the project wins** — but flag the drift to the user
   so we can decide whether to update the project or update this repo.
4. **The live code in `croissan-landing` is the ultimate source of truth** for visual patterns.
   If a snippet here looks outdated, read the actual component before copying.

## Specific instructions

### When writing UI

- Find the closest existing component in `croissan-landing/components/` and copy its pattern. Don't
  invent a new one.
- Always use design tokens, never raw hex. See [`../identity/colors.md`](../identity/colors.md).
- Run through the UI checklist in [`checklists.md`](checklists.md) before reporting work as done.

### When writing copy

- Default language: Russian. See [`../brand/voice-and-tone.md`](../brand/voice-and-tone.md).
- Pull numbers, names, and contacts from the project's `lib/seo/facts.ts` — never inline.
- No emojis as icons. Lucide SVG only.

### When picking a stack

- Default to [`../tech/stack.md`](../tech/stack.md). Deviations need a real reason.

### When you find drift

If the live code in `croissan-landing` does something this repo doesn't document, **the live code is
right**. Update the relevant doc here as part of your task. Never silently follow the doc when the
code disagrees.

### When the user adds a new pattern

If a project ships a new reusable pattern (a new card variant, a new section layout, a new type
scale entry), back-port it here once it's stable. Keep this repo a faithful mirror of how we
actually build, not how we'd like to.

## What NOT to do

- Don't copy snippets from generic Tailwind tutorials, shadcn examples, or AI-generated boilerplate.
  We have opinions, and they're encoded here.
- Don't add aspirational rules. Document only what we actually do.
- Don't rewrite this repo to be "more comprehensive" by inventing rules. Brevity is the feature.
- Don't run `pnpm install` in *this* repo. There's no package.json — it's docs and assets only.
