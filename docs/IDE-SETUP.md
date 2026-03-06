# IDE and AI Coding Tool Setup

Setup directives for using this repository's `llms.txt` files with every major AI coding tool and IDE. Consume the relevant section to configure context for the Bun/Elysia/htmx/Prisma/Tailwind/daisyUI/Better Auth stack.

All raw file URLs follow this pattern:

```
https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/<tool>/llms.txt
```

Full URL table:

| Technology | Raw URL |
|------------|---------|
| Bun | `https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/bun/llms.txt` |
| ElysiaJS | `https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/elysiajs/llms.txt` |
| Better Auth | `https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/better-auth/llms.txt` |
| htmx | `https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/htmx/llms.txt` |
| Prisma | `https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/prisma/llms.txt` |
| Tailwind CSS | `https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/tailwindcss/llms.txt` |
| daisyUI | `https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/daisyui/llms.txt` |

---

## GitHub Copilot in VS Code

### Using `#fetch` in Copilot Chat

Type `#fetch` followed by a raw URL in the Copilot Chat input. Copilot fetches the URL and includes the content as context.

Example prompt:

```
#fetch https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/htmx/llms.txt
How do I use the htmx sse extension to receive server-sent events?
```

Fetch multiple files in one prompt:

```
#fetch https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/elysiajs/llms.txt
#fetch https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/htmx/llms.txt
Show me how to send an htmx partial response from an Elysia route.
```

### Auto-including context with `copilot-instructions.md`

Create `.github/copilot-instructions.md` in your project root. Add a section listing the raw URLs. Copilot reads this file automatically on every chat session.

Example `.github/copilot-instructions.md`:

```markdown
## External Documentation

When working on this project, reference these documentation files for the technology stack:

- Bun runtime and bundler: https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/bun/llms.txt
- ElysiaJS web framework: https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/elysiajs/llms.txt
- Better Auth integration: https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/better-auth/llms.txt
- htmx hypermedia library: https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/htmx/llms.txt
- Tailwind CSS: https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/tailwindcss/llms.txt
- daisyUI component library: https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/daisyui/llms.txt
- Prisma ORM: https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/prisma/llms.txt

Always use the Bun runtime (not Node.js) and Elysia for HTTP handling.
Use htmx attributes for client-side interactivity instead of a JavaScript framework.
```

### Example prompts

```
#fetch https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/prisma/llms.txt
Create a Prisma $extends client extension that adds a softDelete method to all models.
```

```
#fetch https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/bun/llms.txt
Write a Bun plugin that loads YAML files as JavaScript objects.
```

---

## GitHub Copilot in JetBrains IDEs

### Using Copilot Chat in JetBrains

Install the GitHub Copilot plugin from JetBrains Marketplace. Paste a raw URL directly into the Copilot Chat input; Copilot fetches the URL and uses the content as context.

Example:

```
Read this documentation: https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/elysiajs/llms.txt
Now create an Elysia route that validates JWT tokens using the @elysiajs/jwt plugin.
```

### Limitations compared to VS Code

- The `#fetch` shorthand is not available in JetBrains; paste the full URL as plain text.
- The `copilot-instructions.md` file is honoured by Copilot in JetBrains from Copilot plugin version 1.5 and later.
- File attachment via the chat UI is not supported; use URL references instead.

Use the `copilot-instructions.md` file (same as VS Code) for persistent context at `.github/copilot-instructions.md`.

---

## Cursor

### Using `.cursor/rules/` directory

The `.cursor/rules/` directory is the recommended approach for persistent rules and context (`.cursorrules` is deprecated). Create a `.mdc` file (Markdown with YAML frontmatter).

Example `.cursor/rules/llms-stack.mdc`:

```markdown
---
description: Documentation context for the Bun/Elysia/htmx/Prisma/Tailwind/daisyUI stack
globs:
  - "**/*.ts"
  - "**/*.tsx"
  - "**/*.html"
  - "**/*.css"
alwaysApply: false
---

## Stack Documentation

When generating or reviewing code for this project, fetch and read the relevant documentation files:

- Bun: https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/bun/llms.txt
- ElysiaJS: https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/elysiajs/llms.txt
- Better Auth: https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/better-auth/llms.txt
- htmx: https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/htmx/llms.txt
- Prisma: https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/prisma/llms.txt
- Tailwind CSS: https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/tailwindcss/llms.txt
- daisyUI: https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/daisyui/llms.txt

## Conventions

- Use Bun (not Node.js) as the runtime.
- Use Elysia for all HTTP routing.
- Use htmx attributes for interactivity. Do not add a JavaScript framework.
- Use Prisma for database access.
- Use Tailwind CSS and daisyUI for styling.
```

### Using `@docs` in Cursor Chat

Type `@docs` in Cursor Chat to open the documentation picker. Add a documentation source by URL if not already added.

### Using `@web` with raw GitHub URLs

In Cursor Chat, type `@web` followed by a raw URL to fetch and include the file as context:

```
@web https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/bun/llms.txt
How do I register a Bun plugin for loading SVG files?
```

---

## Windsurf (Codeium)

### Configuring Windsurf rules

Add a rule in the Windsurf settings (Rules or Memory section) listing the raw documentation URLs:

```
When working on this project, reference the following documentation files for context:
- https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/bun/llms.txt
- https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/elysiajs/llms.txt
- https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/htmx/llms.txt
- https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/prisma/llms.txt
- https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/tailwindcss/llms.txt
- https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/daisyui/llms.txt
- https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/better-auth/llms.txt
```

### Using Cascade with documentation context

In Cascade (Windsurf's agentic chat panel), paste a raw URL directly into the chat input. Cascade fetches the file.

Example:

```
Fetch this file and use it as context: https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/elysiajs/llms.txt
Create an Elysia application with JWT authentication and a protected route.
```

### Attaching files in Windsurf Chat

Click the attachment icon in the Windsurf Chat input and select a locally cloned `llms.txt` file. The file contents are included as context for the current chat session.

---

## Cline (VS Code extension)

### Creating a `.clinerules` file

Create `.clinerules` at the project root with documentation instructions. Cline reads this file automatically when a task starts.

Example `.clinerules`:

```markdown
## Documentation Context

When working on this project, fetch and read the following documentation files before answering:

- Bun: https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/bun/llms.txt
- ElysiaJS: https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/elysiajs/llms.txt
- htmx: https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/htmx/llms.txt
- Prisma: https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/prisma/llms.txt
- Tailwind CSS: https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/tailwindcss/llms.txt
- daisyUI: https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/daisyui/llms.txt
- Better Auth: https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/better-auth/llms.txt

## Stack Conventions

- Runtime: Bun
- HTTP framework: Elysia
- Database ORM: Prisma
- UI interactivity: htmx (no JavaScript framework)
- Styling: Tailwind CSS + daisyUI
- Auth: Better Auth
```

Cline reads `.clinerules` automatically when a task starts in that workspace.

### Using `@url` in Cline chat

In the Cline chat input, use `@url` to fetch a remote file on demand:

```
@url https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/prisma/llms.txt
Create a Prisma schema for a blog application with users and posts.
```

### Configuring custom instructions

In VS Code settings, search for "Cline: Custom Instructions". Add the documentation URLs and stack conventions as persistent instructions.

---

## Claude (via API or claude.ai)

### Pasting raw URLs

Paste a raw URL directly into the Claude message input. Claude fetches the URL and includes the content as context.

```
Read this documentation file: https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/htmx/llms.txt

Now explain how to build a custom htmx extension that adds a loading spinner during requests.
```

### Attaching downloaded files

Download the `llms.txt` file and attach it using the attachment button in claude.ai.

### Using Claude Projects

Upload `llms.txt` files to a Project's knowledge base. All conversations in the Project will have access to the uploaded files.

Recommended files to upload for this stack:

- `bun/llms.txt`
- `elysiajs/llms.txt`
- `htmx/llms.txt`
- `prisma/llms.txt`
- `tailwindcss/llms.txt`
- `daisyui/llms.txt`
- `better-auth/llms.txt`

### System prompt pattern for API usage

```
You are a TypeScript full-stack developer using the Bun/Elysia/htmx/Prisma/Tailwind CSS/daisyUI stack.

The following documentation indexes are provided as context. Read each one before answering.

<bun_docs>
[contents of bun/llms.txt]
</bun_docs>

<elysia_docs>
[contents of elysiajs/llms.txt]
</elysia_docs>

[... continue for each tool ...]
```

---

## ChatGPT / OpenAI

### Pasting raw URLs

Paste a raw GitHub URL into the ChatGPT message input. ChatGPT will browse to the URL if browsing is enabled.

```
Read this file: https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/elysiajs/llms.txt
Then create an Elysia server with a /users route that returns JSON.
```

Note: URL browsing availability depends on the ChatGPT model and configuration.

### Using Custom GPTs with uploaded knowledge files

In the ChatGPT GPT editor, upload `llms.txt` files in the "Knowledge" section. Set instructions to reference the uploaded files when answering stack-related questions.

Example GPT instructions:

```
You are a full-stack TypeScript developer assistant specializing in the Bun/Elysia/htmx/Prisma/Tailwind/daisyUI stack.

When users ask about any of these technologies, refer to the uploaded documentation files for accurate API details.
```

### Using Code Interpreter with attached files

Enable the Code Interpreter tool and attach a `llms.txt` file using the attachment button. ChatGPT can read the file content and use it in its response.

---

## Aider

### Using `--read` flag

Add a `llms.txt` file as read-only context. Aider includes the file in the LLM context but does not allow the LLM to edit it.

```bash
aider --read bun/llms.txt src/server.ts
```

Pass multiple files:

```bash
aider \
  --read bun/llms.txt \
  --read elysiajs/llms.txt \
  --read htmx/llms.txt \
  src/server.ts src/routes.ts
```

### Configuring `.aider.conf.yml`

Create `.aider.conf.yml` at the project root to always include documentation files:

```yaml
read:
  - /path/to/llms-stack-refresh/bun/llms.txt
  - /path/to/llms-stack-refresh/elysiajs/llms.txt
  - /path/to/llms-stack-refresh/htmx/llms.txt
  - /path/to/llms-stack-refresh/prisma/llms.txt
  - /path/to/llms-stack-refresh/tailwindcss/llms.txt
  - /path/to/llms-stack-refresh/daisyui/llms.txt
  - /path/to/llms-stack-refresh/better-auth/llms.txt
```

Replace `/path/to/llms-stack-refresh/` with the actual path to your local clone of this repository.

### Example aider commands

```bash
# Ask a question with documentation context
aider --read bun/llms.txt --message "How do I write a Bun plugin that loads .env files?"

# Edit a file with documentation context
aider --read elysiajs/llms.txt src/app.ts
```

---

## Continue (VS Code / JetBrains extension)

### Configuring `.continue/config.json`

Create or edit `.continue/config.json` in your project root. Add a `contextProviders` entry with a `url` provider listing the raw URLs.

Example `.continue/config.json`:

```json
{
  "models": [],
  "contextProviders": [
    {
      "name": "url",
      "params": {
        "urls": [
          "https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/bun/llms.txt",
          "https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/elysiajs/llms.txt",
          "https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/htmx/llms.txt",
          "https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/prisma/llms.txt",
          "https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/tailwindcss/llms.txt",
          "https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/daisyui/llms.txt",
          "https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/better-auth/llms.txt"
        ]
      }
    }
  ]
}
```

### Using `@docs` context provider

In Continue Chat, type `@docs` to open the documentation picker and select a configured URL context provider.

### Setting up custom slash commands

Add a custom slash command in `.continue/config.json` that references the stack documentation:

```json
{
  "slashCommands": [
    {
      "name": "stack-docs",
      "description": "Include full stack documentation as context",
      "prompt": "I am working on a Bun/Elysia/htmx/Prisma/Tailwind/daisyUI project. The documentation for each tool is available at these URLs: [list URLs]. Please fetch and read the relevant documentation before answering."
    }
  ]
}
```

---

## Zed AI

### Using the `/file` command

Clone this repository locally. In the Zed AI assistant panel, type `/file` followed by the path to a local `llms.txt` file.

Example:

```
/file /path/to/llms-stack-refresh/htmx/llms.txt
Explain how to use the htmx response-targets extension.
```

### Configuring Zed assistant context

In Zed settings, navigate to the `assistant` section. Add a `default_context` or similar setting pointing to local documentation files.

Note: Zed's assistant configuration evolves rapidly. Check https://zed.dev/docs/assistant for the latest approach.

---

## Local Development (general)

### Cloning the repository

```bash
git clone https://github.com/d4551/llms-stack-refresh.git
cd llms-stack-refresh
```

Files are in: `bun/`, `daisyui/`, `better-auth/`, `elysiajs/`, `htmx/`, `prisma/`, `tailwindcss/`

### Symlinking files into a project

Create a symlink from a project's docs directory to a specific `llms.txt` file:

```bash
mkdir -p my-project/docs/llms
ln -s /path/to/llms-stack-refresh/bun/llms.txt my-project/docs/llms/bun.txt
ln -s /path/to/llms-stack-refresh/elysiajs/llms.txt my-project/docs/llms/elysiajs.txt
ln -s /path/to/llms-stack-refresh/htmx/llms.txt my-project/docs/llms/htmx.txt
```

### Using with any local LLM (Ollama, LM Studio, etc.)

Pass file contents directly to a local model via the command line:

```bash
# Single file
cat bun/llms.txt | ollama run llama3 "Using this documentation, how do I write a Bun plugin?"

# Multiple files concatenated
cat elysiajs/llms.txt htmx/llms.txt | ollama run llama3 "How do I return an htmx partial from an Elysia route?"
```

Use the OpenAI-compatible API to include file contents in a system message:

```bash
curl http://localhost:11434/v1/chat/completions \
  -H "Content-Type: application/json" \
  -d "{
    \"model\": \"llama3\",
    \"messages\": [
      {
        \"role\": \"system\",
        \"content\": \"$(cat elysiajs/llms.txt)\"
      },
      {
        \"role\": \"user\",
        \"content\": \"How do I add CORS to an Elysia app?\"
      }
    ]
  }"
```

### Keeping files up to date

Pull the latest documentation updates:

```bash
cd llms-stack-refresh
git pull origin main
```
