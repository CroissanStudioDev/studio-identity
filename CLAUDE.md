# CLAUDE.md (this repo)

This is `studio-identity` — the **context repo** for Круассан Студио. Docs and assets only, no code.

## What lives here

- Brand voice, messaging, company facts (`brand/`)
- Visual identity: logo, colors, typography, iconography (`identity/`, `assets/`)
- Design system: tokens, components, sections, animations, a11y (`design-system/`)
- Tech stack defaults, Next.js patterns, code standards, SEO/GEO (`tech/`)
- Hard rules and pre-commit checklists for AI agents (`agents/`)

## Working in this repo

- Never run `pnpm install` here. There is no `package.json` and that's intentional.
- Edit Markdown freely. Keep docs **short and scannable** — tables beat paragraphs.
- The live reference is `~/Dev/croissan-landing`. When a doc disagrees with that codebase, the
  codebase wins; update the doc.
- Don't add aspirational content. Only document what we actually do today.

## When you're working in another studio project

Read [`agents/CLAUDE.md`](agents/CLAUDE.md) — that's the file meant to be referenced from project
roots.

## Asset rules

- Keep binary assets (`assets/`) committed. They are the brand.
- Optimize SVGs by hand if needed but don't run a destructive optimizer that changes path data.
- New client logos go into `assets/client-logos/` as SVG, named `kebab-case.svg`.

## When you're asked to "update the brand" / "add something new"

1. Confirm the change with the user — voice, colors, components are studio-wide decisions.
2. Update the relevant doc(s) here.
3. If the change requires code in downstream projects (`croissan-landing`, etc.), call that out
   in the same response — but don't silently edit the downstream repo.
