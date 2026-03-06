# Provenance Policy

This document defines the sourcing and provenance rules for all `llms.txt` files in this repository.

## Why Provenance Matters

AI agents rely on the files in this repository to ground their code generation and reasoning. Low-quality or inaccurate sources produce low-quality outputs. Every item in an `llms.txt` must be traceable to an authoritative source.

## Source Tiers

### Tier 1 — Official `llms.txt`
The technology project publishes an `llms.txt` at a canonical URL (e.g., `https://bun.sh/llms.txt`, `https://daisyui.com/llms.txt`).

- **Action**: Use the official file directly. Link to it in `docs/INDEX.md` and `README.md` with provenance "Official".
- **Updates**: Check the official URL periodically. When the official file changes materially, update the copy in this repository.

### Tier 2 — Official Documentation Source on GitHub
No official `llms.txt` exists, but the project maintains an open-source documentation repository (e.g., `elysiajs/documentation`, `bigskysoftware/htmx`).

- **Action**: Curate an `llms.txt` by reading the official docs and constructing a structured index. Mark it as "Curated — [source URL]" in `docs/INDEX.md` and `README.md`.
- **Content rules**: Every link must point to a real, live page. Every description must accurately reflect the linked page. No invented APIs or behaviors.

### Tier 3 — Official Documentation Website
No official `llms.txt` and no open-source docs repo. The project maintains an official documentation website.

- **Action**: Curate from the documentation website. Mark as "Curated — [docs URL]". This applies to `better-auth/llms.txt`.
- **Content rules**: Same as Tier 2. Be especially careful not to overstate capabilities.

## What Is Not Acceptable

- Content invented without a source URL
- Content copied from unofficial or community-written guides as if it were official
- Speculation about undocumented APIs or behaviors
- Content from outdated versions without a version note

## Marking Provenance

Each `llms.txt` intro paragraph should state the source. Example:

> This file is curated from the official documentation at https://example.com/docs/. No official `llms.txt` was published by the project.

The `docs/INDEX.md` table uses "Official" or "Curated — [URL]" in the Provenance column.

## Updating Stale Content

If a link in an `llms.txt` is broken or the described behavior no longer matches the official docs:

1. Update the file directly with the corrected content, citing the updated source URL.
2. Update the "Notes" column in `docs/INDEX.md` if the file was substantially refreshed.
