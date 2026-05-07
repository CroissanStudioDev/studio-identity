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

## What we don't do

- No barrel files (`index.ts` re-exports).
- No `class` components.
- No CSS Modules / styled-components / emotion.
- No global mutable singletons. Module-level caches in API routes are fine if scoped and documented.
- No `console.log` debugging in committed code.
