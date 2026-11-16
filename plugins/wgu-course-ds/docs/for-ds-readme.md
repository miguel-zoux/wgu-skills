# Handoff for the design system owners

Optional: a pointer the designers can add to the design system's `project/README.md` (for example under "Working with this system"), so people who find the system also find the plugin:

> **Building with this system in Claude Code?** Install the `wgu-course-ds` plugin (https://github.com/miguel-zoux/wgu-skills). It reads this system live, checks your project's version against the Changelog, and reviews code against these rules.

To make sure everyone uses a current version of the plugin, add this line to `project/README.md` and raise the number when the plugin maintainers ask:

> Minimum `wgu-course-ds` plugin version: 1.0.2

The plugin reads it every session. Anyone with an older copy is told to update and given the message to do it.

Nothing else in the artifact needs to change. The plugin reads `project/README.md`, `project/tokens.json`, `project/CHANGELOG.md` and `project/components/<Component>/README.md`. Please keep those paths stable, or tell the plugin maintainers when they move.
