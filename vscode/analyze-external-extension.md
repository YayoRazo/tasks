# Task

Evaluate an external VS Code extension for reusable concepts

## Inputs

- `{{EXTENSION_PATH}}`: absolute path to the external extension you want to evaluate.
- Our extension workspace: `/Users/jorgerazo/projects/razo-nova-vscode`

## Objective

Perform a thorough review of the target extension to identify design patterns, UX ideas, architectural choices, and feature concepts that could enhance our own VS Code extension without copying source code verbatim.

## Constraints & Rules

- Explicitly exclude ideas that we have already implemented or areas where our current solution is equivalent or better. Only surface gaps, enhancements, or new concepts worth considering for our extension.
- Do **not** copy code, assets, schemas, or documentation verbatim from the target extension.
- You may only capture high-level concepts, workflows, or patterns that can inspire an original implementation in our project, and aim to deliver an equal or improved solution when feasible.
- Before writing any code, produce a proposal summarizing the insights discovered and how they could translate into new capabilities or improvements.
- Implementation must create original code or adapt existing modules in our project; no direct transplantation of logic or assets is allowed.
- Any new implementation must be authored in TypeScript and written entirely in English, with concise in-code comments that explain non-obvious logic.
- Add or update automated tests (unit and/or integration in `tests/`) for every module that is modified or created, when applicable.
- Reuse the bundled Font Awesome assets for any new icons instead of introducing custom images or SVGs.
- All user-facing strings must be sourced from the localization bundles (`src/i18n/messages/*`); avoid hard-coded text in TypeScript or HTML templates.
- Do not add the `activationEvents` property to `package.json`; VS Code infers activators automatically and redundant entries trigger warnings.
- Update both internal documentation (`docs/`) and the public README to reflect new features, settings, or workflows derived from the analysis.

## Deliverables

1. **Research brief** (Markdown) describing:
   - Key ideas extracted from `{{EXTENSION_PATH}}` that are not already present or sufficiently addressed in our extension.
   - Rationale for why each idea benefits our extension.
   - Suggested integration plan (update existing module vs. create new module).
   - Potential risks or prerequisites (dependencies, build changes, UX impact).
2. **Implementation plan** outlining prioritized tasks to build the approved ideas, including testing strategy.
3. (Optional) Prototype branches or proof-of-concept snippets created from scratch, if needed to validate the approach.

## Audit Checklists

When reviewing `{{EXTENSION_PATH}}`, explicitly document the status of each area below so nothing is overlooked:

- **Activation & lifecycle**: custom editors, webviews, commands, contribution points, file watchers, messaging, status handling.
- **User experience**: toolbar controls, keybindings, settings/UI flows, context menu entries, error states, accessibility options, theming.
- **Configuration**: user/workspace settings, defaults, migration logic, external dependencies, environment assumptions.
- **Rendering pipeline**: HTML templates, asset bundling, localization support, CSP, resource loading, offline handling.
- **Feature set**: search, outline, thumbnails, annotations, download/print, external open, reload behaviors, multi-tab handling.
- **Testing & tooling**: unit/integration tests, mocks, lint rules, build scripts.
- **Documentation**: README, changelog, contribution notes, troubleshooting guidance.

Document findings for each bullet, noting whether to adopt, adapt, or skip with justification.

## Suggested Workflow

1. Obtain read-only access to the target extension under `{{EXTENSION_PATH}}` (e.g., downloaded source archive or referenced workspace copy). Avoid cloning or copying wholesale into our repository.
2. Review documentation, package manifest, contribution points, commands, webviews, and tests to understand the value proposition.
3. Create the research brief (Deliverable 1) and share it for approval.
4. After approval, refine the implementation plan (Deliverable 2) and share estimated effort.
5. Execute implementation tasks in our repository, ensuring all new code is original.
6. Validate with linting, tests, and manual smoke checks.
7. Summarize completed work and open follow-up tasks for any deferred enhancements.
8. Capture any deferred ideas or gaps in a follow-up backlog entry so future iterations can revisit them.
