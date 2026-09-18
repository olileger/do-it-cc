---
name: front-end-vue
description: Use when writing, reviewing, or refactoring Vue 3 components for a web application — Composition API, the reactivity system (ref/reactive/computed), Single-File Component structure, and component communication (props/emits, v-model). Provides senior-level best practices, common pitfalls, and a review checklist for Vue 3.
---

## When to use this skill

Apply this skill whenever producing or reviewing Vue 3 code for a web
application: Single-File Components, composables, reactive state, component
props/emits/events, or Vue-specific templating (`v-if`, `v-for`, `v-model`,
directives).

## Best practices

- Prefer the Composition API with `<script setup>` for new components, unless
  the project already has an established Options API convention — follow the
  existing codebase pattern consistently.
- Use `ref` for primitives and `reactive` for objects, or default to `ref`
  everywhere if that's the project's convention — either is valid, but stay
  consistent with what's already used.
- Never destructure a `reactive()` object (or a props object) directly into
  loose variables — this breaks reactivity. Access properties on the object,
  or use `toRefs`/`storeToRefs` when destructuring is genuinely needed.
- Use `computed` for any state that can be derived from other reactive state,
  instead of duplicating it in a separate `ref` kept in sync via a `watch`.
- Keep Single-File Components organized (`<script setup>`, `<template>`,
  `<style scoped>`) and scope or module-ize styles to avoid leaking outside
  the component.
- Type props and emits explicitly with `defineProps<T>()`/`defineEmits<T>()`
  (see the `front-end-typescript` skill for typing patterns) rather than
  relying only on runtime prop declarations.
- Use `v-model` (including custom `v-model` bindings on components) for
  two-way binding instead of manually wiring an equivalent prop + emit pair.
- Always give `v-for` a stable, unique `:key` tied to a real identifier (not
  the array index) for any list that can reorder, filter, or have items
  inserted/removed.
- Never combine `v-if` and `v-for` on the same element; filter the list with
  a `computed` first, or wrap the conditional in a `<template>`.
- Use `watch`/`watchEffect` deliberately and only when `computed` can't
  express the logic; clean up any side effects they start (subscriptions,
  timers) in the watcher's cleanup or in `onUnmounted`.
- Treat props as read-only inputs; request changes in a parent's state by
  emitting a well-named event rather than mutating a prop directly.
- Extract reusable reactive logic into composables (`useX` functions) instead
  of duplicating the same reactive logic across multiple components.
- Use `provide`/`inject` sparingly, for genuinely cross-cutting concerns, and
  typed explicitly — not as a shortcut around prop drilling in ordinary cases.

## Common pitfalls

- Destructuring a `reactive()` object or a `props` object directly, silently
  losing reactivity on the extracted variables.
- Using the array index as `:key` in a `v-for` over a list that can reorder
  or be filtered, causing incorrect DOM diffing and stale component state.
- Mutating a prop directly inside a child component instead of emitting an
  event so the parent updates its own state.
- Keeping derived state in a separate `ref` synced by a `watch` instead of
  simply using `computed`, letting the two drift out of sync.
- Watchers that start side effects (timers, subscriptions, listeners)
  without a corresponding cleanup, leaking them across re-renders/unmounts.
- Manually reimplementing `v-model` with an ad hoc prop + emit pair instead
  of using Vue's built-in two-way binding support.
- Combining `v-if` and `v-for` on the same element, causing confusing
  precedence and unnecessary re-renders of filtered-out items.
- Forgetting `.value` when reading or writing a `ref` in `<script setup>`
  code outside the template (auto-unwrapping only applies in the template).
- Reassigning a whole `reactive()` object to a new object, which detaches it
  from the reactivity binding set up at declaration.
- Leaving `<style>` blocks unscoped in an SFC, leaking styles globally.

## Review checklist

- [ ] Are reactive objects/props accessed without destructuring (or
      destructured safely via `toRefs`/`storeToRefs`)?
- [ ] Does every `v-for` use a stable, unique `:key` rather than the array
      index, for any list that can reorder or be filtered?
- [ ] Is derived state computed via `computed` rather than duplicated in a
      separately maintained ref?
- [ ] Are props treated as read-only, with changes requested via emitted
      events instead of direct mutation?
- [ ] Is `v-model` used for two-way binding instead of manual prop+emit
      wiring?
- [ ] Are `v-if` and `v-for` kept off the same element?
- [ ] Do watchers/`watchEffect` clean up any side effects they start, and are
      they used only where `computed` genuinely isn't sufficient?
- [ ] Are `<style>` blocks scoped/module, avoiding unintended global leakage?
- [ ] Is shared reactive logic extracted into composables rather than
      duplicated across components?
- [ ] Are props and emits explicitly typed?
