# Default tech stack

When starting a new studio project, default to this stack. Deviate only when there's a real
constraint (existing client codebase, special runtime, etc.) — and document why.

## Core

| Layer | Choice | Notes |
|-------|--------|-------|
| Framework | **Next.js 16** (App Router) | `cacheComponents: true`, `reactCompiler: true`, Turbopack |
| Language | **TypeScript 5.9+** | `strict: true`, no `any` without comment |
| UI | **React 19** | Server Components by default |
| Styling | **Tailwind CSS 4** | `@theme inline` tokens, no `tailwind.config.js` |
| Components | **shadcn/ui** (new-york, baseColor zinc) | Customized with our tokens |
| Icons | **Lucide** (`lucide-react`) | Locked in `components.json` |
| Forms | **react-hook-form** + **Zod** + `@hookform/resolvers` | |
| Animations | **motion** (motion.dev) | Successor to framer-motion |
| Package manager | **pnpm** (≥10) | `packageManager` field pinned in `package.json` |
| Linter / formatter | **Ultracite** (Biome 2.x) | `pnpm format` before commits |
| Testing | **Vitest** + **Playwright** | unit + e2e |

## AI

| Use case | Default |
|----------|---------|
| Multi-model routing | OpenRouter |
| Default text model | `google/gemini-2.5-flash` for cost-efficient generation |
| Premium reasoning | `anthropic/claude-sonnet-4-6` or newer |
| Voice transcription | OpenAI Whisper (`whisper-1`) |
| Embeddings | OpenAI `text-embedding-3-small` (default), `-large` for accuracy-critical |

When building Anthropic-API apps directly, **enable prompt caching** — see the `claude-api` skill.

## Hosting & ops

- **Docker** for portable deploy (Dockerfile + healthcheck route at `/api/health`).
- Cloudflare or Vercel — pick based on client constraints.
- Always set `NEXT_PUBLIC_SITE_URL` so absolute URLs in metadata are correct in every environment.

## Environment variables

Standard names — keep them consistent across projects:

```
OPENROUTER_API_KEY      # AI generation
OPENAI_API_KEY          # Whisper, embeddings
NEXT_PUBLIC_SITE_URL    # https://yourproject.ru
```

Secrets never go in client-side code. `NEXT_PUBLIC_*` is the only allowed client-readable prefix.

## What we don't reach for by default

| Avoid | Why |
|-------|-----|
| Redux / Zustand | React Server Components + URL state cover most cases |
| GraphQL | REST or Server Actions are simpler |
| CSS-in-JS (styled-components, emotion) | Tailwind covers it |
| ESLint / Prettier | Ultracite (Biome) replaces both |
| `tailwind.config.js` | Tailwind 4 uses `@theme inline` in CSS |
| Heroicons / FontAwesome | Lucide locked in |
| `useState` for derived values | React Compiler memoizes — use plain expressions |
| Manual `useMemo`/`useCallback` | React Compiler handles it |
