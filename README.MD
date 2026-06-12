# WidgetHub Local Widget Library

This repository collects local WidgetHub YAML definitions for Moodle TinyMCE, alongside a copy of the upstream example `repository/` widgets from [`jmulet/moodle-tiny_widgethub`](https://github.com/jmulet/moodle-tiny_widgethub).

WidgetHub lets Moodle authors choose a widget, customize its parameters through a form, and insert or re-edit the resulting HTML in TinyMCE. The upstream plugin is designed around Bootstrap/Boost themes, so these widgets generally assume Bootstrap classes and Font Awesome icons are available in Moodle.

## Reference Material Reviewed

- Upstream source: <https://github.com/jmulet/moodle-tiny_widgethub>
- YAML API: <https://github.com/jmulet/moodle-tiny_widgethub/blob/main/docs/api.md>
- Moodle plugin page and notes: <https://moodle.org/plugins/tiny_widgethub>
- WidgetHub GPT beta: <https://chatgpt.com/g/g-694018e49b888191b04b90e7c7a77a59-widgethub-for-tinymce-gpt-beta>

## Repository Layout

- `repository/` contains stock/example widgets from WidgetHub. These are useful reference implementations for Bootstrap components, bindings, partials, autocomplete, context menus, and media embeds.
- `GB/` contains Greg Bird local widgets. These focus on reusable teaching content blocks, Bootstrap alerts, quotes, tables, tabs, accordions, and learning activity cards.
- `ACBC/` contains brand-specific ACBC widgets: heading, quote, and stat box variants.
- `MP/` contains Melbourne Polytechnic-oriented snippets and widgets, including activity descriptions, submission instructions, image attribution, step cards, follow-up cards, and table patterns.

## WidgetHub YAML Shape

Every ordinary widget should start with the required identity fields:

- `key`: unique machine identifier. Treat this as stable once content has been inserted.
- `name`: human-readable picker label.
- `category`: picker grouping.
- `template` or `filter`: most local widgets use `template`.
- `author`: name and email.
- `version`: semantic-style `major.minor.revision`.

Common optional fields used in this repo:

- `instructions`: short author-facing guidance.
- `engine`: defaults to Mustache; use `ejs` when loops, conditionals, or computed values are needed.
- `selectors`: CSS selector used to recognize an existing inserted widget for re-editing. Required when parameters bind back to existing HTML.
- `insertquery`: CSS selector where selected TinyMCE content is inserted.
- `unwrap`: selector for editable/recoverable content when reconfiguring or extracting from existing markup.
- `parameters`: form controls used by the template.
- `contextmenu`: editing actions for repeated items, such as tabs or accordion items.
- `autocomplete`: parameter key used for variants in the `@` autocomplete popup.
- `scope`: regular expression limiting a widget to Moodle page body IDs.

The upstream API also supports parameter controls such as `textfield`, `textarea`, `numeric`, `select`, `checkbox`, `color`, and transform functions such as `trim`, `toUpperCase`, `ytId`, `vimeoId`, `removeHTML`, `encodeHTML`, and `escapeQuotes`.

## Local Coding Conventions

### Naming

- Local Greg Bird widgets generally use a `gb-` or `gb_` key prefix.
- ACBC widgets use a `gb_acbc_` prefix.
- Melbourne Polytechnic widgets use an `mp-`, `mp_`, or contributor-specific prefix.
- Prefer lowercase category names when creating new cross-library widgets. Existing local examples mix `UI`, `Interactive`, `interactive`, `Snippets`, `ACBC`, `image`, and `tables`, so category normalization would be a future cleanup rather than a silent edit.

### Template Engines

- Use Mustache for simple placeholders and safer content blocks.
- Use EJS only when the widget needs loops, computed classes, conditional blocks, or parameter-derived arrays.
- Keep EJS logic small and local to the template. The upstream security guidance treats EJS as more powerful and therefore more review-worthy than Mustache.

### Bootstrap Compatibility

- Prefer Bootstrap markup that works in Moodle Boost.
- For JavaScript components, include both Bootstrap 4 and Bootstrap 5 data attributes where relevant:
  - `data-toggle` with `data-bs-toggle`
  - `data-target` with `data-bs-target`
  - `data-dismiss` with `data-bs-dismiss`
  - `data-parent` with `data-bs-parent`
- Existing examples already follow this pattern in alerts, tabs, and accordion widgets.

### Re-Editing Support

- Add `selectors` whenever a widget should be detected and reconfigured after insertion.
- Add `insertquery` when selected editor content should be placed into a specific child element.
- Add `unwrap` when WidgetHub should preserve or expose inner editable content rather than treating the whole wrapper as opaque.
- Use stable wrapper markers such as `data-widget="..."`, unique classes, or a predictable component root.

### Parameters and Bindings

- Keep parameter names simple and template-friendly.
- Use `value` for a realistic default; local examples often use bracketed placeholders such as `[Title goes here]`.
- Use `textarea` for author-supplied prose.
- Use `select` with `{ l, v }` option objects when labels and stored values should differ.
- Use built-in bindings such as `hasClass(...)`, `classRegex(...)`, and `text` where possible.
- Use custom `bind.get` and `bind.set` only when the widget must infer or rewrite several related classes, as in `GB/gb-multibox.yml`.

### Editing Actions

- Repeated-item widgets should expose context-menu actions.
- Stock and local tab/accordion widgets use actions such as `moveleft`, `moveright`, `moveup`, `movedown`, `insertafter`, and `remove`.
- Keep predicates narrow, for example `li.nav-item` or `.accordion-item`.

## Local Pattern Summary

### `GB/`

The `GB/` widgets are the strongest local style guide for teaching-content widgets:

- Card-based learning blocks use `card`, `card-body`, `gb-bs-header`, and `gb-bs-content`.
- UI blocks often use Font Awesome icons inside headings.
- More complex components use EJS:
  - `gb-bs-table` adds row/column/header/footer controls.
  - `gb-bs-tabs` loops over tab counts and uses `contextmenu`.
  - `gb_interactive_accordion` generates unique collapsible sections.
  - `gb-multibox` maps a selected style to heading color, icon, and optional alert styling.
- Insertable selected content is supported in alert, quote, and video widgets through `insertquery` and `unwrap`.

### `ACBC/`

The `ACBC/` widgets are brand-specific and mostly presentational:

- They use `category: ACBC`.
- `acbc-heading` and `acbc-quote` include selectors and insert targets for re-editing.
- Stat boxes use EJS to split comma-separated numbers and labels, then loop through a fixed card count.
- These widgets assume external ACBC CSS exists for classes such as `acbc-title`, `acbc-quote-box`, and `acbc-stat-card`.

### `MP/`

The `MP/` widgets mix institutional snippets and richer authored components:

- Activity snippets use `scope` to restrict widgets to matching Moodle activity pages, for example assignment, forum, or quiz pages.
- Snippet templates are direct, mostly static Moodle instructions with one or two editable text parameters.
- Gabriel Tarallo's widgets use richer component structures for image attribution, step cards, post-session follow-up cards, and question-answer tables.
- `MP/gb-bs-table.yaml` appears to be a test copy of the GB table widget, with the name prefixed by `XXXX TEST XXXX`.

## Security and Maintainability Notes

- Treat custom YAML as executable content design. Review third-party widgets before adding them to Moodle.
- Prefer Mustache for ordinary content. Use EJS only when the widget genuinely needs logic.
- Avoid triple braces unless the value is intentionally trusted HTML, as in an embed field.
- Keep external JavaScript dependencies local or from trusted sources only.
- Use `scope` for snippets that only make sense on specific Moodle activity pages.
- Back up custom widgets before updating WidgetHub. Upstream notes that from version 1.5.0 onward, widget definitions are not automatically overwritten during plugin updates.

## Housekeeping Findings

- `GB/gb-box-important.yml` currently duplicates the `gb-box-think` key and name. If this is intended to be an Important Box, it should get its own unique `key`, `name`, icon, and colour.
- `GB/gb-box-law.yml` has a typo in the display name: `Law or standrad`.
- Category casing is inconsistent across local widgets (`UI`, `Interactive`, `interactive`, `Snippets`, `image`, `tables`). This will affect picker grouping unless intentionally configured.
- Some widgets use strong selectors such as `table.table`, which may match ordinary Bootstrap tables not created by WidgetHub. Prefer adding a widget-specific class or `data-widget` marker when re-editing precision matters.
- Some `.yaml` files in `MP/` appear to use Windows-style line endings. This is harmless for Moodle but worth normalizing if diffs become noisy.

## Creating a New Widget

1. Start from the closest existing local example.
2. Choose a unique `key` and a clear `category`.
3. Use Mustache unless loops or computed classes are needed.
4. Add `selectors` and a stable root marker if the widget should be re-edited.
5. Use `insertquery` when selected TinyMCE content should be inserted into a child container.
6. Keep parameters small, typed, and named after their template purpose.
7. Include Bootstrap 4 and 5 data attributes for interactive components.
8. Review any raw HTML fields, embeds, custom bindings, filters, or external dependencies before installing in Moodle.

