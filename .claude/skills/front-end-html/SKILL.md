---
name: front-end-html
description: Use when writing, reviewing, or refactoring HTML markup for a web application — document/semantic structure, accessibility (landmarks, ARIA, forms, headings), and HTML5 idioms. Provides senior-level best practices, common pitfalls, and a review checklist for HTML.
---

## When to use this skill

Apply this skill whenever producing or reviewing HTML markup for a web
application: page/document structure, component templates, forms, or any
markup that will be rendered in a browser.

## Best practices

- Prefer semantic elements (`header`, `nav`, `main`, `footer`, `article`,
  `section`, `aside`, `button`, `a`, list elements, etc.) over generic `div`/
  `span` wherever the semantics fit — semantics drive accessibility, SEO, and
  readability for free.
- Use exactly one `h1` per page/view, and keep heading levels in a logical,
  non-skipping order to preserve a correct document outline.
- Use native interactive elements (`button`, `a`, `input`, `select`, `details`)
  instead of re-implementing their behavior on non-interactive elements —
  native elements give keyboard support, focus handling, and screen-reader
  semantics for free.
- Every `img` needs meaningful `alt` text (or `alt=""` if purely decorative);
  every form control needs a programmatically associated `label`.
- Use `a` for navigation (things that change the URL) and `button` for actions
  (things that don't) — this distinction matters for keyboard users and
  assistive technology.
- Keep markup structure as flat and minimal as the design allows; avoid
  wrapper-div soup that adds no semantic or styling value.
- Use appropriate `input` `type` and `autocomplete` attributes for form fields
  to get correct virtual keyboards, browser validation, and autofill.
- Ensure a logical, predictable tab order; avoid positive `tabindex` values.
- Validate that markup is well-formed (properly nested/closed tags, no
  duplicate `id`s) — malformed markup causes inconsistent, hard-to-debug
  rendering and accessibility bugs.

## Common pitfalls

- Using `div`/`span` with click handlers instead of `button`, breaking
  keyboard and screen-reader access.
- Missing or non-descriptive `alt` text, or decorative images without
  `alt=""`, adding noise for screen-reader users.
- Forms with placeholder text used as a substitute for a real `label`.
- Duplicate `id` attributes on a page, breaking `label`/`aria-*` associations
  and any JS/CSS relying on ID uniqueness.
- Heading levels chosen for visual size rather than document structure (e.g.
  skipping from `h2` to `h4` because it "looks right").
- Non-semantic elements given `role`s and ARIA attributes as a patch instead
  of just using the matching native element.
- Layout tables (using `table` purely for visual layout instead of tabular
  data).
- Inline styles or deprecated presentational attributes mixed into markup
  instead of being handled via styling.

## Review checklist

- [ ] Is there exactly one `h1`, with a logical, non-skipping heading order?
- [ ] Do all images have appropriate `alt` (or `alt=""` if decorative)?
- [ ] Is every form control labeled, and does every form have clear,
      programmatically associated error/help text where relevant?
- [ ] Are interactive elements implemented with native interactive tags
      (`button`, `a`, `input`, etc.) rather than divs/spans with handlers?
- [ ] Is the tab order logical without relying on positive `tabindex`?
- [ ] Are `id`s unique across the document?
- [ ] Does the markup validate (well-formed, no unclosed/mismatched tags)?
- [ ] Is the structure as flat/minimal as the design allows, with no
      unnecessary wrapper elements?
