# Task

Audit and streamline scripts in `/Users/jorgerazo/projects/fontawesome/scripts`

## Objectives

- Catalog every script and its responsibilities.
- Detect duplicated or overlapping behavior across scripts.
- Consolidate or refactor scripts where redundancy exists.
- Reorganize the script directory structure to improve discoverability and cohesion.
- Propose improvements or automation that reduces manual effort.

## Instructions

1. Navigate to `/Users/jorgerazo/projects/fontawesome/scripts` and list all scripts, grouping them by purpose (downloading, processing, utilities, etc.).
   - Treat `download_release_assets.py` as read-only; do not modify it during this task.
2. For each script, document input parameters, dependencies, side effects, and the outputs it produces.
3. Compare scripts to identify duplicated logic or overlapping features; note where functionality can be merged or abstracted.
4. Refactor scripts to eliminate duplication and improve readability, error handling, and configuration (keep changes backwards compatible where possible).
5. Reorganize files or subdirectories so related scripts live together; update module imports or references accordingly.
6. Add or update README-style documentation describing the refined structure and usage of each script.
7. Provide a summary of changes, including before/after structure, key refactors performed, and any follow-up recommendations.

## Deliverables

- Updated scripts and directory layout reflecting the refactors.
- Documentation capturing the final structure, usage instructions, and maintenance guidelines.
- Change summary highlighting major improvements and next steps (if any).
