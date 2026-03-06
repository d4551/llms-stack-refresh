# llms-stack-refresh

> Purpose: Curated `llms.txt` documentation index for the Bun/Elysia/htmx/Prisma/Tailwind/daisyUI/Better Auth stack. Optimised for AI agent context ingestion.

Each file is sourced from official documentation or curated from official primary-source documentation where no official file exists. Format spec: [llmstxt.org](https://llmstxt.org/).

## Repository Map

```
llms-stack-refresh/
├── README.md             Repository overview and agent context routing
├── AGENTS.md             AI agent navigation rules and per-stack guidance
├── CLAUDE.md             Anthropic Claude / Claude Code auto-discovery file
├── CODEX.md              OpenAI Codex auto-discovery file
├── bun/llms.txt          Official Bun docs (runtime, bundler, plugins, macros, workspaces)
├── daisyui/llms.txt      Official daisyUI docs (components, themes, plugin config)
├── better-auth/llms.txt  Better Auth docs (auth library, OAuth, sessions, plugins, Bun/Elysia integration)
├── elysiajs/llms.txt     Curated ElysiaJS docs (routes, lifecycle, plugins, Eden)
├── htmx/llms.txt         Curated htmx docs (attributes, headers, extensions)
├── prisma/llms.txt       Curated Prisma docs (schema, client, migrate, $extends)
├── tailwindcss/llms.txt  Curated Tailwind CSS docs (utilities, @apply, @plugin, @utility)
├── .github/
│   └── copilot-instructions.md  GitHub Copilot auto-discovery file
├── .cursor/
│   └── rules/llms-stack.mdc     Cursor rules file
├── .clinerules           Cline auto-discovery file
├── .windsurfrules        Windsurf/Codeium auto-discovery file
└── docs/
    ├── INDEX.md          Canonical navigation map grouped by role
    ├── PROVENANCE.md     Sourcing and provenance policy
    ├── EXTENSIONS.md     Deep-dive reference for every tool's plugin/extension system
    └── IDE-SETUP.md      Setup directives for every major AI coding tool and IDE
```

## Included Files

| Technology | File | Provenance | Notes |
|------------|------|------------|-------|
| [Bun](./bun/llms.txt) | `bun/llms.txt` | **Official** — https://bun.sh/llms.txt | All-in-one JS/TS runtime, bundler, test runner, package manager; plugin API, macros, workspaces |
| [daisyUI](./daisyui/llms.txt) | `daisyui/llms.txt` | **Official** — https://daisyui.com/llms.txt | Tailwind CSS component library (v5); themes, plugin config, component rules |
| [Better Auth](./better-auth/llms.txt) | `better-auth/llms.txt` | Curated — https://better-auth.com/docs | TypeScript auth library; OAuth providers, sessions, plugins, Bun/Elysia/htmx integration |
| [ElysiaJS](./elysiajs/llms.txt) | `elysiajs/llms.txt` | Curated — https://elysiajs.com | TypeScript web framework for Bun; routes, validation, lifecycle, plugins (`bearer`, `cors`, `jwt`), Eden E2E type safety |
| [htmx](./htmx/llms.txt) | `htmx/llms.txt` | Curated — https://htmx.org | HTML-first AJAX library; full `hx-*` attribute reference, response headers, extensions, extension building |
| [Prisma](./prisma/llms.txt) | `prisma/llms.txt` | Curated — https://www.prisma.io/docs | Node.js/TypeScript ORM; schema, client, migrate, platform, `$extends` client extensions |
| [Tailwind CSS](./tailwindcss/llms.txt) | `tailwindcss/llms.txt` | Curated — https://tailwindcss.com/docs | Utility-first CSS framework; utilities, config, `@apply`, `@plugin`, `@utility`, `@variant`, `@custom-variant` |

> **Note on Tailwind CSS**: Tailwind Labs has not officially published an `llms.txt` file ([see discussion](https://github.com/tailwindlabs/tailwindcss/discussions/18256)). The file here is curated from the official documentation source.
>
> **Note on Better Auth**: No official `llms.txt` was published by Better Auth. `better-auth/llms.txt` is curated from the official Better Auth documentation at https://better-auth.com/docs/.

## Stack Composition

These tools are commonly combined as a full-stack TypeScript/Bun workflow:

| Layer | Tool | Role |
|-------|------|------|
| Runtime / backend | Bun + Elysia | Fast HTTP server with E2E type safety |
| Auth | Better Auth | TypeScript auth library with OAuth, sessions, and plugins |
| Hypermedia UI | htmx | Server-driven UI without a JS framework |
| Data / ORM | Prisma | Type-safe database access and migrations |
| Styling | Tailwind CSS + daisyUI | Utility classes with pre-built components |

### Typical request flow

```
Browser (htmx attributes)
  -> Elysia route handler (Bun)
      -> Better Auth session validation (beforeHandle hook)
      -> Prisma query (type-safe, $extends for custom logic)
  -> Server renders HTML partial (Tailwind CSS + daisyUI classes)
Browser swaps partial into DOM (hx-target / hx-swap)
```

## Plugin / Extension / Customization

Each tool in this stack has official extension mechanisms. Treat these as primary documentation, not advanced topics. The full deep-dive reference is in [`docs/EXTENSIONS.md`](./docs/EXTENSIONS.md).

### Bun -- Plugin API

- **Entry point**: `Bun.plugin()` at runtime, or `plugins` array in `bunfig.toml` for bundler-level registration
- **What it does**: Register custom loaders and module resolution logic for the Bun bundler and runtime. Plugins intercept `import` statements for custom file types.
- **Key concepts**: `setup(build)` callback, `build.onLoad()`, `build.onResolve()`, namespaces, virtual modules
- **Additional mechanisms**: Macros (`import { myMacro } from "module" with { type: "macro" }`) run JavaScript at bundle-time. Workspaces (`workspaces` in `package.json`) manage monorepos.
- **Configuration file**: `bunfig.toml` for bundler-level plugin registration
- **Reference in this repo**: `bun/llms.txt` -- see Plugins and Macros sections
- **Upstream docs**: https://bun.sh/docs/bundler/plugins

### ElysiaJS -- Plugin System

- **Entry point**: `.use(plugin)` method on the Elysia app instance
- **What it does**: Compose Elysia instances together. Each plugin is an Elysia instance. Elysia deduplicates plugins by reference.
- **Official plugins**: `@elysiajs/bearer`, `@elysiajs/cors`, `@elysiajs/cron`, `@elysiajs/html`, `@elysiajs/jwt`, `@elysiajs/openapi`, `@elysiajs/opentelemetry`, `@elysiajs/server-timing`, `@elysiajs/static`
- **Key concepts**: Plugin deduplication by reference, `.macro()` for reusable lifecycle logic, scoped vs global plugins
- **Community ecosystem**: https://elysiajs.com/plugins/overview
- **Reference in this repo**: `elysiajs/llms.txt` -- see Plugins section
- **Upstream docs**: https://elysiajs.com/essential/plugin

### htmx -- Extension System

- **Entry point**: `htmx.defineExtension(name, extensionObject)` in JavaScript
- **Activation**: `hx-ext="extension-name"` attribute on an HTML element
- **What it does**: Add new behaviors to htmx by implementing one or more hook functions.
- **Hooks**: `init`, `getSelectors`, `onEvent`, `transformResponse`, `isInlineSwap`, `handleSwap`, `encodeParameters`
- **Core extensions**: `head-support`, `idiomorph`, `preload`, `response-targets`, `sse`, `ws`
- **Community extensions**: listed at https://htmx.org/extensions/
- **Reference in this repo**: `htmx/llms.txt` -- see Core Extensions and Community Extensions sections
- **Upstream docs**: https://htmx.org/extensions/building/

### Prisma -- Client Extensions

- **Entry point**: `prisma.$extends(extensionObject)` on the PrismaClient instance
- **What it does**: Add custom methods, fields, queries, and client-level logic without modifying generated client code.
- **Extension component types**: `client` (top-level methods), `model` (model-level methods), `query` (intercept queries), `result` (computed fields)
- **Key patterns**: Shared reusable extensions, observability/tracing integration, soft-delete patterns
- **Reference in this repo**: `prisma/llms.txt` -- see Client Extensions section
- **Upstream docs**: https://www.prisma.io/docs/orm/prisma-client/client-extensions

### Tailwind CSS -- Customization Directives

- **Entry points**: `@plugin`, `@utility`, `@variant`, `@custom-variant`, `@apply`, `@reference` directives in CSS
- **What they do**: Extend Tailwind with custom utilities, variants, and plugin integrations directly in CSS (v4 CSS-first approach)
- **Key directive summary**:
  - `@plugin "package-name"` -- load a Tailwind plugin
  - `@utility name { ... }` -- define a custom utility class
  - `@variant name { ... }` -- define a custom variant
  - `@custom-variant name selector` -- define a variant from a CSS selector
  - `@apply class-list` -- apply Tailwind classes inside custom CSS rules
  - `@reference "path"` -- import theme tokens without generating CSS
  - `@theme { ... }` -- define design tokens (v4 CSS-first configuration)
- **Reference in this repo**: `tailwindcss/llms.txt` -- see Customization section
- **Upstream docs**: https://tailwindcss.com/docs/adding-custom-styles

### daisyUI -- Theme and Plugin Configuration

- **Entry point**: `@plugin "daisyui"` in CSS (v4), or `require("daisyui")` in `tailwind.config.js` (v3)
- **What it does**: Add pre-built component classes and a theming system on top of Tailwind CSS.
- **Theme configuration**: `daisyui.themes` array in config specifies active themes. Custom themes use CSS variable overrides.
- **Custom themes**: Define new themes via the `daisyui` config object with named color variables.
- **Component overrides**: Apply Tailwind utility classes alongside daisyUI component classes for per-instance customization.
- **Reference in this repo**: `daisyui/llms.txt` -- see Themes and Configuration sections
- **Upstream docs**: https://daisyui.com/docs/themes/

### Better Auth -- Plugin System and Auth Integration

- **Entry point**: `betterAuth()` configuration with `plugins` array; session validation via `auth.api.getSession()` in Elysia `beforeHandle` lifecycle hook
- **What it does**: Better Auth is a TypeScript authentication library with a real plugin system. It provides handlers for auth routes (sign-in, sign-up, OAuth callback, session) and a typed session validation API.
- **Key integration points**:
  - Mount `auth.handler` in Elysia to handle all auth routes at `/api/auth/*`
  - `auth.api.getSession({ headers })` in `beforeHandle` hook for session validation
  - `HX-Redirect` response header for htmx unauthenticated redirect flows
  - `prismaAdapter` from `better-auth/adapters/prisma` for database integration
- **Plugin system**: Pass plugins to the `plugins` array in `betterAuth()`. Official plugins include `organization()`, `twoFactor()`, `passkey()`, `magicLink()`, `admin()`, `username()`, `bearer()`
- **Reference in this repo**: `better-auth/llms.txt` -- see Plugins and Integration Patterns sections
- **Upstream docs**: https://better-auth.com/docs

## AI Coding Tool Integration

For full setup directives per tool, see [`docs/IDE-SETUP.md`](./docs/IDE-SETUP.md). Quick reference below.

### GitHub Copilot in VS Code

Use `#fetch` in Copilot Chat to pull in an `llms.txt` file:

```
#fetch https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/htmx/llms.txt
How do I use htmx extensions?
```

Place `.github/copilot-instructions.md` in your project to auto-include context:

```markdown
## External Documentation

When working with this project, reference these llms.txt files:
- [Bun](https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/bun/llms.txt)
- [ElysiaJS](https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/elysiajs/llms.txt)
- [Better Auth](https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/better-auth/llms.txt)
- [htmx](https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/htmx/llms.txt)
- [Tailwind CSS](https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/tailwindcss/llms.txt)
- [daisyUI](https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/daisyui/llms.txt)
- [Prisma](https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/prisma/llms.txt)
```

### GitHub Copilot in JetBrains IDEs

Open Copilot Chat and attach a file URL as context using the chat input. Paste the raw URL directly into the chat message. Plugin-based context attachment is more limited than VS Code; use the `copilot-instructions.md` approach instead.

### Cursor

Add documentation context via `.cursor/rules/` directory (preferred over deprecated `.cursorrules`). Create `.cursor/rules/llms-stack.mdc`:

```markdown
---
description: Documentation context for the Bun/Elysia/htmx/Prisma/Tailwind/daisyUI stack
globs: ["**/*.ts", "**/*.html", "**/*.css"]
---

Reference these documentation files when working on this stack:
- https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/bun/llms.txt
- https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/elysiajs/llms.txt
- https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/htmx/llms.txt
- https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/prisma/llms.txt
- https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/tailwindcss/llms.txt
- https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/daisyui/llms.txt
- https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/better-auth/llms.txt
```

Use `@docs` in Cursor Chat to reference documentation, or `@web` with a raw GitHub URL.

### Windsurf (Codeium)

Configure Windsurf memory or rules to include the raw URLs. In Cascade (Windsurf's agentic flow), paste a raw URL into the chat to include it as context. Attach files directly in Windsurf Chat via the attach button.

### Cline (VS Code extension)

Create a `.clinerules` file at the project root:

```markdown
## Documentation Context

When working on this project, fetch and read these documentation files:
- https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/bun/llms.txt
- https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/elysiajs/llms.txt
- https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/htmx/llms.txt
```

Use `@url` in Cline chat to fetch a remote documentation file on demand.

### Claude (via API or claude.ai)

Paste a raw URL directly into the message, or attach a downloaded `llms.txt` file. Use Claude Projects to upload documentation files as persistent project knowledge. System prompt pattern:

```
Read the following documentation index before answering:
https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/elysiajs/llms.txt
```

### ChatGPT / OpenAI

Paste a raw URL into the chat message. For Custom GPTs, upload `llms.txt` files as knowledge files in the GPT configuration. Use Code Interpreter with attached files for offline access.

### Aider

Use `--read` to add files as read-only context:

```bash
aider --read https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/bun/llms.txt
```

Configure `.aider.conf.yml` to always include documentation (requires a local clone; replace the path with the actual path on your machine):

```yaml
read:
  - /path/to/llms-stack-refresh/bun/llms.txt
  - /path/to/llms-stack-refresh/elysiajs/llms.txt
```

### Continue (VS Code / JetBrains extension)

Configure `.continue/config.json` with a docs context provider:

```json
{
  "contextProviders": [
    {
      "name": "url",
      "params": {
        "urls": [
          "https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/bun/llms.txt",
          "https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/elysiajs/llms.txt"
        ]
      }
    }
  ]
}
```

Use `@docs` in Continue Chat to reference a configured documentation source.

### Zed AI

Use the `/file` command in Zed's assistant panel to include a local `llms.txt` file as context. Clone the repository locally and reference files by path.

### Local Development (general)

Clone and reference files locally:

```bash
git clone https://github.com/d4551/llms-stack-refresh.git
# Files are in: bun/, daisyui/, better-auth/, elysiajs/, htmx/, prisma/, tailwindcss/
```

Symlink into a project:

```bash
ln -s /path/to/llms-stack-refresh/bun/llms.txt ./docs/bun-llms.txt
```

Pass file contents to any local LLM (Ollama, LM Studio, etc.):

```bash
cat bun/llms.txt | ollama run llama3 "Using this documentation, how do I write a Bun plugin?"
```

## Raw File URLs

Direct links for use in AI tools:

| Technology | Raw URL |
|------------|---------|
| Bun | `https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/bun/llms.txt` |
| daisyUI | `https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/daisyui/llms.txt` |
| Better Auth | `https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/better-auth/llms.txt` |
| ElysiaJS | `https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/elysiajs/llms.txt` |
| htmx | `https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/htmx/llms.txt` |
| Prisma | `https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/prisma/llms.txt` |
| Tailwind CSS | `https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/tailwindcss/llms.txt` |

## Contributing

See [`docs/PROVENANCE.md`](./docs/PROVENANCE.md) for sourcing rules. Format spec: [llmstxt.org](https://llmstxt.org/).

