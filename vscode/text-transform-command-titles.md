# Razo Nova VS Code – Text Transform Command Title Checklist

This playbook documents the manual steps needed to refresh the localized command titles (keys `commands.transform.*.title`) for the Razo Nova VS Code extension. Follow it whenever new transforms are added or localizations need to be corrected.

## Scope

- Repository: `/Users/jorgerazo/projects/razo-nova-vscode`
- Files:
  - All `package.nls*.json`
  - All `src/i18n/messages/*.json`
- Keys: every `commands.transform.*.title` entry (upper, lower, title, sentence, camel, pascal, snake, kebab, constant, swap, plus any future variants).

## Workflow

1. **Inspect Locales**
   - Confirm all target files are present: `package.nls.json`, localized variants (`package.nls.de.json`, etc.), and the message bundles in `src/i18n/messages/`.
   - Ensure you have a reference for each language’s preferred casing rules (see “Title Case Conventions” below).

2. **Edit Titles Manually**
   - For each file, rewrite the text **before** the arrow `→` so that:
     - The phrasing is idiomatic for the locale.
     - Case-style names remain recognizable to developers (e.g., “Camel Case”, “Snake Case”, “Uppercase”).
     - Small connector words obey the locale’s casing rules (see list below); do not auto-capitalize them when they appear mid-phrase.
   - Never change the transformation example **after** the arrow.
   - Do not perform automatic search-and-replace across languages; review each string in context.

3. **Run Validation**
   - From `/Users/jorgerazo/projects/razo-nova-vscode` execute:

     ```bash
     npm run build
     npm test
     ```

   - Both must succeed; address any parity errors reported by `check-i18n.js` or the localization tests.

4. **Summarize Work**
   - Record which locales were touched.
   - Note the verification commands executed (build/test) and their outcomes.

## Title Case Conventions

Use Title Case for meaningful words, but keep the following connectors lowercase unless they begin the string or follow a punctuation mark that resets casing (colon, period, em dash, etc.). Extend the list if translators request additional words.

### English

- `to`, `of`, `the`, `and`, `for`, `in`

### Spanish

- `a`, `de`, `la`, `el`, `los`, `las`

### French

- `en`, `de`, `la`, `le`, `les`, `du`, `des`

### Italian

- `in`, `di`, `la`, `le`, `il`, `gli`

### Portuguese (pt-BR & pt-PT)

- `para`, `de`, `do`, `da`, `dos`, `das`

### German

- Lowercase after compounds unless language rules require capitalization; keep connectors like `und`, `mit`, `in` lowercase when not leading a clause. Maintain the Title Case on case-style names (`Camel Case`, etc.).

### Russian

- Maintain sentence case with capital letter only for the first word and proper nouns. Lowercase prepositions (`в`, `с`, `к`, etc.) inside the phrase.

### Turkish

- Use sentence case for connectors like `ve`, `ile`, while keeping borrowed case names (`Camel Case`) in Title Case.

### Chinese & Japanese & Korean

- Localized wording generally does not require Title Case adjustments; ensure spacing/punctuation matches locale norms. Keep borrowed terms in their customary script forms.

## Additional Notes

- Keep indentation and JSON formatting consistent (two spaces).
- Verify new transforms receive localized titles in every file before running tests.
- If localization partners provide updated wording, revise the connector lists above accordingly and note the change in this document.
