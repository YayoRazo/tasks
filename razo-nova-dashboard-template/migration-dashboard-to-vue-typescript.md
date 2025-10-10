# Migration Task: HTML/CSS/JS Dashboard to Vue.js + TypeScript

> **Note:** The base code for this migration lives in `/Users/jorgerazo/projects/matoxi`, which contains two layout variants (`vertical-menu/` and `offcanvas-menu/`). Analyse both variants and migrate every template, asset, and interaction they provide.

## Directory Requirement

All files created as part of the migration (pages, components, assets, etc.) must live inside the repository root `/Users/jorgerazo/projects/razo-nova-dashboard-template`, following the standard Nuxt 3 directory structure (`app/`, `pages/`, `components/`, `layouts/`, `composables/`, `assets/`, `public/`, etc.). Do not place generated output outside this path.

## Matoxi Template Overview (Source of Truth)

- **Layouts:** Two independent HTML implementations exist—`vertical-menu/` (default sidebar) and `offcanvas-menu/` (Bootstrap offcanvas navigation). Both variants share the same assets folder structure and must be migrated one-to-one as switchable Nuxt layouts.
- **Dashboards:** Each layout ships two dashboard entry points (`index.html` and `index2.html`) plus dark/semi-dark variants. Provide matching Nuxt routes (`/dashboard/primary`, `/dashboard/alternate`, etc.) with theme parity.
- **HTML Coverage:** Dozens of feature pages are provided and must be migrated, including but not limited to: authentication flows (`auth-*`), ecommerce (`ecommerce-*`), applications (todos, invoices, calendar), tables (`table-basic-table.html`, `table-datatable.html`), widgets (`widgets-data.html`, `widgets-advance.html`), charts (`charts-apex-chart.html`, `charts-chartjs.html`), maps, forms, pricing, FAQs, timelines, profile, error pages, and starter pages. Maintain identical navigation structure across both layouts.
- **Assets:** Shared folders include `assets/css`, `assets/fonts`, `assets/images`, `assets/js`, `assets/plugins`, and `sass/`. Capture every font, image, SVG, and icon referenced by the HTML templates.
- **Styling:** Core styling is authored in `sass/main.scss` with companion theme files (`dark-theme.scss`, `semi-dark.scss`, `bordered-theme.scss`, `responsive.scss`). Extract design tokens (colors, spacing, typography) and recreate them through Tailwind configuration and/or global CSS modules while retaining the theme toggle behaviour.
- **Fonts & Icons:** The template relies on Google Fonts (`Noto Sans`), Google Material Icons Outlined, Bootstrap Icons (served via CDN), and dedicated icon demo pages for Boxicons, Feather Icons, and Line Icons. Ensure all icon families are locally available or loaded through documented providers and exposed via reusable Vue components.
- **JavaScript Behaviour:** `assets/js/main.js` drives global behaviour (PerfectScrollbar initialisation, sidebar hover/toggle, search overlay, theme toggler that flips the `<html data-bs-theme>` attribute, and metismenu activation). `assets/js/index.js` and `assets/js/index2.js` initialise ApexCharts dashboards. Every behaviour must be ported to Vue/TypeScript composables or components without jQuery dependencies.
- **Third-Party Plugins to Migrate:**
  - Layout utilities: `metismenu`, `perfect-scrollbar`, `simplebar`.
  - Data visualisation: `apexcharts`, `chart.js`, `peity`.
  - Data grids: `datatables` (with Buttons extension).
  - Forms & UI helpers: `select2`, `form-repeater`, `bs-stepper`, `input-tags`, `Drag-And-Drop/imageuploadify`, `fancy-file-uploader`, `validation` scripts.
  - Productivity apps: `fullcalendar` (calendar view), todo-specific scripts.
  - Maps: Google Maps (with API key placeholder) and `jquery-jvectormap` variants.
  - Notifications: `Lobibox` assets in `assets/plugins/notifications` (including sounds and images).
  - Miscellaneous: any custom scripts located under `assets/plugins/**` or inline `<script>` blocks inside the HTML files.
- **Hardcoded Keys:** Google Maps pages embed a sample API key inside the HTML. Replace this with secure environment configuration and document how consuming projects should provide their own keys.

Document any additional assets or scripts discovered during migration that are not explicitly listed above so downstream projects understand their provenance.

## Objective

Migrate the complete dashboard project from static HTML, CSS, and JavaScript to a modern Vue.js + TypeScript architecture, preserving the original design, structure, colors, and user experience as faithfully as possible.

## Best Practices & Modularity

- The project must implement best programming practices, including modular architecture and maximum code reusability. Avoid code duplication by creating reusable components, composables, and utility functions wherever possible.
- All user-facing text and strings must be managed using internationalization (i18n) standards. No text or string should be hardcoded in Vue, TypeScript, or any other file. All text must be loaded from translation files (JSON or other standard formats) to support multi-language and easy updates.
- Use a robust i18n solution (such as Vue I18n) and organize translation files for each supported language. Reference all text via i18n keys in the codebase.

## Best Practices & Architecture Guidance

### Internationalization (i18n) Structure

- Create a `locales` directory at the project root.
- For each supported language, create a subdirectory (e.g., `en`, `es`).
- Use modular JSON files for translation keys, organized by feature or domain (not a single large file). Example:
  - `locales/en/common.json` (generic UI text)
  - `locales/en/dashboard.json` (dashboard-specific text)
  - `locales/es/common.json`
  - `locales/es/dashboard.json`
- Use nested keys for organization, e.g.:

  ```json
  {
    "navbar": {
      "home": "Home",
      "settings": "Settings"
    },
    "dashboard": {
      "title": "Dashboard"
    }
  }
  ```

- Use a robust i18n library (e.g., Vue I18n) with lazy loading for language files.
- Document all i18n keys and structure for maintainability.

### Reusable Component Organization

- Store all reusable components in a `components` directory at the project root.
- Use subdirectories for logical grouping, e.g.:
  - `components/ui/` (buttons, modals, cards, etc.)
  - `components/layout/` (header, sidebar, footer)
  - `components/widgets/` (charts, stats, etc.)
- Use clear, descriptive names and follow PascalCase for component files.
- Document props, events, and slots for each component.
- Prefer Composition API and composables for shared logic (store in `composables/`).

### Build & Code Obfuscation

- Production builds must use code obfuscation/minification for all output (TypeScript, Vue, JS, CSS).
- Development builds must avoid obfuscation/minification to allow easy debugging and code inspection.
- Document the build process and how to switch between production and development modes.

### Browser Support Matrix

- Target compatibility with all major modern browsers:
  - Google Chrome
  - Safari
  - Microsoft Edge
  - Firefox
  - Opera
  - Brave
  - Vivaldi
- Do not support legacy browsers or very old versions; focus on current and recent releases.
- Use Babel or similar tools for necessary polyfills and compatibility.
- Document supported browser versions and test coverage.

## Framework Requirement: Nuxt.js

- The migration must use Nuxt.js (latest version) as the core framework, leveraging its advanced features for SSR (server-side rendering), static site generation, and automatic routing.
- Organize the project according to Nuxt conventions: use the `pages/` directory for automatic routing, `layouts/` for shared layouts, and `plugins/` for integrations.
- Configure meta tags, SEO, and head management using Nuxt's built-in tools.
- Document how to build and deploy the dashboard as an SPA, SSR app, or static site, depending on requirements.
- Ensure compatibility with TypeScript and all other requirements previously listed.

## Technology Stack & Tooling Requirements

The migration must use and integrate the following technologies and tools:

- **Vite:** Fast bundler and build tool (integrated with Nuxt 3).
- **Pinia:** State management library for Vue/Nuxt, recommended over Vuex.
- **ESLint + Prettier:** For code linting and automatic formatting.
- **Vitest:** For unit and integration testing (native for Vite/Nuxt).
- **Playwright:** For end-to-end and UI testing.
- **Tailwind CSS:** Utility-first CSS framework for rapid UI development.
- **Husky + lint-staged:** To automate code quality checks and formatting before commits.
- **Storybook:** For documenting and testing UI components in isolation.
- **Babel:** For browser compatibility and polyfills.
- **Vue I18n:** For advanced internationalization support.

All tools must be properly configured and documented in the project. Use the latest stable versions and follow best practices for integration and usage.

## Dependency Management & Security

- Always install and use the latest stable versions of all npm libraries and dependencies.
- Confirm compatibility between all installed packages and frameworks before finalizing the build or deployment.
- Automate dependency updates and compatibility checks using tools like Dependabot or Renovate.
- Ensure production builds always obfuscate/minify all code (TypeScript, Vue, JS, CSS) to protect intellectual property and reduce risk of reverse engineering.
- Apply basic security best practices in the template base:
  - No hardcoded secrets, credentials, or sensitive data in the codebase.
  - Sanitize and validate all user input in reusable components.
  - Document any security considerations for downstream projects using the template.

## Scope

Deliver a faithful Nuxt 3 + TypeScript implementation that reproduces every page, layout, and interaction available in both Matoxi variants (`vertical-menu` and `offcanvas-menu`), while enforcing the tooling, architecture, and quality requirements outlined in this document.

## Analysis & Planning

- Build a master sitemap by enumerating every HTML file in `vertical-menu/` and `offcanvas-menu/`, then map each one to the Nuxt route that will replace it (capture dashboard variants, app pages, forms, widgets, charts, maps, auth flows, error pages, etc.).
- Identify layout-specific elements (e.g., offcanvas navigation markup vs. fixed sidebar) and decide how the Nuxt layout system will expose these options (toggle, settings panel, or separate layouts).
- List all interactive features (search, notifications, theme switcher, offcanvas, dropdowns, charts, etc.).

### 2. **Design Fidelity**

- Extract all color palettes, typography, spacing, and layout rules from CSS/SASS.
- Map variables and mixins declared in `sass/main.scss`, `sass/dark-theme.scss`, `sass/semi-dark.scss`, and `sass/bordered-theme.scss` into Tailwind config tokens or equivalent global CSS utilities so theme switching remains faithful.
- Document all breakpoints and responsive behaviors.
- List all icon sets and custom fonts.
- Note any custom CSS overrides or hacks.

### 3. **Functionality & Interactivity**

- Analyze all JavaScript logic: event handlers, jQuery plugins, chart initializations, menu logic, etc.
- Reverse-engineer `assets/js/main.js`, `index.js`, and `index2.js` to understand sidebar toggling, theme switching (`data-bs-theme` values), search overlays, and dashboard chart data; plan Vue composables/stores that replace each behaviour without jQuery.
- List all third-party plugins (apexcharts, metismenu, perfect-scrollbar, peity, etc.) and their configuration.
- Document all dynamic behaviors (modals, dropdowns, offcanvas, theme switching, etc.).
- Identify all forms and validation logic.

### 4. **Accessibility & Internationalization**

- Audit ARIA roles, semantic HTML, and accessibility features.
- Note language switcher and multi-language assets.

### 5. **Performance & Optimization**

- List all assets and their sizes.
- Identify any performance bottlenecks (large images, blocking scripts, etc.).
- Document lazy loading, code splitting, and optimization opportunities.

## Migration Steps

### 1. **Scaffold Nuxt 3 + TypeScript Project**

- Use `npx nuxi init` (latest Nuxt 3) with the `--typescript` and `--package-manager npm` flags to bootstrap the project inside `/Users/jorgerazo/projects/razo-nova-dashboard-template`.
- Configure `nuxt.config.ts` with required modules and tooling (Tailwind CSS, Pinia, Vue I18n, ESLint, Prettier, Vitest, Playwright, Storybook integration, color-mode/theming helpers, etc.).
- Establish the standard Nuxt folder structure (`app/`, `pages/`, `layouts/`, `components/`, `composables/`, `plugins/`, `assets/`, `server/`, `public/`, `tests/`).
- Set up global styles, Tailwind configuration, and theme variables that mirror the Matoxi Sass sources.

### 2. **Componentization**

- Convert each HTML page into a Vue SFC (`.vue` file), preserving layout and structure.
- Create separate Nuxt layouts (e.g., `layouts/vertical-menu.vue`, `layouts/offcanvas-menu.vue`) that encapsulate navigation, switcher panels, and header/footer variants; expose a runtime toggle if both layouts must be accessible from one build.
- Break down pages into reusable components (header, sidebar, cards, widgets, modals, etc.).
- Extract shared UI like the search overlay, notification dropdowns, switcher offcanvas (`#switcher`), and theme radio buttons into isolated components with documented props and emits.
- Centralize navigation/menu definitions (including multi-level MetisMenu structure) in typed configuration files so both layouts consume the same data source.
- Migrate all interactive elements to Vue components with TypeScript logic.
- Replace jQuery logic with Vue reactivity and event handling.

### 3. **Asset Migration**

- Copy all images, fonts, icons, and flags to the new project.
- Replace CDN dependencies (Google Fonts, Material Icons, Bootstrap Icons) with self-hosted assets or documented Nuxt modules while respecting licensing; ensure icon font demos remain functional.
- Migrate and refactor CSS/SASS to scoped styles or global theme files.
- Configure Nuxt to compile legacy Sass sources when needed (via PostCSS/Sass modules) while gradually moving design tokens into Tailwind utilities.
- Integrate third-party plugins as Vue-compatible packages (or create wrappers if needed).

### 4. **Functionality Migration**

- Reimplement all JavaScript features using Vue and TypeScript.
- Replace jQuery plugins with Vue alternatives or custom components.
- Integrate all third-party plugins through maintained Vue/Nuxt wrappers or custom adapters (`@apexcharts/vue3`, `vue-chartjs`, Vue-friendly DataTables alternative, `fullcalendar`, `vue3-perfect-scrollbar`, `vue3-select`, drag-and-drop/image upload libraries, Lobibox equivalents, vector maps, Google Maps loader, etc.).
- Recreate Bootstrap-driven interactions (modals, dropdowns, accordions, tooltips, offcanvas, steppers) using headless Vue/Tailwind primitives or lightweight Vue Bootstrap libraries to avoid jQuery dependencies while keeping identical UX.
- Implement theme switching, offcanvas navigation, notifications, and other UI logic in Vue; replicate the original behaviour of toggling `data-bs-theme` between `light`, `dark`, `semi-dark`, and `bordered` and persist the preference (e.g., Pinia + cookies/localStorage).
- Rebuild the global search overlay, notification list, and shopping cart dropdowns as composables/components with accessible focus management and keyboard support.
- Store chart datasets, widget counters, and demo table data as typed fixtures or API mocks so they can be replaced with live data sources later without touching presentation components.
- Ensure all forms use Vue's form handling and validation (e.g., Vuelidate, vee-validate).

### 5. **Routing & Navigation**

- Leverage Nuxt's file-based routing: create matching directories and filenames under `pages/` for every original HTML document (including nested paths for categories like `components/`, `forms/`, `charts/`, `tables/`, etc.).
- Implement navigation guards, middleware, and layout selection logic in Nuxt (`middleware/`, `plugins/`) to handle authenticated routes, demo mode restrictions, or layout toggles.

### 6. **Accessibility & i18n**

- Ensure all components use semantic HTML and ARIA roles.
- Integrate Vue I18n for language switching and multi-language support.
- Extract every literal label from the Matoxi HTML (navigation items, widget headings, chart legends, table headings, form labels, placeholder text, notifications, etc.) into i18n keys with English and Spanish translations.

### 7. **Testing & QA**

- Test each page and component for design fidelity and functional parity.
- Validate responsiveness and cross-browser compatibility.
- Perform accessibility audits.
- Optimize performance (lazy loading, code splitting, asset optimization).

### 8. **Documentation**

- Document all architectural decisions, component structure, and migration notes.
- Provide usage guides for new components and plugins.

## Deliverables

- Fully migrated Vue.js + TypeScript dashboard, matching original design and functionality.
- All assets, styles, and plugins integrated and refactored.
- Comprehensive documentation of migration process, decisions, and usage.
- Accessibility and performance improvements where possible.
- Automated test suite for code verification, including unit, integration, and end-to-end tests for all major components and features.
- Automated tests must verify that translation files exist for all supported languages and that all translation keys are present and consistent across language JSON files, to prevent missing translations.
- A `scripts` directory in the project root containing a `build.sh` script that:
  - Installs dependencies with `npm install` (for fresh clones).
  - Compiles the project (e.g., `npm run build`).
  - Starts a local web server to serve the compiled code.
  - Checks if the default port is available; if not, selects an available port automatically.
  - Opens the local server URL in the default browser for immediate verification and review.

## Additional Requirements

- **Supported Languages:**
  - English (default, always required)
  - Spanish (additional, must be fully supported)
  - All i18n text must be managed via translation files (JSON or standard formats) for both languages.

- **Testing Strategy:**
  - Primary tests must be written in TypeScript (unit and integration), as they do not depend on browser simulation.
  - Secondary tests should use Playwright for end-to-end and UI verification.
  - Include regression scenarios that load both Nuxt layouts (vertical and offcanvas), exercise the theme switcher states, and validate core plugins (charts, data tables, forms) render without console errors.

- **Plugin & Technology Migration:**
  - All plugins, libraries, and custom scripts used in the original templates must be migrated to TypeScript and Vue.js, using the latest available technologies and best practices.
  - Avoid legacy dependencies; prefer modern, actively maintained packages and Vue-native solutions.

- **Security:**
  - Security implementation is the responsibility of the future projects that use this template. Only basic best practices (no unsafe code, no hardcoded secrets) are required in the template itself.
  - Move sensitive placeholders from the Matoxi HTML (e.g., Google Maps API key) into environment variables and document safe defaults so no keys leak into version control.

- **Backup:**
  - No backup of the original codebase is required, as it resides in a separate directory and will not be modified. All new code will be stored in `/Users/jorgerazo/projects/razo-nova-dashboard-template`.

## Continuous Improvement & Best Practices (Inspired by Industry Standards)

### i18n Naming and Structure

- Use only ASCII letters, numbers, and underscores for translation keys (no hyphens or dot notation).
- Prefix keys with a concise module/domain name for clarity (e.g., `dashboard_nav_overview`).
- Keep translation keys alphabetically ordered in each file for easy diffing and duplicate detection.
- Enforce strict key parity: all supported languages must have the same keys, with no missing or extra entries.
- Never leave placeholders or untranslated text in any language file.
- Document the workflow for adding new keys and translations, including immediate updates to all languages.
- Provide or automate scripts/tasks to check key parity and alphabetical order (e.g., npm or Python helpers).

### Modular Organization

- Group code by feature and domain in logical directories (e.g., `features/`, `modules/`, `ui/`, `utils/`).
- Use descriptive, consistent naming for files and folders.
- Document the purpose and usage of each module and feature for maintainability.

### Build Validation & Multiplatform Support

- Ensure build scripts work on both Unix (`build.sh`) and Windows (`build.ps1`) if relevant.
- Validate that all expected output files and modules are generated after build.
- Include automated checks for build errors, warnings, and missing outputs.

### Documentation & Task Management

- Maintain a `tasks/` directory for verification, documentation, and workflow tasks.
- Document standards, workflows, and conventions for contributors.
- Encourage regular review and improvement of documentation and processes.

### General Recommendations

- Always prioritize maintainability, clarity, and continuous improvement over strict adherence to legacy patterns.
- Regularly review and refactor code, structure, and workflows to adopt new best practices and technologies.

## Environment Configuration & Logging

- Integrate the use of `.env` files to define environment variables, including at minimum the build mode (development, production, or other custom modes).
- The build and runtime logic must respect the environment mode:
  - In development or non-production modes, allow logs and debug messages in the terminal and browser console for easier debugging.
  - In production mode, suppress all logs and debug messages so that end users do not see internal information or records.
- Document how to configure and use environment variables for different build modes.

## Timeline & Autonomy

- No strict deadline; prioritize quality and fidelity over speed.
- Take all necessary time for analysis, refactoring, and testing.
- Make autonomous decisions to ensure the best possible migration outcome.

## Advanced Project Requirements

- **Monitoring & Reporting:** Integrate tools like Sentry or LogRocket for error and performance monitoring in production. Add Web Vitals and Lighthouse metrics for performance tracking.
- **Storybook:** Use Storybook not only for UI documentation but also for visual regression testing and component review.
- **Accessibility:** Automate accessibility testing with axe-core and Lighthouse. Document and enforce WCAG compliance for all UI components.
- **Dependency & Security Management:** Use Dependabot or Renovate to keep dependencies updated and secure. Automate security audits (e.g., npm audit) and document the process.
- **Advanced Internationalization:** Support pluralization, date/time/currency formatting, and collaborative translation workflows (Crowdin, Lokalise, etc.).
- **Automated Releases & Versioning:** Use Semantic Release or similar tools for automated versioning, changelogs, and release management.
- **Multi-Environment Deployment:** Provide scripts and documentation for deploying to multiple platforms (Vercel, Netlify, AWS, etc.), with environment-specific configuration.
- **Contribution & Review Policy:** Define clear guidelines for pull requests, code reviews, and quality standards. Document the process for onboarding new contributors and maintaining code quality.

## Strategy for Reusability & Integration in Other Projects

To ensure the template can be easily reused, maintained, and updated across multiple projects (such as Razo Nova Webext and Razo Nova Web), follow these steps:

### 1. Convert the Template to a UI Library

- Structure the template as an independent npm package (private or public).
- Export all components, layouts, styles, and utilities as reusable modules.
- Document the API, customization options, and usage for each component.

### 2. Publish the Library

- Use a private npm registry (GitHub Packages, Verdaccio, npm Enterprise, etc.) to publish the template.
- Version the library using semantic versioning (semver) and maintain changelogs.

### 3. Consume the Library in Other Projects

- In each dependent project, install the template as a dependency (e.g., `npm install @razo/razo-nova-dashboard-template`).
- Import and use the exported components in the project’s own logic and pages.
- Customize styles, themes, and behavior via props, slots, or configuration files.

### 4. Update and Maintain the Template

- When improvements or fixes are made, publish a new version of the library.
- Dependent projects update the library version to receive the latest changes.
- Keep business logic and UI code separated for maintainability.

### 5. (Optional) Use a Monorepo for Multiple Projects

- If managing many related projects, consider a monorepo (Nx, Turborepo, Lerna) to centralize dependencies and streamline updates.
- Monorepos simplify cross-project changes, versioning, and CI/CD.

### 6. Documentation and Examples

- Provide integration guides and usage examples in the template’s documentation.
- Use Storybook to showcase components and their variants for easy reference.

**Benefits:**

- Centralized maintenance and updates
- No code duplication across projects
- Easy customization and scalability
- Streamlined onboarding for new projects and contributors

**Note:** This strategy is industry standard for design systems and UI libraries in empresas modernas. It will save significant time and effort in the long term.

---
**Prepared by:** GitHub Copilot
**Date:** October 5, 2025
