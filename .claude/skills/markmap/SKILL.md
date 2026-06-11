---
name: markmap
description: Author and refine Markmap mind maps in Markdown. Use for structure, frontmatter options, and rendering-friendly edits in .mm.md files.
when_to_use: Use this only when the task is about files matching *.mm.md, or when the user explicitly asks for Markmap syntax/options.
argument-hint: [file.mm.md]
paths:
  - "**/*.mm.md"
---

# Markmap Skill

Create or edit mind-map Markdown for Markmap with predictable structure and valid options.

## Scope

- Apply this skill only to `*.mm.md` files.
- Keep output as valid Markdown that Markmap can parse into a hierarchy.

## Markmap authoring rules

1. Use headings and/or nested bullet lists to express hierarchy.
2. Keep heading levels monotonic where possible (avoid skipping levels unless intentional).
3. Keep each node concise; split long nodes into children.
4. Preserve links and inline emphasis (`**bold**`, `_italic_`, `` `code` ``) when useful for node labels.

## Frontmatter and options

If options are needed, place them in YAML frontmatter under `markmap:`:

```yaml
---
markmap:
  color:
    - blue
  colorFreezeLevel: 2
  duration: 500
  maxWidth: 0
  initialExpandLevel: -1
  zoom: true
  pan: true
  spacingHorizontal: 80
  spacingVertical: 5
  lineWidth: 2
---
```

Supported option knowledge to apply when requested:

- `color`: string or list of colors.
- `colorFreezeLevel`: freeze branch colors below a level.
- `duration`: fold/unfold animation duration.
- `maxWidth`: max node content width (`0` means no limit).
- `initialExpandLevel`: default expanded depth (`-1` means all).
- `zoom` / `pan`: interaction toggles.
- `spacingHorizontal` / `spacingVertical`: layout spacing.
- `lineWidth`: branch stroke width.
- `htmlParser.selector`: customize HTML parsing target selector.
- `activeNode.placement`: `visible` or `center` (supported in markmap.js.org and Markmap VSCode extension).
- External plugin assets can be referenced through `markmap` options (e.g., JS/CSS URLs and `npm:` URL form).

## Output pattern

When creating a new file, use this template:

```markdown
---
title: <Mindmap Title>
markmap:
  initialExpandLevel: 2
---

# <Mindmap Title>

## Branch A
- Item A1
- Item A2

## Branch B
### Sub-branch B1
- Item B1.1
```

## Editing behavior

- Prefer surgical edits over rewrites.
- Keep existing node ordering unless the user asks to reorganize.
- If frontmatter is malformed, fix it while preserving intent.
