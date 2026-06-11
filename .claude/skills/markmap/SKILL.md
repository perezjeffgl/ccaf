---
name: markmap
description: Generate an interactive HTML mind map from a .mm.md Markmap file. Runs the markmap CLI, captures errors, validates output, and writes a same-named .html into the assets/ directory.
when_to_use: Use when the user asks to generate, export, or render an SVG from a *.mm.md file, or passes a markmap file name as an argument.
argument-hint: "file.mm.md"
paths:
  - "**/*.mm.md"
---

# Markmap Skill

Convert a `.mm.md` Markmap file into an SVG by running the markmap CLI.

## Primary task — generate SVG

**Note:** `markmap-cli` always produces an interactive HTML file — there is no SVG export option. Output extension must be `.html`.

Given a file path (e.g. `introduction-to-agent-skills.mm.md`), run:

```bash
mkdir -p assets
npx markmap-cli --no-open --output assets/<basename>.html <file.mm.md> 2>&1
```

- Derive `<basename>` from the input filename (strip `.mm.md`, append `.html`).
- Always write to `assets/` relative to the project root; create it if missing.
- Capture both stdout and stderr (`2>&1`) so errors are visible.
- If `markmap-cli` is already installed globally, prefer `markmap` over `npx markmap-cli`.

### Validate output

After generation, verify the file is valid:

```bash
head -1 assets/<basename>.html
```

- Valid output starts with `<!doctype html>` or `<html`.
- If it starts with anything else (error text, empty), the generation failed — show the captured output and stop.
- Also check file size is non-zero: `[ -s assets/<basename>.html ]`.

### Example

Input: `introduction-to-agent-skills.mm.md`
Commands:
```bash
mkdir -p assets
npx markmap-cli --no-open --output assets/introduction-to-agent-skills.html introduction-to-agent-skills.mm.md 2>&1
head -1 assets/introduction-to-agent-skills.html
```
Expected first line: `<!doctype html>`

## Authoring / editing .mm.md files

If the source file needs fixes before rendering, apply these rules:

1. Use headings and/or nested bullet lists for hierarchy.
2. Keep heading levels monotonic (avoid skipping levels).
3. Keep each node concise; split long nodes into children.
4. Preserve links and inline emphasis (`**bold**`, `_italic_`, `` `code` ``).
5. If YAML frontmatter is malformed, fix it while preserving intent.

### Frontmatter reference

```yaml
---
title: <Title>
markmap:
  initialExpandLevel: 2
  maxWidth: 0
  colorFreezeLevel: 2
  duration: 500
  spacingHorizontal: 80
  spacingVertical: 5
  lineWidth: 2
  zoom: true
  pan: true
---
```

## After generating

Report the output path and file size (`ls -lh assets/<basename>.html`). If the command fails or validation fails, show the full captured error output and suggest running `npm install -g markmap-cli` if the CLI is missing.
