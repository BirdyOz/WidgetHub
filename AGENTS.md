# WidgetHub Project Guide

This repository stores local WidgetHub YAML definitions for Moodle TinyMCE, plus a tracked copy of upstream example widgets from `jmulet/moodle-tiny_widgethub`.

## Authority Order

1. Read this file first.
2. Read `README.MD` for widget conventions, layout, and known housekeeping findings.
3. Read `docs/project-context.md`, `docs/setup.md`, `docs/decisions.md`, and `docs/kb-notes.md` when migration, onboarding, or durable context matters.
4. Inspect the actual widget YAML before making changes; existing inserted Moodle content may depend on stable keys and selectors.

## Repository Shape

- `repository/` contains tracked upstream/sample WidgetHub widgets.
- `GB/` contains tracked Greg Bird local widgets.
- `ACBC/` and `MP/` may exist locally, but are currently ignored by `.gitignore` and are not part of a fresh clone unless migrated separately.
- `README.MD` uses an uppercase `.MD` extension.

## Working Safely

- Treat widget `key` values as durable once content may have been inserted into Moodle.
- Avoid broad selector changes unless re-editing behaviour has been checked in Moodle TinyMCE with WidgetHub.
- Prefer Mustache for simple templates and EJS only when loops, conditionals, or computed values are needed.
- Keep Bootstrap 4 and Bootstrap 5 data attributes together for interactive components when relevant.
- Avoid adding remote JavaScript, live service URLs, credentials, or client-sensitive content to widgets or docs.
- Do not silently normalise ignored/local-only files into tracked project state; ask first.

## Verification

There is no build system in this repository. For low-risk checks, parse YAML and inspect Git state:

```sh
git status --short --branch
git status --short --ignored
ruby -e 'require "yaml"; ARGV.each { |f| YAML.load_file(f) }; puts "YAML OK: #{ARGV.length} files"' repository/*.yml GB/*.yml ACBC/*.yml MP/*.{yml,yaml}
```

The Ruby command assumes the local-only `ACBC/` and `MP/` directories exist. If they are absent, adjust the file list. Final validation for authoring and re-editing behaviour should happen in Moodle TinyMCE with WidgetHub.
