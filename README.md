# wheels

A public, open-source plugin marketplace for [Claude Code](https://docs.anthropic.com/en/docs/claude-code). Install skills, MCP servers, hooks, and more directly from this repo.

IMPORTANT! This is *public*. If anything is sensitive, client specific, or otherwise a trade secret it must go in a private repo.

## Quick Start

Add the marketplace (run inside a Claude Code session):

```
/plugin marketplace add asurion-exp/wheels-public

# OR if you have cloned the repo locally
/plugin marketplace add ./
```

Browse and install plugins:

```
/plugin marketplace list
/plugin install <plugin-name>@wheels-public
```

Or install a plugin directly by path:

```bash
claude --plugin-dir ./scopes/<plugin-name>
```

## Available Plugins

| Plugin | Description | Components |
| ------ | ----------- | ---------- |
| [jj](scopes/jj/) | Jujutsu (jj) version control commands — a modern alternative to git | skill, commands |

## How It's Organized

Plugins are organized into **scopes** — topic-based directories under `scopes/`. Each scope is a concept area (e.g., `jj`, `gadget`, `docker`) that bundles whatever plugin components make sense together: skills, hooks, MCP servers, agents, etc.

```
scopes/
├── my-tool/              # A full plugin (has .claude-plugin/plugin.json)
│   ├── .claude-plugin/
│   │   └── plugin.json
│   ├── skills/
│   ├── hooks/
│   └── README.md
├── shared-utils/         # A shared resource (no plugin.json, consumed via symlinks)
│   └── skills/
└── another-tool/         # Can symlink to shared-utils
    └── skills/
        └── util -> ../../shared-utils/skills/util
```

**Key rules:**

- A scope with `.claude-plugin/plugin.json` is installable as a standalone plugin
- A scope _without_ `plugin.json` is a shared resource (only consumed via symlinks from other scopes)
- The root `marketplace.json` only lists scopes that are full plugins
- Symlinks between scopes are followed during plugin install

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for how to add a new plugin. Starter templates are in the `templates/` directory.

## License

[MIT](LICENSE)
