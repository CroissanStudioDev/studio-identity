# Responsive

We are **mobile-first**. Write the mobile layout first, then add `md:` etc.

## Breakpoints (Tailwind defaults)

| Prefix | Min-width | What it means |
|--------|-----------|---------------|
| (none) | 0 | Mobile |
| `sm:` | 640px | Tablet portrait |
| `md:` | **768px** | **Primary breakpoint — desktop starts here** |
| `lg:` | 1024px | Large desktop |
| `xl:` | 1280px | Wide desktop |

`md:` is the workhorse — most layout switches happen there. `sm:` is mostly for arranging buttons
side-by-side. `lg:`/`xl:` are for fine-tuning, not for big layout changes.

## Common patterns

```tsx
// Show/hide
className="hidden md:block"
className="md:hidden"

// Direction switch
className="flex flex-col md:flex-row"

// Type scale step-ups
className="text-3xl md:text-5xl"
className="py-16 md:py-32"
className="gap-4 md:gap-8"

// Buttons full-width on mobile, auto on desktop
className="w-full md:w-auto"
```

## Touch targets

Minimum **44×44 px** for any interactive element. Our `<Button>` enforces `h-[44px]` automatically.
For icon-only controls, use padding to expand the hit-area even if the visible icon is smaller.

## Don'ts

- Don't write `lg:`/`xl:` first and add `md:` as an afterthought — flip your thinking, mobile is the
  base case.
- Don't use `sm:` for desktop layout. `sm:` ends at 768px — desktop browsers don't trigger it the way
  you'd expect.
- Don't hide critical content on mobile. If you can't fit it, redesign it.
