# CLAUDE.md — wheels

## What This Repo Is

A Claude Code plugin marketplace. Plugins are organized into concept-based **scopes** under `scopes/`.

## Key Paths

- `.claude-plugin/marketplace.json` — marketplace catalog (must list all installable plugins)
- `scopes/` — all plugin scopes
- `scopes/<name>/.claude-plugin/plugin.json` — marks a scope as installable
- `templates/` — starter templates for new scopes

## Conventions

- kebab-case for all directory names
- semver for plugin versions
- Every installable scope needs a `README.md`
- Symlinks between scopes are OK and followed during install

## When Adding or Modifying a Plugin

1. Create/edit the scope under `scopes/<name>/`
2. Ensure `.claude-plugin/plugin.json` exists if it should be installable
3. Update `.claude-plugin/marketplace.json` to add/update the plugin entry
4. Update the "Available Plugins" table in `README.md`
5. Test with `claude --plugin-dir ./scopes/<name>`
