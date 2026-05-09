# Code standards

## Linter / formatter

**Ultracite** (Biome 2.x). One tool, one config, no ESLint, no Prettier.

```bash
pnpm lint        # ultracite check
pnpm format      # ultracite fix
pnpm typecheck   # tsc --noEmit
```

Run `pnpm format` before every commit. Don't bypass hooks (`--no-verify`) without a real reason and
the user's explicit say-so.

## Hard rules

- **No `console.log`** in production paths. Strip them or use a real logger.
- **No `any`** without a one-line comment explaining why. Prefer `unknown` + a narrowing check.
- **No raw hex** in JSX/CSS where a token exists. Use `bg-brand`, `text-primary-60`, etc.
- **`aria-label`** on icon-only buttons; **`aria-hidden="true"`** on decorative icons.
- **`alt`** on every `<Image>`. Use `""` + `aria-hidden` for purely decorative duplicates.
- **External links** carry `rel="noopener noreferrer" target="_blank"`.

## Conventions

- File names: `kebab-case.tsx`, `kebab-case.ts`. Components themselves are `PascalCase`.
- Component files default-export the component, named-export the props type:
  ```tsx
  export type ButtonProps = { … };
  export default function Button(props: ButtonProps) { … }
  ```
- Hooks live in `hooks/` and start with `use-`.
- Generic helpers in `lib/utils.ts`. Domain helpers in `lib/<domain>/`.
- Path alias: `@/` maps to project root. Always import via `@/components/...`, never deep relative
  paths (`../../../`).

## Comments

Default to **no comments**. The code and good names should explain themselves. Only comment when:
- The **why** is non-obvious (workaround for a bug, hidden constraint, unusual ordering).
- A `TODO`/`FIXME` flags real follow-up work — with enough context to act on it later.

Don't write comments that just restate the next line. Don't reference tickets or the current task —
that belongs in PR descriptions and rots quickly.

## Testing

- **Unit / integration**: Vitest. Test files sit next to the code (`foo.test.ts`) or under `__tests__/`.
- **E2E**: Playwright. One spec per user-facing flow.
- Aim for **fast** tests over **many** tests. A slow suite stops getting run.

## Commits

- Use **`pnpm`**, not `npm` / `yarn`. The lockfile says so.
- Conventional-commit-ish prefixes are fine (`feat:`, `fix:`, `chore:`) but not required.
- One concern per commit. Don't bundle a refactor into a feature commit.
- Don't `git push --force` without explicit user permission.

## Performance budget

Pre-ship targets per route on the marketing site. If a PR pushes any of these over,
fix the regression before merging — don't normalize a worse baseline.

| Metric | Target | Hard ceiling |
|--------|--------|--------------|
| Lighthouse Performance (mobile) | ≥ 95 | ≥ 90 |
| Lighthouse Accessibility | **100** | 100 (no compromise) |
| Lighthouse SEO | ≥ 95 | ≥ 90 |
| LCP (mobile, 4G) | < 2.0 s | < 2.5 s |
| CLS | < 0.05 | < 0.1 |
| INP (mobile) | < 150 ms | < 200 ms |
| JS shipped per route (gzipped) | < 120 kB | < 200 kB |
| Hero image weight (per asset) | < 80 kB | < 150 kB |
| Total page weight (homepage) | < 600 kB | < 1 MB |

`pnpm lighthouse` runs the audit; CI fails the PR if any hard ceiling is breached.
Specific tactics:

- **`next/image`** for everything photo-shaped. Pre-size with `width`/`height` to lock
  CLS. Use `priority` only on above-the-fold images.
- **`next/font`** for fonts. Don't `<link rel="stylesheet">` Google Fonts manually —
  defeats subsetting and adds a render-blocking request.
- **Dynamic imports** for below-the-fold sections. See the pattern in
  [`tech/nextjs-patterns.md`](nextjs-patterns.md).
- **Motion library lazy-loaded.** `motion` ships ~30 kB; only import it on routes that
  actually animate.
- **`use cache`** on data fetchers (Next 16). Caching errors at the framework level is
  cheaper than caching them in component code.

## What we don't do

- No barrel files (`index.ts` re-exports).
- No `class` components.
- No CSS Modules / styled-components / emotion.
- No global mutable singletons. Module-level caches in API routes are fine if scoped and documented.
- No `console.log` debugging in committed code.
