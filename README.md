# llms-stack-refresh

A curated collection of `llms.txt` files for popular developer tools and frameworks — sourced from official documentation or hand-crafted where no official file exists — making documentation readily accessible to AI coding assistants and LLMs.

## What is llms.txt?

[`llms.txt`](https://llmstxt.org/) is a proposed standard for providing LLM-friendly documentation. Similar to `robots.txt`, it sits at the root of a project's documentation and provides a structured, Markdown-based index of key documentation links that AI tools can efficiently consume.

The format follows a simple structure:
- **H1 title** — the project name
- **Blockquote** — a one-sentence description
- **Sections** (`##`) — topic groups with Markdown links and optional descriptions
- **Optional section** — secondary resources that can be omitted in short-context scenarios

## Included Files

| Technology | File | Source | Notes |
|-----------|------|--------|-------|
| 🍞 [Bun](./bun/llms.txt) | `bun/llms.txt` | https://bun.sh/llms.txt | Official — all-in-one JS/TS runtime, bundler, test runner, package manager |
| 🌼 [daisyUI](./daisyui/llms.txt) | `daisyui/llms.txt` | https://daisyui.com/llms.txt | Official — Tailwind CSS component library (v5) |
| ✨ [ElysiaJS](./elysiajs/llms.txt) | `elysiajs/llms.txt` | Custom (from [elysiajs/documentation](https://github.com/elysiajs/documentation)) | TypeScript web framework for Bun with E2E type safety |
| 🟦 [htmx](./htmx/llms.txt) | `htmx/llms.txt` | Custom (from [bigskysoftware/htmx](https://github.com/bigskysoftware/htmx)) | HTML-first AJAX library — full attribute & extension reference |
| 🔺 [Prisma](./prisma/llms.txt) | `prisma/llms.txt` | Custom (from [prisma.io/docs](https://www.prisma.io/docs)) | Node.js/TypeScript ORM — schema, client, migrate, platform |
| 🌬️ [Tailwind CSS](./tailwindcss/llms.txt) | `tailwindcss/llms.txt` | Custom (from [tailwindlabs/tailwindcss.com](https://github.com/tailwindlabs/tailwindcss.com)) | Utility-first CSS framework — all utility classes documented |

> **Note on Tailwind CSS**: Tailwind Labs has not officially published an `llms.txt` file ([see discussion](https://github.com/tailwindlabs/tailwindcss/discussions/18256)). The file here is community-authored from the official documentation source.

## Usage with AI Tools

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
- https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/prisma/llms.txt
```

### Local Development

Clone and reference files locally:

```bash
git clone https://github.com/d4551/llms-stack-refresh.git
# Files are in: bun/, daisyui/, elysiajs/, htmx/, prisma/, tailwindcss/
```

### GitHub Copilot Instructions File

Place in `.github/copilot-instructions.md` to always include as context:

```markdown
## External Documentation

When working with this project, reference these llms.txt files:
- [htmx](https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/htmx/llms.txt)
- [Tailwind CSS](https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/tailwindcss/llms.txt)
- [daisyUI](https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/daisyui/llms.txt)
```

## Raw File URLs

Direct links for use in AI tools:

| Technology | Raw URL |
|-----------|---------|
| Bun | `https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/bun/llms.txt` |
| daisyUI | `https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/daisyui/llms.txt` |
| ElysiaJS | `https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/elysiajs/llms.txt` |
| htmx | `https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/htmx/llms.txt` |
| Prisma | `https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/prisma/llms.txt` |
| Tailwind CSS | `https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/tailwindcss/llms.txt` |

## Contributing

Contributions are welcome! To add or improve an `llms.txt` file:

1. Fork the repository
2. Create a directory with the technology name (lowercase, no spaces)
3. Add `llms.txt` following the [llmstxt.org specification](https://llmstxt.org/)
4. Update this README with the new entry
5. Open a pull request

When sourcing content, prefer:
- Official `llms.txt` files published by the project
- The project's official documentation source on GitHub
- The official documentation website as a fallback

## Specification

For the full `llms.txt` specification, see [llmstxt.org](https://llmstxt.org/).

