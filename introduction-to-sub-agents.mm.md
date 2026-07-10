# Subagent
## run on its context
each subagent runs on its own context window, separate from the main context. It can use its own tools, memory, and model settings to perform tasks without cluttering the main context.
- main context only receives the final output
- entire subagent context/conversation is discarded after subagent stops
## inputs
- custom system prompt
- task description
## advantages & benefits
- manage its own context window, keeping the main context clean and focused
- helps to break work into smaller, focused pieces
- bring back just information that is relevant to the main context
## built-in subagents
- Explore
- Plan
- ...
## Custom subagents
- can be created by users, *.md files
    - /agents
    - `~/.claude/subagents` (personal)
    - `<project>/.claude/subagents`
- name: unique identifier
- description: "Use.. when.."
- tools
- model [sonnet, opus, haiku, inherit]
- color
- system prompt
    * instructions for the subagent
    * what to focus on
    * how to handle the task
    * how report findings back
## Control/Influence modified prompt
- used for
    - Research, Reviews
    - custom system prompts
- avoid them for
    - expert claims
    - multi step pipelines
    - test runners
- use effectively
    - specific description
    - structured output format
    - report obstacles or issues
    - limit tool access
- ask before creating a subagent
    - does the intermediate work matter?
    - if not, delegate it = subagent

