---
name: markmap
description: Generate an interactive HTML mind map from a .mm.md Markmap file. Runs the markmap CLI, validates output, and writes a same-named .html into the assets/ directory.
when_to_use: Use when the user asks to generate, render, or export a mind map from a *.mm.md file, or passes a markmap filename as an argument.
argument-hint: "file.mm.md"
paths:
  - "**/*.mm.md"
---

# Markmap Skill

Convert a `.mm.md` Markmap file into an interactive HTML mind map using the markmap CLI.

> ref: https://markmap.js.org/

## How to invoke

```
/markmap <file.mm.md>
```

Example: `/markmap introduction-to-agent-skills.mm.md`

The skill derives the output name from the input (strips `.mm.md`, appends `.html`) and saves it to `assets/`.

---

## Generation

```bash
mkdir -p assets
npx markmap-cli --no-open --output assets/<basename>.html <file.mm.md> 2>&1
```

- `markmap-cli` only produces HTML — there is no SVG export option.
- If `markmap` is available globally (`which markmap`), use it instead of `npx markmap-cli`.

### Validate output

```bash
head -1 assets/<basename>.html
ls -lh assets/<basename>.html
```

- Valid output: first line is `<!doctype html>` and file size is non-zero.
- If the file is empty or starts with anything else, the generation failed — show the captured output and stop.

### Full example

```bash
mkdir -p assets
npx markmap-cli --no-open --output assets/introduction-to-agent-skills.html introduction-to-agent-skills.mm.md 2>&1
head -1 assets/introduction-to-agent-skills.html   # expect: <!doctype html>
ls -lh assets/introduction-to-agent-skills.html
```

---

## Authoring / editing .mm.md files

If the source file needs fixes before rendering:

1. Use headings and/or nested bullet lists for hierarchy.
2. Keep heading levels monotonic (avoid skipping levels).
3. Keep each node concise; split long nodes into children.
4. Preserve links and inline emphasis (`**bold**`, `_italic_`, `` `code` ``).
5. Fix malformed YAML frontmatter while preserving intent.

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

---

## After generating

Report the output path and size. On failure, show the full captured error and suggest `npm install -g markmap-cli` if the CLI is missing.
