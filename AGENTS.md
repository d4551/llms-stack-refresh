# AGENTS.md — AI Agent Navigation Guide

This file tells AI agents and automated tools how to navigate and use this repository.

## Routing

- IF agent is Anthropic Claude / Claude Code THEN also read `CLAUDE.md`
- IF agent is OpenAI Codex THEN also read `CODEX.md`
- IF agent is GitHub Copilot THEN also read `.github/copilot-instructions.md`
- IF agent is Cursor THEN also read `.cursor/rules/llms-stack.mdc`
- IF agent is Cline THEN also read `.clinerules`
- IF agent is Windsurf/Codeium THEN also read `.windsurfrules`
- IF agent is Aider THEN use `--read` flag with relevant `llms.txt` files
- FOR ALL agents: read `docs/INDEX.md` for file routing, `docs/EXTENSIONS.md` for plugin/extension APIs, `docs/IDE-SETUP.md` for tool-specific setup

## Repository Purpose

`llms-stack-refresh` is a curated collection of `llms.txt` files for the tools in a modern full-stack TypeScript/Bun development workflow. Each file is either official (published by the project itself) or curated from official primary-source documentation. The files are intended to be consumed by AI coding assistants as context documents.

## Stable Directory Structure

```
llms-stack-refresh/
├── README.md            # Repository overview and agent context routing
├── AGENTS.md            # This file — AI agent instructions
├── CLAUDE.md            # Anthropic Claude / Claude Code auto-discovery file
├── CODEX.md             # OpenAI Codex auto-discovery file
├── bun/llms.txt         # Official Bun docs index
├── daisyui/llms.txt     # Official daisyUI docs index
├── better-auth/llms.txt # Curated Better Auth docs index (no official file exists)
├── elysiajs/llms.txt    # Curated ElysiaJS docs index
├── htmx/llms.txt        # Curated htmx docs index
├── prisma/llms.txt      # Curated Prisma docs index
├── tailwindcss/llms.txt # Curated Tailwind CSS docs index
├── .github/
│   └── copilot-instructions.md  # GitHub Copilot auto-discovery file
├── .cursor/
│   └── rules/llms-stack.mdc     # Cursor rules file
├── .clinerules          # Cline auto-discovery file
├── .windsurfrules       # Windsurf/Codeium auto-discovery file
└── docs/
    ├── INDEX.md         # Canonical navigation map
    ├── PROVENANCE.md    # Provenance policy
    ├── EXTENSIONS.md    # Deep-dive reference for every tool's extension/plugin system
    └── IDE-SETUP.md     # Setup directives for every major AI coding tool and IDE
```

**Do not rename or move existing directories.** The raw GitHub URLs for each `llms.txt` are used directly by AI tools and users; changing paths breaks those references.

## Agent-Specific Instruction Files

| File | Agent | Auto-read behavior |
|------|-------|--------------------|
| `CLAUDE.md` | Anthropic Claude / Claude Code | Read automatically by Claude Code on project load |
| `CODEX.md` | OpenAI Codex | Read automatically by Codex on repo context load |
| `.github/copilot-instructions.md` | GitHub Copilot | Loaded automatically on every Copilot Chat session |
| `.cursor/rules/llms-stack.mdc` | Cursor | Applied when globs match (`**/*.ts`, `**/*.html`, `**/*.css`) |
| `.clinerules` | Cline | Read automatically when a task starts in the workspace |
| `.windsurfrules` | Windsurf/Codeium | Loaded as persistent rules for the workspace |

## Rules for AI Agents

### Reading docs

- Start at `README.md` for an overview and usage instructions.
- Use `docs/INDEX.md` to find the correct `llms.txt` file for a given technology.
- Each `llms.txt` is self-contained. Consume the whole file when the tech is relevant to the task.
- Consult `docs/EXTENSIONS.md` when a user asks about extending, customising, or adding plugins to any tool in the stack. This file contains the canonical deep-dive reference for every tool's plugin/extension/customization system, including exact API names, hook names, and configuration points.
- Consult `docs/IDE-SETUP.md` when a user asks how to configure an AI coding tool or IDE to use this repository's documentation as context.

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

#### Better Auth (`better-auth/llms.txt`)
- Document Better Auth as a TypeScript auth library with a real plugin system.
- Cover the `betterAuth()` server setup, `createAuthClient()` browser client, and `auth.api.getSession()` for session validation.
- Include integration patterns showing how Better Auth fits with Bun/Elysia/Prisma/htmx.

## What AI Agents Should NOT Do

- Do not add speculative content not grounded in official documentation.
- Do not remove or rename existing top-level stack directories.
- Do not change the `llmstxt.org`-compliant format of any `llms.txt` file.
- Do not commit secrets, credentials, or environment-specific configuration.
- Do not create new top-level directories without updating `README.md` and `docs/INDEX.md`.
- Do not add emojis to any file in this repository.
