# Claude Code in Action

Integrate Claude Code into your development workflow for practical application and productivity enhancement.

https://anthropic.skilljar.com/claude-code-in-action

[← Back to Courses Overview](COURSES.md)

## Coding Assistant
IT uses LLM capabilities to assist developers in writing, debugging, and optimizing code. It can provide suggestions, auto-complete code snippets, and even generate entire functions based on user input.

- task
- assistant
    - language model
        - gathers context from
            - codebase
            - user input
        - formulate a plan
        - take action
    - set of tools
        - handle complex tasks
        - extensible platform:
            - add new tools
            - customize existing tools
        - better security
            - navigate codebase without indexing or storing sensitive information
        - strong tool use
- default tools
    - Agent
    - Bash
    - Edit, Read, Write
    - TodoRead, TodoWrite
    - WebSearch, WebFetch
    - Glob, grep, ls
    - MultiEdit
    - NotebookEdit
    - NotebookRead

## Context
Help Claude gather relevant context from the codebase and user input
- memory
    - use # or /memory to store context for future turns
    - Escape
        - interrupts Claude's current reasoning and returns to the main loop
    - /compact
        - compresses memory to save space
        - removes unnecessary details
    - clear
        - 
- /init > CLAUDE.md
    - initialize the coding assistant
    - set up the environment
    - load necessary tools
- files
    - CLAUDE.md
        - generated via /init
        - file included on every request
        - saved under version control
        - shared with other engineers
    - CLAUDE.local.md
        - not shared with others
        - personal instructions and custom Claude preferences
    - ~/.claude/CLAUDE.md
        - used with all projects
        - contains global instructions for the coding assistant across all projects
- Modes
    - /plan
        - Claude generates a plan for the task
    - /effort
        - low: faster and cheaper
        - max: reason longest on hard problems
    - /thinking
        - Claude executes the plan
        - ultrathinking
            - instruct to reason more on this turn
## Commands
- location
    - .claude/commands
        - <command>.md
    - args
        - $ARGUMENTS

## Permissions
- config
    - settings.local.json
        - configure Claude's behavior and permissions
        - set default tools, memory usage, and other preferences
    - allow
    - deny

## Integrations
- github
    - /install-github-app
        - install GitHub integration
        - enable Claude to access repositories, issues, and pull requests
- actions
    - workflows
        - automate tasks and processes
        - trigger Claude actions based on events in the repository

## Hooks
- settings.json
    - hooks
        - PreToolUse
        - PostToolUse
        - Notification
        - Stop
        - SubagentStop
        - PreCompact
        - UserPromptSubmit
        - SessionStart
        - SessionEnd
- implementation
    - matcher
        - Read, Write, Edit, TodoRead TodoWrite, WebSearch, WebFetch, Glob, Grep, LS, MultiEdit, NotebookEdit, NotebookRead
    - matcher: "Read|Grep"
    - hooks
        - type: command
        - command: "node $PWD/.claude/hooks/ReadGrepHook.js $ARGUMENTS"
- Best Practices
    - Validate and sanitize inputs
    - Always quote shell variables
    - Block path traversal
    - Use absolute paths
    - Skip sensitive files

## SDK
- runs CC programatically
- inherits all settings
- R/O permissions by default
- languages
    - CLI
    - Python
    - TypeScript




