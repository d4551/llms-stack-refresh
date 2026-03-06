# Repository Index

Canonical navigation map for `llms-stack-refresh`. Use this file to locate the correct `llms.txt` for a given technology.

## Runtime / Backend

| Stack | File | Provenance | Notes |
|-------|------|------------|-------|
| Bun | [`bun/llms.txt`](../bun/llms.txt) | **Official** — https://bun.sh/llms.txt | All-in-one JS/TS runtime, bundler, test runner, package manager; includes plugin API, macros, workspaces |
| ElysiaJS | [`elysiajs/llms.txt`](../elysiajs/llms.txt) | Curated — https://elysiajs.com | TypeScript web framework for Bun; routes, validation, lifecycle, plugins, Eden E2E type safety |

## Auth

| Stack | File | Provenance | Notes |
|-------|------|------------|-------|
| EasyAuth | [`easy-auth/llms.txt`](../easy-auth/llms.txt) | Curated — https://easyauth.io/docs/ | Managed auth service; OAuth providers, session tokens, user profiles; no official llms.txt exists |

## Hypermedia / Frontend

| Stack | File | Provenance | Notes |
|-------|------|------------|-------|
| htmx | [`htmx/llms.txt`](../htmx/llms.txt) | Curated — https://htmx.org | HTML-first AJAX library; all `hx-*` attributes, request/response headers, CSS classes, extensions |

## ORM / Data

| Stack | File | Provenance | Notes |
|-------|------|------------|-------|
| Prisma | [`prisma/llms.txt`](../prisma/llms.txt) | Curated — https://www.prisma.io/docs | Node.js/TypeScript ORM; schema, client, migrate, platform, `$extends` client extensions |

## Styling / Components

| Stack | File | Provenance | Notes |
|-------|------|------------|-------|
| Tailwind CSS | [`tailwindcss/llms.txt`](../tailwindcss/llms.txt) | Curated — https://tailwindcss.com/docs | Utility-first CSS framework; utilities, config, `@apply`, `@plugin`, `@utility`, `@variant` |
| daisyUI | [`daisyui/llms.txt`](../daisyui/llms.txt) | **Official** — https://daisyui.com/llms.txt | Tailwind CSS component library (v5); themes, plugin config, component usage rules |

## Supporting Docs

| File | Purpose |
|------|---------|
| [`README.md`](../README.md) | Repository overview, usage with AI tools, stack composition guide |
| [`AGENTS.md`](../AGENTS.md) | AI agent navigation rules, structure rules, per-stack plugin/extension guidance |
| [`docs/INDEX.md`](INDEX.md) | This file — canonical navigation map |
| [`docs/CONTRIBUTING.md`](CONTRIBUTING.md) | How to add or improve an `llms.txt` |
| [`docs/PROVENANCE.md`](PROVENANCE.md) | Provenance policy and sourcing rules |

## Provenance Key

- **Official** — the `llms.txt` file is published directly by the project at a canonical URL
- **Curated** — the file is hand-authored from official primary-source documentation; source URL is noted
