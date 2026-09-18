---
name: front-end-vite
description: Use when configuring, reviewing, or troubleshooting Vite for a front-end web app — environment variables, path aliases, dev server/build configuration, and plugin usage. Provides senior-level best practices, common pitfalls, and a review checklist for Vite configuration.
---

## When to use this skill

Apply this skill whenever producing or reviewing Vite configuration or
Vite-dependent setup for a front-end web application: `vite.config.ts`, env
variable usage, build/dev-server settings, path aliases, or plugin choices.

## Best practices

- Only expose environment variables prefixed with the client-exposed prefix
  (`VITE_` by default) to client code; keep server-only secrets and tokens
  out of anything Vite makes available to the browser.
- Use `import.meta.env` (not `process.env`) to read Vite env variables in
  client code, and declare their types via an `env.d.ts`/`ImportMetaEnv`
  augmentation when using TypeScript.
- Keep `.env` files organized per mode (`.env`, `.env.development`,
  `.env.production`, `.env.local`) and never commit `.env.local` or any
  secret-bearing env file to version control.
- Configure path aliases via `resolve.alias` to mirror the project's actual
  folder structure, and keep `tsconfig.json`'s `paths` in sync with them so
  the type checker and the bundler agree.
- Set `base` explicitly whenever the app is deployed under a sub-path,
  instead of assuming root (`/`) deployment.
- Keep the plugin list minimal and purposeful — each plugin adds build time
  and maintenance surface; prefer a built-in Vite feature over a plugin when
  they're equivalent.
- Configure the dev server (`server.port`, `server.proxy`, etc.) to match how
  the team actually develops locally (e.g. proxying API calls to a backend)
  rather than hardcoding assumptions that only work on one machine.
- Use `defineConfig` and keep `vite.config.ts` typed for editor
  autocompletion and validation of config options.
- Reach for build-time code splitting/manual chunking only when there's a
  demonstrated bundle-size or load-performance reason, not preemptively.
- Align `build.target` (or an equivalent browserslist config) with the
  project's actual supported-browser matrix rather than leaving the default
  unexamined.

## Common pitfalls

- Naming a server-only secret with the client-exposed prefix (`VITE_...`),
  accidentally shipping it into the client-visible bundle.
- Reading env variables via `process.env` in client code, where it's
  undefined/unreliable by default in Vite's client runtime.
- Forgetting to set `base` for a non-root deployment, causing broken asset
  paths or a blank page once deployed.
- Path aliases defined in `vite.config.ts` but not mirrored in
  `tsconfig.json` (or vice versa), so type-checking/editor resolution
  disagrees with what the bundler actually resolves.
- Committing `.env.local` or another secret-bearing env file to version
  control.
- Adding a plugin that duplicates functionality Vite already provides
  natively, adding build time and maintenance surface for no real benefit.
- Relying in production on dev-server-only behavior (like the dev proxy),
  which doesn't exist once the app is built and served statically.
- Confusing Vite's `mode` (set via `--mode`) with Node's `NODE_ENV`, causing
  the wrong `.env` files to load for a given build.
- Importing an entire library when only a small part is used, without
  checking that the import path/module actually tree-shakes as expected.

## Review checklist

- [ ] Do only intentionally-public env variables use the client-exposed
      prefix, with anything server-only kept out of it?
- [ ] Is `import.meta.env` used instead of `process.env` in client code, with
      env types declared for TypeScript?
- [ ] Are `.env.local`/secret-bearing env files excluded from version
      control?
- [ ] Is `base` configured correctly for the app's actual deployment path?
- [ ] Do `vite.config.ts` aliases and `tsconfig.json` `paths` match?
- [ ] Is every plugin in the config actually necessary, with no redundant
      overlap with a built-in Vite feature?
- [ ] Is dev-server-only config (e.g. proxying) clearly not relied upon for
      production behavior?
- [ ] Is `build.target`/browser support configured to match the project's
      real supported-browser matrix?
