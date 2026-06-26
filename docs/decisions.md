# Decisions

## Keep Upstream Examples

The `repository/` directory is retained as a tracked reference copy of upstream WidgetHub examples. These files are useful for API patterns, Bootstrap components, bindings, context menus, media embeds, and JavaScript integration.

## Keep Local GB Widgets Separately

Greg Bird local widgets live under `GB/`. This keeps local teaching/content widgets separate from upstream examples.

## Preserve Stable Widget Keys

Widget `key` values should be treated as stable once a widget may have been inserted into Moodle content. Renaming a key can break recognition, re-editing, or author expectations.

## Prefer Narrow Re-Editing Selectors

Selectors should ideally identify widget-created markup rather than broad Bootstrap elements. Prefer stable markers such as `data-widget`, widget-specific classes, or predictable roots when adding or revising widgets.

## Maintain Bootstrap 4 And 5 Compatibility

Interactive Bootstrap components should include both Bootstrap 4 and Bootstrap 5 data attributes where relevant. This matches existing local practice and helps across Moodle theme/version differences.

## Open Decision: ACBC And MP Tracking

`ACBC/` and `MP/` were present locally during the 2026-06-26 audit but ignored by `.gitignore`.

Decide whether these should be:

- tracked here,
- moved to a separate private/client-specific location,
- archived as migration-only local assets,
- or left intentionally ignored.

Until that is decided, do not assume a fresh clone contains them.

## Open Decision: Installation Workflow

The exact path from repository files to Moodle WidgetHub installation is not documented. Add it once confirmed, including any manual copy/import steps, Moodle instance assumptions, and validation checkpoints.
