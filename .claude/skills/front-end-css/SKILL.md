---
name: front-end-css
description: Use when writing, reviewing, or refactoring CSS/styling for a web application — layout, responsive design, the cascade/specificity, and maintainable styling architecture. Provides senior-level best practices, common pitfalls, and a review checklist for CSS.
---

## When to use this skill

Apply this skill whenever producing or reviewing styling for a web
application: layout, responsive/adaptive behavior, visual states, theming, or
any styling architecture decisions.

## Best practices

- Prefer modern layout mechanisms (flexbox, grid) over legacy techniques
  (floats, absolute-positioning hacks) for structural layout.
- Design responsively by default: use relative units (`%`, `rem`, `em`, `fr`,
  viewport units) where appropriate, and verify behavior across a realistic
  range of viewport sizes rather than a single fixed width.
- Keep selectors as simple and low-specificity as the project's architecture
  allows; avoid deep nesting and over-qualified selectors that make future
  overrides fragile.
- Follow the project's existing styling architecture/naming convention
  consistently (whatever methodology or tooling it already uses) rather than
  mixing approaches within the same codebase.
- Avoid `!important` except as a rare, deliberate, commented last resort — it
  is almost always a sign the underlying specificity/architecture needs
  fixing instead.
- Co-locate or organize styles in a way that makes it obvious which markup/
  component they apply to, matching how the rest of the project organizes
  styles.
- Respect user and system preferences where relevant (e.g. reduced-motion,
  color-scheme) rather than forcing a single behavior.
- Keep animations/transitions purposeful and performant; prefer animating
  properties that don't force expensive layout recalculation.
- Reuse existing design tokens/variables (spacing, color, typography scale)
  instead of hardcoding one-off magic values.

## Common pitfalls

- Fixed pixel widths/heights that break on smaller viewports or with larger
  user font sizes.
- Specificity wars: escalating selector specificity or `!important` to win
  cascade conflicts instead of restructuring the styles.
- Deeply nested selectors that closely couple CSS to a specific markup
  structure, breaking the moment markup changes slightly.
- Styling only the "happy path" state and forgetting hover/focus/active/
  disabled/error/empty/loading states.
- Removing focus outlines (`outline: none`) without providing an equally
  visible custom focus style, breaking keyboard navigation.
- Overriding another component's styles by targeting its internals instead of
  through an intended styling API/variant.
- Copy-pasted, near-duplicate style blocks instead of a shared, reusable
  pattern — a common source of visual drift over time.
- Assuming content length/size (text, images) instead of designing for
  variable/overflowing content.

## Review checklist

- [ ] Does the layout hold up across a realistic range of viewport sizes, not
      just the one it was designed at?
- [ ] Are relative units used where the project's convention expects them,
      rather than hardcoded pixel values?
- [ ] Is specificity kept low and selectors simple, with no new
      `!important` added without a documented reason?
- [ ] Are all relevant interactive states styled (hover, focus, active,
      disabled, error), and is focus always visibly indicated?
- [ ] Does the styling follow the project's existing architecture/naming
      convention rather than introducing a new, inconsistent approach?
- [ ] Are existing design tokens/variables reused instead of new magic
      values?
- [ ] Does the styling degrade gracefully for longer/shorter/overflowing
      content than the design assumed?
- [ ] Are transitions/animations reasonably performant and respectful of a
      reduced-motion preference where relevant?
