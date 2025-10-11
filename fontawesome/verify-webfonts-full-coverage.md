# Task

Validate complete Font Awesome webfont coverage (extensions + `pro-` variants)

## Context

- Directory under test: `/Users/jorgerazo/projects/fontawesome/structure/webfonts`
- Expected extension universe: `.eot`, `.otf`, `.svg`, `.svgz`, `.ttf`, `.woff`, `.woff2`
- Naming convention: every core font name should exist in both prefixed (`pro-<name>`) and non-prefixed (`<name>`) forms, each with the full extension set.

## Objectives

- Inventory the distinct extensions present and confirm they match the seven-item universe above.
- Enumerate unique font basenames, grouping by core name (strip `pro-` when present).
- Verify that each core name has both prefixed and non-prefixed variants.
- Ensure that every variant (prefixed and plain) has files for all seven extensions.
- Create zero-byte placeholder files for missing variants or extension gaps so the directory attains full parity.

## Instructions

1. Scan `/Users/jorgerazo/projects/fontawesome/structure/webfonts` and collect:
   - The set of distinct extensions present.
   - Core basenames with their associated prefixed/non-prefixed variants and extensions.
2. Validate the extension set equals `{.eot, .otf, .svg, .svgz, .ttf, .woff, .woff2}`.
3. For each core basename:
   - Confirm both `pro-<core>` and `<core>` variants exist; create missing variants with all seven extensions if necessary (placeholders allowed).
   - For each variant, confirm all seven extensions are present; create placeholders for any missing combinations.
4. Re-run validation to confirm no outstanding gaps (extensions, variants, or files).
5. Document the process and results in a Markdown report stored alongside this task. Include:
   - Extension inventory.

- Core basenames inspected and their coverage status.
- Placeholder files created (variant + extension details).
- Final verification output demonstrating complete coverage.

## Deliverables

- Updated webfont directory with prefixed and non-prefixed variants fully covered across all seven extensions.
- Markdown report summarizing findings, placeholders added, and final verification output.
