# AGENTS.md — AI Agent Navigation Guide

This file tells AI agents and automated tools how to navigate, use, and contribute to this repository correctly.

## Repository Purpose

`llms-stack-refresh` is a curated collection of `llms.txt` files for the tools in a modern full-stack TypeScript/Bun development workflow. Each file is either official (published by the project itself) or curated from official primary-source documentation. The files are intended to be consumed by AI coding assistants as context documents.

## Stable Directory Structure

```
llms-stack-refresh/
├── README.md            # Human and AI entry point; repo overview
├── AGENTS.md            # This file — AI agent instructions
├── bun/llms.txt         # Official Bun docs index
├── daisyui/llms.txt     # Official daisyUI docs index
├── easy-auth/llms.txt   # Curated EasyAuth docs index (no official file exists)
├── elysiajs/llms.txt    # Curated ElysiaJS docs index
├── htmx/llms.txt        # Curated htmx docs index
├── prisma/llms.txt      # Curated Prisma docs index
├── tailwindcss/llms.txt # Curated Tailwind CSS docs index
└── docs/
    ├── INDEX.md         # Canonical navigation map
    ├── CONTRIBUTING.md  # Contribution guide
    └── PROVENANCE.md    # Provenance policy
```

**Do not rename or move existing directories.** The raw GitHub URLs for each `llms.txt` are used directly by AI tools and users; changing paths breaks those references.

## Rules for AI Agents

### Reading docs

- Start at `README.md` for an overview and usage instructions.
- Use `docs/INDEX.md` to find the correct `llms.txt` file for a given technology.
- Each `llms.txt` is self-contained. Consume the whole file when the tech is relevant to the task.

### Editing or adding docs

1. **Preserve provenance.** Every `llms.txt` must include a clear source (official URL or the note "curated from official docs at …"). Never invent content — trace every item to its source URL.
2. **Prefer official `llms.txt`.** If a project publishes an official `llms.txt`, use it verbatim or as the primary source. Do not override official content with curated content.
3. **Follow the llmstxt.org format.** Structure: H1 title → blockquote summary → short intro paragraph → `##` sections → optional `## Optional` section.
4. **Plugin/extension/customization sections are first-class.** When a stack has official plugin or extension mechanisms, these must appear as dedicated sections (not buried in other sections). See the guidance per stack below.
5. **Low ambiguity.** Prefer exact method names, attribute names, and file paths over vague descriptions. Agents rely on precise identifiers.
6. **Keep the `## Optional` section.** Secondary resources that can be dropped in short-context windows belong there.
7. **Update `docs/INDEX.md` and `README.md`** when adding a new stack directory.

### Plugin and extension guidance by stack

#### Bun (`bun/llms.txt`)
- Include coverage of the plugin API, macros, workspaces, and `bunfig.toml`.
- Keep bundler, runtime, test runner, and package manager workflows distinct.

#### Elysia (`elysiajs/llms.txt`)
- The `## Plugins` section must list official plugins (`bearer`, `cors`, `cron`, `html`, `jwt`, `openapi`, `opentelemetry`, `server-timing`, `static`) with install commands.
- Note the community plugin ecosystem in the plugin overview link.
- The `.use()` method and plugin deduplication behavior should be documented.

#### htmx (`htmx/llms.txt`)
- The `## Core Extensions` and `## Community Extensions` sections must be present.
- Document extension building via `htmx.defineExtension()` and the hooks: `init`, `getSelectors`, `onEvent`, `transformResponse`, `isInlineSwap`, `handleSwap`, `encodeParameters`.
- Link to the [Building Extensions](https://htmx.org/extensions/building/) page.

#### Prisma (`prisma/llms.txt`)
- The Client Extensions section must cover `$extends` with all four extension types: `client`, `model`, `query`, `result`.
- Include shared/reusable extension patterns and the observability/tracing integration notes.

#### Tailwind CSS (`tailwindcss/llms.txt`)
- A customization section must cover the key directives and functions: `@apply`, `@plugin`, `@utility`, `@variant`, `@custom-variant`, `@reference`.
- These are the primary extension/customization mechanisms — do not omit them.

#### daisyUI (`daisyui/llms.txt`)
- Include theme configuration, custom theme generation, and CSS plugin configuration.
- Component usage rules and install/config guidance must be present.

#### EasyAuth (`easy-auth/llms.txt`)
- Document EasyAuth primarily as an auth integration layer, not a full framework.
- Do not overstate capabilities beyond what official docs support.
- Include integration patterns showing how EasyAuth fits with Bun/Elysia/Prisma/htmx.

## What AI Agents Should NOT Do

- Do not add speculative content not grounded in official documentation.
- Do not remove or rename existing top-level stack directories.
- Do not change the `llmstxt.org`-compliant format of any `llms.txt` file.
- Do not commit secrets, credentials, or environment-specific configuration.
- Do not create new top-level directories without updating `README.md` and `docs/INDEX.md`.
