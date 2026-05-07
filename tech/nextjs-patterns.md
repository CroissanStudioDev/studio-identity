# Next.js 16 patterns

Reference patterns for App Router projects. All examples are real code from `croissan-landing`.

## Project structure

```
app/
├── layout.tsx              # Fonts, analytics, navbar/footer, base JSON-LD
├── page.tsx                # Home + page-specific JSON-LD
├── api/                    # Route handlers (POST endpoints)
├── error.tsx               # Route-level error boundary
├── global-error.tsx        # Root-layout error boundary
├── not-found.tsx           # Custom 404
├── opengraph-image.tsx     # Dynamic OG image (one per route)
├── sitemap.ts
├── robots.ts
└── [route]/
    ├── page.tsx
    └── opengraph-image.tsx

components/
├── sections/               # Page sections (one file per visible block)
└── ui/                     # shadcn-style reusable primitives

hooks/                      # Custom React hooks
lib/
├── seo/facts.ts            # Single source of truth for marketing content
├── seo/                    # SEO utilities
└── utils.ts                # cn() helper, generic helpers
```

**No barrel files.** No `index.ts` re-exporting `export * from "./foo"`. Import from concrete paths.

## Server vs client components

- **Default to Server Components.** No `"use client"` unless a hook or event handler genuinely needs it.
- Footers, JSON-LD blocks, static layouts, anything that just renders → Server Component.
- Forms with state, modals, interactive widgets → Client Component (`"use client"` at file top).

## Caching (Next 16)

```tsx
import { cacheLife, cacheTag } from "next/cache";

async function getData() {
  "use cache";
  cacheLife("hours");
  cacheTag("my-tag");
  // ...
}
```

`cacheComponents: true` must be enabled in `next.config.ts`. Tag related caches so a single
`revalidateTag("my-tag")` invalidates everything.

## Dynamic imports for below-fold sections

Below-the-fold sections lazy-load with skeletons to keep initial JS small:

```tsx
const Cases = dynamic(
  () => import("@/components/sections/cases").then((m) => ({ default: m.Cases })),
  { loading: () => <div className="py-16 md:py-32" /> },
);
```

## Fonts (`layout.tsx`)

```tsx
import { Geist_Mono, Golos_Text } from "next/font/google";
import localFont from "next/font/local";

const golos = Golos_Text({ subsets: ["cyrillic", "latin"], variable: "--font-geist-sans" });
const geistMono = Geist_Mono({ subsets: ["latin"], variable: "--font-geist-mono" });
const rightGrotesk = localFont({
  src: "../public/fonts/RightGrotesk.woff2",
  variable: "--font-right-grotesk",
});

<html className={`${golos.variable} ${geistMono.variable} ${rightGrotesk.variable}`}>
```

## Metadata

Per-page `metadata` export with `openGraph`, `alternates.canonical`, `description`. Pull facts from
`lib/seo/facts.ts` so updating a number propagates everywhere automatically.

## API route pattern

```tsx
// app/api/foo/route.ts
import { NextRequest } from "next/server";
import { z } from "zod";

const Schema = z.object({ description: z.string().min(10).max(5000) });

export async function POST(req: NextRequest) {
  const parsed = Schema.safeParse(await req.json());
  if (!parsed.success) {
    return Response.json({ error: "Bad request" }, { status: 400 });
  }
  // Rate-limit, do work, return Response.json(...)
}
```

- **Always validate input with Zod.** No exceptions.
- **Always rate-limit.** Use the in-memory limiter pattern from `lib/rate-limit/`.
- Return structured JSON. No HTML responses from JSON endpoints.

## Error boundaries

Three levels:
- `app/error.tsx` — route-level, catches errors below the layout.
- `app/global-error.tsx` — root, catches errors in the root layout itself.
- `app/not-found.tsx` — explicit 404.

All three should match the brand visually and offer a way back to `/`.

## Don'ts

- Don't use Pages Router. Hard no.
- Don't use `getServerSideProps` / `getStaticProps` patterns — they don't exist in App Router.
- Don't manually `useMemo`/`useCallback` — React Compiler handles it. Trust the compiler.
- Don't use `<a>` for internal navigation. `next/link` only.
- Don't use `<img>`. `next/image` only.
- Don't put secrets in `NEXT_PUBLIC_*` env vars.
