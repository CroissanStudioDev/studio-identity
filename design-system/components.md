# Components

Live snippets pulled from `croissan-landing/components/`. When in doubt, find the closest existing
component there and copy it — don't invent a new one.

We extend **shadcn/ui (new-york style)** with our own opinions. Base alias setup:

```json
{ "style": "new-york", "tailwind": { "baseColor": "zinc", "cssVariables": true } }
```

## Buttons

Base lives in `components/ui/button.tsx` (shadcn) using `cva`. Built-ins: `h-[44px]` touch target,
`cursor-pointer`, `focus-visible:ring-[3px]`, `transition-all`.

```tsx
// Primary CTA
<Button className="bg-brand hover:bg-[var(--brand-primary-hover)] text-white">
  Забронировать звонок
</Button>

// Hero-sized primary (taller, larger radius)
<Button className="w-full rounded-[16px] bg-brand px-8 py-7 text-[16px] hover:bg-[var(--brand-primary-hover)] md:w-auto">

// Secondary outline (hero-sized)
<Button className="rounded-[16px] py-7 pr-6 pl-7 text-[16px]" variant="outline">
```

| Param | Value |
|-------|-------|
| Min height | `h-[44px]` (built-in) |
| Standard radius | `rounded-[12px]` |
| Hero radius | `rounded-[16px]` |
| Hero vertical padding | `py-7` |

## Cards

```tsx
// Standard
<div className="rounded-3xl border border-black/5 bg-white">

// Case-card with cover image
<div className="group flex flex-col overflow-hidden rounded-3xl border border-black/5 bg-white">
  <div className="relative m-2 mb-0 h-auto w-[calc(100%-1rem)] overflow-hidden rounded-2xl">
    {/* Image */}
  </div>
  <div className="flex flex-1 flex-col p-8">{/* Content */}</div>
</div>

// Glass (navbar, forms)
<div className="rounded-[20px] bg-background/80 backdrop-blur-md">

// Heavy-glass (CTA, hero overlays)
<div className="rounded-3xl bg-gradient-to-br from-white/10 to-white/5 shadow-sm backdrop-blur-[100px]">
```

## Badges / tags

```tsx
<span className="rounded-full bg-black/5 px-3 py-1 font-medium text-primary-70 text-xs">
  {tag}
</span>
```

## Links

```tsx
// Internal — always next/link, never <a href="/...">
<Link href="/brief">Создать бриф</Link>

// External — always rel + target
<Link href="https://t.me/vilfer" rel="noopener noreferrer" target="_blank">
```

## Forms

```tsx
// Always a visible label, not placeholder-only
<label htmlFor="name" className="block text-lg font-medium text-brand-dark mb-3">
  Имя
</label>
<Textarea
  id="name"
  className="min-h-[200px] rounded-xl border-2 border-gray-200 text-base focus:border-brand"
/>

// Inline error under field
<p className="text-error text-sm" role="alert">{error.message}</p>

// Global error above submit
<div
  className="flex items-center gap-2 rounded-xl border border-red-200 bg-red-50 p-4 text-error"
  role="alert"
>
  <AlertCircle aria-hidden="true" className="h-5 w-5" />
  <span>{error}</span>
</div>
```

Form rules:
- Every input has a `<label htmlFor>` matching its `id` — even when the label is visually compressed.
- Validate with **Zod**. Wire with **react-hook-form** + `@hookform/resolvers`.
- Error messages are specific and actionable («Укажите телефон или Telegram», not «Ошибка»).
- `role="alert"` on the element that displays the error.

## Images

```tsx
// Fixed size
<Image alt="Описание" height={32} width={32} src="/logo.svg" />

// Fill parent (parent must be relative)
<Image alt="Описание" className="object-cover" fill src="/image.webp" />

// Above-the-fold (hero) — set priority
<Image alt={`Логотип ${brand.name}`} height={32} priority src={brand.svg} width={120} />

// Decorative — text already conveys meaning
<Image alt="" aria-hidden="true" ... />
```

- Always `next/image`. Never `<img>`.
- Photo content is **WebP only**. JPEG/PNG only if a tool requires it.
- Always set `alt` (use `""` + `aria-hidden` for purely decorative duplicates).

## Don't invent new primitives

If you need a tooltip, popover, dropdown, or any common UI primitive — install the corresponding
shadcn component (`pnpm dlx shadcn@latest add tooltip`) before writing one from scratch. Customize
it with our tokens, don't fork it.
