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

## Canonical icon allowlist

When the same concept appears in multiple places, use the same Lucide icon. Different
agents shouldn't pick `Sparkles` in one section and `Zap` in another for the same idea.
This is the studio-wide registry — if you need a concept that's not here, add it to the
list rather than picking ad-hoc.

| Concept | Icon | Notes |
|---------|------|-------|
| Speed / performance | `Zap` | Default. Don't substitute with `Bolt` / `Sparkles`. |
| AI / "smart" | `Brain` | Reserve for genuine AI features, not all features. |
| Team / people | `Users` | Plural. `User` only for single-person UI (account, profile). |
| Code / technical | `Code` | Inline code & dev contexts. `Terminal` for shells specifically. |
| Settings / config | `Settings` | The gear. Don't use `Sliders` unless it's literally sliders. |
| Search | `Search` | The magnifier. Period. |
| Calendar / scheduling | `Calendar` | `CalendarDays` only when grid view is the point. |
| Documentation / spec | `FileText` | `File` is for generic files; `FileText` for written content. |
| Link / external | `ArrowUpRight` | Default for "open in new tab" / external link affordance. |
| Internal forward | `ArrowRight` | Default CTA arrow. Don't substitute with `ChevronRight`. |
| Close / dismiss | `X` | Always. `XCircle` only when the X is itself a state indicator. |
| Success / check | `Check` | Plain. `CheckCircle` only when it's a status badge. |
| Warning | `TriangleAlert` | Not the older `AlertTriangle` name. |
| Error | `CircleAlert` | Pairs with `text-error`. |
| Info | `Info` | The lowercase i circle. |
| Telegram | hand-drawn `/public/icons/telegram.svg` | Lucide doesn't ship Telegram. Keep one custom SVG, reuse. |
| Email | `Mail` | Don't use `AtSign` — that's for handles. |
| Phone | `Phone` | — |
| Download | `Download` | — |
| Copy | `Copy` | Pairs with a brief tooltip / toast on click. |

Rule: **if you find yourself picking a synonym** (`Star` instead of the documented icon
for "favorite"), check this table first. If your concept genuinely isn't here, add it
in a PR — don't ad-hoc.

## Don'ts

- **Never use emoji as icons.** They render inconsistently across OSes, don't follow color tokens,
  and clash with the brand voice.
- Don't mix Lucide with another icon library in the same project.
- Don't recolor by overriding `stroke` directly — use Tailwind text color (`text-brand`,
  `text-primary-60`), since Lucide inherits `currentColor`.
- **Don't use icons as bullets.** A `<ul>` with a Lucide icon prefix on every `<li>`
  is the "AI-dashboard" tell — see [`agents/anti-ai-slop.md`](../agents/anti-ai-slop.md).
  Icons earn their place by adding meaning the text alone doesn't, or get cut.
