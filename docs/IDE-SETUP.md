# IDE and AI Coding Tool Setup

Step-by-step instructions for using this repository's `llms.txt` files with every major AI coding tool and IDE. Each section covers how to include documentation context so the AI assistant understands the Bun/Elysia/htmx/Prisma/Tailwind/daisyUI/EasyAuth stack.

All raw file URLs follow this pattern:

```
https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/<tool>/llms.txt
```

Full URL table:

| Technology | Raw URL |
|------------|---------|
| Bun | `https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/bun/llms.txt` |
| ElysiaJS | `https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/elysiajs/llms.txt` |
| EasyAuth | `https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/easy-auth/llms.txt` |
| htmx | `https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/htmx/llms.txt` |
| Prisma | `https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/prisma/llms.txt` |
| Tailwind CSS | `https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/tailwindcss/llms.txt` |
| daisyUI | `https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/daisyui/llms.txt` |

---

## GitHub Copilot in VS Code

### Using `#fetch` in Copilot Chat

1. Open the Copilot Chat panel in VS Code.
2. In the chat input, type `#fetch` followed by a raw URL.
3. Copilot fetches the URL and includes the content as context for your prompt.

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

1. Create `.github/copilot-instructions.md` in your project root.
2. Add a section listing the raw URLs of the `llms.txt` files you want Copilot to always reference.

Example `.github/copilot-instructions.md`:

```markdown
## External Documentation

When working on this project, reference these documentation files for the technology stack:

- Bun runtime and bundler: https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/bun/llms.txt
- ElysiaJS web framework: https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/elysiajs/llms.txt
- EasyAuth integration: https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/easy-auth/llms.txt
- htmx hypermedia library: https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/htmx/llms.txt
- Tailwind CSS: https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/tailwindcss/llms.txt
- daisyUI component library: https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/daisyui/llms.txt
- Prisma ORM: https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/prisma/llms.txt

Always use the Bun runtime (not Node.js) and Elysia for HTTP handling.
Use htmx attributes for client-side interactivity instead of a JavaScript framework.
```

Copilot reads `copilot-instructions.md` automatically on every chat session in that workspace.

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

1. Install the GitHub Copilot plugin from JetBrains Marketplace.
2. Open the Copilot Chat tool window (View > Tool Windows > GitHub Copilot Chat).
3. Paste a raw URL directly into the chat input. Copilot will fetch the URL and use the content as context.

Example:

```
Read this documentation: https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/elysiajs/llms.txt
Now create an Elysia route that validates JWT tokens using the @elysiajs/jwt plugin.
```

### Limitations compared to VS Code

- The `#fetch` shorthand is not available in JetBrains; paste the full URL as plain text.
- The `copilot-instructions.md` file is honoured by Copilot in JetBrains from Copilot plugin version 1.5 and later.
- File attachment via the chat UI is not supported; use URL references instead.

### Recommended approach

Use the `copilot-instructions.md` file (same as VS Code) for persistent context. Place the file at `.github/copilot-instructions.md` in the project root.

---

## Cursor

### Using `.cursor/rules/` directory

The `.cursor/rules/` directory is the current recommended approach for persistent rules and context. The older `.cursorrules` file is deprecated.

1. Create the directory `.cursor/rules/` in your project root.
2. Create a file with a `.mdc` extension (Markdown with YAML frontmatter).

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
- EasyAuth: https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/easy-auth/llms.txt
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

1. Open Cursor Chat (Cmd+L or Ctrl+L).
2. Type `@docs` to open the documentation picker.
3. Add a documentation source by URL if not already added.
4. Reference the documentation source by name in your prompt.

### Using `@web` with raw GitHub URLs

In Cursor Chat, type `@web` followed by a raw URL to fetch and include the file as context:

```
@web https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/bun/llms.txt
How do I register a Bun plugin for loading SVG files?
```

---

## Windsurf (Codeium)

### Configuring Windsurf rules

1. Open the Windsurf settings panel.
2. Navigate to the Rules or Memory section.
3. Add a rule that lists the raw URLs of the documentation files.

Example rule text:

```
When working on this project, reference the following documentation files for context:
- https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/bun/llms.txt
- https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/elysiajs/llms.txt
- https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/htmx/llms.txt
- https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/prisma/llms.txt
- https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/tailwindcss/llms.txt
- https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/daisyui/llms.txt
- https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/easy-auth/llms.txt
```

### Using Cascade with documentation context

1. Open Cascade (Windsurf's agentic chat panel).
2. Paste a raw URL directly into the chat input. Cascade fetches the file.
3. Proceed with your prompt after the file is loaded.

Example:

```
Fetch this file and use it as context: https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/elysiajs/llms.txt
Create an Elysia application with JWT authentication and a protected route.
```

### Attaching files in Windsurf Chat

1. Click the attachment icon in the Windsurf Chat input.
2. Select a locally cloned `llms.txt` file from the filesystem.
3. The file contents are included as context for the current chat session.

---

## Cline (VS Code extension)

### Creating a `.clinerules` file

1. Create `.clinerules` at the project root.
2. Add documentation instructions in plain text or Markdown.

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
- EasyAuth: https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/easy-auth/llms.txt

## Stack Conventions

- Runtime: Bun
- HTTP framework: Elysia
- Database ORM: Prisma
- UI interactivity: htmx (no JavaScript framework)
- Styling: Tailwind CSS + daisyUI
- Auth: EasyAuth
```

Cline reads `.clinerules` automatically when a task starts in that workspace.

### Using `@url` in Cline chat

In the Cline chat input, use `@url` to fetch a remote file on demand:

```
@url https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/prisma/llms.txt
Create a Prisma schema for a blog application with users and posts.
```

### Configuring custom instructions

1. Open VS Code settings.
2. Search for "Cline: Custom Instructions".
3. Add the documentation URLs and stack conventions as persistent instructions.

---

## Claude (via API or claude.ai)

### Pasting raw URLs

Paste a raw URL directly into the Claude message input. Claude fetches the URL and includes the content as context.

```
Read this documentation file: https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/htmx/llms.txt

Now explain how to build a custom htmx extension that adds a loading spinner during requests.
```

### Attaching downloaded files

1. Download the `llms.txt` file to your local machine.
2. Attach the file using the attachment button in claude.ai.
3. Reference the file in your prompt.

### Using Claude Projects

1. Create a new Project in claude.ai.
2. Upload `llms.txt` files to the Project's knowledge base.
3. All conversations in the Project will have access to the uploaded files.

Recommended files to upload for this stack:

- `bun/llms.txt`
- `elysiajs/llms.txt`
- `htmx/llms.txt`
- `prisma/llms.txt`
- `tailwindcss/llms.txt`
- `daisyui/llms.txt`
- `easy-auth/llms.txt`

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

1. Open the ChatGPT GPT editor (explore.openai.com/gpts/editor).
2. In the "Knowledge" section, upload one or more `llms.txt` files.
3. Set instructions to reference the uploaded files when answering stack-related questions.

Example GPT instructions:

```
You are a full-stack TypeScript developer assistant specializing in the Bun/Elysia/htmx/Prisma/Tailwind/daisyUI stack.

When users ask about any of these technologies, refer to the uploaded documentation files for accurate API details.
```

### Using Code Interpreter with attached files

1. Enable the Code Interpreter tool in a ChatGPT conversation.
2. Attach a `llms.txt` file using the attachment button.
3. ChatGPT can read the file content and use it in its response.

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
  - /path/to/llms-stack-refresh/easy-auth/llms.txt
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

1. Create or edit `.continue/config.json` in your project root.
2. Add a `contextProviders` entry with a `url` provider listing the raw URLs.

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
          "https://raw.githubusercontent.com/d4551/llms-stack-refresh/main/easy-auth/llms.txt"
        ]
      }
    }
  ]
}
```

### Using `@docs` context provider

1. In Continue Chat, type `@docs` to open the documentation picker.
2. Select a URL context provider you have configured.
3. The documentation is included as context for the current prompt.

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

1. Clone this repository locally.
2. Open your project in Zed.
3. Open the AI assistant panel (Cmd+? or Ctrl+?).
4. Type `/file` followed by the path to a local `llms.txt` file.

Example:

```
/file /path/to/llms-stack-refresh/htmx/llms.txt
Explain how to use the htmx response-targets extension.
```

### Configuring Zed assistant context

1. Open Zed settings (Cmd+, or Ctrl+,).
2. Navigate to the `assistant` section.
3. Add a `default_context` or similar setting pointing to local documentation files.

Note: Zed's assistant configuration evolves rapidly. Check the Zed documentation at https://zed.dev/docs/assistant for the latest approach.

---

## Local Development (general)

### Cloning the repository

```bash
git clone https://github.com/d4551/llms-stack-refresh.git
cd llms-stack-refresh
```

Files are in: `bun/`, `daisyui/`, `easy-auth/`, `elysiajs/`, `htmx/`, `prisma/`, `tailwindcss/`

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
