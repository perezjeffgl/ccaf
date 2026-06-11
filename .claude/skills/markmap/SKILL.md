---
name: markmap
description: Generate an SVG file from a .mm.md Markmap file. Runs the markmap CLI to render the mind map and writes a same-named .svg alongside the source file.
when_to_use: Use when the user asks to generate, export, or render an SVG from a *.mm.md file, or passes a markmap file name as an argument.
argument-hint: "file.mm.md"
paths:
  - "**/*.mm.md"
---

# Markmap Skill

Convert a `.mm.md` Markmap file into an SVG by running the markmap CLI.

## Primary task — generate SVG

Given a file path (e.g. `introduction-to-agent-skills.mm.md`), run:

```bash
npx markmap-cli --no-open --output <basename>.svg <file.mm.md>
```

- Derive `<basename>` from the input filename (strip `.mm.md`, append `.svg`).
- Write the SVG to the same directory as the source file.
- If `markmap-cli` is already installed globally, prefer `markmap` over `npx markmap-cli`.
- Check availability with `which markmap || npx markmap-cli --version` before running.

### Example

Input: `introduction-to-agent-skills.mm.md`
Command: `npx markmap-cli --no-open --output introduction-to-agent-skills.svg introduction-to-agent-skills.mm.md`
Output: `introduction-to-agent-skills.svg` (same directory)

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

Report the output path and file size. If the command fails, show the error and suggest running `npm install -g markmap-cli` to install the CLI.
