# Task

Summarize and commit staged files in `{{PROJECT_NAME}}`

## Inputs

- `{{PROJECT_NAME}}`: Directory name under `/Users/jorgerazo/projects/` (e.g., `fontawesome`).

## Instructions

1. Navigate to `/Users/jorgerazo/projects/{{PROJECT_NAME}}`.
2. Review only the files already staged for commit; do not stage or modify additional files.
3. Write a concise English summary describing the staged files and their purpose.
4. Derive an English commit message based on the staged changes (conventional style preferred, e.g., `chore: ...`, `fix: ...`, etc.).
5. Run `git commit -m "<generated message>"` to record the staged files.
6. Report both the summary and the exact commit command executed.
7. Run `git push` to publish the commit to the remote repository, and report the exact `git push` command and its outcome.

## Deliverables

- English summary of the staged files.
- Generated commit message and confirmation of the `git commit -m "…"` command executed.
- Exact `git push` command executed and a brief push result/confirmation.
