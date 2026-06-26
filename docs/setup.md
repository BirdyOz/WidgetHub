# Setup And Verification

## Fresh Clone

Clone the repository and check the branch:

```sh
git status --short --branch
git remote -v
```

The tracked repository currently contains the upstream/sample widgets in `repository/` and Greg Bird widgets in `GB/`. Local ignored directories such as `ACBC/` and `MP/` may need separate migration if they are still required.

## Dependencies

There is no package manager, build step, or test runner for this repository.

Runtime dependencies live in Moodle rather than this repo:

- Moodle TinyMCE.
- WidgetHub plugin.
- A Bootstrap-compatible Moodle theme such as Boost.
- Font Awesome where templates use `fa` icon classes.

## Local Checks

Check Git state:

```sh
git status --short --branch
git status --short --ignored
```

Parse YAML files when all local directories are present:

```sh
ruby -e 'require "yaml"; ARGV.each { |f| YAML.load_file(f) }; puts "YAML OK: #{ARGV.length} files"' repository/*.yml GB/*.yml ACBC/*.yml MP/*.{yml,yaml}
```

If `ACBC/` or `MP/` are absent, remove those globs from the command.

Check line endings if diffs look noisy:

```sh
file repository/*.yml GB/*.yml ACBC/*.yml MP/*
git ls-files --eol
```

## Moodle Verification

The authoritative verification path is Moodle itself:

1. Install or update the relevant YAML widget definitions in WidgetHub.
2. Insert the widget through TinyMCE.
3. Save and re-open the Moodle content.
4. Confirm rendered output, Bootstrap behaviour, icons, and accessibility basics.
5. Re-edit the inserted widget through WidgetHub and confirm selectors/bindings recover the expected parameters.

## Deployment Path

The exact local install/import path for these widget files is not documented yet. Before migration, record how widgets are currently moved from this repository into Moodle or WidgetHub, including whether `GB/`, `ACBC/`, `MP/`, and `repository/` are handled differently.
