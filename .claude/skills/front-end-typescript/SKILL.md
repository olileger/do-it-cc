---
name: front-end-typescript
description: Use when writing, reviewing, or refactoring TypeScript for front-end/client-side code — typing component props and emits, avoiding `any`, type-only imports, generics, and type narrowing. Provides senior-level best practices, common pitfalls, and a review checklist for front-end TypeScript.
---

## When to use this skill

Apply this skill whenever producing or reviewing TypeScript in front-end
code: component prop/emit types, composables/utility function signatures,
API response typing, and general type design for client-side logic.

## Best practices

- Keep `strict` mode enabled and honor it; don't work around strict-mode
  errors by widening a type until the error disappears.
- Prefer precise, narrow types (union types, literal types, discriminated
  unions) over broad ones (`string`, `object`, `any`) whenever the set of
  valid values is actually known.
- Avoid `any`. When a type genuinely can't be known up front, use `unknown`
  and narrow it explicitly before use, rather than defaulting to `any`.
- Type component props and emits explicitly (e.g. `defineProps<T>()` /
  `defineEmits<T>()`), rather than relying only on inferred default values.
- Use type-only imports (`import type { X } from '...'`) for anything used
  purely as a type, keeping type-only code out of the runtime bundle and
  avoiding circular-import issues between type and value graphs.
- Pick `interface` or `type` per the project's existing convention and use it
  consistently (e.g. `interface` for extendable object shapes, `type` for
  unions/aliases/mapped types) rather than mixing arbitrarily.
- Model state that can take several distinct shapes as a discriminated union
  (a shared literal `kind`/`status` field) instead of one type with many
  optional fields that don't logically belong together.
- Narrow types explicitly with type guards, `in`, `instanceof`, or discriminant
  checks, rather than reaching for a type assertion (`as`) to silence the
  compiler.
- Use generics in reusable functions, composables, and components so they stay
  correctly typed across call sites, instead of duplicating near-identical
  typed variants or falling back to `any`.
- Derive types from a single source of truth (inferred from a schema/
  validator, or via `typeof`/`ReturnType` on real code) rather than
  hand-maintaining a parallel type definition that can drift out of sync.
- Validate external/API response shapes at the boundary rather than casting
  `unknown`/parsed JSON straight to a type and trusting it.
- Avoid non-null assertions (`!`) except where non-nullability is genuinely
  proven and the compiler just can't see it; prefer optional chaining (`?.`)
  and nullish coalescing (`??`) over reaching for `!`.

## Common pitfalls

- Reaching for `any` (or `as any`) to silence a type error instead of fixing
  or properly narrowing the underlying type.
- Overusing type assertions (`as X`) instead of real narrowing, hiding type
  mismatches that only surface as a runtime bug later.
- Non-null assertions (`!`) on values that can genuinely be `null`/
  `undefined` at runtime, causing crashes the type system should have caught.
- Hand-duplicating types that could instead be inferred or derived from
  existing runtime code/schemas, letting the two drift apart over time.
- Leaving component emit payloads untyped or typed as `any`, losing type
  safety at a key API boundary between parent and child.
- Importing types without `import type` when the project's build/bundler
  config expects type-only imports to be marked, risking unwanted runtime
  bundling or circular-import breakage.
- Reaching for loose catch-all types (`Record<string, any>`, `any`-valued
  index signatures) where the actual shape is known and could be precise.
- Suppressing a `strict`-mode nullability error instead of actually handling
  the `null`/`undefined` case it's flagging.
- Mixing `interface` and `type` inconsistently within the same codebase
  without a clear, followed convention.

## Review checklist

- [ ] Is `any` absent (or replaced with `unknown` plus proper narrowing)
      everywhere it appears?
- [ ] Are component props and emits explicitly and precisely typed?
- [ ] Are type-only imports marked with `import type` where the project's
      config expects it?
- [ ] Are type assertions (`as`) and non-null assertions (`!`) rare,
      justified, and not masking a real nullability/type issue?
- [ ] Is state with several distinct shapes modeled as a discriminated union
      rather than one type with many loosely-related optional fields?
- [ ] Are types derived from a single source of truth rather than
      hand-duplicated and at risk of drifting?
- [ ] Are external/API response shapes validated (not just cast) at the
      boundary?
- [ ] Is `interface` vs `type` used consistently with the project's existing
      convention?
- [ ] Do generics in reusable code actually constrain/flow correctly, rather
      than silently degrading to `any`?
