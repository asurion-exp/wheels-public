# jj

Jujutsu (jj) version control plugin for Claude Code — a modern alternative to git.

## Installation

```bash
claude /plugin install wheels/jj
```

## What's Included

### Skills

- **jj** — Quick reference guide with essential commands, revsets, and git-to-jj translations. Invoke with `/jj [question]`.

### Commands

- **/commit** `[message]` — Create a jj commit with a descriptive message
- **/rebase-main** — Rebase current changes onto main
- **/squash** — Squash current revision into parent

## Why jj?

Jujutsu is a Git-compatible VCS with no staging area, automatic change tracking, and first-class support for rebasing and stacking changes. This plugin teaches Claude Code how to use `jj` instead of `git`.
