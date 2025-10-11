# Task

Summarize, selectively stage, and commit files in `{{PROJECT_NAME}}`

## Inputs

- `{{PROJECT_NAME}}`: dir_name
- `paths_to_add`: Optional.

## Instructions

1. Navigate to `/Users/jorgerazo/projects/{{PROJECT_NAME}}`.
2. Validate `paths_to_add` if provided:
   - Only add paths that exist inside the project directory.
   - Do not accept absolute paths or any path containing `..` that would traverse outside the repository root. Examples that will be rejected: `/etc/passwd`, `../other-repo/`, `/Users/you/...`.
   - If any provided path does not exist, is a symlink that resolves outside the repo, or is outside the repo root, report an error and stop without making any changes.
3. If `paths_to_add` is provided and valid, run `git add -- <each path>` for exactly those paths (do not add any others).
4. Review only the files currently staged for commit (i.e., `git status --porcelain` filtered for staged entries). Do NOT stage or modify additional files beyond step 3.
5. Write a concise English summary describing the staged files and their purpose.
6. Derive an English commit message from the staged changes (conventional style preferred, e.g., `chore: ...`, `fix: ...`, `feat: ...`).
7. Run `git commit -m "<generated message>"` to record the staged files.
8. Report the summary and the exact `git commit` command executed.
9. Run `git push` and report the exact `git push` command executed and a brief push result/confirmation.

## Safety and constraints

- The task will only add the specific `paths_to_add` you supply. It will never run `git add .`, `git add -A`, or any pattern that would include files you didn't explicitly list.
- Paths must be relative to the project root and must not use `..` or be absolute. Symlinks that resolve outside the repo will be rejected.
- If `paths_to_add` is empty or not provided, the task acts in "staged-only" mode and will only commit files already staged.
- The task will refuse to run if any requested path points outside the repository root.

### Large commits

If the provided `paths_to_add` would stage a very large number of files (thousands), consider pre-staging a smaller subset or using directory-level adds intentionally. You can also request a dry-run (list only) to review counts before committing.

## Deliverables

- English summary of the staged files and their purpose.
- Generated commit message and confirmation of the `git commit -m "…"` command executed.
- Exact `git push` command executed and a brief push result/confirmation.

## Examples

- Staged-only mode (commit files that are already staged):

      Example inputs:

      - `{{PROJECT_NAME}}`: `fontawesome`
      - `paths_to_add`: (omit or empty)

   Behavior: the task will not run any `git add`; it will summarize the currently staged files, generate a commit message, run `git commit -m "..."`, and `git push`.

- Stage-then-commit mode (validate and add provided paths):

      Example inputs:

      - `{{PROJECT_NAME}}`: `fontawesome`
      - `paths_to_add`: `["v6.1.2/"]`

   Behavior: the task will validate `v6.1.2/` is a relative path inside the repo, run `git add -- v6.1.2/`, summarize staged files, generate a commit message, run `git commit -m "..."`, and `git push`.

## Notes for operators

- This task is intended to be used interactively by a human (who provides `paths_to_add`) or by automation that has validated the list of paths beforehand.
- If the project contains very large numbers of files, prefer providing directory paths to add selectively or pre-stage exact files to avoid huge commits.
- Optional: run a dry-run by asking the operator to list staged files first (e.g., `git add -- v6.1.2/ && git status --porcelain`) and confirm counts before `git commit`.

--

This file is the unified task that replaces the older `summarize-staged-files.md`. It supports two modes:

- Staged-only mode: if you do not provide `paths_to_add`, the task will operate only on files already staged.
- Stage-then-commit mode: if you provide `paths_to_add`, the task will validate and `git add --` only those paths, then summarize and commit them.

Use this canonical task from now on. It enforces the same safety constraints as the original tasks.
