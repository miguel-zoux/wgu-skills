# wgu-skills

A Claude Code plugin marketplace for people building WGU courses. Each plugin adds skills that make Claude work the way WGU teams do.

## Plugins

| Plugin | What it does |
|---|---|
| [`wgu-course-ds`](plugins/wgu-course-ds/README.md) | Builds and reviews WGU course pages against the live WGU Course Design System: its tokens, components and rules. |

## Install a plugin in a project

Plugins here are meant to be installed per project, so they're only active in the folders that need them.

**In the Claude app** (Code tab, with your project folder open), send Claude this message and click **Allow** each time it asks:

```
Set up the WGU course design system plugin for this project only: add the plugin marketplace miguel-zoux/wgu-skills, then install wgu-course-ds@wgu-skills with project scope.
```

Then start a new chat.

**In a terminal**, from the project folder:

```
claude plugin marketplace add miguel-zoux/wgu-skills
claude plugin install wgu-course-ds@wgu-skills --scope project
```

## Updates

A plugin only counts as updated when its `version` changes, so every release bumps it. Each plugin's README explains how people get new versions.

Each plugin's README lists anything else it needs. For `wgu-course-ds`, that's view access to the design system.

## Adding a plugin

Put it in `plugins/<name>/` with its own `.claude-plugin/plugin.json`, README and CHANGELOG, and add an entry for it in `.claude-plugin/marketplace.json`.
