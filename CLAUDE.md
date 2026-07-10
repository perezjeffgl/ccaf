# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## About This Repository

Study sandbox for the **Claude Certified Architect – Foundations** (CCAF) certification — a 4-course learning path from the [Claude Partner Network](https://anthropic.skilljar.com/page/claude-partner-network-learning-path). Content is documentation-only; there is no build pipeline or test suite.

## Repository Structure

| Path | Contents |
|------|----------|
| `mindmaps/introduction-to-agent-skills.mm.md` | Agent Skills: reusable markdown instructions, creating/configuring/distributing skills in Claude Code |
| `mindmaps/building-with-the-claude-api.mm.md` | Claude API: authentication, prompt engineering, vision, tool use, batch processing, streaming, error handling, production scaling |
| `mindmaps/introduction-to-model-context-protocol.mm.md` | MCP: architecture, core primitives (tools/resources/prompts), building servers and clients in Python, integration patterns |
| `mindmaps/claude-code-in-action.mm.md` | Claude Code: setup, core features, workflow integration, debugging, team collaboration |
| `mindmaps/introduction-to-sub-agents.mm.md` | Sub-agents: context isolation, delegation patterns, and practical usage notes |

## Working in This Repo

All course notes live as Markmap-flavored Markdown files in `mindmaps/`. When adding or updating notes:

- Keep each course/topic's notes in its own `.mm.md` file; cross-reference with links rather than duplicating content.
- Update `README.md` course links when files are added, removed, or moved.
- Code snippets in the notes are illustrative examples from the courses, not production code.
