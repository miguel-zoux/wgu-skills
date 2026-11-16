# Handoff for the design system owners

Optional: a pointer the designers can add to the design system's `project/README.md` (for example under "Working with this system"), so people who find the system also find the plugin:

> **Building with this system in Claude Code?** Install the `wgu-course-ds` plugin (https://github.com/miguel-zoux/wgu-skills). It reads this system live, checks your project's version against the Changelog, and reviews code against these rules.

Nothing else in the artifact needs to change. The plugin reads `project/README.md`, `project/tokens.json`, `project/CHANGELOG.md` and `project/components/<Component>/README.md`. Please keep those paths stable, or tell the plugin maintainers when they move.
