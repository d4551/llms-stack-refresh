# Contributing

This document explains how to add or improve an `llms.txt` file in this repository.

## Before You Start

- Check `docs/INDEX.md` to confirm the stack is not already covered.
- Review `docs/PROVENANCE.md` to understand the sourcing rules.
- Read the existing `llms.txt` files for style reference.

## Adding a New Stack

1. Fork the repository.
2. Create a directory using the technology name in lowercase with hyphens (e.g., `my-tool/`).
3. Add `llms.txt` following the [llmstxt.org specification](https://llmstxt.org/):
   - **H1** — technology name
   - **Blockquote** — one-sentence description
   - **Short intro paragraph** — install command, primary use, key concept
   - **`##` sections** — topic groups with Markdown links and short descriptions
   - **`## Optional` section** — secondary resources (blog, Discord, GitHub, etc.)
4. If the technology has official plugin or extension mechanisms, add a dedicated section for them. Do not bury extension docs in unrelated sections.
5. Update `README.md` — add a row to the "Included Files" table and to the "Raw File URLs" table.
6. Update `docs/INDEX.md` — add a row to the appropriate group table.
7. Open a pull request with a clear description of the source used.

## Improving an Existing File

- Keep changes grounded in official documentation. Cite the source URL for every added item.
- Prefer adding missing official content over rewriting existing correct content.
- If an official `llms.txt` has been published since the curated file was created, replace the curated file with the official one and update the provenance note in `docs/INDEX.md` and `README.md`.

## Sourcing Priority

1. Official `llms.txt` published by the project (use verbatim or as primary source)
2. Official documentation source repository on GitHub
3. Official documentation website as a fallback

## Style Rules

- Use exact method names, attribute names, and file paths — avoid vague descriptions.
- Keep section headings stable; AI tools may reference them directly.
- Group related items together; use sub-sections (`###`) only when a section is long enough to warrant it.
- Place secondary resources (community links, blogs, full-text dumps) in `## Optional`.
- Do not add speculative or unverified content.
