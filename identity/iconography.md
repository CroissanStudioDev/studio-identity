# Iconography

## Library

**[Lucide](https://lucide.dev) only.** Imported via `lucide-react`. Locked in `components.json`:
```json
"iconLibrary": "lucide"
```

No Heroicons, no Material, no FontAwesome, no Phosphor, no custom SVG icon kit. If Lucide doesn't have it,
either rephrase the UI to avoid the icon or hand-draw a one-off SVG and check it into `public/`.

## Sizes

| Size class | Use |
|------------|-----|
| `size-4` (16px) | Inline next to text |
| `size-5` (20px) | Inside buttons |
| `size-6` (24px) | Standalone |

Don't pass arbitrary `width`/`height` — use `size-N` so the icon scales correctly with text.

## Accessibility

```tsx
// Decorative icon next to text — text already conveys the meaning
<Zap aria-hidden="true" size={20} /> Скорость

// Icon-only button — must have aria-label
<button aria-label="Закрыть меню">
  <X aria-hidden="true" className="size-5" />
</button>
```

The two patterns:
- Decorative + text → icon gets `aria-hidden="true"`.
- Icon-only interactive → wrapper gets `aria-label`, icon gets `aria-hidden="true"`.

## Don'ts

- **Never use emoji as icons.** They render inconsistently across OSes, don't follow color tokens,
  and clash with the brand voice.
- Don't mix Lucide with another icon library in the same project.
- Don't recolor by overriding `stroke` directly — use Tailwind text color (`text-brand`,
  `text-primary-60`), since Lucide inherits `currentColor`.
