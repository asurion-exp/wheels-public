# Agents Guide — wheels

## Repo Structure

```
wheels/
├── .claude-plugin/marketplace.json   # Marketplace catalog
├── scopes/                           # All plugin scopes live here
│   └── <scope-name>/                 # One directory per concept
├── templates/                        # Starter templates for new scopes
├── CLAUDE.md                         # Repo conventions for Claude Code
├── CONTRIBUTING.md                   # Human contributor guide
└── AGENTS.md                         # This file
```

## How Scopes Work

Each directory under `scopes/` is a **scope** — a concept area that bundles related plugin components.

### Full plugins (installable)

A scope is a full plugin if it contains `.claude-plugin/plugin.json`. These are listed in the root `marketplace.json` and can be installed by users.

```
scopes/my-plugin/
├── .claude-plugin/
│   └── plugin.json       # Makes this scope installable
├── skills/
│   └── do-thing/
│       └── SKILL.md
├── hooks/                # Optional
├── commands/             # Optional
├── agents/               # Optional
├── .mcp.json             # Optional MCP server config
└── README.md
```

### Shared resources (not installable)

A scope without `plugin.json` is a shared resource. It exists only to be consumed by other scopes via symlinks.

```
scopes/shared-utils/
└── skills/
    └── common-skill/
        └── SKILL.md
```

Another scope references it:

```
scopes/my-plugin/skills/common-skill -> ../../shared-utils/skills/common-skill
```

## Conventions

- **Naming**: kebab-case for all scope and component directory names
- **Versioning**: semver in `plugin.json` (`"version": "1.0.0"`)
- **Self-contained**: Each plugin scope must be self-contained (symlinks to other scopes are the only allowed cross-references)
- **marketplace.json sync**: When adding or removing a plugin scope, update `.claude-plugin/marketplace.json`
- **README**: Every installable scope should have a `README.md`

## Testing a Plugin Locally

```bash
claude --plugin-dir ./scopes/<scope-name>
```

## Adding a New Scope — Step by Step

1. Copy a template from `templates/` into `scopes/<new-name>/`
2. Edit `.claude-plugin/plugin.json` with the scope's name, description, and version
3. Add components (skills, hooks, MCP config, etc.)
4. Add a `README.md` to the scope
5. Register the plugin in `.claude-plugin/marketplace.json`:
   ```json
   {
     "name": "<new-name>",
     "description": "What this plugin does",
     "version": "1.0.0"
   }
   ```
6. Test locally with `claude --plugin-dir ./scopes/<new-name>`
7. Open a PR

## Adding a Shared Resource Scope

1. Create `scopes/<shared-name>/` with the desired components (no `plugin.json`)
2. Do **not** add it to `marketplace.json`
3. Create symlinks from consuming scopes to the shared resources
4. Document the relationship in the consuming scope's README
