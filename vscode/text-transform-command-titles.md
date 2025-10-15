# Razo Nova VS Code - Text Transform Command Title Checklist

This playbook documents the manual steps needed to refresh the localized command titles (keys `commands.transform.*.title`) for the Razo Nova VS Code extension. Follow it whenever new transforms are added or localizations need to be corrected.

## Scope

* Repository: `/Users/jorgerazo/projects/razo-nova-vscode`
* Files:

  * All `package.nls*.json`
  * All `src/i18n/messages/*.json`
* Keys: every `commands.transform.*.title` entry (upper, lower, title, sentence, camel, pascal, snake, kebab, constant, swap, plus any future variants).

## Workflow

1. **Inspect Locales**

   * Confirm all target files are present: `package.nls.json`, localized variants (`package.nls.de.json`, `package.nls.pl.json`, `package.nls.cs.json`, `package.nls.hu.json`, etc.), and the message bundles in `src/i18n/messages/`.
   * Ensure you have a reference for each language's preferred casing rules (see "Title Case Conventions" below).

2. **Edit Titles Manually**

   * For each file, rewrite the text before the arrow `→` so that:

     * The phrasing is idiomatic for the locale.
     * Case-style names remain recognizable to developers (for example, "Camel Case", "Snake Case", "Uppercase").
     * Small connector words obey the locale's casing rules (see lists below); do not auto-capitalize them when they appear mid-phrase.
   * Never change the transformation example after the arrow.
   * Do not perform automatic search-and-replace across languages; review each string in context.

3. **Run Validation**

   * From `/Users/jorgerazo/projects/razo-nova-vscode` execute:

     ```bash
     npm run build
     npm test
     ```

   * Both must succeed; address any parity errors reported by `check-i18n.js` or the localization tests (which also ensure manifest/message locale coverage stays in sync).

4. **Summarize Work**

   * Record which locales were touched.
   * Note the verification commands executed (build and test) and their outcomes.

## Title Case Conventions

Use Title Case for languages that employ Title Case in UI titles. For languages that prefer sentence case, follow that practice. In all cases, keep the following small connector words lowercase unless they begin the string or follow punctuation that resets casing (colon, period, em dash, etc.). Extend the lists if translators request additional words.

### English

* `to`, `of`, `the`, `and`, `for`, `in`, `on`, `at`, `by`

### Spanish

* `a`, `de`, `la`, `el`, `los`, `las`, `y`, `o`

### French

* `en`, `de`, `la`, `le`, `les`, `du`, `des`, `et`

### Italian

* `in`, `di`, `la`, `le`, `il`, `gli`, `e`, `o`

### Portuguese (pt-BR and pt-PT)

* `para`, `de`, `do`, `da`, `dos`, `das`, `e`, `ou`

### Polish

* Keep short function words (conjunctions and prepositions) like `i`, `w`, `z`, `na`, `do`, `po` lowercase mid-phrase; retain English case-style labels when they are widely used (for example, `Camel Case`).

### Czech

* Lowercase short connectors such as `a`, `v`, `s`, `do`, `na`, `z` unless they start the string; keep borrowed case names (`Camel Case`) capitalized as loanwords.

### Hungarian

* Use sentence-style capitalization (only the first word capitalized) unless a proper noun appears; keep connectors like `és`, `a`, `az`, `meg` lowercase mid-phrase and leave borrowed case names in their established English form.

### German

* Use sentence-style capitalization overall; capitalize nouns per German grammar. Keep connectors like `und`, `mit`, `in` lowercase when not leading a clause. Maintain Title Case on case-style names (`Camel Case`, etc.).

### Russian

* Use sentence case, capitalizing only the first word and proper nouns. Lowercase prepositions (`в`, `с`, `к`, etc.) mid-phrase.

### Turkish

* Use sentence case overall; keep connectors like `ve`, `ile` lowercase, while keeping borrowed case names (`Camel Case`) in Title Case.

### Chinese, Japanese, and Korean

* Localized wording generally does not require Title Case adjustments; ensure spacing and punctuation match locale norms. Keep borrowed terms in their customary script forms.

## Additional Notes

* Keep indentation and JSON formatting consistent (two spaces).
* Verify that new transforms receive localized titles in every file before running tests.
* If localization partners provide updated wording, revise the connector lists above accordingly and note the change in this document.
