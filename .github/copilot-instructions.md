# GitHub Copilot Instructions

## Stack

This project uses the Bun/Elysia/htmx/Prisma/Tailwind CSS/daisyUI/EasyAuth stack.

| Layer | Tool | Role |
|-------|------|------|
| Runtime / backend | Bun + Elysia | Fast HTTP server with E2E type safety |
| Auth | EasyAuth | Managed OAuth / session layer |
| Hypermedia UI | htmx | Server-driven UI without a JS framework |
| Data / ORM | Prisma | Type-safe database access and migrations |
| Styling | Tailwind CSS + daisyUI | Utility classes with pre-built components |

## Conventions

- Use Bun (not Node.js) as the runtime.
- Use Elysia for all HTTP routing.
- Use htmx attributes for interactivity. Do not add a JavaScript framework.
- Use Prisma for database access.
- Use Tailwind CSS and daisyUI for styling.
- Use EasyAuth for authentication.

## External Documentation

When working on this project or any project using this stack, fetch and reference these documentation files:

- Bun runtime and bundler: https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/bun/llms.txt
- ElysiaJS web framework: https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/elysiajs/llms.txt
- EasyAuth integration: https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/easy-auth/llms.txt
- htmx hypermedia library: https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/htmx/llms.txt
- Tailwind CSS: https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/tailwindcss/llms.txt
- daisyUI component library: https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/daisyui/llms.txt
- Prisma ORM: https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/prisma/llms.txt
- Plugin/extension systems: https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/docs/EXTENSIONS.md
