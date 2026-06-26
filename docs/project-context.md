# Project Context

## Purpose

WidgetHub is a local widget library for Moodle TinyMCE. It collects custom YAML widget definitions used to insert and re-edit structured Moodle content through the WidgetHub plugin.

The repository also carries a tracked copy of upstream example widgets under `repository/` for reference.

## Scope

In scope:

- WidgetHub YAML definitions.
- Small supporting JavaScript files used by WidgetHub examples.
- Local documentation about widget conventions, setup, and migration state.

Out of scope:

- Moodle plugin source code.
- Moodle theme source code.
- Production Moodle configuration.
- Credentials, client contact details, private Moodle URLs, and live service secrets.

## Important Paths

- `README.MD`: main project README and local conventions.
- `AGENTS.md`: working guide for Codex sessions.
- `repository/`: tracked upstream/sample widgets.
- `GB/`: tracked Greg Bird local widgets.
- `ACBC/`: local ignored ACBC-specific widgets, if present.
- `MP/`: local ignored Melbourne Polytechnic-oriented widgets, if present.
- `docs/setup.md`: setup and verification notes.
- `docs/decisions.md`: decisions and open questions.
- `docs/kb-notes.md`: reusable knowledge routing notes.

## Current Git State At Audit

Audit date: 2026-06-26.

- Branch: `main`.
- Remote: `origin` points to `https://github.com/BirdyOz/WidgetHub.git`.
- `main` matched `origin/main` at commit `977dd07 Adjust accordion template spacing`.
- Working tree was clean.
- `ACBC/` and `MP/` were present locally but ignored by `.gitignore`.

Recheck this before migration because branch, remote, and ignored-file state can change.

## Runtime Assumptions

These widgets assume:

- Moodle TinyMCE with the WidgetHub plugin.
- Moodle Boost or another Bootstrap-compatible theme.
- Bootstrap classes are available in rendered Moodle content.
- Font Awesome icons are available where widget templates use `fa` classes.
- WidgetHub supports Mustache templates, EJS templates, parameters, selectors, bindings, `insertquery`, `unwrap`, `contextmenu`, and `scope` as described by the upstream plugin.

## Local-Only Migration Warning

The README describes `ACBC/` and `MP/`, but those directories are currently ignored and are not tracked by Git.

Before rebuilding on a new Mac, decide whether these directories should be:

- tracked in this repository,
- archived or migrated separately,
- kept out of Git because they are client-specific, experimental, or otherwise private.

A fresh clone from GitHub is expected to include `repository/`, `GB/`, and `README.MD`, but not ignored local-only assets.

## Known Fragile Areas

- Widget keys may already be embedded in Moodle content and should not be renamed casually.
- Selectors control re-editing and can accidentally match ordinary Moodle/Bootstrap content if too broad.
- `GB/gb-box-important.yml` duplicates the `gb-box-think` key and name.
- `GB/gb-box-law.yml` has the display-name typo `Law or standrad`.
- Category casing is inconsistent across widgets and may affect picker grouping.
- Some local `MP/` files use CRLF line endings.
- EJS widgets are more powerful and deserve closer review than simple Mustache widgets.

## Client And Privacy Constraints

Keep client-specific details minimal in project documentation. Avoid adding credentials, private contacts, Moodle URLs, sensitive content samples, or private operational notes. Prefer generic descriptions unless a detail is necessary to work safely in this repository.
