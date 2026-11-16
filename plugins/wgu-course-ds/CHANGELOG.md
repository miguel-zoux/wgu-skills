# Changelog

## 1.0.2 · 2026-11-16

Checked against **WGU Course Design System 2.1**.

- The skill checks its own version against a "Minimum `wgu-course-ds` plugin version" line in the DS README, and tells anyone on an older copy how to update.
- The setup message also turns on auto-update for the project.

## 1.0.1 · 2026-11-16

Checked against **WGU Course Design System 2.1**.

- Now part of the `wgu-skills` marketplace (`wgu-course-ds@wgu-skills`).
- Install instructions are now per project (project scope), with a setup message for the Claude app.
- Clearer wording in the rules and the request process.

## 1.0.0 · 2026-11-16

Checked against **WGU Course Design System 2.1** (2026-11-13).

- `wgu-course-ds` skill: reads the live DS each session, checks the project's `ds-version` against the DS changelog, and includes the shared rules, workflow (design → code, DS version sync) and the `TODO(ds)` request process.
- `wgu-course-ds-review` skill: stack-neutral audit checklist with severity levels.
