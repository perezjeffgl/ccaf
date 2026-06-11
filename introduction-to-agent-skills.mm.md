---
title: s
markmap:
  maxWidht: 20
---

# Agent Skills

Learn how to build, configure, and share Skills in Claude Code Reusable markdown instructions that Claude automatically applies to the right tasks at the right time.
> Anthropic Learning Path**: https://anthropic.skilljar.com/introduction-to-agent-skills

## Fundamentals
Understanding Skills as reusable markdown instructions and their role in Claude Code

* folders of instructions
  * .../skills/mySkillName/SKILL.md
* use description to match skills to request
* paths
  * `~/.claude/skills` (personal)
  * `<project>/.claude/skills`
* load on demand

> If you find yourself explaining the same thing to Claude repeatedly, that's a skill waiting to be written

## Anathomy 
Creating Your First Skill
Building basic Skills from scratch with proper syntax and structure

- *name = identifier
- *description = when to use it
- model
  - sonnet
  - opus
  - hiaku
- allowed-tools = restricts what Claude can use
  - Read
  - Grep
  - Glob
  - Bash
 
Configuring Skills
Advanced configuration options, parameters, and customization
Create/Split into directories if SKILL exceeds 500 lines, use reference files

## Distribute
Distributing Skills Across Teams
Sharing, collaboration, and version management
- via git(.claude/skills/*)
- plugins(not load skills auto)
- enterprise settings(deploy skill org-wide)
  * managed-settings.json
- build-in agents(can not access skills)
  * Explore
  * Plan
  * Verify
- custom subagents(load only skills defined in field)

## Other Features 
- CLAUDE.md
  * load on every conversation
- subagents
- hooks
- mcp servers

## Troubleshooting
- skills validator tool
  * uv
- check description
  * specifics
  * make them distinct
- SKILL.md path/location, case
  * `claude --debug`
- runtime errors ~ file permissions
  * `chmod +x`
- priority
  * enterprise
  * personal
  * project
  * plugins

[← Back to Courses Overview](COURSES.md)
