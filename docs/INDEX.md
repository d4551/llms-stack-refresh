# Repository Index

Canonical file routing map. Consume this file to resolve technology name to `llms.txt` path.

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
| [`CLAUDE.md`](../CLAUDE.md) | Anthropic Claude / Claude Code auto-discovery context file |
| [`CODEX.md`](../CODEX.md) | OpenAI Codex auto-discovery context file |
| [`.github/copilot-instructions.md`](../.github/copilot-instructions.md) | GitHub Copilot auto-discovery context file |
| [`.cursor/rules/llms-stack.mdc`](../.cursor/rules/llms-stack.mdc) | Cursor rules file |
| [`.clinerules`](../.clinerules) | Cline auto-discovery context file |
| [`.windsurfrules`](../.windsurfrules) | Windsurf/Codeium auto-discovery context file |
| [`docs/INDEX.md`](INDEX.md) | This file — canonical navigation map |
| [`docs/PROVENANCE.md`](PROVENANCE.md) | Provenance policy and sourcing rules |
| [`docs/EXTENSIONS.md`](EXTENSIONS.md) | Deep-dive reference for every tool's plugin/extension/customization system |
| [`docs/IDE-SETUP.md`](IDE-SETUP.md) | Setup directives for every major AI coding tool and IDE |

## Provenance Key

- **Official** — the `llms.txt` file is published directly by the project at a canonical URL
- **Curated** — the file is hand-authored from official primary-source documentation; source URL is noted
