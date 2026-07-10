# Copilot Instructions

## Build, test, and lint commands

- This repository has no automated build, test, or lint pipeline configured.
- There is no single-test command because no test suite is present.

### Markmap render command (used in this repo)

- Generate one mind map HTML from one source file:
  - `mkdir -p assets && npx markmap-cli --no-open --output assets/<basename>.html mindmaps/<file>.mm.md`
- Example:
  - `mkdir -p assets && npx markmap-cli --no-open --output assets/introduction-to-agent-skills.html mindmaps/introduction-to-agent-skills.mm.md`

## High-level architecture

- This is a documentation/study repository for Claude Certified Architect – Foundations content.
- Primary authored content lives in `mindmaps/*.mm.md` as Markmap-oriented markdown notes (course/topic mind maps).
- `assets/` stores generated visual/export artifacts referenced by docs.
- `labs/` contains course lab artifacts (mostly notebooks, datasets, and bundled files) that are treated as supporting materials rather than application code.
- `.claude/skills/markmap/SKILL.md` defines the project’s Markmap generation workflow and expected output conventions.

## Key conventions for this codebase

- Prefer editing `mindmaps/*.mm.md` source files; treat generated artifacts in `assets/` as outputs.
- Keep notes course-scoped and cross-reference related material instead of duplicating content.
- Preserve Markmap-compatible structure in `.mm.md` files (hierarchical headings/lists and valid YAML frontmatter when present).
- Keep examples/snippets as instructional material from coursework, not production-ready implementation code.
- When generating Markmap output, write files to `assets/` with matching basenames and `.html` extension.
