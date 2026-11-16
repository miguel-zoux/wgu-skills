# wgu-course-ds

A Claude Code plugin, part of the [`wgu-skills` marketplace](../../README.md), that helps everyone building WGU course UI (Open edX course pages, templates, blocks and interactive activities) work the same way against the **WGU Course Design System**, in any stack.

The design system itself (tokens, rules, component guides, changelog) stays in the designers' claude.ai artifact. This plugin holds the *way of working*: it makes Claude read the live system every session, check your project's DS version against the changelog, follow the shared rules, and review code against them.

## What's inside

| Skill | Use it for |
|---|---|
| `wgu-course-ds` | Building or changing course UI, implementing a Figma design, syncing a project to a new DS version |
| `wgu-course-ds-review` | Auditing a diff, branch or folder against the DS (reports, doesn't fix) |

Both trigger on their own when the work matches; you can also ask for them by name.

## Install (per project)

Install it in each course project folder, so it's only active there.

**In the Claude app** (Code tab, with your course folder open), send Claude this message and click **Allow** each time it asks:

```
Set up the WGU course design system plugin for this project only: add the plugin marketplace miguel-zoux/wgu-skills, install wgu-course-ds@wgu-skills with project scope, then turn on auto-update for the wgu-skills marketplace in this project's settings.
```

Then start a new chat. The skills show under **+ → Slash commands** as `wgu-course-ds:…`.

**In a terminal**, from the project folder:

```
claude plugin marketplace add miguel-zoux/wgu-skills
claude plugin install wgu-course-ds@wgu-skills --scope project
```

Then add `"autoUpdate": true` to the `wgu-skills` entry under `extraKnownMarketplaces` in the project's `.claude/settings.json`.

Project scope records the plugin in the folder's `.claude/settings.json`, so it doesn't load anywhere else.

## Updates

- **Automatic:** with auto-update on, new versions arrive within about ten minutes of starting a session and load in the next chat.
- **By hand:** send Claude *"Update the WGU course design system plugin: run claude plugin marketplace update wgu-skills, then claude plugin update wgu-course-ds@wgu-skills --scope project."*, then start a new chat.
- **Making sure everyone updates:** the design system's `project/README.md` can name a minimum plugin version (see `docs/for-ds-readme.md`). When someone's copy is older, the skill tells them and gives them the update message.

## Requirements

- **View access to the design system artifact** (`https://claude.ai/artifact/9JwcPY7YVU4vAcsKXzBwDD`). Ask the design system's owners to share it with you. Without access, the skill stops and tells you instead of guessing values.
- Claude Code (the Claude app's Code tab, the terminal or an IDE) with the Artifact tool. Headless `claude -p` runs don't have it.

## Set up a project

Add one line to the project's `CLAUDE.md`, naming the DS version its tokens match:

```
ds-version: 2.1
```

(or put `2.1` in a `.wgu-ds-version` file). The skill compares it with the DS changelog and tells you what changed since.

## Precedence

Live design system → this plugin's rules → Figma → existing code. When the plugin and the design system disagree, Claude follows the design system and flags the difference. Please open an issue or PR so the plugin gets fixed.

## Changing the plugin

- Rules: `skills/wgu-course-ds/references/rules.md`. Keep exact values out; they belong in the design system's `tokens.json`.
- Bump the version in three places: this plugin's `.claude-plugin/plugin.json`, the marketplace's `.claude-plugin/marketplace.json` at the repo root, and `PLUGIN_VERSION` in `skills/wgu-course-ds/SKILL.md`. Without a bump, nobody receives the change. Add a `CHANGELOG.md` entry naming the DS version it was checked against.
- Tokens and components aren't added here. New ones are requested from the designers (see `references/requests.md`).
