# Pre-commit checklists

Copy these into your TodoWrite when finishing UI / content work.

## UI checklist

### Anti-slop pre-flight (before you start)
- [ ] Read [`anti-ai-slop.md`](anti-ai-slop.md) once. All P0 cardinal sins are non-negotiable — fix them before declaring done. The "good tells" companion section at the bottom is what to grade toward.

### Visual
- [ ] Tokens only — no `bg-[#...]`, no `text-gray-*`/`text-zinc-*` for body
- [ ] No Tailwind indigo (`#6366f1` etc.) anywhere — use `--brand-primary`
- [ ] No two-stop "trust" gradients on hero — flat surfaces
- [ ] Heading hierarchy intact (one H1, no skip-levels)
- [ ] Icons are Lucide SVG, not emoji
- [ ] No drop-shadows on cards (polaroids are the only exception)
- [ ] Animations 150–300 ms, only `transform` / `opacity`

### Accessibility
- [ ] `aria-label` on icon-only buttons
- [ ] `aria-hidden="true"` on decorative icons
- [ ] External links: `rel="noopener noreferrer" target="_blank"`
- [ ] Every input has `<label htmlFor>` matching its `id`
- [ ] Body text contrast ≥ `text-primary-60`
- [ ] Touch targets ≥ 44×44 px
- [ ] Tab-order works and focus is visible

### Next.js
- [ ] `next/image` (with `width`+`height` or `fill`), never `<img>`
- [ ] `next/link`, never `<a href="/...">`
- [ ] `"use client"` only when hooks/event handlers genuinely require it
- [ ] New page → `app/<route>/page.tsx` + `metadata` + `alternates.canonical`

### SEO / content
- [ ] Numbers and names from `lib/seo/facts.ts`, not inlined
- [ ] New page added to `app/sitemap.ts`
- [ ] Meta description 140–160 chars, ≥3 GEO signals
- [ ] If structural → matching JSON-LD schema in `components/seo/schemas/`
- [ ] If important → mentioned in `public/llms.txt`

### Code
- [ ] `pnpm lint` — passes
- [ ] `pnpm typecheck` — passes
- [ ] `pnpm test` — passes
- [ ] `pnpm build` — passes

---

## Copy checklist

- [ ] Russian by default (unless audience is explicitly English)
- [ ] No corporate hedging — concrete numbers, named clients
- [ ] **No invented metrics.** Every number traces to `facts.md` or a real engagement
- [ ] **No Latin quotes** in Russian copy — «…», not "…"
- [ ] **Em-dashes** (`—`) where parenthetical, not hyphens with spaces
- [ ] **Non-breaking spaces** before short Russian prepositions: `с&nbsp;ИИ`, `за&nbsp;2-4&nbsp;недели`
- [ ] CTAs match our library («Написать нам», «Создать бриф», not «Оставить заявку»)
- [ ] No «заказчик / исполнитель» framing in КП copy
- [ ] No emoji as icons
- [ ] No filler («Тут будет описание», "lorem ipsum", "Feature one/two/three")
- [ ] No keyword repetition (hurts GEO)
- [ ] Technical terms used where they belong (`ИИ-агент`, `RAG`, `LLM`)

---

## Pre-deploy / pre-PR

- [ ] Lighthouse: Performance, Accessibility, SEO ≥ 95 (Accessibility = 100)
- [ ] Test on real mobile (touch, orientation, zoom to 200%)
- [ ] Check `/sitemap.xml`, `/robots.txt`, `/llms.txt` in production build
- [ ] Open the OG image — looks right, fonts loaded
- [ ] All client logos render (SVG paths correct, fallback `alt`)
- [ ] Forms submit successfully end-to-end
