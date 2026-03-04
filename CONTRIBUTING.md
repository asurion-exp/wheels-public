# Contributing to wheels

## Adding a New Plugin

### 1. Choose a template

Copy a starter template into `scopes/`:

```bash
cp -r templates/skill scopes/my-plugin
# or: templates/hook, templates/mcp-server
```

### 2. Configure the plugin

Edit `scopes/my-plugin/.claude-plugin/plugin.json`:

```json
{
  "name": "my-plugin",
  "description": "What this plugin does",
  "version": "1.0.0"
}
```

### 3. Add your components

- **Skills**: `skills/<skill-name>/SKILL.md`
- **Hooks**: `hooks/<hook-name>.sh` (or other executable)
- **MCP servers**: `.mcp.json` at the scope root
- **Commands**: `commands/<command-name>/`
- **Agents**: `agents/<agent-name>/`

### 4. Add a README

Write a `README.md` in your scope directory explaining what the plugin does and how to use it.

### 5. Register the plugin

Add an entry to `.claude-plugin/marketplace.json` in the `plugins` array:

```json
{
  "name": "my-plugin",
  "description": "What this plugin does",
  "version": "1.0.0"
}
```

### 6. Test locally

```bash
claude --plugin-dir ./scopes/my-plugin
```

### 7. Open a PR

## Using Shared Resources

If your plugin needs a skill or resource that already exists in another scope, symlink it:

```bash
cd scopes/my-plugin/skills
ln -s ../../shared-scope/skills/shared-skill shared-skill
```

Don't copy files between scopes — symlinks keep things in sync.

## Creating a Shared Resource Scope

If you have components that multiple plugins should share:

1. Create `scopes/<shared-name>/` with the components (no `plugin.json`)
2. Don't add it to `marketplace.json`
3. Have consuming scopes symlink to it
4. Document the relationship in consuming scopes' READMEs

## Naming

- Use **kebab-case** for all directory names
- Use **semver** for versions

## Checklist Before Submitting

- [ ] `plugin.json` has name, description, and version
- [ ] Plugin is registered in `marketplace.json`
- [ ] `README.md` exists in the scope
- [ ] Tested locally with `claude --plugin-dir`
- [ ] No files copied between scopes (use symlinks instead)
