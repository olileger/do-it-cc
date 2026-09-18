---
name: front-end-javascript
description: Use when writing, reviewing, or refactoring client-side JavaScript for a web application — DOM interaction, event/state handling, asynchronous code, and runtime performance. Provides senior-level best practices, common pitfalls, and a review checklist for front-end JavaScript.
---

## When to use this skill

Apply this skill whenever producing or reviewing client-side JavaScript for a
web application: DOM/UI interaction, state management, event handling,
asynchronous logic (network requests, timers), or client-side application
logic in general.

## Best practices

- Keep functions small and focused; separate concerns (data fetching, state
  updates, DOM/UI updates) rather than mixing them in one block.
- Prefer immutable, predictable data flow (deriving UI from state rather than
  mutating the DOM ad hoc) so behavior stays easy to reason about as the app
  grows.
- Handle the full lifecycle of asynchronous operations: loading, success,
  error, and — where relevant — cancellation/race conditions (e.g. a stale
  request resolving after a newer one).
- Always handle errors explicitly (rejected promises, failed requests,
  unexpected input) rather than letting them fail silently or crash the UI.
- Clean up anything you set up: event listeners, timers/intervals,
  subscriptions, observers — especially for elements/components that can be
  removed or re-rendered, to avoid memory leaks and duplicate handlers.
- Avoid unnecessary global state and globally-scoped variables; keep state as
  local/encapsulated as the design allows.
- Debounce/throttle expensive handlers that fire at high frequency (scroll,
  resize, input) rather than doing expensive work on every event.
- Validate and sanitize any data that ends up rendered into the page, and
  never build DOM content by concatenating untrusted strings.
- Write code that fails predictably on unexpected input (missing fields,
  wrong types, empty arrays) rather than assuming the "happy path" shape.
- Keep naming, structure, and patterns consistent with the rest of the
  codebase (module boundaries, existing utilities, existing conventions for
  state/async handling) rather than introducing a parallel pattern.

## Common pitfalls

- Adding event listeners without ever removing them, leaking listeners on
  elements/components that get recreated.
- Ignoring race conditions between overlapping asynchronous calls (e.g. a
  slow earlier request overwriting the result of a faster, more recent one).
- Swallowing errors (empty `catch` blocks) instead of handling or surfacing
  them.
- Directly mutating shared state/objects in place when the rest of the
  codebase expects immutable updates, causing subtle, hard-to-trace bugs.
- Doing expensive work (layout reads/writes, heavy computation) inside
  high-frequency event handlers without debouncing/throttling.
- Relying on implicit type coercion or loose equality where it obscures
  intent or hides bugs.
- Building HTML via raw string concatenation/interpolation of
  user-influenced data, risking injection issues.
- Tight coupling between unrelated parts of the app through shared globals
  instead of clear, explicit interfaces.
- Not accounting for the component/element being removed, unmounted, or
  re-rendered while an asynchronous operation is still in flight.

## Review checklist

- [ ] Are all asynchronous operations' error and loading states handled, not
      just the success path?
- [ ] Are event listeners, timers, and subscriptions cleaned up when no
      longer needed?
- [ ] Is there a check for race conditions between overlapping async calls
      where relevant (e.g. stale responses)?
- [ ] Is any data rendered into the page properly handled to avoid injecting
      untrusted content?
- [ ] Are high-frequency event handlers debounced/throttled if they do
      non-trivial work?
- [ ] Is state handled consistently with the rest of the codebase's existing
      pattern (no new parallel state-management approach introduced
      silently)?
- [ ] Does the code handle unexpected/missing/malformed input predictably
      instead of assuming ideal input?
- [ ] Are functions small, focused, and named clearly enough to be understood
      without extra context?
