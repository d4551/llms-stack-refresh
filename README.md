# llms-stack-refresh

A curated collection of `llms.txt` files for the tools in a modern full-stack TypeScript/Bun workflow — sourced from official documentation or hand-crafted where no official file exists — optimized for AI coding assistants and human contributors.

## What is llms.txt?

[`llms.txt`](https://llmstxt.org/) is a proposed standard for LLM-friendly documentation. Each file is a structured, Markdown-based index of key documentation links that AI tools can efficiently consume. The format: H1 title → blockquote summary → short intro → `##` sections → optional `## Optional` section.

## Repository Map

```
llms-stack-refresh/
├── README.md            ← You are here
├── AGENTS.md            ← AI agent navigation rules and per-stack guidance
├── bun/llms.txt         ← Official Bun docs (runtime, bundler, plugins, macros, workspaces)
├── daisyui/llms.txt     ← Official daisyUI docs (components, themes, plugin config)
├── easy-auth/llms.txt   ← Curated EasyAuth docs (OAuth, sessions, Bun/Elysia integration)
├── elysiajs/llms.txt    ← Curated ElysiaJS docs (routes, lifecycle, plugins, Eden)
├── htmx/llms.txt        ← Curated htmx docs (attributes, headers, extensions)
├── prisma/llms.txt      ← Curated Prisma docs (schema, client, migrate, $extends)
├── tailwindcss/llms.txt ← Curated Tailwind CSS docs (utilities, @apply, @plugin, @utility)
└── docs/
    ├── INDEX.md         ← Canonical navigation map grouped by role
    ├── CONTRIBUTING.md  ← How to add or improve an llms.txt
    └── PROVENANCE.md    ← Sourcing and provenance policy
```

## Included Files

| Technology | File | Provenance | Notes |
|-----------|------|------------|-------|
| 🍞 [Bun](./bun/llms.txt) | `bun/llms.txt` | **Official** — https://bun.sh/llms.txt | All-in-one JS/TS runtime, bundler, test runner, package manager; plugin API, macros, workspaces |
| 🌼 [daisyUI](./daisyui/llms.txt) | `daisyui/llms.txt` | **Official** — https://daisyui.com/llms.txt | Tailwind CSS component library (v5); themes, plugin config, component rules |
| 🔐 [EasyAuth](./easy-auth/llms.txt) | `easy-auth/llms.txt` | Curated — https://easyauth.io/docs/ | Managed auth service; OAuth, sessions, user profiles; Bun/Elysia/htmx integration patterns |
| ✨ [ElysiaJS](./elysiajs/llms.txt) | `elysiajs/llms.txt` | Curated — https://elysiajs.com | TypeScript web framework for Bun; routes, validation, lifecycle, plugins (`bearer`, `cors`, `jwt`, …), Eden E2E type safety |
| 🟦 [htmx](./htmx/llms.txt) | `htmx/llms.txt` | Curated — https://htmx.org | HTML-first AJAX library; full `hx-*` attribute reference, response headers, extensions, extension building |
| 🔺 [Prisma](./prisma/llms.txt) | `prisma/llms.txt` | Curated — https://www.prisma.io/docs | Node.js/TypeScript ORM; schema, client, migrate, platform, `$extends` client extensions |
| 🌬️ [Tailwind CSS](./tailwindcss/llms.txt) | `tailwindcss/llms.txt` | Curated — https://tailwindcss.com/docs | Utility-first CSS framework; utilities, config, `@apply`, `@plugin`, `@utility`, `@variant`, `@custom-variant` |

> **Note on Tailwind CSS**: Tailwind Labs has not officially published an `llms.txt` file ([see discussion](https://github.com/tailwindlabs/tailwindcss/discussions/18256)). The file here is curated from the official documentation source.
>
> **Note on EasyAuth**: No official `llms.txt` was found. `easy-auth/llms.txt` is curated from the official EasyAuth documentation at https://easyauth.io/docs/.

## Stack Composition — First-Class Approach

These tools are commonly combined as a full-stack TypeScript/Bun workflow:

| Layer | Tool | Role |
|-------|------|------|
| Runtime / backend | **Bun** + **Elysia** | Fast HTTP server with E2E type safety |
| Auth | **EasyAuth** | Managed OAuth / session layer |
| Hypermedia UI | **htmx** | Server-driven UI without a JS framework |
| Data / ORM | **Prisma** | Type-safe database access and migrations |
| Styling | **Tailwind CSS** + **daisyUI** | Utility classes with pre-built components |

### Typical request flow

```
Browser (htmx attributes)
  → Elysia route handler (Bun)
      → EasyAuth session validation (beforeHandle hook)
      → Prisma query (type-safe, $extends for custom logic)
  → Server renders HTML partial (Tailwind CSS + daisyUI classes)
Browser swaps partial into DOM (hx-target / hx-swap)
```

### Plugin / Extension / Customization — first-class concepts

Each tool in this stack has official extension mechanisms. AI agents and contributors should treat these as primary documentation, not advanced topics:

- **Bun** — plugin API (`Bun.plugin()`), macros, `bunfig.toml`, workspaces
- **Elysia** — `.use()` for plugins; official plugins: `bearer`, `cors`, `cron`, `html`, `jwt`, `openapi`, `opentelemetry`, `server-timing`, `static`; large community plugin ecosystem
- **htmx** — `htmx.defineExtension()` with hooks: `init`, `getSelectors`, `onEvent`, `transformResponse`, `isInlineSwap`, `handleSwap`, `encodeParameters`; see `htmx/llms.txt` § Core Extensions and § Community Extensions
- **Prisma** — `$extends` client extensions: `client`, `model`, `query`, `result` component types; shared extension patterns
- **Tailwind CSS** — `@apply`, `@plugin`, `@utility`, `@variant`, `@custom-variant`, `@reference`
- **daisyUI** — CSS plugin configured in `tailwind.config`; custom themes via `daisyui.themes`; component-level overrides
- **EasyAuth** — auth integration layer; session token validation in Elysia `beforeHandle`; `HX-Redirect` for htmx unauthenticated flows

## Using This Repository with AI Tools

### GitHub Copilot (VS Code)

Reference a file directly in your prompt with `#fetch`:

```
#fetch https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/htmx/llms.txt
```

### Claude / ChatGPT

Paste the raw URL in your message, or download and attach the file:

```
Read this documentation index: https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/elysiajs/llms.txt
```

### Cursor / Windsurf / Cline

Add to your project's context or rules directory. Example `.cursorrules`:

```
Documentation context:
- https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/bun/llms.txt
- https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/elysiajs/llms.txt
- https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/easy-auth/llms.txt
- https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/prisma/llms.txt
- https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/htmx/llms.txt
- https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/tailwindcss/llms.txt
- https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/daisyui/llms.txt
```

### GitHub Copilot Instructions File

Place in `.github/copilot-instructions.md` to always include as context:

```markdown
## External Documentation

When working with this project, reference these llms.txt files:
- [Bun](https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/bun/llms.txt)
- [ElysiaJS](https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/elysiajs/llms.txt)
- [EasyAuth](https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/easy-auth/llms.txt)
- [htmx](https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/htmx/llms.txt)
- [Tailwind CSS](https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/tailwindcss/llms.txt)
- [daisyUI](https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/daisyui/llms.txt)
- [Prisma](https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/prisma/llms.txt)
```

### Local Development

Clone and reference files locally:

```bash
git clone https://github.com/d4551/llms-stack-refresh.git
# Files are in: bun/, daisyui/, easy-auth/, elysiajs/, htmx/, prisma/, tailwindcss/
```

## Raw File URLs

Direct links for use in AI tools:

| Technology | Raw URL |
|-----------|---------|
| Bun | `https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/bun/llms.txt` |
| daisyUI | `https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/daisyui/llms.txt` |
| EasyAuth | `https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/easy-auth/llms.txt` |
| ElysiaJS | `https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/elysiajs/llms.txt` |
| htmx | `https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/htmx/llms.txt` |
| Prisma | `https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/prisma/llms.txt` |
| Tailwind CSS | `https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/tailwindcss/llms.txt` |

## Contributing

See [`docs/CONTRIBUTING.md`](./docs/CONTRIBUTING.md) for full instructions. In brief:

1. Fork the repository.
2. Create a directory with the technology name (lowercase, hyphens for spaces).
3. Add `llms.txt` following the [llmstxt.org specification](https://llmstxt.org/).
4. Update `README.md` and `docs/INDEX.md` with the new entry.
5. Open a pull request with a clear description of the source used.

Sourcing priority: official `llms.txt` → official docs GitHub repo → official docs website. See [`docs/PROVENANCE.md`](./docs/PROVENANCE.md) for the full policy.

## Specification

For the full `llms.txt` specification, see [llmstxt.org](https://llmstxt.org/).

