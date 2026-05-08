# Круассан Студио — Identity & Design System

Single source of truth for everything that defines **Круассан Студио** as a brand and as a product team:
brand voice, visual identity, design system, code conventions, SEO playbooks, and agent guidelines.

This repo is meant to be **read** — by humans starting a new project, and by AI agents (Claude, Cursor,
Copilot, custom subagents) that need durable context about how we work.

> Primary live references:
> - **Code**: `~/Dev/croissan-landing` — when this repo and the codebase disagree, **the code is right**. Update this repo to match.
> - **Visual brand**: internal Figma `Branding` file — logo lockups, wordmark, color tiles.
> - **Sales decks**: internal Figma `Studio Sales` master.
> - **Client proposals (КП)**: internal Figma `КПшки` file (page «Самая Новая» is the canonical template).
>
> Figma file URLs are intentionally not committed — those files are private to the studio. Ask a founder for access if you need it.

---

## Use this in another workspace (3 ways)

### 1. Just paste a URL (zero install)

The single-file context summary lives at:

> https://raw.githubusercontent.com/CroissanStudioDev/studio-identity/main/SUMMARY.md

In Cursor, Claude.ai, ChatGPT, Windsurf, Continue — paste that URL into the chat (or
attach it as context). [`SUMMARY.md`](SUMMARY.md) is ~250 lines and self-contained —
it's the 20% of the brand that delivers 80% of the value (color tokens, type scale,
voice principles, top do/don'ts, anti-slop pre-flight). No clone, no install.

### 2. Install as a Claude Code skill (one line)

```bash
curl -sL https://raw.githubusercontent.com/CroissanStudioDev/studio-identity/main/bin/install | bash
```

This:
- Clones (or updates) the repo at `~/.croissan/identity`
- Symlinks the skill to `~/.claude/skills/croissan-identity`
- Auto-detects [`open-design`](https://github.com/nexu-io/open-design) at common paths
  and links the integration in too

After install, **every project** on the machine has access. Claude Code activates the
skill when the user mentions Croissan, the studio, or asks for KP / commercial-proposal
output.

To update later: re-run the same one-liner. To re-sync just the open-design integration
after editing the brand:
`bash ~/.croissan/identity/bin/sync-opendesign`. To uninstall:
`bash ~/.croissan/identity/bin/uninstall` (add `--purge` to also remove the cloned repo).

### 3. Clone the full repo

For editing the brand itself, or for projects that need the actual binary assets
(logo SVGs, font files, deck-template HTML):

```bash
git clone https://github.com/CroissanStudioDev/studio-identity ~/Dev/studio-identity
```

Then point your project's `CLAUDE.md` / `.cursorrules` at the cloned path.

---

## How to use this repo

### Starting a new project
1. Read [`SUMMARY.md`](SUMMARY.md) and [`brand/voice-and-tone.md`](brand/voice-and-tone.md)
   to set the mood.
2. Copy [`design-system/design-tokens.css`](design-system/design-tokens.css) into your `globals.css`.
3. Copy logo assets from [`assets/logos/`](assets/logos) and fonts from [`assets/fonts/`](assets/fonts).
4. Drop [`agents/CLAUDE.md`](agents/CLAUDE.md) into the new project root (or extend the existing one).
5. Default to the stack in [`tech/stack.md`](tech/stack.md) unless there's a real reason not to.

### Working inside an existing studio project
1. Make sure the project's `CLAUDE.md` references back to this repo.
2. When you're unsure about a decision (color, copy, naming, structure), grep here first.
3. If you ship something new and good, **back-port the pattern** to the relevant doc here.

### As an AI agent
Read [`agents/README.md`](agents/README.md) first. It tells you which files to load up-front, which
rules are hard, and how to reconcile this repo with the project you're working in.

---

## Repo map

```
SUMMARY.md         — single-file self-contained brand context (paste-into-any-chat)
brand/             — voice, tone, messaging, company facts, sub-brands, proposal structure
identity/          — logo, colors, typography, iconography
design-system/     — tokens, components, sections, decks, animations, a11y
tech/              — default stack, Next.js patterns, code standards, SEO/GEO
agents/            — rules, checklists, and the creative-latitude principle
assets/            — logos, client logos, fonts, deck-template (single-file HTML deck)
skills/            — Claude Code skill (croissan-identity) — symlinked into ~/.claude/skills/
integrations/      — plug-in artifacts for external tools (open-design skill registry)
bin/               — install / uninstall scripts for the curl one-liner
```

### How to think about it

There are three concentric rings:
- **Locked** — brand colors, typefaces, logo, voice principles, factual metrics, accessibility.
  See [`agents/design-rules.md`](agents/design-rules.md) and [`agents/content-rules.md`](agents/content-rules.md).
- **Negotiable** — spacing, motion durations, novel pill variants, slight type-scale tweaks.
  Adjust with cause; document the deviation.
- **Free** — section layouts, copy, slide compositions, novel section types not in the docs.
  Invent freely inside the token system.

This is documented top-to-bottom in [`agents/creative-latitude.md`](agents/creative-latitude.md).
Read that **first** if you're an AI agent. It's the lens for everything else here.

Also read [`agents/anti-ai-slop.md`](agents/anti-ai-slop.md) **before generating** —
concrete LLM defaults the studio explicitly rejects (Tailwind indigo, two-stop trust
gradients, emoji as icons, invented metrics, Latin quotes in Russian copy, etc.). The 7
generic + 8 Croissan-specific cardinal sins are P0 — fix them before declaring done, no
exceptions.

---

## What we are

- **Круассан Студио** — full-cycle AI product studio based in Innopolis, Russia.
- Founded **2022**. Around 10 people, 5 founders, 15+ shipped projects.
- We embed AI into existing products and ship new ones from scratch in 2–4 weeks.
- Clients include МТС, Ростелеком, Яндекс, T1, Positive Technologies.
- Core message: **«Зовите нас, когда нужен продукт с ИИ»**.

Full company facts live in [`brand/facts.md`](brand/facts.md).

---

## Maintaining this repo

- This is a **context repo**, not a published library. No CI, no versioning beyond git.
- When you change a token or brand decision, update both this repo and any downstream project.
- Don't add aspirational content — only document what we actually do. If a rule isn't followed
  in `croissan-landing`, it isn't a rule.
- Keep docs short. A scannable table beats a paragraph.
