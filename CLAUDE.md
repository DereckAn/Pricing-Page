# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Commands

Use **bun** as the package manager (not npm/yarn):

```bash
bun dev              # Start dev server at localhost:4321
bun build            # Build production site to ./dist/
bun preview          # Preview production build locally
bun astro check      # Type-check all .astro files
bun astro add        # Add integrations (e.g., tailwind, react)
```

Requires Node >= 22.12.0.

## Architecture

This is an **Astro 6** static site project for a pricing page. Astro uses file-based routing — every `.astro` file in `src/pages/` becomes a route.

Key directories:
- `src/pages/` — Routes. `index.astro` is the homepage (`/`).
- `src/components/` — Reusable Astro components.
- `src/layouts/` — HTML shell templates. `Layout.astro` wraps pages with `<head>` and `<body>`.
- `src/assets/` — Images and SVGs processed by Astro's asset pipeline (import to use).
- `public/` — Static assets served as-is (favicon, etc.).
- `.astro/` — Auto-generated TypeScript types; do not edit.

## TypeScript

Config extends `astro/tsconfigs/strict`. Astro component props must be typed via the `interface Props` pattern in the component frontmatter. Run `bun astro check` to validate types across all `.astro` files.

## Astro Component Pattern

```astro
---
// Frontmatter: runs at build time (server-side only)
import Component from '../components/Component.astro';
interface Props { title: string; }
const { title } = Astro.props;
---

<!-- Template: HTML + component slots -->
<Component>{title}</Component>
```

No client-side JavaScript ships by default. Use `client:load`, `client:idle`, or `client:visible` directives only when interactivity is required.
