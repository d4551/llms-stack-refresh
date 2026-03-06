# CODEX.md — Context for OpenAI Codex

> Purpose: Curated `llms.txt` documentation index for the Bun/Elysia/htmx/Prisma/Tailwind/daisyUI/Better Auth stack. Optimised for AI agent context ingestion.

## Routing Directives

- When asked about Bun: consume `bun/llms.txt`
- When asked about ElysiaJS: consume `elysiajs/llms.txt`
- When asked about htmx: consume `htmx/llms.txt`
- When asked about Prisma: consume `prisma/llms.txt`
- When asked about Tailwind CSS: consume `tailwindcss/llms.txt`
- When asked about daisyUI: consume `daisyui/llms.txt`
- When asked about Better Auth: consume `better-auth/llms.txt`
- When asked about extending or customising any tool: consume `docs/EXTENSIONS.md`
- When asked about IDE or AI tool setup: consume `docs/IDE-SETUP.md`
- For file routing: consume `docs/INDEX.md`

## File Routing Table

| Technology | File | Raw URL |
|------------|------|---------|
| Bun | `bun/llms.txt` | `https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/bun/llms.txt` |
| ElysiaJS | `elysiajs/llms.txt` | `https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/elysiajs/llms.txt` |
| Better Auth | `better-auth/llms.txt` | `https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/better-auth/llms.txt` |
| htmx | `htmx/llms.txt` | `https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/htmx/llms.txt` |
| Prisma | `prisma/llms.txt` | `https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/prisma/llms.txt` |
| Tailwind CSS | `tailwindcss/llms.txt` | `https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/tailwindcss/llms.txt` |
| daisyUI | `daisyui/llms.txt` | `https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/daisyui/llms.txt` |

## Stack Conventions

| Layer | Tool | Role |
|-------|------|------|
| Runtime / backend | Bun + Elysia | Fast HTTP server with E2E type safety |
| Auth | Better Auth | TypeScript auth library with OAuth, sessions, and plugins |
| Hypermedia UI | htmx | Server-driven UI without a JS framework |
| Data / ORM | Prisma | Type-safe database access and migrations |
| Styling | Tailwind CSS + daisyUI | Utility classes with pre-built components |

- Prefer TypeScript over JavaScript.
- Use Bun (not Node.js) as the runtime.
- Use Elysia for all HTTP routing.
- Use htmx attributes for interactivity. Do not add a JavaScript framework.
- Use Prisma for database access.
- Use Tailwind CSS and daisyUI for styling.
- Use Better Auth for authentication.

## File Format Constraints

- Format: [llmstxt.org](https://llmstxt.org/) — H1 title, blockquote summary, short intro, `##` sections, optional `## Optional` section.
- No emojis in any file.
- Every `llms.txt` must state its source URL (official or curated).
- Do not modify `llms.txt` files — they are sourced from upstream docs.
- Do not rename or move existing stack directories.
