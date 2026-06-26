# KB Notes

This file records durable routing notes for knowledge that should live outside this project if promoted.

## Keep Project-Local

- Exact widget filenames, keys, selectors, and known issues in this repository.
- Current tracked versus ignored file state.
- Project-specific setup and migration details.
- Any confirmed install/import workflow for this widget library.

## Candidate Promotions

### `moodle-content-authoring`

Promote general WidgetHub authoring guidance that is not specific to this repository:

- Treat widget keys as durable once content has been inserted.
- Use selectors, `insertquery`, and `unwrap` to support re-editing.
- Validate insert, save, reopen, render, and re-edit behaviour in Moodle TinyMCE.
- Keep snippets scoped to appropriate Moodle page types when they only make sense in certain activity contexts.

### `moodle-theming-css-fixes`

Promote reusable Moodle frontend compatibility patterns:

- Include both Bootstrap 4 and Bootstrap 5 data attributes for interactive components when supporting multiple Moodle/theme environments.
- Assume Boost/Bootstrap and Font Awesome availability only after checking the target Moodle theme.
- Prefer widget-specific wrapper classes or `data-widget` attributes to avoid CSS/JS collisions.

### `codex-common-core`

No profile change is needed from this audit. The existing routing rules already say project-local facts stay in the project and reusable Moodle authoring/theming knowledge belongs in the relevant domain KB.

## Leave Behind

- Raw chat history.
- Temporary audit command output.
- One-off troubleshooting noise.
- Credentials, private contacts, private Moodle URLs, or sensitive client data.
