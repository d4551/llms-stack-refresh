# llms-stack-refresh

A collection of `llms.txt` files for popular developer tools and frameworks, making their documentation accessible to AI coding assistants and LLMs.

## What is llms.txt?

[`llms.txt`](https://llmstxt.org/) is a proposed standard for providing LLM-friendly documentation. Similar to `robots.txt`, it sits at the root of a project's documentation and provides a structured, Markdown-based summary of key documentation links that AI tools can easily consume.

## Included llms.txt Files

| Technology | Source | Description |
|-----------|--------|-------------|
| [Bun](./bun/llms.txt) | https://bun.sh/llms.txt | All-in-one JavaScript/TypeScript toolkit and runtime |
| [daisyUI](./daisyui/llms.txt) | https://daisyui.com/llms.txt | Tailwind CSS component library |
| [ElysiaJS](./elysiajs/llms.txt) | https://elysiajs.com/llms.txt | TypeScript web framework for Bun |
| [htmx](./htmx/llms.txt) | Custom (from https://htmx.org/extensions/) | HTML-first AJAX and dynamic UI library |
| [Prisma](./prisma/llms.txt) | https://www.prisma.io/docs/llms.txt | TypeScript ORM for Node.js |

## Usage

You can use these files with AI coding assistants by referencing them directly. For example, in VS Code with GitHub Copilot:

```
#fetch https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/bun/llms.txt
```

Or download them for use in your project's `.github/instructions/` directory.
