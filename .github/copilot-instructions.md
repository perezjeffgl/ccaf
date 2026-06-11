# Copilot Instructions

## Commit-main workflow

When the user asks to **commit and push latest changes to main upstream** (examples: "commit-main", "commit & push to main", "push latest to upstream"), follow this exact sequence:

1. Run `git --no-pager status --short`, `git --no-pager branch --show-current`, and `git --no-pager remote -v` first.
2. Confirm the current branch is `main`.
3. If author identity is missing, ask for `Name <email>` and set repo-local config:
   - `git config user.name "<name>"`
   - `git config user.email "<email>"`
4. Stage all current changes with `git add -A`.
5. Commit with the user-provided message; if none is provided, use:
   - `chore: update repository files`
6. Include this trailer in commit messages unless user says otherwise:
   - `Co-authored-by: Copilot <223556219+Copilot@users.noreply.github.com>`
7. Push with `git push origin main`.
8. Return the commit SHA and commit message in the response.

## Safety constraints

- Never force push.
- Never use destructive git commands (`reset --hard`, `checkout --`, `clean -fd`) unless the user explicitly requests them.
- Do not alter unrelated files beyond staging/committing current workspace changes.
