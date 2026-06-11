# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## About This Repository

Study sandbox for the **Claude Certified Architect – Foundations** (CCAF) certification — a 4-course learning path from the [Claude Partner Network](https://anthropic.skilljar.com/page/claude-partner-network-learning-path). Content is documentation-only; there is no build pipeline or test suite.

## Repository Structure

| File | Contents |
|------|----------|
| `COURSES.md` | Top-level index linking all four course notes |
| `introduction-to-agent-skills.md` | Agent Skills: reusable markdown instructions, creating/configuring/distributing skills in Claude Code |
| `building-with-the-claude-api.md` | Claude API: authentication, prompt engineering, vision, tool use, batch processing, streaming, error handling, production scaling |
| `introduction-to-model-context-protocol.md` | MCP: architecture, core primitives (tools/resources/prompts), building servers and clients in Python, integration patterns |
| `claude-code-in-action.md` | Claude Code: setup, core features, workflow integration, debugging, team collaboration |

## Working in This Repo

All content lives in Markdown files. When adding or updating notes:

- Keep each course's notes in its own file; cross-reference with links rather than duplicating content.
- `COURSES.md` is the navigation hub — update it if new course files are added.
- Code snippets in the notes are illustrative examples from the courses, not production code.
